
![[Pasted image 20260709032749.png]]




![[Pasted image 20260709024416.png]]

```


┌──(root㉿kali)-[/home/kali/Desktop/HTB]
└─# cat /etc/hosts
127.0.0.1   localhost
::1         localhost ip6-localhost ip6-loopback
ff02::1     ip6-allnodes
ff02::2     ip6-allrouter

10.129.131.210 unika.htb


```

```
nmap -sV -A 10.129.131.210                      
Starting Nmap 7.99 ( https://nmap.org ) at 2026-07-08 16:48 -0400
Nmap scan report for unika.htb (10.129.131.210)
Host is up (0.29s latency).
Not shown: 998 filtered tcp ports (no-response)
PORT     STATE SERVICE VERSION
80/tcp   open  http    Apache httpd 2.4.52 ((Win64) OpenSSL/1.1.1m PHP/8.1.1)
|_http-server-header: Apache/2.4.52 (Win64) OpenSSL/1.1.1m PHP/8.1.1
|_http-title: Unika
5985/tcp open  http    Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Device type: general purpose
Running (JUST GUESSING): Microsoft Windows 10|2019 (97%)
OS CPE: cpe:/o:microsoft:windows_10 cpe:/o:microsoft:windows_server_2019
Aggressive OS guesses: Microsoft Windows 10 1903 - 22H2 (97%), Microsoft Windows 10 1909 - 2004 (91%), Microsoft Windows Server 2019 (91%), Microsoft Windows 10 1803 (89%), Microsoft Windows 10 22H2 (89%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 2 hops
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

TRACEROUTE (using port 80/tcp)
HOP RTT       ADDRESS
1   282.78 ms 10.10.14.1
2   282.90 ms unika.htb (10.129.131.210)

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 46.27 seconds

```



```
katana -u http://unika.htb

   __        __                
  / /_____ _/ /____ ____  ___ _
 /  '_/ _  / __/ _  / _ \/ _  /
/_/\_\\_,_/\__/\_,_/_//_/\_,_/                                                   

                projectdiscovery.io

[INF] Current katana version v1.5.0 (outdated)
[INF] Started standard crawling for => http://unika.htb
http://unika.htb
http://unika.htb/js/theme.js
http://unika.htb/inc/jquery.counterup.min.js
http://unika.htb/inc/owl-carousel/js/owl.carousel.min.js
http://unika.htb/inc/jquery.easing.min.js
http://unika.htb/inc/animations/js/wow.min.js
http://unika.htb/inc/waypoints.min.js
http://unika.htb/inc/classie.js
http://unika.htb/inc/stellar/js/jquery.stellar.min.js
http://unika.htb/inc/smoothscroll.js
http://unika.htb/inc/bootstrap/js/bootstrap.min.js
http://unika.htb/inc/isotope.pkgd.min.js
http://unika.htb/css/skin/cool-gray.css
http://unika.htb/css/mobile.css
http://unika.htb/css/reset.css
http://unika.htb/inc/owl-carousel/css/owl.theme.css
http://unika.htb/inc/owl-carousel/css/owl.carousel.css
http://unika.htb/inc/font-awesome/css/font-awesome.min.css
http://unika.htb
http://unika.htb/css/style.css
http://unika.htb/body
http://unika.htb/index.php?page=french.html
http://unika.htb/index.php?page=german.html
http://unika.htb/index.html
http://unika.htb/inc/animations/css/animate.min.css
http://unika.htb/inc/jquery/jquery-1.11.1.min.js
http://unika.htb/inc/bootstrap/css/bootstrap.min.css
http://unika.htb/index.php?page=german.html
http://unika.htb/
http://unika.htb/index.php?page=french.html
http://unika.htb/a
 
```

![[Pasted image 20260709025108.png]]



```
responder -I tun0        
                                         __
  .----.-----.-----.-----.-----.-----.--|  |.-----.----.
  |   _|  -__|__ --|  _  |  _  |     |  _  ||  -__|   _|
  |__| |_____|_____|   __|_____|__|__|_____||_____|__|
                   |__|


[*] Tips jar:
    USDT -> 0xCc98c1D3b8cd9b717b5257827102940e4E17A19A
    BTC  -> bc1q9360jedhhmps5vpl3u05vyg4jryrl52dmazz49

[+] Poisoners:
    LLMNR                      [ON]
    NBT-NS                     [ON]
    MDNS                       [ON]
    DNS                        [ON]
    DHCP                       [OFF]
    DHCPv6                     [OFF]

[+] Servers:
    HTTP server                [ON]
    HTTPS server               [ON]
    WPAD proxy                 [OFF]
    Auth proxy                 [OFF]
    SMB server                 [ON]
    Kerberos server            [ON]
    SQL server                 [ON]
    FTP server                 [ON]
    IMAP server                [ON]
    POP3 server                [ON]
    SMTP server                [ON]
    DNS server                 [ON]
    LDAP server                [ON]
    MQTT server                [ON]
    RDP server                 [ON]
    DCE-RPC server             [ON]
    WinRM server               [ON]
    SNMP server                [ON]

[+] HTTP Options:
    Always serving EXE         [OFF]
    Serving EXE                [OFF]
    Serving HTML               [OFF]
    Upstream Proxy             [OFF]

[+] Poisoning Options:
    Analyze Mode               [OFF]
    Force WPAD auth            [OFF]
    Force Basic Auth           [OFF]
    Force LM downgrade         [OFF]
    Force ESS downgrade        [OFF]

[+] Generic Options:
    Responder NIC              [tun0]
    Responder IP               [10.10.14.189]
    Responder IPv6             [fe80::7521:fe52:19b0:d971]
    Challenge set              [random]
    Don't Respond To Names     ['ISATAP', 'ISATAP.LOCAL']
    Don't Respond To MDNS TLD  ['_DOSVC']
    TTL for poisoned response  [default]

[+] Current Session Variables:
    Responder Machine Name     [WIN-USIRZSEKUL3]
    Responder Domain Name      [J2JL.LOCAL]
    Responder DCE-RPC Port     [49503]

[*] Version: Responder 3.2.2.0
[*] Author: Laurent Gaffie, <lgaffie@secorizon.com>

[+] Listening for events...      
```

![[Pasted image 20260709031522.png]]


![[Pasted image 20260709031449.png]]

![[Pasted image 20260709031712.png]]


![[Pasted image 20260709032228.png]]



![[Pasted image 20260709032351.png]]


![[Pasted image 20260709032649.png]]


