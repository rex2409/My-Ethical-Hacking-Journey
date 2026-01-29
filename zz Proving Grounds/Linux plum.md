# nmap
```
┌──(kali㉿kali)-[~/PG/plum]
└─$ nmap -p- --min-rate 10000 192.168.113.28
Starting Nmap 7.95 ( https://nmap.org ) at 2025-04-17 07:14 EDT
Nmap scan report for 192.168.113.28
Host is up (0.085s latency).
Not shown: 65533 closed tcp ports (reset)
PORT   STATE SERVICE
22/tcp open  ssh
80/tcp open  http

Nmap done: 1 IP address (1 host up) scanned in 7.46 seconds
                                                                                                                                                                                                                                                                                                                           
┌──(kali㉿kali)-[~/PG/plum]
└─$ nmap -p 22,80 -sCV 192.168.113.28       
Starting Nmap 7.95 ( https://nmap.org ) at 2025-04-17 07:14 EDT
Nmap scan report for 192.168.113.28
Host is up (0.045s latency).

PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.4p1 Debian 5+deb11u1 (protocol 2.0)
| ssh-hostkey: 
|   3072 c9:c3:da:15:28:3b:f1:f8:9a:36:df:4d:36:6b:a7:44 (RSA)
|   256 26:03:2b:f6:da:90:1d:1b:ec:8d:8f:8d:1e:7e:3d:6b (ECDSA)
|_  256 fb:43:b2:b0:19:2f:d3:f6:bc:aa:60:67:ab:c1:af:37 (ED25519)
80/tcp open  http    Apache httpd 2.4.56 ((Debian))
|_http-title: PluXml - Blog or CMS, XML powered !
|_http-server-header: Apache/2.4.56 (Debian)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 9.23 seconds
```
![Pasted image 20250417191517](<0. Attachments/Pasted image 20250417191517.png>)

# web enum
![Pasted image 20250417191607](<0. Attachments/Pasted image 20250417191607.png>)

![Pasted image 20250417191640](<0. Attachments/Pasted image 20250417191640.png>)

![Pasted image 20250417191704](<0. Attachments/Pasted image 20250417191704.png>)

# exploit
[CVE-2022-25018/CVE-2022-25018.pdf at main · MoritzHuppert/CVE-2022-25018 · GitHub](https://github.com/MoritzHuppert/CVE-2022-25018/blob/main/CVE-2022-25018.pdf)

![Pasted image 20250417192624](<0. Attachments/Pasted image 20250417192624.png>)

![Pasted image 20250417192639](<0. Attachments/Pasted image 20250417192639.png>)

# initial access
![Pasted image 20250417192826](<0. Attachments/Pasted image 20250417192826.png>)

after opening page

![Pasted image 20250417192856](<0. Attachments/Pasted image 20250417192856.png>)

# local.txt
![Pasted image 20250417193200](<0. Attachments/Pasted image 20250417193200.png>)

# priv esc enum
![Pasted image 20250417193621](<0. Attachments/Pasted image 20250417193621.png>)

![Pasted image 20250417193722](<0. Attachments/Pasted image 20250417193722.png>)

![Pasted image 20250417193823](<0. Attachments/Pasted image 20250417193823.png>)

![Pasted image 20250417194902](<0. Attachments/Pasted image 20250417194902.png>)

# priv esc
![Pasted image 20250417194945](<0. Attachments/Pasted image 20250417194945.png>)

# proof.txt
![Pasted image 20250417195046](<0. Attachments/Pasted image 20250417195046.png>)
