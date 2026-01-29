# nmap
```
┌──(kali㉿kali)-[~/PG/hepet]
└─$ nmap -p- --min-rate 10000 192.168.227.140                 
Starting Nmap 7.95 ( https://nmap.org ) at 2025-03-02 21:42 EST
Nmap scan report for 192.168.227.140
Host is up (0.032s latency).
Not shown: 65511 closed tcp ports (reset)
PORT      STATE    SERVICE
25/tcp    open     smtp
79/tcp    open     finger
105/tcp   open     csnet-ns
106/tcp   open     pop3pw
110/tcp   open     pop3
135/tcp   open     msrpc
139/tcp   open     netbios-ssn
143/tcp   open     imap
443/tcp   open     https
445/tcp   open     microsoft-ds
2224/tcp  open     efi-mg
5040/tcp  open     unknown
7680/tcp  open     pando-pub
8000/tcp  open     http-alt
11100/tcp open     unknown
20001/tcp open     microsan
33006/tcp open     unknown
49664/tcp open     unknown
49665/tcp open     unknown
49666/tcp open     unknown
49667/tcp open     unknown
49668/tcp open     unknown
49669/tcp open     unknown
59709/tcp filtered unknown

Nmap done: 1 IP address (1 host up) scanned in 10.84 seconds
                                                                                                                                                      
┌──(kali㉿kali)-[~/PG/hepet]
└─$ nmap -p 25,79,105,106,110,135,139,143,443,445,2224,5040,7680,8000,11100,20001 -sCV 192.168.227.140
Starting Nmap 7.95 ( https://nmap.org ) at 2025-03-02 21:44 EST
Nmap scan report for 192.168.227.140
Host is up (0.0092s latency).

PORT      STATE SERVICE        VERSION
25/tcp    open  smtp           Mercury/32 smtpd (Mail server account Maiser)
| smtp-commands: localhost Hello nmap.scanme.org; ESMTPs are:, TIME, SIZE 0, HELP
|_ Recognized SMTP commands are: HELO EHLO MAIL RCPT DATA RSET AUTH NOOP QUIT HELP VRFY SOML Mail server account is 'Maiser'.
79/tcp    open  finger         Mercury/32 fingerd
| finger: Login: Admin         Name: Mail System Administrator\x0D
| \x0D
|_[No profile information]\x0D
105/tcp   open  ph-addressbook Mercury/32 PH addressbook server
106/tcp   open  pop3pw         Mercury/32 poppass service
110/tcp   open  pop3           Mercury/32 pop3d
135/tcp   open  msrpc          Microsoft Windows RPC
139/tcp   open  netbios-ssn    Microsoft Windows netbios-ssn
143/tcp   open  imap           Mercury/32 imapd 4.62
443/tcp   open  ssl/http       Apache httpd 2.4.46 ((Win64) OpenSSL/1.1.1g PHP/7.3.23)
|_ssl-date: TLS randomness does not represent time
| tls-alpn: 
|_  http/1.1
| ssl-cert: Subject: commonName=localhost
| Not valid before: 2009-11-10T23:48:47
|_Not valid after:  2019-11-08T23:48:47
|_http-server-header: Apache/2.4.46 (Win64) OpenSSL/1.1.1g PHP/7.3.23
|_http-title: Time Travel Company Page
| http-methods: 
|_  Potentially risky methods: TRACE
445/tcp   open  microsoft-ds?
2224/tcp  open  http           Mercury/32 httpd
|_http-title: Mercury HTTP Services
5040/tcp  open  unknown
7680/tcp  open  pando-pub?
8000/tcp  open  http           Apache httpd 2.4.46 ((Win64) OpenSSL/1.1.1g PHP/7.3.23)
|_http-open-proxy: Proxy might be redirecting requests
|_http-server-header: Apache/2.4.46 (Win64) OpenSSL/1.1.1g PHP/7.3.23
|_http-title: Time Travel Company Page
11100/tcp open  vnc            VNC (protocol 3.8)
| vnc-info: 
|   Protocol version: 3.8
|   Security types: 
|_    Unknown security type (40)
20001/tcp open  ftp            FileZilla ftpd 0.9.41 beta
Service Info: Host: localhost; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| smb2-time: 
|   date: 2025-03-03T02:47:10
|_  start_date: N/A
|_clock-skew: 1s
| smb2-security-mode: 
|   3:1:1: 
|_    Message signing enabled but not required

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 177.91 seconds
```
![Pasted image 20250303110517](<0. Attachments/Pasted image 20250303110517.png>)

# web enum
potential users
![Pasted image 20250303111000](<0. Attachments/Pasted image 20250303111000.png>)

![Pasted image 20250303111144](<0. Attachments/Pasted image 20250303111144.png>)

# port 79 finger enum
[79 - Pentesting Finger - HackTricks](https://book.hacktricks.wiki/en/network-services-pentesting/pentesting-finger.html)

![Pasted image 20250303112016](<0. Attachments/Pasted image 20250303112016.png>)

![Pasted image 20250303112155](<0. Attachments/Pasted image 20250303112155.png>)

# imap enum
using hydra to brute force
create a wordlist first using cewl
![Pasted image 20250303113115](<0. Attachments/Pasted image 20250303113115.png>)

![Pasted image 20250303113231](<0. Attachments/Pasted image 20250303113231.png>)

we have a hit

Jonas --> SicMundusCreatusEst
# pop3 enum

forget it it requires mitm
[OSCP-Notes/Proving_Grounds_Writeups/Hepet.md at master · tedchen0001/OSCP-Notes · GitHub](https://github.com/tedchen0001/OSCP-Notes/blob/master/Proving_Grounds_Writeups/Hepet.md)

