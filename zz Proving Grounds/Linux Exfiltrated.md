```
┌──(kali㉿kali)-[~/PG/exfiltrated]
└─$ nmap -p- --min-rate 10000 192.168.202.163          
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-09 20:54 EST
Nmap scan report for 192.168.202.163
Host is up (0.039s latency).
Not shown: 65533 closed tcp ports (reset)
PORT   STATE SERVICE
22/tcp open  ssh
80/tcp open  http

Nmap done: 1 IP address (1 host up) scanned in 8.05 seconds
                                                                                                                                              
┌──(kali㉿kali)-[~/PG/exfiltrated]
└─$ nmap -p 22,80 -sCV 192.168.202.163                 
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-09 20:54 EST
Nmap scan report for 192.168.202.163
Host is up (0.039s latency).

PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.2 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 c1:99:4b:95:22:25:ed:0f:85:20:d3:63:b4:48:bb:cf (RSA)
|   256 0f:44:8b:ad:ad:95:b8:22:6a:f0:36:ac:19:d0:0e:f3 (ECDSA)
|_  256 32:e1:2a:6c:cc:7c:e6:3e:23:f4:80:8d:33:ce:9b:3a (ED25519)
80/tcp open  http    Apache httpd 2.4.41 ((Ubuntu))
| http-robots.txt: 7 disallowed entries 
| /backup/ /cron/? /front/ /install/ /panel/ /tmp/ 
|_/updates/
|_http-title: Did not follow redirect to http://exfiltrated.offsec/
|_http-server-header: Apache/2.4.41 (Ubuntu)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 9.29 seconds
```

```
┌──(kali㉿kali)-[~/PG/exfiltrated]
└─$ dirsearch -u http://192.168.202.163/ -x 300-500
/usr/lib/python3/dist-packages/dirsearch/dirsearch.py:23: DeprecationWarning: pkg_resources is deprecated as an API. See https://setuptools.pypa.io/en/latest/pkg_resources.html
  from pkg_resources import DistributionNotFound, VersionConflict

  _|. _ _  _  _  _ _|_    v0.4.3
 (_||| _) (/_(_|| (_| )

Extensions: php, aspx, jsp, html, js | HTTP method: GET | Threads: 25 | Wordlist size: 11460

Output File: /home/kali/PG/exfiltrated/reports/http_192.168.202.163/__25-02-09_21-19-00.txt

Target: http://192.168.202.163/

[21:19:00] Starting: 
[21:19:06] 200 -  247B  - /.gitignore                                       
[21:20:05] 200 -   15KB - /changelog.txt                                    
[21:20:11] 200 -    4KB - /CONTRIBUTING.md                                  
[21:20:29] 200 -  851B  - /favicon.ico                                      
[21:20:49] 200 -   12KB - /license.txt                                      
[21:21:09] 200 -    1KB - /panel.php                                        
[21:21:09] 200 -    1KB - /panel.jsp                                        
[21:21:09] 200 -    1KB - /panel/
[21:21:09] 200 -    1KB - /panel.html                                       
[21:21:09] 200 -    1KB - /panel.aspx                                       
[21:21:27] 200 -    5KB - /README.md                                        
[21:21:30] 200 -   94B  - /robots.txt                                       
[21:21:38] 200 -  212B  - /sitemap.xml                                      
                                                                             
Task Completed
```

![Pasted image 20250210100858](<0. Attachments/Pasted image 20250210100858.png>)

![Pasted image 20250210101236](<0. Attachments/Pasted image 20250210101236.png>)

![Pasted image 20250210101428](<0. Attachments/Pasted image 20250210101428.png>)

![Pasted image 20250210101740](<0. Attachments/Pasted image 20250210101740.png>)

![Pasted image 20250210102148](<0. Attachments/Pasted image 20250210102148.png>)

trying admin:admin works on subrion

![Pasted image 20250210115031](<0. Attachments/Pasted image 20250210115031.png>)

![Pasted image 20250210120706](<0. Attachments/Pasted image 20250210120706.png>)

renamed it as there was something blocking it

![Pasted image 20250210121321](<0. Attachments/Pasted image 20250210121321.png>)

```
python3 -c 'import pty; pty.spawn("/bin/bash")'
stty raw -echo ; fg ;reset ;
```

![Pasted image 20250210123139](<0. Attachments/Pasted image 20250210123139.png>)

![Pasted image 20250210123801](<0. Attachments/Pasted image 20250210123801.png>)

we see something called pwnkit so we check it out

![Pasted image 20250210123841](<0. Attachments/Pasted image 20250210123841.png>)

after using those steps

![Pasted image 20250210123941](<0. Attachments/Pasted image 20250210123941.png>)

![Pasted image 20250210124154](<0. Attachments/Pasted image 20250210124154.png>)

