<h1>Utilization of the SMBmap Tool</h1>


<h2>Description</h2>
This project consists of using SMBMap as a Kali Linux tool to enumerate share drives across a domain. SMBMap also allows the abilities to list drive permissions, share contents, upload & download functionality, file name auto-download pattern matching, and even execution of remote commands which I will provide an example of down below.
<br />
<br />

Disclaimer: The Kali Linux user machine and target machine used in this project was provided to me by INE for educational purposes. The misuse of the information in this project lab can result in criminal charges brought against the individual/individuals in question.
<br />


<h2>Languages and Utilities Used</h2>

- <b>Nmap</b>
- <b>SMBMap</b>


<h2>Environments Used </h2>

- <b>Kali Linux</b>

<h2>Project walk-through:</h2>

<p align="left">
Run Nmap scan against target machine IP: <br/>
- It looks like the target has multiple tcp ports open with SMB (port 445) being one of the open ports. <br/>
<br/>
Command: nmap 10.3.21.33
 <br/>
<br/>
<img src="https://i.imgur.com/MfX2Fc9.png" height="80%" width="80%" alt="SMB Nmap Scripting" class="center"/>
<br />
<br />
<br />
<br />
<br />
<br />
<br />
Run Nmap script on port 445 to enumerate SMB protocols and dialects: <br/>
- We can see that SMB version 1 is a dialect which may be quite dangerous. <br/>
<br/>
Command: nmap 10.3.21.33 -p 445 --script smb-protocols
<br/>
<br/>
<img src="https://i.imgur.com/wp0D99U.png" height="80%" width="80%" alt="SMB Nmap Scripting" class="center"/>
<br />
<br />
<br />
<br />
<br />
<br />
<br />
Knowing that SMBv1 is being used as a dialect, we will use SMBMap to check if a null session is allowed: <br/>
- It looks like the guest session did in fact connect, and you can see a list of shares that were found.  We can then see that the guest user has read access to the IPC$ and print$ shares. <br/>
<br/>
Command: smbmap -u guest -p "" -d . -H 10.3.21.33
<br/>
<br/>
<img src="https://i.imgur.com/9pkTdmH.png" height="80%" width="80%" alt="SMB Nmap Scripting" class="center"/>
<br />
<br />
<br />
<br />
<br />
<br />
<br />
We will now use SMBMap to login in with administrator along with a password which was provided by INE: <br/>
- Now we can see that the administrator user has different permissions such as read, write access for multiple shares. <br/>
<br/>
Command: smbmap -u administrator -p *password_not_shown* -d . -H 10.3.21.33
<br/>
<br/>
<img src="https://i.imgur.com/1PiKpIL.png" height="80%" width="80%" alt="SMB Nmap Scripting" class="center"/>
<br />
<br />
<br />
<br />
<br />
<br />
<br />

</p>

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
