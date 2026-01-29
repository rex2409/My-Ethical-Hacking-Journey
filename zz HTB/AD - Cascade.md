nmap
```
┌──(kali㉿kali)-[~/HTB/cascade-AD]
└─$ nmap -p- --min-rate 10000 10.129.189.76                                                
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-06 04:43 EST
Nmap scan report for 10.129.189.76
Host is up (0.11s latency).
Not shown: 65520 filtered tcp ports (no-response)
PORT      STATE SERVICE
53/tcp    open  domain
88/tcp    open  kerberos-sec
135/tcp   open  msrpc
139/tcp   open  netbios-ssn
389/tcp   open  ldap
445/tcp   open  microsoft-ds
636/tcp   open  ldapssl
3268/tcp  open  globalcatLDAP
3269/tcp  open  globalcatLDAPssl
5985/tcp  open  wsman
49154/tcp open  unknown
49155/tcp open  unknown
49157/tcp open  unknown
49158/tcp open  unknown
49165/tcp open  unknown

Nmap done: 1 IP address (1 host up) scanned in 40.46 seconds
                                                                                                                                                       
┌──(kali㉿kali)-[~/HTB/cascade-AD]
└─$ nmap -p 53,88,135,389,445,636,3268,3269,5985 -sCV 10.129.189.76 
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-06 04:45 EST
Nmap scan report for 10.129.189.76
Host is up (0.051s latency).

PORT     STATE SERVICE       VERSION
53/tcp   open  domain        Microsoft DNS 6.1.7601 (1DB15D39) (Windows Server 2008 R2 SP1)
| dns-nsid: 
|_  bind.version: Microsoft DNS 6.1.7601 (1DB15D39)
88/tcp   open  kerberos-sec  Microsoft Windows Kerberos (server time: 2025-02-06 09:45:35Z)
135/tcp  open  msrpc         Microsoft Windows RPC
389/tcp  open  ldap          Microsoft Windows Active Directory LDAP (Domain: cascade.local, Site: Default-First-Site-Name)
445/tcp  open  microsoft-ds?
636/tcp  open  tcpwrapped
3268/tcp open  ldap          Microsoft Windows Active Directory LDAP (Domain: cascade.local, Site: Default-First-Site-Name)
3269/tcp open  tcpwrapped
5985/tcp open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-title: Not Found
|_http-server-header: Microsoft-HTTPAPI/2.0
Service Info: Host: CASC-DC1; OS: Windows; CPE: cpe:/o:microsoft:windows_server_2008:r2:sp1, cpe:/o:microsoft:windows

Host script results:
| smb2-security-mode: 
|   2:1:0: 
|_    Message signing enabled and required
| smb2-time: 
|   date: 2025-02-06T09:45:42
|_  start_date: 2025-02-06T09:42:09

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 51.88 seconds
```

![Pasted image 20250206222552](<0. Attachments/Pasted image 20250206222552.png>)

refer - [HTB: Cascade | 0xdf hacks stuff](https://0xdf.gitlab.io/2020/07/25/htb-cascade.html)
