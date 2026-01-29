nmap
```
┌──(kali㉿kali)-[~/HTB/poison]
└─$ sudo nmap -T5 -p- -A -oN nmap 10.129.1.254 
[sudo] password for kali: 
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-01-08 22:47 EST
Warning: 10.129.1.254 giving up on port because retransmission cap hit (2).
Nmap scan report for 10.129.1.254
Host is up (0.044s latency).
Not shown: 64242 closed tcp ports (reset), 1291 filtered tcp ports (no-response)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.2 (FreeBSD 20161230; protocol 2.0)
| ssh-hostkey: 
|   2048 e3:3b:7d:3c:8f:4b:8c:f9:cd:7f:d2:3a:ce:2d:ff:bb (RSA)
|   256 4c:e8:c6:02:bd:fc:83:ff:c9:80:01:54:7d:22:81:72 (ECDSA)
|_  256 0b:8f:d5:71:85:90:13:85:61:8b:eb:34:13:5f:94:3b (ED25519)
80/tcp open  http    Apache httpd 2.4.29 ((FreeBSD) PHP/5.6.32)
|_http-title: Site doesn't have a title (text/html; charset=UTF-8).
|_http-server-header: Apache/2.4.29 (FreeBSD) PHP/5.6.32
Aggressive OS guesses: FreeBSD 11.1-RELEASE (97%), FreeBSD 11.0-RELEASE (96%), FreeBSD 11.2-RELEASE - 11.3 RELEASE or 11.2-STABLE (96%), FreeBSD 11.1-STABLE (95%), FreeBSD 11.0-RELEASE - 12.0-CURRENT (95%), FreeBSD 11.0-CURRENT (94%), FreeBSD 11.3-RELEASE (93%), FreeBSD 12.0-RELEASE - 13.0-CURRENT (93%), FreeBSD 11.2-RELEASE - 11.3-RELEASE (93%), FreeBSD 11.0-STABLE (92%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 2 hops
Service Info: OS: FreeBSD; CPE: cpe:/o:freebsd:freebsd

TRACEROUTE (using port 5900/tcp)
HOP RTT      ADDRESS
1   43.11 ms 10.10.14.1
2   43.33 ms 10.129.1.254

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 669.94 seconds
```

```
┌──(kali㉿kali)-[~/HTB/poison]
└─$ dirsearch -u http://10.129.1.254/      
/usr/lib/python3/dist-packages/dirsearch/dirsearch.py:23: DeprecationWarning: pkg_resources is deprecated as an API. See https://setuptools.pypa.io/en/latest/pkg_resources.html
  from pkg_resources import DistributionNotFound, VersionConflict

  _|. _ _  _  _  _ _|_    v0.4.3
 (_||| _) (/_(_|| (_| )

Extensions: php, aspx, jsp, html, js | HTTP method: GET | Threads: 25 | Wordlist size: 11460

Output File: /home/kali/HTB/poison/reports/http_10.129.1.254/__25-01-08_22-47-51.txt

Target: http://10.129.1.254/

[22:47:51] Starting: 
[22:47:59] 403 -  223B  - /.htaccess.bak1                                   
[22:47:59] 403 -  224B  - /.htaccess_extra
[22:47:59] 403 -  223B  - /.htaccess.save                                   
[22:47:59] 403 -  220B  - /.ht_wsr.txt
[22:47:59] 403 -  223B  - /.htaccess_orig                                   
[22:47:59] 403 -  221B  - /.htaccess_sc
[22:47:59] 403 -  221B  - /.htaccessBAK
[22:47:59] 403 -  223B  - /.htaccess.orig
[22:47:59] 403 -  225B  - /.htaccess.sample
[22:47:59] 403 -  221B  - /.htaccessOLD                                     
[22:47:59] 403 -  222B  - /.htaccessOLD2                                    
[22:47:59] 403 -  213B  - /.htm
[22:47:59] 403 -  220B  - /.httr-oauth                                      
[22:47:59] 403 -  223B  - /.htpasswd_test                                   
[22:47:59] 403 -  214B  - /.html                                            
[22:47:59] 403 -  219B  - /.htpasswds                                       
[22:49:00] 403 -  225B  - /cgi-bin/printenv                                 
[22:49:00] 403 -  225B  - /cgi-bin/test-cgi                                 
[22:49:45] 200 -  157B  - /info.php                                         
[22:50:17] 200 -   68KB - /phpinfo.php    
```

![Pasted image 20250109120228](<0. Attachments/Pasted image 20250109120228.png>)

![Pasted image 20250109120243](<0. Attachments/Pasted image 20250109120243.png>)

![Pasted image 20250109120258](<0. Attachments/Pasted image 20250109120258.png>)

![Pasted image 20250109120315](<0. Attachments/Pasted image 20250109120315.png>)

![Pasted image 20250109120332](<0. Attachments/Pasted image 20250109120332.png>)

decoding the base64 password (i guess because it looks like its b64 encoded)
```
data=$(cat pwd.b64); for i in $(seq 1 13); do data=$(echo $data | tr -d ' ' | base64 -d); done; echo $data
```

![Pasted image 20250109120716](<0. Attachments/Pasted image 20250109120716.png>)

password - Charix!2#4%6&8(0

LFI
![Pasted image 20250109121058](<0. Attachments/Pasted image 20250109121058.png>)

![Pasted image 20250109121229](<0. Attachments/Pasted image 20250109121229.png>)

![Pasted image 20250109121455](<0. Attachments/Pasted image 20250109121455.png>)

getting the zip file
![Pasted image 20250109122228](<0. Attachments/Pasted image 20250109122228.png>)

no idea what it means
![Pasted image 20250109122423](<0. Attachments/Pasted image 20250109122423.png>)

interesting info (VNC)
![Pasted image 20250109122615](<0. Attachments/Pasted image 20250109122615.png>)

5801 and 5901 are VNC ports, for remote desktop access.

```
root   608   0.0  0.9  23620  8868 v0- I    04:47    0:00.04 Xvnc :1 -desktop X -httpd /usr/local/share/tightvnc/classes -auth /root/.Xauthority -geometry 1280x800 -depth 24 -rfbwait 120000 -rfbauth /root/.vnc/passwd -rfbport 5901 -localhost -nolisten tcp :1
charix 976   0.0  0.0    412   328  1  R+   05:25    0:00.00 grep vnc
```

using proxychains and ssh for RDP
![Pasted image 20250109123126](<0. Attachments/Pasted image 20250109123126.png>)

![Pasted image 20250109123223](<0. Attachments/Pasted image 20250109123223.png>)

CRACKING VNC Password
[GitHub - trinitronx/vncpasswd.py: A Python implementation of vncpasswd, w/decryption abilities & extra features ;-)](https://github.com/trinitronx/vncpasswd.py)
