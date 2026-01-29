nmap
```
┌──(kali㉿kali)-[~/HTB/legacy]
└─$ sudo nmap -T5 -p- -A -oN namp 10.129.248.73                
[sudo] password for kali: 
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-12-16 03:14 EST
Warning: 10.129.248.73 giving up on port because retransmission cap hit (2).
Nmap scan report for 10.129.248.73
Host is up (0.082s latency).
Not shown: 65064 closed tcp ports (reset), 468 filtered tcp ports (no-response)
PORT    STATE SERVICE      VERSION
135/tcp open  msrpc        Microsoft Windows RPC
139/tcp open  netbios-ssn  Microsoft Windows netbios-ssn
445/tcp open  microsoft-ds Windows XP microsoft-ds
Device type: general purpose|phone|media device
Running (JUST GUESSING): Microsoft Windows XP|2003|2000|PocketPC/CE (92%), Microsoft Windows Mobile 6.X|5.X (86%), Microsoft embedded (86%)
OS CPE: cpe:/o:microsoft:windows_xp::sp3 cpe:/o:microsoft:windows_server_2003::sp2 cpe:/o:microsoft:windows_2000::sp4 cpe:/o:microsoft:windows_ce:6.0 cpe:/o:microsoft:windows_mobile:6 cpe:/o:microsoft:windows_mobile:5
Aggressive OS guesses: Microsoft Windows XP SP3 (92%), Microsoft Windows Server 2003 SP2 (91%), Microsoft Windows 2000 SP4 or Windows XP Professional SP1 (91%), Microsoft Windows XP SP2 (90%), Microsoft Windows XP SP2 - SP3 (90%), Microsoft Windows XP SP2 or Windows Server 2003 SP2 (90%), Microsoft Windows 2003 SP2 (90%), Microsoft Windows XP SP2 or SP3 (90%), Microsoft Windows XP Professional SP2 (90%), Microsoft Windows 2000 (90%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 2 hops
Service Info: OSs: Windows, Windows XP; CPE: cpe:/o:microsoft:windows, cpe:/o:microsoft:windows_xp

Host script results:
| smb-os-discovery: 
|   OS: Windows XP (Windows 2000 LAN Manager)
|   OS CPE: cpe:/o:microsoft:windows_xp::-
|   Computer name: legacy
|   NetBIOS computer name: LEGACY\x00
|   Workgroup: HTB\x00
|_  System time: 2024-12-21T12:19:04+02:00
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
|_nbstat: NetBIOS name: nil, NetBIOS user: <unknown>, NetBIOS MAC: 00:50:56:b9:4a:38 (VMware)
|_smb2-time: Protocol negotiation failed (SMB2)
|_clock-skew: mean: 5d00h57m39s, deviation: 1h24m51s, median: 4d23h57m39s

TRACEROUTE (using port 8080/tcp)
HOP RTT      ADDRESS
1   80.06 ms 10.10.14.1
2   80.20 ms 10.129.248.73

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 431.93 seconds
```

```
┌──(kali㉿kali)-[~/HTB/legacy]
└─$ sudo nmap -T5 10.129.248.73 --script=smb-vuln*
[sudo] password for kali: 
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-12-16 03:37 EST
Warning: 10.129.248.73 giving up on port because retransmission cap hit (2).
Nmap scan report for 10.129.248.73
Host is up (0.080s latency).
Not shown: 997 closed tcp ports (reset)
PORT    STATE SERVICE
135/tcp open  msrpc
139/tcp open  netbios-ssn
445/tcp open  microsoft-ds

Host script results:
|_smb-vuln-ms10-054: false
|_smb-vuln-ms10-061: ERROR: Script execution failed (use -d to debug)
| smb-vuln-ms17-010: 
|   VULNERABLE:
|   Remote Code Execution vulnerability in Microsoft SMBv1 servers (ms17-010)
|     State: VULNERABLE
|     IDs:  CVE:CVE-2017-0143
|     Risk factor: HIGH
|       A critical remote code execution vulnerability exists in Microsoft SMBv1
|        servers (ms17-010).
|           
|     Disclosure date: 2017-03-14
|     References:
|       https://technet.microsoft.com/en-us/library/security/ms17-010.aspx
|       https://blogs.technet.microsoft.com/msrc/2017/05/12/customer-guidance-for-wannacrypt-attacks/
|_      https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-0143
| smb-vuln-ms08-067: 
|   VULNERABLE:
|   Microsoft Windows system vulnerable to remote code execution (MS08-067)
|     State: VULNERABLE
|     IDs:  CVE:CVE-2008-4250
|           The Server service in Microsoft Windows 2000 SP4, XP SP2 and SP3, Server 2003 SP1 and SP2,
|           Vista Gold and SP1, Server 2008, and 7 Pre-Beta allows remote attackers to execute arbitrary
|           code via a crafted RPC request that triggers the overflow during path canonicalization.
|           
|     Disclosure date: 2008-10-23
|     References:
|       https://technet.microsoft.com/en-us/library/security/ms08-067.aspx
|_      https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2008-4250

Nmap done: 1 IP address (1 host up) scanned in 19.03 seconds
```

```
C:\>set
set
ALLUSERSPROFILE=C:\Documents and Settings\All Users
CommonProgramFiles=C:\Program Files\Common Files
COMPUTERNAME=LEGACY
ComSpec=C:\WINDOWS\system32\cmd.exe
FP_NO_HOST_CHECK=NO
NUMBER_OF_PROCESSORS=1
OS=Windows_NT
Path=C:\WINDOWS\system32;C:\WINDOWS;C:\WINDOWS\System32\Wbem
PATHEXT=.COM;.EXE;.BAT;.CMD;.VBS;.VBE;.JS;.JSE;.WSF;.WSH
PROCESSOR_ARCHITECTURE=x86
PROCESSOR_IDENTIFIER=x86 Family 23 Model 49 Stepping 0, AuthenticAMD
PROCESSOR_LEVEL=23
PROCESSOR_REVISION=3100
ProgramFiles=C:\Program Files
PROMPT=$P$G
SystemDrive=C:
SystemRoot=C:\WINDOWS
TEMP=C:\WINDOWS\system32\config\SYSTEM~1\LOCALS~1\Temp
TMP=C:\WINDOWS\system32\config\SYSTEM~1\LOCALS~1\Temp
USERDOMAIN=HTB
USERNAME=LEGACY$
USERPROFILE=C:\WINDOWS\system32\config\systemprofile
windir=C:\WINDOWS
```

setting up an smbserver
```
┌──(kali㉿kali)-[~/HTB/legacy]
└─$ sudo python3 /home/kali/.local/bin/smbserver.py kali .
Impacket v0.12.0 - Copyright Fortra, LLC and its affiliated companies 

[*] Config file parsed
[*] Callback added for UUID 4B324FC8-1670-01D3-1278-5A47BF6EE188 V:3.0
[*] Callback added for UUID 6BFFD098-A112-3610-9833-46C3F87E345A V:1.0
[*] Config file parsed
[*] Config file parsed
12/16/2024 03:57:09 AM: INFO: Config file parsed
12/16/2024 03:58:01 AM: INFO: Incoming connection (10.10.14.4,53534)
12/16/2024 03:58:03 AM: INFO: AUTHENTICATE_MESSAGE (WORKGROUP\kali,KALI)
12/16/2024 03:58:03 AM: INFO: User KALI\kali authenticated successfully
```

checking if its working
```
┌──(kali㉿kali)-[~/HTB/legacy]
└─$ smbclient //10.10.14.4/kali                                                
Password for [WORKGROUP\kali]:
Try "help" to get a list of possible commands.
smb: \> ls
  .                                   D     4096  Mon Dec 16 03:53:55 2024
  ..                                  D     4096  Mon Dec 16 03:12:59 2024
  namp                               AN     2497  Mon Dec 16 03:21:34 2024
  whoami.exe                         AN   146289  Mon Dec 16 03:53:55 2024

                148529400 blocks of size 7680. 148529400 blocks available
```

