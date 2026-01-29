# nmap
```
┌──(kali㉿kali)-[~/PG/pc]
└─$ nmap -p- --min-rate 10000 192.168.237.210         
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-24 06:18 EST
Nmap scan report for 192.168.237.210
Host is up (0.070s latency).
Not shown: 65533 closed tcp ports (reset)
PORT     STATE SERVICE
22/tcp   open  ssh
8000/tcp open  http-alt

Nmap done: 1 IP address (1 host up) scanned in 8.54 seconds
                                                                                                                                                      
┌──(kali㉿kali)-[~/PG/pc]
└─$ nmap -p 22,8000 -sCV 192.168.237.210              
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-24 06:19 EST
Nmap scan report for 192.168.237.210
Host is up (0.079s latency).

PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.9 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 62:36:1a:5c:d3:e3:7b:e1:70:f8:a3:b3:1c:4c:24:38 (RSA)
|   256 ee:25:fc:23:66:05:c0:c1:ec:47:c6:bb:00:c7:4f:53 (ECDSA)
|_  256 83:5c:51:ac:32:e5:3a:21:7c:f6:c2:cd:93:68:58:d8 (ED25519)
8000/tcp open  http    ttyd 1.7.3-a2312cb (libwebsockets 3.2.0)
|_http-title: ttyd - Terminal
|_http-server-header: ttyd/1.7.3-a2312cb (libwebsockets/3.2.0)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 18.47 seconds
```
![Pasted image 20250224191957](<0. Attachments/Pasted image 20250224191957.png>)

# web enum
![Pasted image 20250224192106](<0. Attachments/Pasted image 20250224192106.png>)

![Pasted image 20250224192208](<0. Attachments/Pasted image 20250224192208.png>)

# priv esc enum
so pretty ez rev shell and upload linpeas we find some interesting things
![Pasted image 20250224194913](<0. Attachments/Pasted image 20250224194913.png>)
local port

![Pasted image 20250224195119](<0. Attachments/Pasted image 20250224195119.png>)
==very tricky find==

![Pasted image 20250224195239](<0. Attachments/Pasted image 20250224195239.png>)

# exploit
https://www.exploit-db.com/exploits/50983

removed some artifacts and changed this line (artifacts were '3D')
![Pasted image 20250224201654](<0. Attachments/Pasted image 20250224201654.png>)

# priv esc
![Pasted image 20250224201725](<0. Attachments/Pasted image 20250224201725.png>)

![Pasted image 20250224201740](<0. Attachments/Pasted image 20250224201740.png>)
