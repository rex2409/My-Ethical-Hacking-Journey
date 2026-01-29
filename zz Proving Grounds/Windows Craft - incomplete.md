```
┌──(kali㉿kali)-[~/PG/craft]
└─$ nmap -p- -Pn --min-rate 10000 192.168.140.169
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-11 23:10 EST
Nmap scan report for 192.168.140.169
Host is up (0.046s latency).
Not shown: 65534 filtered tcp ports (no-response)
PORT   STATE SERVICE
80/tcp open  http

Nmap done: 1 IP address (1 host up) scanned in 13.45 seconds

┌──(kali㉿kali)-[~/PG/craft]
└─$ nmap -p 80 -Pn -sCV 192.168.140.169
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-11 23:11 EST
Nmap scan report for 192.168.140.169
Host is up (0.047s latency).

PORT   STATE SERVICE VERSION
80/tcp open  http    Apache httpd 2.4.48 ((Win64) OpenSSL/1.1.1k PHP/8.0.7)
|_http-title: Craft
|_http-server-header: Apache/2.4.48 (Win64) OpenSSL/1.1.1k PHP/8.0.7

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 12.44 seconds
```

```
┌──(kali㉿kali)-[~/PG/craft]
└─$ dirsearch -u http://192.168.140.169/
/usr/lib/python3/dist-packages/dirsearch/dirsearch.py:23: DeprecationWarning: pkg_resources is deprecated as an API. See https://setuptools.pypa.io/en/latest/pkg_resources.html
  from pkg_resources import DistributionNotFound, VersionConflict

  _|. _ _  _  _  _ _|_    v0.4.3
 (_||| _) (/_(_|| (_| )

Extensions: php, aspx, jsp, html, js | HTTP method: GET | Threads: 25 | Wordlist size: 11460

Output File: /home/kali/PG/craft/reports/http_192.168.140.169/__25-02-11_23-14-11.txt

Target: http://192.168.140.169/

[23:14:11] Starting: 
[23:14:12] 403 -  304B  - /%C0%AE%C0%AE%C0%AF                               
[23:14:12] 403 -  304B  - /%3f/                                             
[23:14:12] 301 -  339B  - /js  ->  http://192.168.140.169/js/
[23:14:12] 403 -  304B  - /%ff                                              
[23:14:17] 403 -  304B  - /.ht_wsr.txt                                      
[23:14:17] 403 -  304B  - /.htaccess.orig                                   
[23:14:17] 403 -  304B  - /.htaccess.save                                   
[23:14:17] 403 -  304B  - /.htaccess.sample
[23:14:17] 403 -  304B  - /.htaccess_extra
[23:14:17] 403 -  304B  - /.htaccess_sc                                     
[23:14:17] 403 -  304B  - /.htaccessBAK
[23:14:17] 403 -  304B  - /.htaccess.bak1
[23:14:17] 403 -  304B  - /.htaccessOLD                                     
[23:14:17] 403 -  304B  - /.htaccessOLD2                                    
[23:14:17] 403 -  304B  - /.htm                                             
[23:14:17] 403 -  304B  - /.html
[23:14:17] 403 -  304B  - /.htaccess_orig
[23:14:17] 403 -  304B  - /.htpasswd_test                                   
[23:14:17] 403 -  304B  - /.htpasswds                                       
[23:14:18] 403 -  304B  - /.httr-oauth
[23:14:51] 301 -  343B  - /assets  ->  http://192.168.140.169/assets/       
[23:14:51] 200 -    1KB - /assets/                                          
[23:14:59] 403 -  304B  - /cgi-bin/                                         
[23:15:00] 200 -    2KB - /cgi-bin/printenv.pl                              
[23:15:07] 301 -  340B  - /css  ->  http://192.168.140.169/css/             
[23:15:18] 503 -  404B  - /examples                                         
[23:15:18] 503 -  404B  - /examples/jsp/snp/snoop.jsp                       
[23:15:18] 503 -  404B  - /examples/jsp/index.html
[23:15:18] 503 -  404B  - /examples/servlets/servlet/RequestHeaderExample
[23:15:18] 503 -  404B  - /examples/                                        
[23:15:18] 503 -  404B  - /examples/jsp/%252e%252e/%252e%252e/manager/html/
[23:15:18] 503 -  404B  - /examples/servlets/index.html
[23:15:18] 503 -  404B  - /examples/websocket/index.xhtml                   
[23:15:18] 503 -  404B  - /examples/servlets/servlet/CookieExample          
[23:15:18] 503 -  404B  - /examples/servlet/SnoopServlet
[23:15:29] 403 -  304B  - /index.php::$DATA                                 
[23:15:33] 200 -  981B  - /js/                                              
[23:15:57] 403 -  423B  - /phpmyadmin                                       
[23:16:00] 403 -  423B  - /phpmyadmin/doc/html/index.html                   
[23:16:00] 403 -  423B  - /phpmyadmin/docs/html/index.html                  
[23:16:00] 403 -  423B  - /phpmyadmin/phpmyadmin/index.php                  
[23:16:00] 403 -  423B  - /phpmyadmin/ChangeLog                             
[23:16:00] 403 -  423B  - /phpmyadmin/
[23:16:00] 403 -  423B  - /phpmyadmin/scripts/setup.php
[23:16:00] 403 -  423B  - /phpmyadmin/index.php                             
[23:16:00] 403 -  423B  - /phpmyadmin/README                                
[23:16:14] 403 -  423B  - /server-status                                    
[23:16:14] 403 -  423B  - /server-info                                      
[23:16:14] 403 -  423B  - /server-status/                                   
[23:16:34] 403 -  304B  - /Trace.axd::$DATA                                 
[23:16:36] 200 -  537B  - /upload.php                                       
[23:16:36] 301 -  344B  - /uploads  ->  http://192.168.140.169/uploads/     
[23:16:36] 200 -  777B  - /uploads/                                         
[23:16:45] 403 -  304B  - /web.config::$DATA                                
[23:16:45] 403 -  423B  - /webalizer                                        
[23:16:45] 403 -  423B  - /webalizer/                                       
                                                                             
Task Completed 
```

![Pasted image 20250212121320](<0. Attachments/Pasted image 20250212121320.png>)

![Pasted image 20250212121432](<0. Attachments/Pasted image 20250212121432.png>)

![Pasted image 20250212121705](<0. Attachments/Pasted image 20250212121705.png>)

[Proving Grounds Practice — Craft. This is an intermediate box on Offsec’s… | by Dpsypher | Medium](https://medium.com/@Dpsypher/proving-grounds-practice-craft-4a62baf140cc)

refer to above its very detailed