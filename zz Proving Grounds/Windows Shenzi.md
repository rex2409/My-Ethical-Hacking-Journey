# nmap
```
┌──(kali㉿kali)-[~/PG/shenzi]
└─$ nmap -p- --min-rate 10000 192.168.205.55 
Starting Nmap 7.95 ( https://nmap.org ) at 2025-04-10 21:40 EDT
Nmap scan report for 192.168.205.55
Host is up (0.051s latency).
Not shown: 65520 closed tcp ports (reset)
PORT      STATE SERVICE
21/tcp    open  ftp
80/tcp    open  http
135/tcp   open  msrpc
139/tcp   open  netbios-ssn
443/tcp   open  https
445/tcp   open  microsoft-ds
3306/tcp  open  mysql
5040/tcp  open  unknown
7680/tcp  open  pando-pub
49664/tcp open  unknown
49665/tcp open  unknown
49666/tcp open  unknown
49667/tcp open  unknown
49668/tcp open  unknown
49669/tcp open  unknown

Nmap done: 1 IP address (1 host up) scanned in 9.19 seconds
                                                                                                                                                                                                                   
┌──(kali㉿kali)-[~/PG/shenzi]
└─$ nmap -p 21,80,135,139,443,445,3306,5040,7680 -sCV 192.168.205.55
Starting Nmap 7.95 ( https://nmap.org ) at 2025-04-10 21:41 EDT
Nmap scan report for 192.168.205.55
Host is up (0.049s latency).

PORT     STATE SERVICE       VERSION
21/tcp   open  ftp           FileZilla ftpd 0.9.41 beta
| ftp-syst: 
|_  SYST: UNIX emulated by FileZilla
80/tcp   open  http          Apache httpd 2.4.43 ((Win64) OpenSSL/1.1.1g PHP/7.4.6)
|_http-server-header: Apache/2.4.43 (Win64) OpenSSL/1.1.1g PHP/7.4.6
| http-title: Welcome to XAMPP
|_Requested resource was http://192.168.205.55/dashboard/
135/tcp  open  msrpc         Microsoft Windows RPC
139/tcp  open  netbios-ssn   Microsoft Windows netbios-ssn
443/tcp  open  ssl/http      Apache httpd 2.4.43 ((Win64) OpenSSL/1.1.1g PHP/7.4.6)
| tls-alpn: 
|_  http/1.1
|_ssl-date: TLS randomness does not represent time
| ssl-cert: Subject: commonName=localhost
| Not valid before: 2009-11-10T23:48:47
|_Not valid after:  2019-11-08T23:48:47
| http-title: Welcome to XAMPP
|_Requested resource was https://192.168.205.55/dashboard/
|_http-server-header: Apache/2.4.43 (Win64) OpenSSL/1.1.1g PHP/7.4.6
445/tcp  open  microsoft-ds?
3306/tcp open  mysql         MariaDB 10.3.24 or later (unauthorized)
5040/tcp open  unknown
7680/tcp open  pando-pub?
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| smb2-security-mode: 
|   3:1:1: 
|_    Message signing enabled but not required
| smb2-time: 
|   date: 2025-04-11T01:43:58
|_  start_date: N/A

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 175.45 seconds
```

![Pasted image 20250411094452](<0. Attachments/Pasted image 20250411094452.png>)

# web enum
![Pasted image 20250411095804](<0. Attachments/Pasted image 20250411095804.png>)

![Pasted image 20250411105738](<0. Attachments/Pasted image 20250411105738.png>)

using smb enum stuff we have admin login
![Pasted image 20250411115424](<0. Attachments/Pasted image 20250411115424.png>)

# smb enum
![Pasted image 20250411095943](<0. Attachments/Pasted image 20250411095943.png>)

![Pasted image 20250411100144](<0. Attachments/Pasted image 20250411100144.png>)

![Pasted image 20250411100237](<0. Attachments/Pasted image 20250411100237.png>)

![Pasted image 20250411100332](<0. Attachments/Pasted image 20250411100332.png>)

![Pasted image 20250411100503](<0. Attachments/Pasted image 20250411100503.png>)

# initial access
![Pasted image 20250411115854](<0. Attachments/Pasted image 20250411115854.png>)

![Pasted image 20250411115935](<0. Attachments/Pasted image 20250411115935.png>)

getting a reverse shell
![Pasted image 20250411120130](<0. Attachments/Pasted image 20250411120130.png>)

![Pasted image 20250411120155](<0. Attachments/Pasted image 20250411120155.png>)

![Pasted image 20250411120212](<0. Attachments/Pasted image 20250411120212.png>)

# local.txt
![Pasted image 20250411120401](<0. Attachments/Pasted image 20250411120401.png>)

# priv esc enum
![Pasted image 20250411121055](<0. Attachments/Pasted image 20250411121055.png>)

# priv esc
![Pasted image 20250411121806](<0. Attachments/Pasted image 20250411121806.png>)

![Pasted image 20250411121850](<0. Attachments/Pasted image 20250411121850.png>)

![Pasted image 20250411121905](<0. Attachments/Pasted image 20250411121905.png>)

# proof.txt
![Pasted image 20250411122026](<0. Attachments/Pasted image 20250411122026.png>)
