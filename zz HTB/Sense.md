nmap
```
┌──(kali㉿kali)-[~/HTB/sense]
└─$ sudo nmap -T5 -p- -A -oN nmap 10.129.254.100
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-01-01 20:29 EST
Nmap scan report for 10.129.254.100
Host is up (0.082s latency).
Not shown: 65533 filtered tcp ports (no-response)
PORT    STATE SERVICE  VERSION
80/tcp  open  http     lighttpd 1.4.35
|_http-server-header: lighttpd/1.4.35
|_http-title: Did not follow redirect to https://10.129.254.100/
443/tcp open  ssl/http lighttpd 1.4.35
|_ssl-date: TLS randomness does not represent time
|_http-server-header: lighttpd/1.4.35
| ssl-cert: Subject: commonName=Common Name (eg, YOUR name)/organizationName=CompanyName/stateOrProvinceName=Somewhere/countryName=US
| Not valid before: 2017-10-14T19:21:35
|_Not valid after:  2023-04-06T19:21:35
|_http-title: Login
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Device type: general purpose
Running (JUST GUESSING): OpenBSD 4.X (90%), Linux 2.6.X (87%)
OS CPE: cpe:/o:openbsd:openbsd:4.0 cpe:/o:linux:linux_kernel:2.6.29
Aggressive OS guesses: OpenBSD 4.0 (90%), Linux 2.6.29 (87%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 2 hops

TRACEROUTE (using port 443/tcp)
HOP RTT      ADDRESS
1   81.36 ms 10.10.14.1
2   82.29 ms 10.129.254.100

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 121.67 seconds
```


**By default it does not search txt files**
```
┌──(kali㉿kali)-[~/HTB/sense]
└─$ dirsearch -u https://10.129.254.100/
/usr/lib/python3/dist-packages/dirsearch/dirsearch.py:23: DeprecationWarning: pkg_resources is deprecated as an API. See https://setuptools.pypa.io/en/latest/pkg_resources.html
  from pkg_resources import DistributionNotFound, VersionConflict

  _|. _ _  _  _  _ _|_    v0.4.3
 (_||| _) (/_(_|| (_| )

Extensions: php, aspx, jsp, html, js | HTTP method: GET | Threads: 25 | Wordlist size: 11460

Output File: /home/kali/HTB/sense/reports/https_10.129.254.100/__25-01-01_20-36-23.txt

Target: https://10.129.254.100/

[20:36:24] Starting: 
[20:36:31] 403 -  345B  - /.dep.inc                                         
[20:36:32] 403 -  345B  - /.env~                                            
[20:36:34] 403 -  345B  - /.gitignore~                                      
[20:36:36] 403 -  345B  - /.inc                                             
[20:36:42] 403 -  345B  - /.ssh/id_rsa.priv~                                
[20:36:42] 403 -  345B  - /.ssh/id_rsa.key~                                 
[20:36:42] 403 -  345B  - /.ssh/id_rsa~                                     
[20:36:42] 403 -  345B  - /.ssh/know_hosts~                                 
[20:36:42] 403 -  345B  - /.ssh/id_rsa.pub~                                 
[20:36:43] 403 -  345B  - /.travis.yml~                                     
[20:36:49] 403 -  345B  - /_config.inc                                      
[20:36:58] 403 -  345B  - /admin/includes/configure.php~                    
[20:37:19] 403 -  345B  - /adovbs.inc                                       
[20:37:22] 403 -  345B  - /app/config/database.yml~                         
[20:37:24] 403 -  345B  - /auth.inc                                         
[20:37:26] 403 -  345B  - /backup.inc                                       
[20:37:26] 403 -  345B  - /backups.inc                                      
[20:37:31] 403 -  345B  - /cabal.project.local~                             
[20:37:33] 200 -  199B  - /changelog.txt                                    
[20:37:35] 301 -    0B  - /classes  ->  https://10.129.254.100/classes/     
[20:37:36] 403 -  345B  - /common.inc                                       
[20:37:36] 403 -  345B  - /conf.inc.php~                                    
[20:37:37] 403 -  345B  - /config.inc.php~                                  
[20:37:37] 403 -  345B  - /config.inc~                                      
[20:37:37] 403 -  345B  - /config.local.php~                                
[20:37:37] 403 -  345B  - /config.php.inc                                   
[20:37:37] 403 -  345B  - /config.php~                                      
[20:37:37] 403 -  345B  - /config.php.inc~
[20:37:37] 403 -  345B  - /config.inc                                       
[20:37:37] 403 -  345B  - /config/db.inc                                    
[20:37:37] 403 -  345B  - /config/config.inc
[20:37:37] 403 -  345B  - /config/database.yml~                             
[20:37:37] 403 -  345B  - /config/settings.inc                              
[20:37:38] 403 -  345B  - /configuration~                                   
[20:37:38] 403 -  345B  - /configuration.inc.php~
[20:37:38] 403 -  345B  - /configuration.php~                               
[20:37:38] 403 -  345B  - /config~                                          
[20:37:38] 403 -  345B  - /connect.inc                                      
[20:37:38] 403 -  345B  - /conf~                                            
[20:37:41] 301 -    0B  - /css  ->  https://10.129.254.100/css/             
[20:37:42] 403 -  345B  - /database.inc                                     
[20:37:42] 403 -  345B  - /database.yml~                                    
[20:37:42] 403 -  345B  - /database_credentials.inc                         
[20:37:42] 403 -  345B  - /db.inc                                           
[20:37:43] 403 -  345B  - /debug.inc                                        
[20:37:47] 403 -  345B  - /dump.inc                                         
[20:37:48] 200 -    6KB - /edit.php                                         
[20:37:52] 200 -    1KB - /favicon.ico                                      
[20:37:57] 403 -  345B  - /globals.inc                                      
[20:38:02] 403 -  345B  - /inc/config.inc                                   
[20:38:03] 403 -  345B  - /includes/bootstrap.inc                           
[20:38:03] 403 -  345B  - /includes/adovbs.inc                              
[20:38:03] 403 -  345B  - /includes/configure.php~
[20:38:03] 301 -    0B  - /includes  ->  https://10.129.254.100/includes/
[20:38:03] 200 -  329B  - /index.html                                       
[20:38:03] 403 -  345B  - /index.inc                                        
[20:38:03] 403 -  345B  - /index.php~                                       
[20:38:04] 403 -  345B  - /index~                                           
[20:38:05] 403 -  345B  - /install.inc                                      
[20:38:05] 301 -    0B  - /installer  ->  https://10.129.254.100/installer/ 
[20:38:06] 301 -    0B  - /javascript  ->  https://10.129.254.100/javascript/
[20:38:15] 200 -    6KB - /license.php                                      
[20:38:16] 403 -  345B  - /localsettings.php~                               
[20:38:39] 403 -  345B  - /php.ini~                                         
[20:38:54] 403 -  345B  - /revision.inc                                     
[20:38:56] 403 -  345B  - /sample.txt~                                      
[20:39:00] 403 -  345B  - /settings.php~                                    
[20:39:09] 403 -  345B  - /sql.inc                                          
[20:39:12] 200 -    6KB - /stats.php                                        
[20:39:12] 200 -    6KB - /status.php                                       
[20:39:16] 200 -    6KB - /system.php                                       
[20:39:20] 301 -    0B  - /themes  ->  https://10.129.254.100/themes/       
[20:39:37] 403 -  345B  - /wp-config.inc                                    
[20:39:38] 403 -  345B  - /wp-config.php~                                   
[20:39:38] 403 -  345B  - /wp-config.php.inc                                
[20:39:41] 200 -  384B  - /xmlrpc.php                                       
                                                                             
Task Completed                       
```

![Pasted image 20250102095623](<0. Attachments/Pasted image 20250102095623.png>)

![Pasted image 20250102095638](<0. Attachments/Pasted image 20250102095638.png>)

I need to focus more on directory busting, always end up short on this.

![Pasted image 20250102135745](<0. Attachments/Pasted image 20250102135745.png>)

![Pasted image 20250102153911](<0. Attachments/Pasted image 20250102153911.png>)

[Default Username and Password | pfSense Documentation](https://docs.netgate.com/pfsense/en/latest/usermanager/defaults.html)

![Pasted image 20250102153222](<0. Attachments/Pasted image 20250102153222.png>)

![Pasted image 20250102153956](<0. Attachments/Pasted image 20250102153956.png>)

![Pasted image 20250102154016](<0. Attachments/Pasted image 20250102154016.png>)

![Pasted image 20250102154038](<0. Attachments/Pasted image 20250102154038.png>)

![Pasted image 20250102154105](<0. Attachments/Pasted image 20250102154105.png>)
