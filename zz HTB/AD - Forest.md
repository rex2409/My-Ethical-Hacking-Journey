nmap
```
┌──(kali㉿kali)-[~/HTB/forest-AD]
└─$ nmap -p- --min-rate 10000 10.129.189.235
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-05 23:29 EST
Warning: 10.129.189.235 giving up on port because retransmission cap hit (10).
Nmap scan report for 10.129.189.235
Host is up (0.073s latency).
Not shown: 65345 closed tcp ports (reset), 167 filtered tcp ports (no-response)
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
47001/tcp open  winrm
49664/tcp open  unknown
49665/tcp open  unknown
49666/tcp open  unknown
49667/tcp open  unknown
49671/tcp open  unknown
49676/tcp open  unknown
49677/tcp open  unknown
49681/tcp open  unknown
49698/tcp open  unknown

Nmap done: 1 IP address (1 host up) scanned in 14.52 seconds
                                                                                                                                                       
┌──(kali㉿kali)-[~/HTB/forest-AD]
└─$ nmap -p 53,88,135,139,389,445,464,593,636,3268,3269,5985,9389,47001 -sCV 10.129.189.235 
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-05 23:31 EST
Nmap scan report for 10.129.189.235
Host is up (0.050s latency).

PORT      STATE SERVICE      VERSION
53/tcp    open  domain       Simple DNS Plus
88/tcp    open  kerberos-sec Microsoft Windows Kerberos (server time: 2025-02-06 04:38:33Z)
135/tcp   open  msrpc        Microsoft Windows RPC
139/tcp   open  netbios-ssn  Microsoft Windows netbios-ssn
389/tcp   open  ldap         Microsoft Windows Active Directory LDAP (Domain: htb.local, Site: Default-First-Site-Name)
445/tcp   open  microsoft-ds Windows Server 2016 Standard 14393 microsoft-ds (workgroup: HTB)
464/tcp   open  kpasswd5?
593/tcp   open  ncacn_http   Microsoft Windows RPC over HTTP 1.0
636/tcp   open  tcpwrapped
3268/tcp  open  ldap         Microsoft Windows Active Directory LDAP (Domain: htb.local, Site: Default-First-Site-Name)
3269/tcp  open  tcpwrapped
5985/tcp  open  http         Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
9389/tcp  open  mc-nmf       .NET Message Framing
47001/tcp open  http         Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
Service Info: Host: FOREST; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
|_clock-skew: mean: 2h46m50s, deviation: 4h37m11s, median: 6m48s
| smb-os-discovery: 
|   OS: Windows Server 2016 Standard 14393 (Windows Server 2016 Standard 6.3)
|   Computer name: FOREST
|   NetBIOS computer name: FOREST\x00
|   Domain name: htb.local
|   Forest name: htb.local
|   FQDN: FOREST.htb.local
|_  System time: 2025-02-05T20:38:41-08:00
| smb2-security-mode: 
|   3:1:1: 
|_    Message signing enabled and required
| smb2-time: 
|   date: 2025-02-06T04:38:37
|_  start_date: 2025-02-06T04:35:11
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: required

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 22.97 seconds
```

![Pasted image 20250206124825](<0. Attachments/Pasted image 20250206124825.png>)

![Pasted image 20250206124858](<0. Attachments/Pasted image 20250206124858.png>)

There is an option for an account to have the property “Do not require Kerberos preauthentication” or UF_DONT_REQUIRE_PREAUTH set to true. AS-REP Roasting is an attack against Kerberos for these accounts. I have a list of accounts from my RPC enumeration above. I’ll start without the SM* or HealthMailbox* accounts:

![Pasted image 20250206124915](<0. Attachments/Pasted image 20250206124915.png>)

![Pasted image 20250206125223](<0. Attachments/Pasted image 20250206125223.png>)

svc-alfresco --> s3rvice

![Pasted image 20250206171552](<0. Attachments/Pasted image 20250206171552.png>)

![Pasted image 20250206171658](<0. Attachments/Pasted image 20250206171658.png>)

![Pasted image 20250206171717](<0. Attachments/Pasted image 20250206171717.png>)

administrator --> aad3b435b51404eeaad3b435b51404ee:32693b11e6aa90eb43d32c72a07ceea6

![Pasted image 20250206173514](<0. Attachments/Pasted image 20250206173514.png>)

