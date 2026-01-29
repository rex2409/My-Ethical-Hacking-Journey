# nmap
```
┌──(kali㉿kali)-[~/PG/ochima]
└─$ nmap -p- --min-rate 10000 192.168.167.32 
Starting Nmap 7.95 ( https://nmap.org ) at 2025-04-14 21:02 EDT
Nmap scan report for 192.168.167.32
Host is up (0.049s latency).
Not shown: 65532 filtered tcp ports (no-response)
PORT     STATE SERVICE
22/tcp   open  ssh
80/tcp   open  http
8338/tcp open  unknown

Nmap done: 1 IP address (1 host up) scanned in 13.56 seconds
                                                                                                                                                                                                                                                                                         
┌──(kali㉿kali)-[~/PG/ochima]
└─$ nmap -p 22,80,8338 -sCV 192.168.167.32   
Starting Nmap 7.95 ( https://nmap.org ) at 2025-04-14 21:03 EDT
Nmap scan report for 192.168.167.32
Host is up (0.049s latency).

PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 8.9p1 Ubuntu 3ubuntu0.4 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   256 b9:bc:8f:01:3f:85:5d:f9:5c:d9:fb:b6:15:a0:1e:74 (ECDSA)
|_  256 53:d9:7f:3d:22:8a:fd:57:98:fe:6b:1a:4c:ac:79:67 (ED25519)
80/tcp   open  http    Apache httpd 2.4.52 ((Ubuntu))
|_http-server-header: Apache/2.4.52 (Ubuntu)
|_http-title: Apache2 Ubuntu Default Page: It works
8338/tcp open  http    Python http.server 3.5 - 3.10
|_http-server-header: Maltrail/0.52
|_http-title: Maltrail
| http-robots.txt: 1 disallowed entry 
|_/
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 13.48 seconds
```

![Pasted image 20250415090437](<0. Attachments/Pasted image 20250415090437.png>)

# web enum
![Pasted image 20250415103640](<0. Attachments/Pasted image 20250415103640.png>)

![Pasted image 20250415103659](<0. Attachments/Pasted image 20250415103659.png>)

![Pasted image 20250415103828](<0. Attachments/Pasted image 20250415103828.png>)

![Pasted image 20250415103857](<0. Attachments/Pasted image 20250415103857.png>)

# initial access
![Pasted image 20250415105255](<0. Attachments/Pasted image 20250415105255.png>)

# local.txt
![Pasted image 20250415105753](<0. Attachments/Pasted image 20250415105753.png>)

# priv esc enum
![Pasted image 20250415110008](<0. Attachments/Pasted image 20250415110008.png>)

![Pasted image 20250415110026](<0. Attachments/Pasted image 20250415110026.png>)

# priv esc
![Pasted image 20250415110319](<0. Attachments/Pasted image 20250415110319.png>)
![Pasted image 20250415110336](<0. Attachments/Pasted image 20250415110336.png>)

![Pasted image 20250415110411](<0. Attachments/Pasted image 20250415110411.png>)

![Pasted image 20250415110514](<0. Attachments/Pasted image 20250415110514.png>)

![Pasted image 20250415110550](<0. Attachments/Pasted image 20250415110550.png>)

# proof.txt
![Pasted image 20250415110608](<0. Attachments/Pasted image 20250415110608.png>)