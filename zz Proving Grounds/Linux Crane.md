```
┌──(kali㉿kali)-[~/PG/crane]
└─$ nmap -p- --min-rate 10000 192.168.193.146
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-17 23:32 EST
Nmap scan report for 192.168.193.146
Host is up (0.080s latency).
Not shown: 65531 closed tcp ports (reset)
PORT      STATE SERVICE
22/tcp    open  ssh
80/tcp    open  http
3306/tcp  open  mysql
33060/tcp open  mysqlx

Nmap done: 1 IP address (1 host up) scanned in 7.24 seconds
                                                                                                                                                     
┌──(kali㉿kali)-[~/PG/crane]
└─$ nmap -p 22,80,3306,33060 -sCV 192.168.193.146
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-17 23:33 EST
Nmap scan report for 192.168.193.146
Host is up (0.047s latency).

PORT      STATE SERVICE VERSION
22/tcp    open  ssh     OpenSSH 7.9p1 Debian 10+deb10u2 (protocol 2.0)
| ssh-hostkey: 
|   2048 37:80:01:4a:43:86:30:c9:79:e7:fb:7f:3b:a4:1e:dd (RSA)
|   256 b6:18:a1:e1:98:fb:6c:c6:87:55:45:10:c6:d4:45:b9 (ECDSA)
|_  256 ab:8f:2d:e8:a2:04:e7:b7:65:d3:fe:5e:93:1e:03:67 (ED25519)
80/tcp    open  http    Apache httpd 2.4.38 ((Debian))
| http-title: SuiteCRM
|_Requested resource was index.php?action=Login&module=Users
|_http-server-header: Apache/2.4.38 (Debian)
| http-cookie-flags: 
|   /: 
|     PHPSESSID: 
|_      httponly flag not set
| http-robots.txt: 1 disallowed entry 
|_/
3306/tcp  open  mysql   MySQL (unauthorized)
33060/tcp open  mysqlx  MySQL X protocol listener
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 9.90 seconds
```

![Pasted image 20250218123510](<0. Attachments/Pasted image 20250218123510.png>)

guessing admin admin
![Pasted image 20250218123542](<0. Attachments/Pasted image 20250218123542.png>)

![Pasted image 20250218124404](<0. Attachments/Pasted image 20250218124404.png>)

```
/home/kali/Tools/username-anarchy-0.6/username-anarchy -i users > best_userlist
```

![Pasted image 20250218124501](<0. Attachments/Pasted image 20250218124501.png>)
found exploit --> https://github.com/manuelz120/CVE-2022-23940

![Pasted image 20250218132017](<0. Attachments/Pasted image 20250218132017.png>)

![Pasted image 20250218132031](<0. Attachments/Pasted image 20250218132031.png>)

![Pasted image 20250218132156](<0. Attachments/Pasted image 20250218132156.png>)

![Pasted image 20250218132208](<0. Attachments/Pasted image 20250218132208.png>)

![Pasted image 20250218132250](<0. Attachments/Pasted image 20250218132250.png>)

![Pasted image 20250218132351](<0. Attachments/Pasted image 20250218132351.png>)

