nmap
```
┌──(kali㉿kali)-[~/HTB/jeeves]
└─$ sudo nmap -T5 -p- -A -oN nmap 10.129.228.112
[sudo] password for kali: 
Starting Nmap 7.95 ( https://nmap.org ) at 2025-01-16 19:03 EST
Nmap scan report for 10.129.228.112
Host is up (0.046s latency).
Not shown: 65531 filtered tcp ports (no-response)
PORT      STATE SERVICE      VERSION
80/tcp    open  http         Microsoft IIS httpd 10.0
| http-methods: 
|_  Potentially risky methods: TRACE
|_http-title: Ask Jeeves
135/tcp   open  msrpc        Microsoft Windows RPC
445/tcp   open  microsoft-ds Microsoft Windows 7 - 10 microsoft-ds (workgroup: WORKGROUP)
50000/tcp open  http         Jetty 9.4.z-SNAPSHOT
|_http-title: Error 404 Not Found
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Device type: general purpose
Running (JUST GUESSING): Microsoft Windows 2008|7|10 (89%)
OS CPE: cpe:/o:microsoft:windows_server_2008:r2 cpe:/o:microsoft:windows_7 cpe:/o:microsoft:windows_10
Aggressive OS guesses: Microsoft Windows 7 or Windows Server 2008 R2 (89%), Microsoft Windows 10 1607 (87%), Microsoft Windows Server 2008 R2 (87%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 2 hops
Service Info: Host: JEEVES; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
|_smb2-time: Protocol negotiation failed (SMB2)

TRACEROUTE (using port 80/tcp)
HOP RTT      ADDRESS
1   46.31 ms 10.10.14.1
2   46.41 ms 10.129.228.112

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 192.45 seconds
```

```
┌──(kali㉿kali)-[~/HTB/jeeves]
└─$ dirsearch -u http://10.129.228.112/      
/usr/lib/python3/dist-packages/dirsearch/dirsearch.py:23: DeprecationWarning: pkg_resources is deprecated as an API. See https://setuptools.pypa.io/en/latest/pkg_resources.html
  from pkg_resources import DistributionNotFound, VersionConflict

  _|. _ _  _  _  _ _|_    v0.4.3
 (_||| _) (/_(_|| (_| )

Extensions: php, aspx, jsp, html, js | HTTP method: GET | Threads: 25 | Wordlist size: 11460

Output File: /home/kali/HTB/jeeves/reports/http_10.129.228.112/__25-01-16_19-13-58.txt

Target: http://10.129.228.112/

[19:13:58] Starting: 
[19:13:59] 403 -  312B  - /%2e%2e//google.com                               
[19:14:00] 403 -  312B  - /.%2e/%2e%2e/%2e%2e/%2e%2e/etc/passwd             
[19:14:23] 403 -  312B  - /\..\..\..\..\..\..\..\..\..\etc\passwd           
[19:15:06] 403 -  312B  - /cgi-bin/.%2e/%2e%2e/%2e%2e/%2e%2e/etc/passwd     
[19:15:24] 200 -   50B  - /error.html                                       
                                                                             
Task Completed

┌──(kali㉿kali)-[~/HTB/jeeves]
└─$ gobuster dir -u http://10.129.228.112:50000/ -w /home/kali/offsec/SecLists/Discovery/Web-Content/directory-list-2.3-medium.txt -k -t 30
===============================================================
Gobuster v3.6
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.129.228.112:50000/
[+] Method:                  GET
[+] Threads:                 30
[+] Wordlist:                /home/kali/offsec/SecLists/Discovery/Web-Content/directory-list-2.3-medium.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.6
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
/askjeeves            (Status: 302) [Size: 0] [--> http://10.129.228.112:50000/askjeeves/]
Progress: 220559 / 220560 (100.00%)
===============================================================
Finished
===============================================================
```

![Pasted image 20250117080922](<0. Attachments/Pasted image 20250117080922.png>)

![Pasted image 20250117081035](<0. Attachments/Pasted image 20250117081035.png>)

![Pasted image 20250117081335](<0. Attachments/Pasted image 20250117081335.png>)

![Pasted image 20250117081917](<0. Attachments/Pasted image 20250117081917.png>)

Click on create item --> Freestyle project --> scroll down and choose Execute windows batch command under build dropdown --> click save
![Pasted image 20250117090419](<0. Attachments/Pasted image 20250117090419.png>)

then go to click build --> click the built version --> go to console output
![Pasted image 20250117090608](<0. Attachments/Pasted image 20250117090608.png>)

a typical groovyscript
![Pasted image 20250117090834](<0. Attachments/Pasted image 20250117090834.png>)

we went here by clicking manage Jenkins --> script console (From the dashboard)

![Pasted image 20250117091050](<0. Attachments/Pasted image 20250117091050.png>)

The above are 2 methods use anything, 2nd one looks more convenient
![Pasted image 20250117091231](<0. Attachments/Pasted image 20250117091231.png>)

priv esc
![Pasted image 20250117103150](<0. Attachments/Pasted image 20250117103150.png>)

now we can obtain the password via `keepass2john`
![Pasted image 20250117103818](<0. Attachments/Pasted image 20250117103818.png>)

![Pasted image 20250117103838](<0. Attachments/Pasted image 20250117103838.png>)

now to check the db using kpcli
![Pasted image 20250117104053](<0. Attachments/Pasted image 20250117104053.png>)

```
kpcli:/> show -f 0

 Path: /CEH/
Title: Backup stuff
Uname: ?
 Pass: aad3b435b51404eeaad3b435b51404ee:e0fb1fb85756c24235ff238cbe81fe00
  URL: 
Notes: 

kpcli:/> show -f 1

 Path: /CEH/
Title: Bank of America
Uname: Michael321
 Pass: 12345
  URL: https://www.bankofamerica.com
Notes: 

kpcli:/> show -f 2

 Path: /CEH/
Title: DC Recovery PW
Uname: administrator
 Pass: S1TjAtJHKsugh9oC4VZl
  URL: 
Notes: 

kpcli:/> show -f 3

 Path: /CEH/
Title: EC-Council
Uname: hackerman123
 Pass: pwndyouall!
  URL: https://www.eccouncil.org/programs/certified-ethical-hacker-ceh
Notes: Personal login

kpcli:/> show -f 4

 Path: /CEH/
Title: It's a secret
Uname: admin
 Pass: F7WhTrSFDKB6sxHU1cUn
  URL: http://localhost:8180/secret.jsp
Notes: 

kpcli:/> show -f 5

 Path: /CEH/
Title: Jenkins admin
Uname: admin
 Pass: 
  URL: http://localhost:8080
Notes: We don't even need creds! Unhackable! 

kpcli:/> show -f 6

 Path: /CEH/
Title: Keys to the kingdom
Uname: bob
 Pass: lCEUnYPjNfIuPZSzOySA
  URL: 
Notes: 

kpcli:/> show -f 7

 Path: /CEH/
Title: Walmart.com
Uname: anonymous
 Pass: Password
  URL: http://www.walmart.com
Notes: Getting my shopping on
```
this looks like an ntlm hash
![Pasted image 20250117104259](<0. Attachments/Pasted image 20250117104259.png>)

lets try it
![Pasted image 20250117104458](<0. Attachments/Pasted image 20250117104458.png>)

now we can enter and obtain flag
![Pasted image 20250117104950](<0. Attachments/Pasted image 20250117104950.png>)

weird flag
![Pasted image 20250117105243](<0. Attachments/Pasted image 20250117105243.png>)

