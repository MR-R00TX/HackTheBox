## 1. Initial Reconnaissance
The engagement began by accessing the provided target URL:

[https://154.57.164.79:30594/dashboard](https://154.57.164.79:30594/dashboard 

<img width="1601" height="373" alt="image" src="https://github.com/user-attachments/assets/4747a77f-a592-4a2c-bcd2-d653a9507fb2" />
 <img width="1886" height="606" alt="image" src="https://github.com/user-attachments/assets/d2d3999c-34bc-42a6-8093-f7ab7b9b2c86" />


Upon navigating to the target IP and port, we are presented with the main application interface. The initial enumeration focused on analyzing the dashboard's features, accessible endpoints, and any visible user roles or authentication mechanisms.

2. Vulnerability Discovery
Visual Reference: <img width="1918" height="962" alt="image" src="https://github.com/user-attachments/assets/d469fd87-a0c7-462a-b4d4-e2aa97f4c62c" />
<img width="1918" height="897" alt="image" src="https://github.com/user-attachments/assets/3c4f12e4-6c6a-4026-ba67-be810cb267aa" />

During the interaction with the dashboard, a potential attack vector was identified.

Vulnerability Type: [Insert Vulnerability Type Here - e.g., File Upload, SQLi, IDOR]

Observation: By manipulating the input or analyzing the server's response (as shown in the screenshots), it became evident that the application failed to properly sanitize user-supplied data.

Proof of Concept (PoC): [Insert the initial test payload or parameter changed here]

3. Exploitation Phase
Visual Reference: <img width="1889" height="931" alt="image" src="https://github.com/user-attachments/assets/bf434bac-5e6e-4506-a394-a8558f01a98b" />
 <img width="1350" height="829" alt="image" src="https://github.com/user-attachments/assets/a5f06138-7c0a-4d16-93ba-695f4f87b581" />




With the vulnerability confirmed, the next step was to craft a functional exploit to gain deeper access to the system.

Payload Used: [Insert the exact payload or script executed]

Execution: Sending the malicious request successfully bypassed the application's restrictions. As seen in the provided images, this granted us [e.g., Remote Code Execution (RCE) / Admin access].

4. Post-Exploitation & Flag Retrieval
Visual Reference:<img width="1862" height="942" alt="image" src="https://github.com/user-attachments/assets/fc1975cb-e45c-4b5f-a30a-3e922655d8a2" />
 <img width="1877" height="885" alt="image" src="https://github.com/user-attachments/assets/8a991666-546d-45f6-8771-7c2cef2786ae" />
<img width="1239" height="766" alt="image" src="https://github.com/user-attachments/assets/c553c225-b95c-4255-9754-5401b88bc3ad" />



Having established a foothold on the server, we proceeded to enumerate the internal file system to locate the objective.

Command Executed: [e.g., cat /root/flag.txt or ls -la]

Result: The final screenshots demonstrate successful retrieval of the target file.

Flag: [Insert Final Flag Here]
