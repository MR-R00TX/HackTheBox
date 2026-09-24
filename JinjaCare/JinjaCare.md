# JinjaCare CTF Write-up: From HTML Injection to SSTI and RCE

## Introduction
In this write-up, we will see how a simple HTML Injection in the "JinjaCare" challenge leads to a Server-Side Template Injection (SSTI) vulnerability. Finally, we will use Remote Code Execution (RCE) to find and read the flag.

## Step 1: Account Creation and Dashboard Access
First, we need to create a new account on the web application and sign in to the dashboard. 

<img width="1604" height="627" alt="image" src="https://github.com/user-attachments/assets/636388a3-9cff-4864-8d01-d3babe3a8cdb" />

<img width="1903" height="856" alt="image" src="https://github.com/user-attachments/assets/3fe6ab07-2aba-473e-a928-a2d0e0195f48" />

<img width="1908" height="892" alt="image" src="https://github.com/user-attachments/assets/ae0e493d-85cf-4254-aa84-c3eed5715b0f" />

<img width="1471" height="590" alt="image" src="https://github.com/user-attachments/assets/f4b76069-ce36-43e5-9129-7423e76fbb45" />

<img width="1904" height="815" alt="image" src="https://github.com/user-attachments/assets/9e31e0df-999a-47cd-a602-dceb346e4fcd" />

<img width="1654" height="931" alt="image" src="https://github.com/user-attachments/assets/dd70c87f-4821-4250-a79b-e3e22c7550e2" />

## Step 2: Testing for HTML Injection
After going to the dashboard, we find an option to change our name in the profile section. To test for HTML injection, we enter the following payload into the name field:

```html
<u> jack </u>
<img width="1763" height="890" alt="image" src="https://github.com/user-attachments/assets/9ee81a31-5191-422e-a5f8-2f755898f74e" />


After saving the name and downloading the certificate, we can see that the HTML tag worked successfully. The name "jack" has an underline. This confirms that HTML injection is possible.

<img width="1591" height="775" alt="image" src="https://github.com/user-attachments/assets/47cbd652-3f20-415a-b8e2-fadf8a9a8a11" />


Step 3: Verifying SSTI (Server-Side Template Injection)
Since HTML injection works, we decide to test for SSTI. We enter a basic template logic value (like a simple math problem) as our name and save the changes.

<img width="1676" height="918" alt="image" src="https://github.com/user-attachments/assets/cca37c08-62f3-462f-a1c0-aba1a33ce31b" />


When we download the certificate again, we see that the backend template engine calculated and executed our logic. This proves that the application is vulnerable to Server-Side Template Injection (SSTI).

<img width="1670" height="904" alt="image" src="https://github.com/user-attachments/assets/b5fbc2a0-ba9a-4120-b480-597c8c89f311" />


Step 4: Remote Code Execution (RCE) and Getting the Flag
Now that SSTI is confirmed, we can use a Jinja2 template payload to run system commands (RCE). First, we use this payload to list the files in the root directory:

Python
{{ self.__init__.__globals__.__builtins__.__import__('os').popen('ls /').read() }}
<img width="1628" height="929" alt="image" src="https://github.com/user-attachments/assets/abb3841f-3cd7-40c1-9ae5-63dd498d6e66" />

<img width="1535" height="930" alt="image" src="https://github.com/user-attachments/assets/3c0adebf-f6b7-49e5-9f12-4994e598ea97" />

After running this command, we look at the certificate and see a file named flag.txt in the root directory. Now, we use the cat command in our final payload to read the contents of this file:

Python
{{ self.__init__.__globals__.__builtins__.__import__('os').popen('cat /flag.txt').read() }}
After downloading the certificate one last time, we successfully get our flag!

<img width="1201" height="739" alt="image" src="https://github.com/user-attachments/assets/82024a00-5500-4b5a-a1ff-147404c56eee" />


Conclusion
This challenge shows how a simple HTML injection can turn into a critical SSTI vulnerability if user inputs are not properly sanitized. This flaw eventually allows an attacker to take full control of the server using RCE.
