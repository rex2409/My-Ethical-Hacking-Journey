# nmap
```
┌──(kali㉿kali)-[~/PG/spx]
└─$ nmap -p- --min-rate 10000 192.168.168.108
Starting Nmap 7.95 ( https://nmap.org ) at 2025-05-10 22:12 EDT
Nmap scan report for 192.168.168.108
Host is up (0.048s latency).
Not shown: 65533 filtered tcp ports (no-response)
PORT   STATE SERVICE
22/tcp open  ssh
80/tcp open  http

Nmap done: 1 IP address (1 host up) scanned in 13.56 seconds
                                                                                                                                                                                                                                                                                                                            
┌──(kali㉿kali)-[~/PG/spx]
└─$ nmap -p 22,80 -sCV 192.168.168.108       
Starting Nmap 7.95 ( https://nmap.org ) at 2025-05-10 22:13 EDT
Nmap scan report for 192.168.168.108
Host is up (0.047s latency).

PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.9p1 Ubuntu 3ubuntu0.10 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   256 b9:bc:8f:01:3f:85:5d:f9:5c:d9:fb:b6:15:a0:1e:74 (ECDSA)
|_  256 53:d9:7f:3d:22:8a:fd:57:98:fe:6b:1a:4c:ac:79:67 (ED25519)
80/tcp open  http    Apache httpd 2.4.52 ((Ubuntu))
|_http-server-header: Apache/2.4.52 (Ubuntu)
|_http-title: Tiny File Manager
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 12.72 seconds
```

![Pasted image 20250511101426](<0. Attachments/Pasted image 20250511101426.png>)

# web enum
![Pasted image 20250511101530](<0. Attachments/Pasted image 20250511101530.png>)

![Pasted image 20250511102610](<0. Attachments/Pasted image 20250511102610.png>)

![Pasted image 20250511102822](<0. Attachments/Pasted image 20250511102822.png>)

![Pasted image 20250511103906](<0. Attachments/Pasted image 20250511103906.png>)

# exploit
[GitHub - BubblyCola/CVE_2024_42007: Python exploit for CVE-2024-42007 — a path traversal vulnerability in php-spx <= 0.4.15 that allows arbitrary file read via SPX_UI_URI parameter.](https://github.com/BubblyCola/CVE_2024_42007)

[Novel Escape from the SPX jungle - Path traversal in PHP-SPX (CVE-2024-42007) - vsociety](https://www.vicarius.io/vsociety/posts/novel-escape-from-the-spx-jungle-path-traversal-in-php-spx-cve-2024-42007)

read the SPX key and change it in exploit
![Pasted image 20250511105218](<0. Attachments/Pasted image 20250511105218.png>)

they work but don't give substantial info

doing it via burpsuite now
![Pasted image 20250511110501](<0. Attachments/Pasted image 20250511110501.png>)

![Pasted image 20250511110629](<0. Attachments/Pasted image 20250511110629.png>)

# hash cracking
![Pasted image 20250511150318](<0. Attachments/Pasted image 20250511150318.png>)

using the /etc/passwd
we can try bruteforcing ssh

did not work, instead we can go back to webapp and try logging in

after logging in we can upload a rev.php

# initial access
![Pasted image 20250511152259](<0. Attachments/Pasted image 20250511152259.png>)

changed profiler using password lowprofile

# local.txt
![Pasted image 20250511152617](<0. Attachments/Pasted image 20250511152617.png>)

# priv esc enum
![Pasted image 20250511152643](<0. Attachments/Pasted image 20250511152643.png>)

# priv esc
there is a makefile, we will edit this to obtain root
we need to write the exploit in this manner
![Pasted image 20250511153427](<0. Attachments/Pasted image 20250511153427.png>)

something like this
![Pasted image 20250511153624](<0. Attachments/Pasted image 20250511153624.png>)

run the superuser command
![Pasted image 20250511153938](<0. Attachments/Pasted image 20250511153938.png>)

![Pasted image 20250511154027](<0. Attachments/Pasted image 20250511154027.png>)

# root.txt
![Pasted image 20250511154135](<0. Attachments/Pasted image 20250511154135.png>)

