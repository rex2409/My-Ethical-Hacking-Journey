# nmap
```
┌──(kali㉿kali)-[~/PG/jordak]
└─$ ip=192.168.203.109
                                                                                                                                                                                                                                                                                                                            
┌──(kali㉿kali)-[~/PG/jordak]
└─$ echo $ip
192.168.203.109
                                                                                                                                                                                                                                                                                                                            
┌──(kali㉿kali)-[~/PG/jordak]
└─$ nmap -p- --min-rate 10000 $ip            
Starting Nmap 7.95 ( https://nmap.org ) at 2025-05-11 21:41 EDT
Nmap scan report for 192.168.203.109
Host is up (0.053s latency).
Not shown: 65533 closed tcp ports (reset)
PORT   STATE SERVICE
22/tcp open  ssh
80/tcp open  http

Nmap done: 1 IP address (1 host up) scanned in 7.94 seconds
                                                                                                                                                                                                                                                                                                                            
┌──(kali㉿kali)-[~/PG/jordak]
└─$ nmap -p 22,80 -sCV $ip            
Starting Nmap 7.95 ( https://nmap.org ) at 2025-05-11 21:42 EDT
Nmap scan report for 192.168.203.109
Host is up (0.046s latency).

PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 9.6p1 Ubuntu 3ubuntu13.5 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   256 76:18:f1:19:6b:29:db:da:3d:f6:7b:ab:f4:b5:63:e0 (ECDSA)
|_  256 cb:d8:d6:ef:82:77:8a:25:32:08:dd:91:96:8d:ab:7d (ED25519)
80/tcp open  http    Apache httpd 2.4.58 ((Ubuntu))
|_http-server-header: Apache/2.4.58 (Ubuntu)
|_http-trane-info: Problem with XML parsing of /evox/about
|_http-title: Apache2 Ubuntu Default Page: It works
| http-robots.txt: 1 disallowed entry 
|_/
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 9.53 seconds
```

![Pasted image 20250512094243](<0. Attachments/Pasted image 20250512094243.png>)

# web enum
![Pasted image 20250512094425](<0. Attachments/Pasted image 20250512094425.png>)

![Pasted image 20250512094528](<0. Attachments/Pasted image 20250512094528.png>)

![Pasted image 20250512095338](<0. Attachments/Pasted image 20250512095338.png>)

![Pasted image 20250512095409](<0. Attachments/Pasted image 20250512095409.png>)

![Pasted image 20250512103302](<0. Attachments/Pasted image 20250512103302.png>)

![Pasted image 20250512103413](<0. Attachments/Pasted image 20250512103413.png>)

![Pasted image 20250512103639](<0. Attachments/Pasted image 20250512103639.png>)

[CVE-repository/PoCs/CVE_Jorani.py at master · Orange-Cyberdefense/CVE-repository · GitHub](https://github.com/Orange-Cyberdefense/CVE-repository/blob/master/PoCs/CVE_Jorani.py)

