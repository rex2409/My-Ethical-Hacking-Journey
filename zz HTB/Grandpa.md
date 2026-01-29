nmap
```
┌──(kali㉿kali)-[~/HTB/grandpa]
└─$ sudo nmap -T5 -p- -A -oN nmap 10.129.95.233            
[sudo] password for kali: 
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-12-24 22:34 EST
Nmap scan report for 10.129.95.233
Host is up (0.081s latency).
Not shown: 65534 filtered tcp ports (no-response)
PORT   STATE SERVICE VERSION
80/tcp open  http    Microsoft IIS httpd 6.0
| http-webdav-scan: 
|   Allowed Methods: OPTIONS, TRACE, GET, HEAD, COPY, PROPFIND, SEARCH, LOCK, UNLOCK
|   Server Type: Microsoft-IIS/6.0
|   Public Options: OPTIONS, TRACE, GET, HEAD, DELETE, PUT, POST, COPY, MOVE, MKCOL, PROPFIND, PROPPATCH, LOCK, UNLOCK, SEARCH
|   WebDAV type: Unknown
|_  Server Date: Wed, 25 Dec 2024 03:37:06 GMT
|_http-server-header: Microsoft-IIS/6.0
|_http-title: Under Construction
| http-methods: 
|_  Potentially risky methods: TRACE COPY PROPFIND SEARCH LOCK UNLOCK DELETE PUT MOVE MKCOL PROPPATCH
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Device type: general purpose
Running (JUST GUESSING): Microsoft Windows 2003|2008|XP|2000 (90%)
OS CPE: cpe:/o:microsoft:windows_server_2003::sp1 cpe:/o:microsoft:windows_server_2003::sp2 cpe:/o:microsoft:windows_server_2008::sp2 cpe:/o:microsoft:windows_xp::sp3 cpe:/o:microsoft:windows_2000::sp4
Aggressive OS guesses: Microsoft Windows Server 2003 SP1 or SP2 (90%), Microsoft Windows Server 2008 Enterprise SP2 (90%), Microsoft Windows Server 2003 SP2 (88%), Microsoft Windows XP SP3 (88%), Microsoft Windows 2000 SP4 or Windows XP Professional SP1 (88%), Microsoft Windows 2003 SP2 (87%), Microsoft Windows XP (85%), Microsoft Windows Server 2003 SP1 - SP2 (85%), Microsoft Windows XP SP2 or SP3 (85%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 2 hops
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

TRACEROUTE (using port 80/tcp)
HOP RTT      ADDRESS
1   82.14 ms 10.10.14.1
2   82.18 ms 10.129.95.233

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 142.65 seconds
```

```
┌──(kali㉿kali)-[~/HTB/grandpa]
└─$ nmap 10.129.95.233 -p 80 --script=http-webdav-scan
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-12-24 22:42 EST
Nmap scan report for 10.129.95.233
Host is up (0.081s latency).

PORT   STATE SERVICE
80/tcp open  http
| http-webdav-scan: 
|   Public Options: OPTIONS, TRACE, GET, HEAD, DELETE, PUT, POST, COPY, MOVE, MKCOL, PROPFIND, PROPPATCH, LOCK, UNLOCK, SEARCH
|   Server Type: Microsoft-IIS/6.0
|   Allowed Methods: OPTIONS, TRACE, GET, HEAD, COPY, PROPFIND, SEARCH, LOCK, UNLOCK
|   Server Date: Wed, 25 Dec 2024 03:42:56 GMT
|_  WebDAV type: Unknown

Nmap done: 1 IP address (1 host up) scanned in 1.13 seconds
```

```
┌──(kali㉿kali)-[~/HTB/grandpa]
└─$ dirsearch -u http://10.129.95.233 -x 400-599                      
/usr/lib/python3/dist-packages/dirsearch/dirsearch.py:23: DeprecationWarning: pkg_resources is deprecated as an API. See https://setuptools.pypa.io/en/latest/pkg_resources.html
  from pkg_resources import DistributionNotFound, VersionConflict

  _|. _ _  _  _  _ _|_    v0.4.3
 (_||| _) (/_(_|| (_| )

Extensions: php, aspx, jsp, html, js | HTTP method: GET | Threads: 25 | Wordlist size: 11460

Output File: /home/kali/HTB/grandpa/reports/http_10.129.95.233/_24-12-24_22-39-18.txt

Target: http://10.129.95.233/

[22:39:18] Starting: 
[22:39:38] 301 -  157B  - /_vti_bin  ->  http://10.129.95.233/%5Fvti%5Fbin/ 
[22:39:38] 200 -  195B  - /_vti_bin/_vti_adm/admin.dll                      
[22:39:38] 200 -  195B  - /_vti_bin/_vti_aut/author.dll                     
[22:39:38] 200 -   96B  - /_vti_bin/shtml.exe?_vti_rpc                      
[22:39:38] 200 -    2KB - /_vti_inf.html
[22:39:38] 200 -   96B  - /_vti_bin/shtml.dll                               
[22:40:40] 301 -  151B  - /images  ->  http://10.129.95.233/images/         
[22:41:17] 200 -    2KB - /postinfo.html                                    
                                                                             
Task Completed
```

[GitHub - g0rx/iis6-exploit-2017-CVE-2017-7269: iis6 exploit 2017 CVE-2017-7269](https://github.com/g0rx/iis6-exploit-2017-CVE-2017-7269)

![Pasted image 20241225120359](<0. Attachments/Pasted image 20241225120359.png>)

![Pasted image 20241225120345](<0. Attachments/Pasted image 20241225120345.png>)

trying
```
┌──(kali㉿kali)-[~/HTB/grandpa]
└─$ /home/kali/Windows-Exploit-Suggester/windows-exploit-suggester.py --update                       
[*] initiating winsploit version 3.3...
[+] writing to file 2024-12-24-mssb.xls
[*] done
                                                                                                                                                            
┌──(kali㉿kali)-[~/HTB/grandpa]
└─$ /home/kali/Windows-Exploit-Suggester/windows-exploit-suggester.py --database 2024-12-24-mssb.xls --systeminfo systeminfo
```

[Churrasco/churrasco.exe at master · Re4son/Churrasco · GitHub](https://github.com/Re4son/Churrasco/blob/master/churrasco.exe)

transfer files, we open a share
```
┌──(kali㉿kali)-[~/HTB/grandpa]
└─$ sudo python3 /home/kali/.local/bin/smbserver.py kali .
[sudo] password for kali: 
Impacket v0.12.0 - Copyright Fortra, LLC and its affiliated companies 
```

then we transfer
![Pasted image 20241225125512](<0. Attachments/Pasted image 20241225125512.png>)

now running churrasco to get back a priv esc connection
![Pasted image 20241225125725](<0. Attachments/Pasted image 20241225125725.png>)

![Pasted image 20241225125859](<0. Attachments/Pasted image 20241225125859.png>)
