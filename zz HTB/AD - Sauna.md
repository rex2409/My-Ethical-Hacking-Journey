nmap
```
┌──(kali㉿kali)-[~/HTB/sauna-AD]
└─$ sudo nmap -T5 -p- -A -oN nmap 10.129.113.161
[sudo] password for kali: 
Starting Nmap 7.95 ( https://nmap.org ) at 2025-01-22 23:44 EST
Nmap scan report for 10.129.113.161
Host is up (0.054s latency).
Not shown: 65516 filtered tcp ports (no-response)
PORT      STATE SERVICE       VERSION
53/tcp    open  domain        Simple DNS Plus
80/tcp    open  http          Microsoft IIS httpd 10.0
| http-methods: 
|_  Potentially risky methods: TRACE
|_http-title: Egotistical Bank :: Home
|_http-server-header: Microsoft-IIS/10.0
88/tcp    open  kerberos-sec  Microsoft Windows Kerberos (server time: 2025-01-23 11:46:44Z)
135/tcp   open  msrpc         Microsoft Windows RPC
139/tcp   open  netbios-ssn   Microsoft Windows netbios-ssn
389/tcp   open  ldap          Microsoft Windows Active Directory LDAP (Domain: EGOTISTICAL-BANK.LOCAL0., Site: Default-First-Site-Name)
445/tcp   open  microsoft-ds?
464/tcp   open  kpasswd5?
593/tcp   open  ncacn_http    Microsoft Windows RPC over HTTP 1.0
636/tcp   open  tcpwrapped
3268/tcp  open  ldap          Microsoft Windows Active Directory LDAP (Domain: EGOTISTICAL-BANK.LOCAL0., Site: Default-First-Site-Name)
3269/tcp  open  tcpwrapped
5985/tcp  open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-title: Not Found
|_http-server-header: Microsoft-HTTPAPI/2.0
9389/tcp  open  mc-nmf        .NET Message Framing
49667/tcp open  msrpc         Microsoft Windows RPC
49673/tcp open  ncacn_http    Microsoft Windows RPC over HTTP 1.0
49674/tcp open  msrpc         Microsoft Windows RPC
49676/tcp open  msrpc         Microsoft Windows RPC
49696/tcp open  msrpc         Microsoft Windows RPC
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Device type: general purpose
Running (JUST GUESSING): Microsoft Windows 2019|10 (97%)
OS CPE: cpe:/o:microsoft:windows_server_2019 cpe:/o:microsoft:windows_10
Aggressive OS guesses: Windows Server 2019 (97%), Microsoft Windows 10 1903 - 21H1 (91%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 2 hops
Service Info: Host: SAUNA; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| smb2-security-mode: 
|   3:1:1: 
|_    Message signing enabled and required
|_clock-skew: 7h00m01s
| smb2-time: 
|   date: 2025-01-23T11:47:46
|_  start_date: N/A

TRACEROUTE (using port 53/tcp)
HOP RTT      ADDRESS
1   55.37 ms 10.10.14.1
2   55.69 ms 10.129.113.161

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 256.82 seconds
```

possible users
![Pasted image 20250203110345](<0. Attachments/Pasted image 20250203110345.png>)

https://github.com/urbanadventurer/username-anarchy/releases/tag/v0.6

[How To Attack Kerberos 101](https://m0chan.github.io/2019/07/31/How-To-Attack-Kerberos-101.html#as-rep-roasting)

![Pasted image 20250203111832](<0. Attachments/Pasted image 20250203111832.png>)

![Pasted image 20250203113408](<0. Attachments/Pasted image 20250203113408.png>)

using hashcat
![Pasted image 20250203114128](<0. Attachments/Pasted image 20250203114128.png>)
fsmith-->Thestrokes23

![Pasted image 20250203114726](<0. Attachments/Pasted image 20250203114726.png>)
![Pasted image 20250203114819](<0. Attachments/Pasted image 20250203114819.png>)

```
reg.exe query "HKLM\software\microsoft\windows nt\currentversion\winlogon"
```

![Pasted image 20250203115241](<0. Attachments/Pasted image 20250203115241.png>)

svc_loanmgr --> Moneymakestheworldgoround!

![Pasted image 20250203115326](<0. Attachments/Pasted image 20250203115326.png>)

![Pasted image 20250203115415](<0. Attachments/Pasted image 20250203115415.png>)

![Pasted image 20250203115511](<0. Attachments/Pasted image 20250203115511.png>)

![Pasted image 20250203115524](<0. Attachments/Pasted image 20250203115524.png>)

![Pasted image 20250203115540](<0. Attachments/Pasted image 20250203115540.png>)

My preferred way to do a DCSync attack is using `secretsdump.py`, which allows me to run DCSync attack from my Kali box, provided I can talk to the DC on TCP 445 and 135 and a high RPC port. This avoids fighting with AV, though it does create network traffic.

![Pasted image 20250203134102](<0. Attachments/Pasted image 20250203134102.png>)

![Pasted image 20250203135924](<0. Attachments/Pasted image 20250203135924.png>)

