nmap
```
┌──(kali㉿kali)-[~/HTB/monteverde-AD]
└─$ nmap -p- --min-rate 10000 10.129.228.111
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-04 03:31 EST
Nmap scan report for 10.129.228.111
Host is up (0.098s latency).
Not shown: 65517 filtered tcp ports (no-response)
PORT      STATE SERVICE
53/tcp    open  domain
88/tcp    open  kerberos-sec
135/tcp   open  msrpc
139/tcp   open  netbios-ssn
389/tcp   open  ldap
445/tcp   open  microsoft-ds
464/tcp   open  kpasswd5
593/tcp   open  http-rpc-epmap
636/tcp   open  ldapssl
3268/tcp  open  globalcatLDAP
3269/tcp  open  globalcatLDAPssl
5985/tcp  open  wsman
9389/tcp  open  adws
49667/tcp open  unknown
49673/tcp open  unknown
49674/tcp open  unknown
49676/tcp open  unknown
49693/tcp open  unknown

Nmap done: 1 IP address (1 host up) scanned in 20.19 seconds
                                                                                                                                               
┌──(kali㉿kali)-[~/HTB/monteverde-AD]
└─$ nmap -p 53,88,135,139,389,445,464,593,636,3268,3269,5985,9389,49667,49673,49674,49676,49693 -sCV 10.129.228.111
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-04 03:35 EST
Nmap scan report for 10.129.228.111
Host is up (0.044s latency).

PORT      STATE SERVICE       VERSION
53/tcp    open  domain        Simple DNS Plus
88/tcp    open  kerberos-sec  Microsoft Windows Kerberos (server time: 2025-02-04 08:35:19Z)
135/tcp   open  msrpc         Microsoft Windows RPC
139/tcp   open  netbios-ssn   Microsoft Windows netbios-ssn
389/tcp   open  ldap          Microsoft Windows Active Directory LDAP (Domain: MEGABANK.LOCAL0., Site: Default-First-Site-Name)
445/tcp   open  microsoft-ds?
464/tcp   open  kpasswd5?
593/tcp   open  ncacn_http    Microsoft Windows RPC over HTTP 1.0
636/tcp   open  tcpwrapped
3268/tcp  open  ldap          Microsoft Windows Active Directory LDAP (Domain: MEGABANK.LOCAL0., Site: Default-First-Site-Name)
3269/tcp  open  tcpwrapped
5985/tcp  open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-title: Not Found
|_http-server-header: Microsoft-HTTPAPI/2.0
9389/tcp  open  mc-nmf        .NET Message Framing
49667/tcp open  msrpc         Microsoft Windows RPC
49673/tcp open  ncacn_http    Microsoft Windows RPC over HTTP 1.0
49674/tcp open  msrpc         Microsoft Windows RPC
49676/tcp open  msrpc         Microsoft Windows RPC
49693/tcp open  msrpc         Microsoft Windows RPC
Service Info: Host: MONTEVERDE; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| smb2-security-mode: 
|   3:1:1: 
|_    Message signing enabled and required
| smb2-time: 
|   date: 2025-02-04T08:36:12
|_  start_date: N/A

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 98.32 seconds
```

![Pasted image 20250204164525](<0. Attachments/Pasted image 20250204164525.png>)

![Pasted image 20250204164824](<0. Attachments/Pasted image 20250204164824.png>)

![Pasted image 20250204164951](<0. Attachments/Pasted image 20250204164951.png>)

![Pasted image 20250204165122](<0. Attachments/Pasted image 20250204165122.png>)

![Pasted image 20250204195205](<0. Attachments/Pasted image 20250204195205.png>)

https://github.com/VbScrub/AdSyncDecrypt/releases

```
C:\Program Files\Microsoft Azure AD Sync\Bin> C:\users\mhope\documents\AdDecrypt.exe -FullSql
```

we added the exploit in a writeable folder and called it

![Pasted image 20250204225205](<0. Attachments/Pasted image 20250204225205.png>)

administrator --> d0m@in4dminyeah!

![Pasted image 20250204225401](<0. Attachments/Pasted image 20250204225401.png>)

