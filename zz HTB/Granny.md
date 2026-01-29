nmap
```
┌──(kali㉿kali)-[~/HTB/granny]
└─$ sudo nmap -T5 -p- -A -oN nmap 10.129.250.197
[sudo] password for kali: 
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-12-24 01:13 EST
Nmap scan report for 10.129.250.197
Host is up (0.083s latency).
Not shown: 65534 filtered tcp ports (no-response)
PORT   STATE SERVICE VERSION
80/tcp open  http    Microsoft IIS httpd 6.0
|_http-title: Under Construction
|_http-server-header: Microsoft-IIS/6.0
| http-webdav-scan: 
|   Public Options: OPTIONS, TRACE, GET, HEAD, DELETE, PUT, POST, COPY, MOVE, MKCOL, PROPFIND, PROPPATCH, LOCK, UNLOCK, SEARCH
|   Server Date: Tue, 24 Dec 2024 06:16:15 GMT
|   Server Type: Microsoft-IIS/6.0
|   WebDAV type: Unknown
|_  Allowed Methods: OPTIONS, TRACE, GET, HEAD, DELETE, COPY, MOVE, PROPFIND, PROPPATCH, SEARCH, MKCOL, LOCK, UNLOCK
| http-methods: 
|_  Potentially risky methods: TRACE DELETE COPY MOVE PROPFIND PROPPATCH SEARCH MKCOL LOCK UNLOCK PUT
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Device type: general purpose
Running (JUST GUESSING): Microsoft Windows 2003|2008|XP|2000 (90%)
OS CPE: cpe:/o:microsoft:windows_server_2003::sp1 cpe:/o:microsoft:windows_server_2003::sp2 cpe:/o:microsoft:windows_server_2008::sp2 cpe:/o:microsoft:windows_xp::sp3 cpe:/o:microsoft:windows_2000::sp4
Aggressive OS guesses: Microsoft Windows Server 2003 SP1 or SP2 (90%), Microsoft Windows Server 2008 Enterprise SP2 (90%), Microsoft Windows Server 2003 SP2 (89%), Microsoft Windows 2003 SP2 (88%), Microsoft Windows XP SP3 (88%), Microsoft Windows 2000 SP4 or Windows XP Professional SP1 (88%), Microsoft Windows XP SP2 or SP3 (86%), Microsoft Windows XP (85%), Microsoft Windows Server 2003 (85%), Microsoft Windows XP SP2 (85%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 2 hops
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

TRACEROUTE (using port 80/tcp)
HOP RTT      ADDRESS
1   82.93 ms 10.10.14.1
2   82.96 ms 10.129.250.197

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 139.28 seconds
```

directory busting
```
┌──(kali㉿kali)-[~/HTB/granny]
└─$ dirsearch -u http://10.129.250.197 -x 400-599 
/usr/lib/python3/dist-packages/dirsearch/dirsearch.py:23: DeprecationWarning: pkg_resources is deprecated as an API. See https://setuptools.pypa.io/en/latest/pkg_resources.html
  from pkg_resources import DistributionNotFound, VersionConflict

  _|. _ _  _  _  _ _|_    v0.4.3
 (_||| _) (/_(_|| (_| )

Extensions: php, aspx, jsp, html, js | HTTP method: GET | Threads: 25 | Wordlist size: 11460

Output File: /home/kali/HTB/granny/reports/http_10.129.250.197/_24-12-24_01-21-08.txt

Target: http://10.129.250.197/

[01:21:08] Starting: 
[01:21:29] 301 -  156B  - /_private  ->  http://10.129.250.197/%5Fprivate/  
[01:21:29] 200 -  252B  - /_private/                                        
[01:21:29] 200 -  765B  - /_vti_bin/                                        
[01:21:29] 301 -  158B  - /_vti_log  ->  http://10.129.250.197/%5Fvti%5Flog/
[01:21:29] 200 -    2KB - /_vti_inf.html
[01:21:29] 301 -  158B  - /_vti_bin  ->  http://10.129.250.197/%5Fvti%5Fbin/
[01:21:30] 200 -  195B  - /_vti_bin/_vti_aut/author.dll                     
[01:21:30] 200 -  195B  - /_vti_bin/_vti_adm/admin.dll
[01:21:30] 200 -   96B  - /_vti_bin/shtml.exe?_vti_rpc
[01:21:30] 200 -   96B  - /_vti_bin/shtml.dll                               
[01:21:30] 200 -  252B  - /_vti_log/                                        
[01:21:55] 301 -  161B  - /aspnet_client  ->  http://10.129.250.197/aspnet%5Fclient/
[01:21:55] 200 -  375B  - /aspnet_client/                                   
[01:22:31] 200 -  248B  - /images/                                          
[01:22:31] 301 -  152B  - /images  ->  http://10.129.250.197/images/        
[01:23:09] 200 -    2KB - /postinfo.html                                    
                                                                             
Task Completed
```

![Pasted image 20241224142637](<0. Attachments/Pasted image 20241224142637.png>)

after reading we can check the source code to see what is present

![Pasted image 20241224142746](<0. Attachments/Pasted image 20241224142746.png>)

```
┌──(kali㉿kali)-[~/HTB/granny]
└─$ nmap 10.129.250.197 -p 80 --script=http-frontpage-login
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-12-24 01:38 EST
Nmap scan report for 10.129.250.197
Host is up (0.099s latency).

PORT   STATE SERVICE
80/tcp open  http
| http-frontpage-login: 
|   VULNERABLE:
|   Frontpage extension anonymous login
|     State: VULNERABLE
|       Default installations of older versions of frontpage extensions allow anonymous logins which can lead to server compromise.
|       
|     References:
|_      http://insecure.org/sploits/Microsoft.frontpage.insecurities.html

Nmap done: 1 IP address (1 host up) scanned in 1.29 seconds
```

USE davtest

![Pasted image 20241224182344](<0. Attachments/Pasted image 20241224182344.png>)

![Pasted image 20241224205644](<0. Attachments/Pasted image 20241224205644.png>)

![Pasted image 20241224205738](<0. Attachments/Pasted image 20241224205738.png>)

![Pasted image 20241224211225](<0. Attachments/Pasted image 20241224211225.png>)

![Pasted image 20241224211415](<0. Attachments/Pasted image 20241224211415.png>)

![Pasted image 20241224211603](<0. Attachments/Pasted image 20241224211603.png>)

![Pasted image 20241224212942](<0. Attachments/Pasted image 20241224212942.png>)

![Pasted image 20241224213002](<0. Attachments/Pasted image 20241224213002.png>)

![Pasted image 20241224214004](<0. Attachments/Pasted image 20241224214004.png>)

![Pasted image 20241224214540](<0. Attachments/Pasted image 20241224214540.png>)

![Pasted image 20241224214517](<0. Attachments/Pasted image 20241224214517.png>)
