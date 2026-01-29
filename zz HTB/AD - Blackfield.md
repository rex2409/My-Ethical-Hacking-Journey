nmap
```
┌──(kali㉿kali)-[~/HTB/blackfield-AD]
└─$ nmap -p- --min-rate 10000 10.129.190.77                        
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-07 05:35 EST
Nmap scan report for 10.129.190.77
Host is up (0.077s latency).
Not shown: 65527 filtered tcp ports (no-response)
PORT     STATE SERVICE
53/tcp   open  domain
88/tcp   open  kerberos-sec
135/tcp  open  msrpc
389/tcp  open  ldap
445/tcp  open  microsoft-ds
593/tcp  open  http-rpc-epmap
3268/tcp open  globalcatLDAP
5985/tcp open  wsman

Nmap done: 1 IP address (1 host up) scanned in 13.70 seconds
                                                                                                                                                     
┌──(kali㉿kali)-[~/HTB/blackfield-AD]
└─$ nmap -p 53,88,135,389,445,593,3268,5985 -sCV 10.129.190.77
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-07 05:35 EST
Nmap scan report for 10.129.190.77
Host is up (0.062s latency).

PORT     STATE SERVICE       VERSION
53/tcp   open  domain        Simple DNS Plus
88/tcp   open  kerberos-sec  Microsoft Windows Kerberos (server time: 2025-02-07 17:36:08Z)
135/tcp  open  msrpc         Microsoft Windows RPC
389/tcp  open  ldap          Microsoft Windows Active Directory LDAP (Domain: BLACKFIELD.local0., Site: Default-First-Site-Name)
445/tcp  open  microsoft-ds?
593/tcp  open  ncacn_http    Microsoft Windows RPC over HTTP 1.0
3268/tcp open  ldap          Microsoft Windows Active Directory LDAP (Domain: BLACKFIELD.local0., Site: Default-First-Site-Name)
5985/tcp open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
Service Info: Host: DC01; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| smb2-security-mode: 
|   3:1:1: 
|_    Message signing enabled and required
| smb2-time: 
|   date: 2025-02-07T17:36:13
|_  start_date: N/A
|_clock-skew: 7h00m01s

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 51.61 seconds
```

![Pasted image 20250207192231](<0. Attachments/Pasted image 20250207192231.png>)

[HTB: Blackfield | 0xdf hacks stuff](https://0xdf.gitlab.io/2020/10/03/htb-blackfield.html#)

