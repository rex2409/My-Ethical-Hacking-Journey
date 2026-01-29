```
┌──(kali㉿kali)-[~/PG/codo]
└─$ nmap -p- --min-rate 10000 192.168.134.23
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-17 01:36 EST
Nmap scan report for 192.168.134.23
Host is up (0.046s latency).
Not shown: 65533 filtered tcp ports (no-response)
PORT   STATE SERVICE
22/tcp open  ssh
80/tcp open  http

Nmap done: 1 IP address (1 host up) scanned in 13.55 seconds
                                                                                                                                                         
┌──(kali㉿kali)-[~/PG/codo]
└─$ nmap -p 22,80 -sCV 192.168.134.23       
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-17 01:37 EST
Nmap scan report for 192.168.134.23
Host is up (0.084s latency).

Bug in http-generator: no string output.
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.7 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 62:36:1a:5c:d3:e3:7b:e1:70:f8:a3:b3:1c:4c:24:38 (RSA)
|   256 ee:25:fc:23:66:05:c0:c1:ec:47:c6:bb:00:c7:4f:53 (ECDSA)
|_  256 83:5c:51:ac:32:e5:3a:21:7c:f6:c2:cd:93:68:58:d8 (ED25519)
80/tcp open  http    Apache httpd 2.4.41 ((Ubuntu))
|_http-title: All topics | CODOLOGIC
| http-cookie-flags: 
|   /: 
|     PHPSESSID: 
|_      httponly flag not set
|_http-server-header: Apache/2.4.41 (Ubuntu)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 13.33 seconds
```

```
┌──(kali㉿kali)-[~/PG/codo]
└─$ dirsearch -u http://192.168.134.23/ 
/usr/lib/python3/dist-packages/dirsearch/dirsearch.py:23: DeprecationWarning: pkg_resources is deprecated as an API. See https://setuptools.pypa.io/en/latest/pkg_resources.html
  from pkg_resources import DistributionNotFound, VersionConflict

  _|. _ _  _  _  _ _|_    v0.4.3
 (_||| _) (/_(_|| (_| )

Extensions: php, aspx, jsp, html, js | HTTP method: GET | Threads: 25 | Wordlist size: 11460

Output File: /home/kali/PG/codo/reports/http_192.168.134.23/__25-02-17_01-38-55.txt

Target: http://192.168.134.23/

[01:38:56] Starting: 
[01:38:57] 200 -  105B  - /.babelrc                                         
[01:39:02] 403 -  279B  - /.ht_wsr.txt                                      
[01:39:02] 403 -  279B  - /.htaccess.bak1                                   
[01:39:02] 403 -  279B  - /.htaccess.save                                   
[01:39:02] 403 -  279B  - /.htaccess.sample                                 
[01:39:02] 403 -  279B  - /.htaccess.orig                                   
[01:39:02] 403 -  279B  - /.htaccess_extra
[01:39:02] 403 -  279B  - /.htaccess_orig
[01:39:02] 403 -  279B  - /.htaccessOLD
[01:39:02] 403 -  279B  - /.htaccessBAK                                     
[01:39:02] 403 -  279B  - /.htaccess_sc
[01:39:02] 403 -  279B  - /.htaccessOLD2                                    
[01:39:02] 403 -  279B  - /.html
[01:39:02] 403 -  279B  - /.htm                                             
[01:39:02] 403 -  279B  - /.htpasswd_test                                   
[01:39:02] 403 -  279B  - /.htpasswds                                       
[01:39:02] 403 -  279B  - /.httr-oauth
[01:39:06] 403 -  279B  - /.php                                             
[01:39:21] 301 -  316B  - /admin  ->  http://192.168.134.23/admin/          
[01:39:23] 200 -    2KB - /admin/                                           
[01:39:24] 200 -    2KB - /admin/index.php                                  
[01:39:24] 200 -    1KB - /admin/login.php                                  
[01:39:50] 301 -  316B  - /cache  ->  http://192.168.134.23/cache/          
[01:39:50] 200 -  489B  - /cache/                                           
[01:40:26] 200 -    8KB - /index.php                                        
[01:40:26] 200 -    4KB - /index.php/login/                                 
[01:41:09] 200 -   24KB - /README.md                                        
[01:41:15] 403 -  279B  - /server-status                                    
[01:41:15] 403 -  279B  - /server-status/                                   
[01:41:21] 301 -  316B  - /sites  ->  http://192.168.134.23/sites/          
                                                                             
Task Completed
```

![Pasted image 20250217143824](<0. Attachments/Pasted image 20250217143824.png>)

tried admin --> admin
![Pasted image 20250217144949](<0. Attachments/Pasted image 20250217144949.png>)

![Pasted image 20250217150506](<0. Attachments/Pasted image 20250217150506.png>)

![Pasted image 20250217150447](<0. Attachments/Pasted image 20250217150447.png>)

![Pasted image 20250217150432](<0. Attachments/Pasted image 20250217150432.png>)

![Pasted image 20250217150416](<0. Attachments/Pasted image 20250217150416.png>)

![Pasted image 20250217150739](<0. Attachments/Pasted image 20250217150739.png>)

