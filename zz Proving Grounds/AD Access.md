practice test using these machines:
This one
[Linux Boolean](Linux%20Boolean.md)
[Windows Hutch](Windows%20Hutch.md)
[Linux Clue](Linux%20Clue.md)

nmap
```
┌──(kali㉿kali)-[~/PG/access-ad]
└─$ nmap -p- --min-rate 10000 192.168.174.187    
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-15 22:14 EST
Nmap scan report for 192.168.174.187
Host is up (0.042s latency).
Not shown: 65509 closed tcp ports (reset)
PORT      STATE SERVICE
53/tcp    open  domain
80/tcp    open  http
88/tcp    open  kerberos-sec
135/tcp   open  msrpc
139/tcp   open  netbios-ssn
389/tcp   open  ldap
443/tcp   open  https
445/tcp   open  microsoft-ds
464/tcp   open  kpasswd5
593/tcp   open  http-rpc-epmap
636/tcp   open  ldapssl
3268/tcp  open  globalcatLDAP
3269/tcp  open  globalcatLDAPssl
5985/tcp  open  wsman
9389/tcp  open  adws
47001/tcp open  winrm
49664/tcp open  unknown
49665/tcp open  unknown
49666/tcp open  unknown
49668/tcp open  unknown
49669/tcp open  unknown
49670/tcp open  unknown
49671/tcp open  unknown
49674/tcp open  unknown
49679/tcp open  unknown
49701/tcp open  unknown

Nmap done: 1 IP address (1 host up) scanned in 9.02 seconds


┌──(kali㉿kali)-[~/PG/access-ad]
└─$ nmap -p 53,80,88,135,139,389,443,445,464,593,636,3268,3269,5985,9389,47001 -sCV 192.168.174.187
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-15 22:16 EST
Nmap scan report for 192.168.174.187
Host is up (0.039s latency).

PORT      STATE SERVICE       VERSION
53/tcp    open  domain        Simple DNS Plus
80/tcp    open  http          Apache httpd 2.4.48 ((Win64) OpenSSL/1.1.1k PHP/8.0.7)
|_http-server-header: Apache/2.4.48 (Win64) OpenSSL/1.1.1k PHP/8.0.7
| http-methods: 
|_  Potentially risky methods: TRACE
|_http-title: Access The Event
88/tcp    open  kerberos-sec  Microsoft Windows Kerberos (server time: 2025-02-16 03:17:08Z)
135/tcp   open  msrpc         Microsoft Windows RPC
139/tcp   open  netbios-ssn   Microsoft Windows netbios-ssn
389/tcp   open  ldap          Microsoft Windows Active Directory LDAP (Domain: access.offsec0., Site: Default-First-Site-Name)
443/tcp   open  ssl/http      Apache httpd 2.4.48 ((Win64) OpenSSL/1.1.1k PHP/8.0.7)
|_http-server-header: Apache/2.4.48 (Win64) OpenSSL/1.1.1k PHP/8.0.7
| ssl-cert: Subject: commonName=localhost
| Not valid before: 2009-11-10T23:48:47
|_Not valid after:  2019-11-08T23:48:47
|_http-title: Access The Event
| http-methods: 
|_  Potentially risky methods: TRACE
| tls-alpn: 
|_  http/1.1
|_ssl-date: TLS randomness does not represent time
445/tcp   open  microsoft-ds?
464/tcp   open  kpasswd5?
593/tcp   open  ncacn_http    Microsoft Windows RPC over HTTP 1.0
636/tcp   open  tcpwrapped
3268/tcp  open  ldap          Microsoft Windows Active Directory LDAP (Domain: access.offsec0., Site: Default-First-Site-Name)
3269/tcp  open  tcpwrapped
5985/tcp  open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
9389/tcp  open  mc-nmf        .NET Message Framing
47001/tcp open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
Service Info: Host: SERVER; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
|_clock-skew: 2s
| smb2-time: 
|   date: 2025-02-16T03:17:16
|_  start_date: N/A
| smb2-security-mode: 
|   3:1:1: 
|_    Message signing enabled and required

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 26.20 seconds
```

```
┌──(kali㉿kali)-[~/PG/access-ad]
└─$ dirsearch -u http://192.168.174.187/
/usr/lib/python3/dist-packages/dirsearch/dirsearch.py:23: DeprecationWarning: pkg_resources is deprecated as an API. See https://setuptools.pypa.io/en/latest/pkg_resources.html
  from pkg_resources import DistributionNotFound, VersionConflict

  _|. _ _  _  _  _ _|_    v0.4.3
 (_||| _) (/_(_|| (_| )

Extensions: php, aspx, jsp, html, js | HTTP method: GET | Threads: 25 | Wordlist size: 11460

Output File: /home/kali/PG/access-ad/reports/http_192.168.174.187/__25-02-15_22-22-28.txt

Target: http://192.168.174.187/

[22:22:28] Starting: 
[22:22:29] 403 -  304B  - /%C0%AE%C0%AE%C0%AF
[22:22:29] 403 -  304B  - /%3f/                                             
[22:22:29] 403 -  304B  - /%ff                                              
[22:22:34] 403 -  304B  - /.ht_wsr.txt                                      
[22:22:34] 403 -  304B  - /.htaccess.bak1                                   
[22:22:34] 403 -  304B  - /.htaccess.orig                                   
[22:22:34] 403 -  304B  - /.htaccess.sample                                 
[22:22:34] 403 -  304B  - /.htaccess.save                                   
[22:22:34] 403 -  304B  - /.htaccess_sc                                     
[22:22:34] 403 -  304B  - /.htaccessBAK
[22:22:34] 403 -  304B  - /.htaccessOLD
[22:22:34] 403 -  304B  - /.htaccessOLD2                                    
[22:22:34] 403 -  304B  - /.htm
[22:22:34] 403 -  304B  - /.htaccess_extra
[22:22:34] 403 -  304B  - /.html                                            
[22:22:34] 403 -  304B  - /.htaccess_orig
[22:22:35] 403 -  304B  - /.htpasswds                                       
[22:22:35] 403 -  304B  - /.httr-oauth                                      
[22:22:35] 403 -  304B  - /.htpasswd_test                                   
[22:23:14] 301 -  343B  - /assets  ->  http://192.168.174.187/assets/       
[22:23:14] 200 -    2KB - /assets/                                          
[22:23:22] 403 -  304B  - /cgi-bin/                                         
[22:23:23] 200 -    2KB - /cgi-bin/printenv.pl                              
[22:23:46] 503 -  404B  - /examples/jsp/%252e%252e/%252e%252e/manager/html/ 
[22:23:46] 503 -  404B  - /examples/jsp/index.html                          
[22:23:46] 503 -  404B  - /examples/jsp/snp/snoop.jsp
[22:23:46] 503 -  404B  - /examples/
[22:23:46] 503 -  404B  - /examples/servlets/index.html                     
[22:23:46] 503 -  404B  - /examples/servlet/SnoopServlet
[22:23:46] 503 -  404B  - /examples                                         
[22:23:46] 503 -  404B  - /examples/servlets/servlet/RequestHeaderExample   
[22:23:46] 503 -  404B  - /examples/websocket/index.xhtml                   
[22:23:46] 503 -  404B  - /examples/servlets/servlet/CookieExample          
[22:23:49] 301 -  342B  - /forms  ->  http://192.168.174.187/forms/         
[22:23:59] 403 -  304B  - /index.php::$DATA                                 
[22:24:30] 403 -  423B  - /phpmyadmin                                       
[22:24:33] 403 -  423B  - /phpmyadmin/ChangeLog                             
[22:24:33] 403 -  423B  - /phpmyadmin/docs/html/index.html
[22:24:33] 403 -  423B  - /phpmyadmin/                                      
[22:24:34] 403 -  423B  - /phpmyadmin/index.php                             
[22:24:34] 403 -  423B  - /phpmyadmin/phpmyadmin/index.php                  
[22:24:34] 403 -  423B  - /phpmyadmin/scripts/setup.php
[22:24:34] 403 -  423B  - /phpmyadmin/doc/html/index.html                   
[22:24:34] 403 -  423B  - /phpmyadmin/README                                
[22:24:47] 403 -  423B  - /server-info                                      
[22:24:48] 403 -  423B  - /server-status                                    
[22:24:48] 403 -  423B  - /server-status/                                   
[22:25:05] 403 -  304B  - /Trace.axd::$DATA                                 
[22:25:07] 200 -  777B  - /uploads/                                         
[22:25:07] 301 -  344B  - /uploads  ->  http://192.168.174.187/uploads/     
[22:25:16] 403 -  304B  - /web.config::$DATA                                
[22:25:17] 403 -  423B  - /webalizer                                        
[22:25:17] 403 -  423B  - /webalizer/                                       
                                                                             
Task Completed 
```

![Pasted image 20250216112116](<0. Attachments/Pasted image 20250216112116.png>)

![Pasted image 20250216112451](<0. Attachments/Pasted image 20250216112451.png>)

It can be noticed that the server running on the machine is apache. So we could potentially upload a ".htaccess" file to the directory to let the server render my ".xxx" extension as PHP script.

![Pasted image 20250216131209](<0. Attachments/Pasted image 20250216131209.png>)

![Pasted image 20250216131143](<0. Attachments/Pasted image 20250216131143.png>)

![Pasted image 20250216131352](<0. Attachments/Pasted image 20250216131352.png>)

![Pasted image 20250216131528](<0. Attachments/Pasted image 20250216131528.png>)

![Pasted image 20250216131434](<0. Attachments/Pasted image 20250216131434.png>)

![Pasted image 20250216131559](<0. Attachments/Pasted image 20250216131559.png>)

![Pasted image 20250216132805](<0. Attachments/Pasted image 20250216132805.png>)

![Pasted image 20250216132927](<0. Attachments/Pasted image 20250216132927.png>)

![Pasted image 20250216133054](<0. Attachments/Pasted image 20250216133054.png>)
svc_mssql --> trustno1

![Pasted image 20250216133347](<0. Attachments/Pasted image 20250216133347.png>)

https://github.com/antonioCoco/RunasCs

![Pasted image 20250216141540](<0. Attachments/Pasted image 20250216141540.png>)

![Pasted image 20250216142856](<0. Attachments/Pasted image 20250216142856.png>)

![Pasted image 20250216142925](<0. Attachments/Pasted image 20250216142925.png>)

![Pasted image 20250216142947](<0. Attachments/Pasted image 20250216142947.png>)

https://github.com/CsEnox/SeManageVolumeExploit

![Pasted image 20250216145625](<0. Attachments/Pasted image 20250216145625.png>)

![Pasted image 20250216145732](<0. Attachments/Pasted image 20250216145732.png>)

![Pasted image 20250216150035](<0. Attachments/Pasted image 20250216150035.png>)

![Pasted image 20250216150052](<0. Attachments/Pasted image 20250216150052.png>)

3 Major things
1. Service accounts can be kerberoasted
2. sometimes we need to use Runas tool if we cant go anywhere else
3. SeManageVolume can allow us to write into all files.

Find out
1. How the hell are we supposed to know above
2. why that particular dll
3. why does systeminfo call that dll

[Proving Grounds Practice — Access | by Dpsypher | Medium](https://medium.com/@Dpsypher/proving-grounds-practice-access-b95d3146cfe9)
[Proving Grounds Practice | Active Directory Box: Access | by J0s3phKg | System Weakness](https://systemweakness.com/proving-grounds-practise-active-directory-box-access-79b1fe662f4d)
[Access | SecJournal](https://rouvin.gitbook.io/ibreakstuff/writeups/proving-grounds-practice/windows/access)

