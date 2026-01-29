nmap
```
┌──(kali㉿kali)-[~/HTB/solidstate]
└─$ sudo nmap -T5 -p- -A -oN nmap 10.129.203.111                     
[sudo] password for kali: 
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-01-14 01:06 EST
Warning: 10.129.203.111 giving up on port because retransmission cap hit (2).
Nmap scan report for 10.129.203.111
Host is up (0.045s latency).
Not shown: 64603 closed tcp ports (reset), 926 filtered tcp ports (no-response)
PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 7.4p1 Debian 10+deb9u1 (protocol 2.0)
| ssh-hostkey: 
|   2048 77:00:84:f5:78:b9:c7:d3:54:cf:71:2e:0d:52:6d:8b (RSA)
|   256 78:b8:3a:f6:60:19:06:91:f5:53:92:1d:3f:48:ed:53 (ECDSA)
|_  256 e4:45:e9:ed:07:4d:73:69:43:5a:12:70:9d:c4:af:76 (ED25519)
25/tcp   open  smtp?
|_smtp-commands: Couldn't establish connection on port 25
80/tcp   open  http    Apache httpd 2.4.25 ((Debian))
|_http-title: Home - Solid State Security
|_http-server-header: Apache/2.4.25 (Debian)
110/tcp  open  pop3?
119/tcp  open  nntp?
4555/tcp open  rsip?
Aggressive OS guesses: Linux 3.12 (96%), Linux 3.13 (96%), Linux 3.16 (96%), Linux 3.2 - 4.9 (96%), Linux 3.8 - 3.11 (96%), Linux 4.8 (96%), Linux 4.4 (95%), Linux 4.9 (95%), Linux 3.18 (95%), Linux 4.2 (95%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 2 hops
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE (using port 8888/tcp)
HOP RTT      ADDRESS
1   43.02 ms 10.10.14.1
2   46.12 ms 10.129.203.111

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 506.66 seconds



```

```
┌──(kali㉿kali)-[~/HTB/solidstate]
└─$ dirsearch -u http://10.129.203.111/
/usr/lib/python3/dist-packages/dirsearch/dirsearch.py:23: DeprecationWarning: pkg_resources is deprecated as an API. See https://setuptools.pypa.io/en/latest/pkg_resources.html
  from pkg_resources import DistributionNotFound, VersionConflict

  _|. _ _  _  _  _ _|_    v0.4.3
 (_||| _) (/_(_|| (_| )

Extensions: php, aspx, jsp, html, js | HTTP method: GET | Threads: 25 | Wordlist size: 11460

Output File: /home/kali/HTB/solidstate/reports/http_10.129.203.111/__25-01-14_01-07-04.txt

Target: http://10.129.203.111/

[01:07:04] Starting: 
[01:07:11] 403 -  300B  - /.ht_wsr.txt                                      
[01:07:12] 403 -  303B  - /.htaccess_orig                                   
[01:07:12] 403 -  303B  - /.htaccess.orig                                   
[01:07:12] 403 -  303B  - /.htaccess.save
[01:07:12] 403 -  305B  - /.htaccess.sample                                 
[01:07:12] 403 -  301B  - /.htaccessOLD
[01:07:12] 403 -  301B  - /.htaccessBAK
[01:07:12] 403 -  293B  - /.htm                                             
[01:07:12] 403 -  301B  - /.htaccess_sc                                     
[01:07:12] 403 -  303B  - /.htpasswd_test
[01:07:12] 403 -  304B  - /.htaccess_extra                                  
[01:07:12] 403 -  299B  - /.htpasswds
[01:07:12] 403 -  294B  - /.html                                            
[01:07:12] 403 -  303B  - /.htaccess.bak1
[01:07:12] 403 -  302B  - /.htaccessOLD2
[01:07:12] 403 -  300B  - /.httr-oauth                                      
[01:07:27] 200 -    3KB - /about.html                                       
[01:08:05] 301 -  317B  - /assets  ->  http://10.129.203.111/assets/        
[01:08:05] 200 -  471B  - /assets/                                          
[01:08:48] 200 -  573B  - /images/                                          
[01:08:48] 301 -  317B  - /images  ->  http://10.129.203.111/images/
[01:08:58] 200 -    6KB - /LICENSE.txt                                      
[01:09:41] 200 -  606B  - /README.txt                                       
[01:09:47] 403 -  303B  - /server-status/                                   
[01:09:48] 403 -  302B  - /server-status                                    
                                                                             
Task Completed
```

![Pasted image 20250114144133](<0. Attachments/Pasted image 20250114144133.png>)

![Pasted image 20250114144231](<0. Attachments/Pasted image 20250114144231.png>)

we can nc into james mailserver
![Pasted image 20250114145652](<0. Attachments/Pasted image 20250114145652.png>)

after changing creds, me check for mails
![Pasted image 20250114145928](<0. Attachments/Pasted image 20250114145928.png>)

![Pasted image 20250114150234](<0. Attachments/Pasted image 20250114150234.png>)
mindy - P@55W0rd1!2@

to quit
```
^]
telnet> quit
Connection closed.
```

my first time coming across rbash
![Pasted image 20250114150804](<0. Attachments/Pasted image 20250114150804.png>)

we can remove this rbash by adding a -t bash at the end of our ssh
![Pasted image 20250114151131](<0. Attachments/Pasted image 20250114151131.png>)

priv esc
we find a file in opt that root runs, so we can edit it to catch a rev shell
![Pasted image 20250114151414](<0. Attachments/Pasted image 20250114151414.png>)

![Pasted image 20250114151537](<0. Attachments/Pasted image 20250114151537.png>)

I was confused how to identify this as a james server but ig this is the easiest explanation
![Pasted image 20250114152136](<0. Attachments/Pasted image 20250114152136.png>)

