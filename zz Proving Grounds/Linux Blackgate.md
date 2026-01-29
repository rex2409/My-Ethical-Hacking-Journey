```
┌──(kali㉿kali)-[~/PG/blackgate]
└─$ nmap -p- --min-rate 10000 192.168.140.176    
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-11 21:01 EST
Nmap scan report for 192.168.140.176
Host is up (0.051s latency).
Not shown: 65533 closed tcp ports (reset)
PORT     STATE SERVICE
22/tcp   open  ssh
6379/tcp open  redis

Nmap done: 1 IP address (1 host up) scanned in 9.97 seconds
                                                                                                                                                 
┌──(kali㉿kali)-[~/PG/blackgate]
└─$ nmap -p 22,6379 -sCV 192.168.140.176         
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-11 21:02 EST
Nmap scan report for 192.168.140.176
Host is up (0.044s latency).

PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 8.3p1 Ubuntu 1ubuntu0.1 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 37:21:14:3e:23:e5:13:40:20:05:f9:79:e0:82:0b:09 (RSA)
|   256 b9:8d:bd:90:55:7c:84:cc:a0:7f:a8:b4:d3:55:06:a7 (ECDSA)
|_  256 07:07:29:7a:4c:7c:f2:b0:1f:3c:3f:2b:a1:56:9e:0a (ED25519)
6379/tcp open  redis   Redis key-value store 4.0.14
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 10.05 seconds
```

https://github.com/n0b0dyCN/redis-rogue-server/tree/master

![Pasted image 20250212101659](<0. Attachments/Pasted image 20250212101659.png>)

![Pasted image 20250212101713](<0. Attachments/Pasted image 20250212101713.png>)

![Pasted image 20250212105103](<0. Attachments/Pasted image 20250212105103.png>)

![Pasted image 20250212105312](<0. Attachments/Pasted image 20250212105312.png>)

