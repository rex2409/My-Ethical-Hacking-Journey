nmap
```
┌──(kali㉿kali)-[~/HTB/flight-AD]
└─$ nmap -p- --min-rate 10000 10.129.228.120                  
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-07 06:35 EST
Nmap scan report for 10.129.228.120
Host is up (0.10s latency).
Not shown: 65521 filtered tcp ports (no-response)
PORT      STATE SERVICE
53/tcp    open  domain
80/tcp    open  http
88/tcp    open  kerberos-sec
135/tcp   open  msrpc
139/tcp   open  netbios-ssn
389/tcp   open  ldap
445/tcp   open  microsoft-ds
464/tcp   open  kpasswd5
636/tcp   open  ldapssl
3268/tcp  open  globalcatLDAP
3269/tcp  open  globalcatLDAPssl
9389/tcp  open  adws
49674/tcp open  unknown
65003/tcp open  unknown

Nmap done: 1 IP address (1 host up) scanned in 20.31 seconds
                                                                                                                                                     
┌──(kali㉿kali)-[~/HTB/flight-AD]
└─$ nmap -p 53,80,88,135,139,389,445,464,593,636,5985,9389 -sCV 10.129.228.120
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-07 06:36 EST
Nmap scan report for 10.129.228.120
Host is up (0.052s latency).

PORT     STATE SERVICE       VERSION
53/tcp   open  domain        Simple DNS Plus
80/tcp   open  http          Apache httpd 2.4.52 ((Win64) OpenSSL/1.1.1m PHP/8.1.1)
|_http-server-header: Apache/2.4.52 (Win64) OpenSSL/1.1.1m PHP/8.1.1
|_http-title: g0 Aviation
| http-methods: 
|_  Potentially risky methods: TRACE
88/tcp   open  kerberos-sec  Microsoft Windows Kerberos (server time: 2025-02-07 18:36:27Z)
135/tcp  open  msrpc         Microsoft Windows RPC
139/tcp  open  netbios-ssn   Microsoft Windows netbios-ssn
389/tcp  open  ldap          Microsoft Windows Active Directory LDAP (Domain: flight.htb0., Site: Default-First-Site-Name)
445/tcp  open  microsoft-ds?
464/tcp  open  kpasswd5?
593/tcp  open  ncacn_http    Microsoft Windows RPC over HTTP 1.0
636/tcp  open  tcpwrapped
5985/tcp open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
9389/tcp open  mc-nmf        .NET Message Framing
Service Info: Host: G0; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
|_clock-skew: 6h59m59s
| smb2-security-mode: 
|   3:1:1: 
|_    Message signing enabled and required
| smb2-time: 
|   date: 2025-02-07T18:36:36
|_  start_date: N/A

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 54.36 seconds
```

![Pasted image 20250207194037](<0. Attachments/Pasted image 20250207194037.png>)

[HTB: Flight | 0xdf hacks stuff](https://0xdf.gitlab.io/2023/05/06/htb-flight.html#)

