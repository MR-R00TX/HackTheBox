
<img width="1604" height="349" alt="image" src="https://github.com/user-attachments/assets/e1b2d26c-f4b5-4b76-bbc7-399f6d6f94f6" />




```
nmap -sV -Pn 10.129.112.179           
Starting Nmap 7.99 ( https://nmap.org ) at 2026-07-16 14:18 -0400
Nmap scan report for 10.129.112.179
Host is up (0.36s latency).
Not shown: 998 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 9.6p1 Ubuntu 3ubuntu13.16 (Ubuntu Linux; protocol 2.0)
80/tcp open  http    nginx 1.24.0 (Ubuntu)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 33.03 seconds

```
<img width="1631" height="697" alt="image" src="https://github.com/user-attachments/assets/f67dd9f6-1e97-46ef-8ebf-ee63d71d0169" />



```
wfuzz -c --hw 10 -Z -w /usr/share/wordlists/seclists/Discovery/DNS/subdomains-top1million-5000.txt -H "Host: FUZZ.nexus.htb" http://10.129.112.179
 /usr/lib/python3/dist-packages/wfuzz/__init__.py:34: UserWarning:Pycurl is not compiled against Openssl. Wfuzz might not work correctly when fuzzing SSL sites. Check Wfuzz's documentation for more information.
********************************************************
* Wfuzz 3.1.0 - The Web Fuzzer                         *
********************************************************

Target: http://10.129.112.179/
Total requests: 4989

=====================================================================
ID           Response   Lines    Word       Chars       Payload                                                                                      
=====================================================================

000000206:   302        11 L     22 W       390 Ch      "billing"                                                                                    
000000262:   200        241 L    1366 W     14362 Ch    "git"                                                                                        

Total time: 0
Processed Requests: 4989
Filtered Requests: 4987
Requests/sec.: 0

```





<img width="1450" height="858" alt="image" src="https://github.com/user-attachments/assets/cbeaeb12-494d-4040-947b-0c98f427ee03" />


<img width="1452" height="787" alt="image" src="https://github.com/user-attachments/assets/a2b61945-b72a-45ff-a47c-cdc8a08b29a8" />


<img width="959" height="793" alt="image" src="https://github.com/user-attachments/assets/5324f109-83c6-4712-9fe8-f3019cf2efb1" />


```
git diff 9b817fa 1615c46
diff --git a/.env b/.env
index 5ae1bb2..cb7ccc3 100644
--- a/.env
+++ b/.env
@@ -2,7 +2,7 @@ APP_NAME='Krayin CRM'
 APP_ENV=local
 APP_KEY=
 APP_DEBUG=true
-APP_URL=http://billing.nexus.htb
+APP_URL=http://nexus.htb
 APP_TIMEZONE=Asia/Kolkata
 APP_LOCALE=en
 APP_CURRENCY=USD
@@ -15,7 +15,7 @@ DB_HOST=krayin-mysql
 DB_PORT=3306
 DB_DATABASE=krayin
 DB_USERNAME=krayin
-DB_PASSWORD=
+DB_PASSWORD=N27xh!!2ucY04
 DB_PREFIX=
 BROADCAST_DRIVER=log
 CACHE_DRIVER=file

```

![[Pasted image 20260729010626.png]]

![[Pasted image 20260729013733.png]]



![[Pasted image 20260729013819.png]]

![[Pasted image 20260729014608.png]]

y27xb3ha!!74GbR

```
git -c http.curloptResolve="git.nexus.htb:80:10.129.64.165" -c http.curloptPort=3000 push -u origin main
```
