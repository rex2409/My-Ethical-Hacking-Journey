# nmap
```
┌──(kali㉿kali)-[~/PG/pyloader]
└─$ nmap -p- --min-rate 10000 192.168.113.26
Starting Nmap 7.95 ( https://nmap.org ) at 2025-04-17 06:51 EDT
Nmap scan report for 192.168.113.26
Host is up (0.054s latency).
Not shown: 65533 closed tcp ports (reset)
PORT     STATE SERVICE
22/tcp   open  ssh
9666/tcp open  zoomcp

Nmap done: 1 IP address (1 host up) scanned in 9.36 seconds
                                                                                                                                                                                                                                                                                                                            
┌──(kali㉿kali)-[~/PG/pyloader]
└─$ nmap -p 22,9666 -sCV 192.168.113.26     
Starting Nmap 7.95 ( https://nmap.org ) at 2025-04-17 06:52 EDT
Nmap scan report for 192.168.113.26
Host is up (0.043s latency).

PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 8.9p1 Ubuntu 3ubuntu0.1 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   256 b9:bc:8f:01:3f:85:5d:f9:5c:d9:fb:b6:15:a0:1e:74 (ECDSA)
|_  256 53:d9:7f:3d:22:8a:fd:57:98:fe:6b:1a:4c:ac:79:67 (ED25519)
9666/tcp open  http    CherryPy wsgiserver
| http-title: Login - pyLoad 
|_Requested resource was /login?next=http://192.168.113.26:9666/
| http-robots.txt: 1 disallowed entry 
|_/
|_http-server-header: Cheroot/8.6.0
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 36.99 seconds
```
![Pasted image 20250417185400](<0. Attachments/Pasted image 20250417185400.png>)

# web enum
![Pasted image 20250417185533](<0. Attachments/Pasted image 20250417185533.png>)

![Pasted image 20250417185816](<0. Attachments/Pasted image 20250417185816.png>)

![Pasted image 20250417185921](<0. Attachments/Pasted image 20250417185921.png>)

# exploit
[GitHub - JacobEbben/CVE-2023-0297: Unauthenticated Remote Code Execution in PyLoad <0.5.0b3.dev31](https://github.com/JacobEbben/CVE-2023-0297)

# access
![Pasted image 20250417191111](<0. Attachments/Pasted image 20250417191111.png>)

![Pasted image 20250417191207](<0. Attachments/Pasted image 20250417191207.png>)

