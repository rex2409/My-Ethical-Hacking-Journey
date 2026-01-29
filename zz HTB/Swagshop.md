nmap
```
┌──(kali㉿kali)-[~/HTB/swagshop]
└─$ sudo nmap -T5 -p- -A -oN nmap 10.129.229.138                                 
[sudo] password for kali: 
Starting Nmap 7.95 ( https://nmap.org ) at 2025-01-14 19:15 EST
Warning: 10.129.229.138 giving up on port because retransmission cap hit (2).
Nmap scan report for 10.129.229.138
Host is up (0.044s latency).
Not shown: 65112 closed tcp ports (reset), 421 filtered tcp ports (no-response)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.7 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 b6:55:2b:d2:4e:8f:a3:81:72:61:37:9a:12:f6:24:ec (RSA)
|   256 2e:30:00:7a:92:f0:89:30:59:c1:77:56:ad:51:c0:ba (ECDSA)
|_  256 4c:50:d5:f2:70:c5:fd:c4:b2:f0:bc:42:20:32:64:34 (ED25519)
80/tcp open  http    Apache httpd 2.4.29 ((Ubuntu))
|_http-title: Did not follow redirect to http://swagshop.htb/
|_http-server-header: Apache/2.4.29 (Ubuntu)
Device type: general purpose
Running: Linux 4.X|5.X
OS CPE: cpe:/o:linux:linux_kernel:4 cpe:/o:linux:linux_kernel:5
OS details: Linux 4.15 - 5.19
Network Distance: 2 hops
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE (using port 8888/tcp)
HOP RTT      ADDRESS
1   42.13 ms 10.10.14.1
2   42.42 ms 10.129.229.138

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 105.27 seconds
```

```
┌──(kali㉿kali)-[~/HTB/swagshop]
└─$ dirsearch -u http://10.129.229.138/ 
/usr/lib/python3/dist-packages/dirsearch/dirsearch.py:23: DeprecationWarning: pkg_resources is deprecated as an API. See https://setuptools.pypa.io/en/latest/pkg_resources.html
  from pkg_resources import DistributionNotFound, VersionConflict

  _|. _ _  _  _  _ _|_    v0.4.3
 (_||| _) (/_(_|| (_| )

Extensions: php, aspx, jsp, html, js | HTTP method: GET | Threads: 25 | Wordlist size: 11460

Output File: /home/kali/HTB/swagshop/reports/http_10.129.229.138/__25-01-14_19-15-22.txt

Target: http://10.129.229.138/

[19:15:22] Starting: 
[19:15:27] 301 -  313B  - /js  ->  http://10.129.229.138/js/                
[19:15:30] 403 -  279B  - /.ht_wsr.txt                                      
[19:15:30] 403 -  279B  - /.htaccess.orig                                   
[19:15:30] 403 -  279B  - /.htaccess.sample                                 
[19:15:30] 403 -  279B  - /.htaccess.bak1
[19:15:30] 403 -  279B  - /.htaccess_extra                                  
[19:15:30] 403 -  279B  - /.htaccess_sc
[19:15:30] 403 -  279B  - /.htaccessBAK
[19:15:30] 403 -  279B  - /.htaccess.save
[19:15:30] 403 -  279B  - /.html                                            
[19:15:30] 403 -  279B  - /.htaccess_orig                                   
[19:15:30] 403 -  279B  - /.htaccessOLD                                     
[19:15:30] 403 -  279B  - /.htm
[19:15:30] 403 -  279B  - /.htpasswd_test
[19:15:30] 403 -  279B  - /.htpasswds
[19:15:30] 403 -  279B  - /.httr-oauth                                      
[19:15:30] 403 -  279B  - /.htaccessOLD2                                    
[19:15:34] 403 -  279B  - /.php                                             
[19:15:34] 403 -  279B  - /.php3
[19:16:06] 200 -   37B  - /api.php                                          
[19:16:07] 301 -  314B  - /app  ->  http://10.129.229.138/app/              
[19:16:07] 200 -  527B  - /app/                                             
[19:16:07] 200 -    1KB - /app/etc/config.xml                               
[19:16:07] 200 -  998B  - /app/etc/local.xml                                
[19:16:07] 200 -    3KB - /app/etc/local.xml.additional                     
[19:16:07] 200 -  895B  - /app/etc/local.xml.template                       
[19:16:23] 200 -    0B  - /cron.php                                         
[19:16:23] 200 -  717B  - /cron.sh                                          
[19:16:32] 200 -  575B  - /errors/                                          
[19:16:32] 301 -  317B  - /errors  ->  http://10.129.229.138/errors/        
[19:16:34] 200 -    1KB - /favicon.ico                                      
[19:16:41] 404 -    0B  - /get.php                                          
[19:16:47] 200 -  460B  - /includes/                                        
[19:16:47] 301 -  319B  - /includes  ->  http://10.129.229.138/includes/    
[19:16:48] 200 -   44B  - /install.php                                      
[19:16:49] 200 -   44B  - /install.php?profile=default                      
[19:16:51] 200 -  703B  - /js/tiny_mce/                                     
[19:16:51] 301 -  322B  - /js/tiny_mce  ->  http://10.129.229.138/js/tiny_mce/
[19:16:51] 404 -   52B  - /js/
[19:16:53] 301 -  314B  - /lib  ->  http://10.129.229.138/lib/              
[19:16:53] 200 -  556B  - /lib/                                             
[19:16:53] 200 -    4KB - /LICENSE.txt                                      
[19:17:00] 301 -  316B  - /media  ->  http://10.129.229.138/media/          
[19:17:00] 200 -  506B  - /media/                                           
[19:17:15] 200 -  886B  - /php.ini.sample                                   
[19:17:20] 301 -  318B  - /pkginfo  ->  http://10.129.229.138/pkginfo/      
[19:17:26] 200 -  571KB - /RELEASE_NOTES.txt                                
[19:17:30] 403 -  279B  - /server-status/                                   
[19:17:30] 403 -  279B  - /server-status                                    
[19:17:32] 301 -  316B  - /shell  ->  http://10.129.229.138/shell/          
[19:17:32] 200 -  508B  - /shell/                                           
[19:17:36] 301 -  315B  - /skin  ->  http://10.129.229.138/skin/            
[19:17:54] 301 -  314B  - /var  ->  http://10.129.229.138/var/                
[19:17:54] 200 -  574B  - /var/cache/                                       
[19:17:54] 200 -  412B  - /var/backups/
[19:17:54] 200 -  582B  - /var/                                             
[19:17:54] 200 -    1KB - /var/package/                                     
                                                                             
Task Completed 
```

![Pasted image 20250115082850](<0. Attachments/Pasted image 20250115082850.png>)

![Pasted image 20250115083229](<0. Attachments/Pasted image 20250115083229.png>)

![Pasted image 20250115083256](<0. Attachments/Pasted image 20250115083256.png>)

[Magento-Shoplift-SQLI/poc.py at master · joren485/Magento-Shoplift-SQLI · GitHub](https://github.com/joren485/Magento-Shoplift-SQLI/blob/master/poc.py)

![Pasted image 20250115085518](<0. Attachments/Pasted image 20250115085518.png>)

![Pasted image 20250115085652](<0. Attachments/Pasted image 20250115085652.png>)

![Pasted image 20250115085754](<0. Attachments/Pasted image 20250115085754.png>)

requirement for an exploit 
![Pasted image 20250115090321](<0. Attachments/Pasted image 20250115090321.png>)

above exploit does not work

refer - [[HTB] SwagShop — Write-up. Welcome to the hackthebox write-up for… | by bigb0ss | Medium](https://bigb0ss.medium.com/htb-swagshop-write-up-50a560aa7a56)

![Pasted image 20250115104248](<0. Attachments/Pasted image 20250115104248.png>)

![Pasted image 20250115104412](<0. Attachments/Pasted image 20250115104412.png>)
