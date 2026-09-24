# JinjaCare CTF Write-up: From HTML Injection to SSTI and RCE

## Introduction
In this write-up, we will see how a simple HTML Injection in the "JinjaCare" challenge leads to a Server-Side Template Injection (SSTI) vulnerability. Finally, we will use Remote Code Execution (RCE) to find and read the flag.

## Step 1: Account Creation and Dashboard Access
First, we need to create a new account on the web application and sign in to the dashboard. 

![[Pasted image 20260924122139.png]]
![[Pasted image 20260924124954.png]]
![[Pasted image 20260924122311.png]]
![[Pasted image 20260924124853.png]]
![[Pasted image 20260924122952.png]]
![[Pasted image 20260924123026.png]]

## Step 2: Testing for HTML Injection
After going to the dashboard, we find an option to change our name in the profile section. To test for HTML injection, we enter the following payload into the name field:

```html
<u> jack </u>
![[Pasted image 20260924123225.png]]

After saving the name and downloading the certificate, we can see that the HTML tag worked successfully. The name "jack" has an underline. This confirms that HTML injection is possible.

![[Pasted image 20260924123414.png]]

Step 3: Verifying SSTI (Server-Side Template Injection)
Since HTML injection works, we decide to test for SSTI. We enter a basic template logic value (like a simple math problem) as our name and save the changes.

![[Pasted image 20260924123656.png]]

When we download the certificate again, we see that the backend template engine calculated and executed our logic. This proves that the application is vulnerable to Server-Side Template Injection (SSTI).

![[Pasted image 20260924123809.png]]

Step 4: Remote Code Execution (RCE) and Getting the Flag
Now that SSTI is confirmed, we can use a Jinja2 template payload to run system commands (RCE). First, we use this payload to list the files in the root directory:

Python
{{ self.__init__.__globals__.__builtins__.__import__('os').popen('ls /').read() }}
![[Pasted image 20260924124038.png]]
![[Pasted image 20260924124148.png]]

After running this command, we look at the certificate and see a file named flag.txt in the root directory. Now, we use the cat command in our final payload to read the contents of this file:

Python
{{ self.__init__.__globals__.__builtins__.__import__('os').popen('cat /flag.txt').read() }}
After downloading the certificate one last time, we successfully get our flag!

![[Pasted image 20260924124540.png]]

Conclusion
This challenge shows how a simple HTML injection can turn into a critical SSTI vulnerability if user inputs are not properly sanitized. This flaw eventually allows an attacker to take full control of the server using RCE.
