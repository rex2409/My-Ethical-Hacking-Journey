nmap
```
┌──(kali㉿kali)-[~/HTB/beep]
└─$ sudo nmap -T5 -p- -A -oN nmap 10.129.255.251
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-01-06 00:33 EST
Warning: 10.129.255.251 giving up on port because retransmission cap hit (2).
Nmap scan report for 10.129.255.251
Host is up (0.047s latency).
Not shown: 64159 closed tcp ports (reset), 1360 filtered tcp ports (no-response)
PORT      STATE SERVICE    VERSION
22/tcp    open  ssh        OpenSSH 4.3 (protocol 2.0)
| ssh-hostkey: 
|   1024 ad:ee:5a:bb:69:37:fb:27:af:b8:30:72:a0:f9:6f:53 (DSA)
|_  2048 bc:c6:73:59:13:a1:8a:4b:55:07:50:f6:65:1d:6d:0d (RSA)
25/tcp    open  smtp?
|_smtp-commands: Couldn't establish connection on port 25
80/tcp    open  http       Apache httpd 2.2.3
|_http-server-header: Apache/2.2.3 (CentOS)
|_http-title: Did not follow redirect to https://10.129.255.251/
110/tcp   open  pop3?
111/tcp   open  rpcbind    2 (RPC #100000)
| rpcinfo: 
|   program version    port/proto  service
|   100000  2            111/tcp   rpcbind
|   100000  2            111/udp   rpcbind
|   100024  1            855/udp   status
|_  100024  1            858/tcp   status
143/tcp   open  imap?
443/tcp   open  ssl/http   Apache httpd 2.2.3 ((CentOS))
| ssl-cert: Subject: commonName=localhost.localdomain/organizationName=SomeOrganization/stateOrProvinceName=SomeState/countryName=--
| Not valid before: 2017-04-07T08:22:08
|_Not valid after:  2018-04-07T08:22:08
|_ssl-date: 2025-01-06T05:42:02+00:00; +5s from scanner time.
|_http-server-header: Apache/2.2.3 (CentOS)
|_http-title: Elastix - Login page
858/tcp   open  status     1 (RPC #100024)
993/tcp   open  imaps?
995/tcp   open  pop3s?
3306/tcp  open  mysql?
4190/tcp  open  sieve?
4445/tcp  open  upnotifyp?
4559/tcp  open  hylafax?
5038/tcp  open  asterisk   Asterisk Call Manager 1.1
10000/tcp open  http       MiniServ 1.570 (Webmin httpd)
|_http-title: Site doesn't have a title (text/html; Charset=iso-8859-1).
Device type: general purpose|media device|PBX|WAP|printer|specialized
Running (JUST GUESSING): Linux 2.6.X|2.4.X (96%), Linksys embedded (94%), Osmosys embedded (94%), HP embedded (94%), Enterasys embedded (94%), Netgear embedded (94%), Riverbed RiOS (93%)
OS CPE: cpe:/o:linux:linux_kernel:2.6.27 cpe:/o:linux:linux_kernel:2.6.18 cpe:/o:linux:linux_kernel:2.4.32 cpe:/h:linksys:wrv54g cpe:/h:enterasys:ap3620 cpe:/h:netgear:eva9100 cpe:/o:riverbed:rios
Aggressive OS guesses: Linux 2.6.27 (96%), Linux 2.6.9 - 2.6.30 (96%), Linux 2.6.27 (likely embedded) (96%), Linux 2.6.18 (95%), Linux 2.6.20-1 (Fedora Core 5) (95%), Linux 2.6.30 (95%), Linux 2.6.5 (Fedora Core 2) (95%), Linux 2.6.5 - 2.6.12 (95%), Elastix PBX (Linux 2.6.18) (95%), Linux 2.6.9 - 2.6.24 (95%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 2 hops
Service Info: Host: 127.0.0.1

Host script results:
|_clock-skew: 4s

TRACEROUTE (using port 554/tcp)
HOP RTT      ADDRESS
1   45.05 ms 10.10.14.1
2   45.06 ms 10.129.255.251

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 814.40 seconds
```

```
┌──(kali㉿kali)-[~/HTB/beep]
└─$ dirsearch -u http://10.129.255.251/            
/usr/lib/python3/dist-packages/dirsearch/dirsearch.py:23: DeprecationWarning: pkg_resources is deprecated as an API. See https://setuptools.pypa.io/en/latest/pkg_resources.html
  from pkg_resources import DistributionNotFound, VersionConflict

  _|. _ _  _  _  _ _|_    v0.4.3
 (_||| _) (/_(_|| (_| )

Extensions: php, aspx, jsp, html, js | HTTP method: GET | Threads: 25 | Wordlist size: 11460

Output File: /home/kali/HTB/beep/reports/http_10.129.255.251/__25-01-06_00-33-22.txt

Target: http://10.129.255.251/

[00:33:22] Starting: 
[00:33:25] 302 -  288B  - /%3f/  ->  https://10.129.255.251/?/
[00:33:25] 302 -  296B  - /%2e%2e//google.com  ->  https://10.129.255.251/google.com
[00:33:36] 403 -  292B  - /.ht_wsr.txt                                      
[00:33:37] 403 -  295B  - /.htaccess.bak1                                   
[00:33:37] 403 -  295B  - /.htaccess.orig                                   
[00:33:37] 403 -  295B  - /.htaccess.save                                   
[00:33:37] 403 -  297B  - /.htaccess.sample
[00:33:37] 403 -  293B  - /.htaccess_sc
[00:33:37] 403 -  293B  - /.htaccessBAK
[00:33:37] 403 -  293B  - /.htaccessOLD                                     
[00:33:37] 403 -  295B  - /.htaccess_orig                                   
[00:33:37] 403 -  285B  - /.htm
[00:33:37] 403 -  286B  - /.html                                            
[00:33:37] 403 -  295B  - /.htpasswd_test                                   
[00:33:37] 403 -  291B  - /.htpasswds                                       
[00:33:37] 403 -  292B  - /.httr-oauth                                      
[00:33:37] 403 -  294B  - /.htaccessOLD2
[00:33:38] 403 -  296B  - /.htaccess_extra                                  
[00:34:12] 403 -  317B  - /admin/views/ajax/autocomplete/user/a             
[00:34:47] 404 -  293B  - /cgi-bin/awstats/                                 
[00:34:47] 403 -  289B  - /cgi-bin/                                         
[00:34:47] 404 -  297B  - /cgi-bin/imagemap.exe?2,2                         
[00:34:47] 404 -  295B  - /cgi-bin/awstats.pl
[00:34:47] 404 -  295B  - /cgi-bin/htmlscript
[00:34:47] 404 -  296B  - /cgi-bin/htimage.exe?2,2                          
[00:34:47] 404 -  303B  - /cgi-bin/a1stats/a1disp.cgi
[00:34:47] 404 -  295B  - /cgi-bin/index.html
[00:34:47] 404 -  294B  - /cgi-bin/login.php
[00:34:47] 404 -  290B  - /cgi-bin/login
[00:34:47] 404 -  294B  - /cgi-bin/mt/mt.cgi
[00:34:47] 404 -  291B  - /cgi-bin/mt.cgi
[00:34:47] 404 -  298B  - /cgi-bin/mt-xmlrpc.cgi
[00:34:47] 404 -  294B  - /cgi-bin/login.cgi
[00:34:47] 404 -  296B  - /cgi-bin/ViewLog.asp
[00:34:47] 404 -  301B  - /cgi-bin/mt/mt-xmlrpc.cgi
[00:34:47] 404 -  296B  - /cgi-bin/printenv.pl
[00:34:47] 404 -  293B  - /cgi-bin/test-cgi
[00:34:47] 404 -  295B  - /cgi-bin/mt7/mt.cgi
[00:34:47] 404 -  293B  - /cgi-bin/printenv
[00:34:47] 404 -  302B  - /cgi-bin/mt7/mt-xmlrpc.cgi
[00:34:47] 404 -  292B  - /cgi-bin/php.ini                                  
[00:34:47] 404 -  293B  - /cgi-bin/test.cgi                                 
[00:35:09] 404 -  292B  - /error/error.log                                  
[00:35:09] 403 -  287B  - /error/                                           
[00:35:48] 200 -  548B  - /mailman/listinfo                                 
[00:35:48] 403 -  289B  - /mailman/                                         
                                                                             
Task Completed     
```

![Pasted image 20250107091243](<0. Attachments/Pasted image 20250107091243.png>)

```
┌──(kali㉿kali)-[~/HTB/beep]
└─$ gobuster dir -u https://10.129.229.183/ -w /home/kali/offsec/SecLists/Discovery/Web-Content/directory-list-2.3-medium.txt -k
===============================================================
Gobuster v3.6
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     https://10.129.229.183/
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /home/kali/offsec/SecLists/Discovery/Web-Content/directory-list-2.3-medium.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.6
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
/images               (Status: 301) [Size: 318] [--> https://10.129.229.183/images/]
/help                 (Status: 301) [Size: 316] [--> https://10.129.229.183/help/]
/themes               (Status: 301) [Size: 318] [--> https://10.129.229.183/themes/]
/modules              (Status: 301) [Size: 319] [--> https://10.129.229.183/modules/]
/mail                 (Status: 301) [Size: 316] [--> https://10.129.229.183/mail/]
/admin                (Status: 301) [Size: 317] [--> https://10.129.229.183/admin/]
/static               (Status: 301) [Size: 318] [--> https://10.129.229.183/static/]
/lang                 (Status: 301) [Size: 316] [--> https://10.129.229.183/lang/]
/var                  (Status: 301) [Size: 315] [--> https://10.129.229.183/var/]
/panel                (Status: 301) [Size: 317] [--> https://10.129.229.183/panel/]
/libs                 (Status: 301) [Size: 316] [--> https://10.129.229.183/libs/]
/recordings           (Status: 301) [Size: 322] [--> https://10.129.229.183/recordings/]
/configs              (Status: 301) [Size: 319] [--> https://10.129.229.183/configs/]
Progress: 49857 / 220560 (22.60%)[ERROR] Get "https://10.129.229.183/xfiles": context deadline exceeded (Client.Timeout exceeded while awaiting headers)
Progress: 137667 / 220560 (62.42%)[ERROR] Get "https://10.129.229.183/metanews": EOF
[ERROR] Get "https://10.129.229.183/metea": EOF
/vtigercrm            (Status: 301) [Size: 321] [--> https://10.129.229.183/vtigercrm/]
Progress: 220559 / 220560 (100.00%)
===============================================================
Finished
===============================================================
                                                                  
```

LFI
![Pasted image 20250107111410](<0. Attachments/Pasted image 20250107111410.png>)

![Pasted image 20250107111446](<0. Attachments/Pasted image 20250107111446.png>)

![Pasted image 20250107111823](<0. Attachments/Pasted image 20250107111823.png>)

logged in as root via password found from LFI
![Pasted image 20250107113018](<0. Attachments/Pasted image 20250107113018.png>)

created a cron job to gove back a reverse shell
![Pasted image 20250107113748](<0. Attachments/Pasted image 20250107113748.png>)

![Pasted image 20250107113813](<0. Attachments/Pasted image 20250107113813.png>)

![Pasted image 20250107114057](<0. Attachments/Pasted image 20250107114057.png>)

