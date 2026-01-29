nmap
```
┌──(kali㉿kali)-[~/HTB/servmon]
└─$ sudo nmap -T5 -p- -A -oN nmap 10.129.227.77 
[sudo] password for kali: 
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-01-13 01:57 EST
Warning: 10.129.227.77 giving up on port because retransmission cap hit (2).
Nmap scan report for 10.129.227.77
Host is up (0.050s latency).
Not shown: 64555 closed tcp ports (reset), 964 filtered tcp ports (no-response)
PORT      STATE SERVICE       VERSION
21/tcp    open  ftp           Microsoft ftpd
| ftp-syst: 
|_  SYST: Windows_NT
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
|_02-28-22  06:35PM       <DIR>          Users
22/tcp    open  ssh           OpenSSH for_Windows_8.0 (protocol 2.0)
| ssh-hostkey: 
|   3072 c7:1a:f6:81:ca:17:78:d0:27:db:cd:46:2a:09:2b:54 (RSA)
|   256 3e:63:ef:3b:6e:3e:4a:90:f3:4c:02:e9:40:67:2e:42 (ECDSA)
|_  256 5a:48:c8:cd:39:78:21:29:ef:fb:ae:82:1d:03:ad:af (ED25519)
80/tcp    open  http
|_http-title: Site doesn't have a title (text/html).
| fingerprint-strings: 
|   GetRequest, HTTPOptions, RTSPRequest: 
|     HTTP/1.1 200 OK
|     Content-type: text/html
|     Content-Length: 340
|     Connection: close
|     AuthInfo: 
|     <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
|     <html xmlns="http://www.w3.org/1999/xhtml">
|     <head>
|     <title></title>
|     <script type="text/javascript">
|     window.location.href = "Pages/login.htm";
|     </script>
|     </head>
|     <body>
|     </body>
|     </html>
|   X11Probe: 
|     HTTP/1.1 408 Request Timeout
|     Content-type: text/html
|     Content-Length: 0
|     Connection: close
|_    AuthInfo:
135/tcp   open  msrpc         Microsoft Windows RPC
139/tcp   open  netbios-ssn   Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds?
5666/tcp  open  tcpwrapped
6699/tcp  open  tcpwrapped
8443/tcp  open  ssl/https-alt
| http-title: NSClient++
|_Requested resource was /index.html
|_ssl-date: TLS randomness does not represent time
| ssl-cert: Subject: commonName=localhost
| Not valid before: 2020-01-14T13:24:20
|_Not valid after:  2021-01-13T13:24:20
| fingerprint-strings: 
|   FourOhFourRequest, HTTPOptions, RTSPRequest, SIPOptions: 
|     HTTP/1.1 404
|     Content-Length: 18
|     Document not found
|   GetRequest: 
|     HTTP/1.1 302
|     Content-Length: 0
|     Location: /index.html
|     iday
|     Sat:Saturday
|     workers
|_    jobs
49664/tcp open  msrpc         Microsoft Windows RPC
49665/tcp open  msrpc         Microsoft Windows RPC
49666/tcp open  msrpc         Microsoft Windows RPC
49667/tcp open  msrpc         Microsoft Windows RPC
49668/tcp open  msrpc         Microsoft Windows RPC
49669/tcp open  msrpc         Microsoft Windows RPC
49670/tcp open  msrpc         Microsoft Windows RPC
2 services unrecognized despite returning data. If you know the service/version, please submit the following fingerprints at https://nmap.org/cgi-bin/submit.cgi?new-service :
==============NEXT SERVICE FINGERPRINT (SUBMIT INDIVIDUALLY)==============
SF-Port80-TCP:V=7.94SVN%I=7%D=1/13%Time=6784B9DB%P=x86_64-pc-linux-gnu%r(G
SF:etRequest,1B4,"HTTP/1\.1\x20200\x20OK\r\nContent-type:\x20text/html\r\n
SF:Content-Length:\x20340\r\nConnection:\x20close\r\nAuthInfo:\x20\r\n\r\n
SF:\xef\xbb\xbf<!DOCTYPE\x20html\x20PUBLIC\x20\"-//W3C//DTD\x20XHTML\x201\
SF:.0\x20Transitional//EN\"\x20\"http://www\.w3\.org/TR/xhtml1/DTD/xhtml1-
SF:transitional\.dtd\">\r\n\r\n<html\x20xmlns=\"http://www\.w3\.org/1999/x
SF:html\">\r\n<head>\r\n\x20\x20\x20\x20<title></title>\r\n\x20\x20\x20\x2
SF:0<script\x20type=\"text/javascript\">\r\n\x20\x20\x20\x20\x20\x20\x20\x
SF:20window\.location\.href\x20=\x20\"Pages/login\.htm\";\r\n\x20\x20\x20\
SF:x20</script>\r\n</head>\r\n<body>\r\n</body>\r\n</html>\r\n")%r(HTTPOpt
SF:ions,1B4,"HTTP/1\.1\x20200\x20OK\r\nContent-type:\x20text/html\r\nConte
SF:nt-Length:\x20340\r\nConnection:\x20close\r\nAuthInfo:\x20\r\n\r\n\xef\
SF:xbb\xbf<!DOCTYPE\x20html\x20PUBLIC\x20\"-//W3C//DTD\x20XHTML\x201\.0\x2
SF:0Transitional//EN\"\x20\"http://www\.w3\.org/TR/xhtml1/DTD/xhtml1-trans
SF:itional\.dtd\">\r\n\r\n<html\x20xmlns=\"http://www\.w3\.org/1999/xhtml\
SF:">\r\n<head>\r\n\x20\x20\x20\x20<title></title>\r\n\x20\x20\x20\x20<scr
SF:ipt\x20type=\"text/javascript\">\r\n\x20\x20\x20\x20\x20\x20\x20\x20win
SF:dow\.location\.href\x20=\x20\"Pages/login\.htm\";\r\n\x20\x20\x20\x20</
SF:script>\r\n</head>\r\n<body>\r\n</body>\r\n</html>\r\n")%r(RTSPRequest,
SF:1B4,"HTTP/1\.1\x20200\x20OK\r\nContent-type:\x20text/html\r\nContent-Le
SF:ngth:\x20340\r\nConnection:\x20close\r\nAuthInfo:\x20\r\n\r\n\xef\xbb\x
SF:bf<!DOCTYPE\x20html\x20PUBLIC\x20\"-//W3C//DTD\x20XHTML\x201\.0\x20Tran
SF:sitional//EN\"\x20\"http://www\.w3\.org/TR/xhtml1/DTD/xhtml1-transition
SF:al\.dtd\">\r\n\r\n<html\x20xmlns=\"http://www\.w3\.org/1999/xhtml\">\r\
SF:n<head>\r\n\x20\x20\x20\x20<title></title>\r\n\x20\x20\x20\x20<script\x
SF:20type=\"text/javascript\">\r\n\x20\x20\x20\x20\x20\x20\x20\x20window\.
SF:location\.href\x20=\x20\"Pages/login\.htm\";\r\n\x20\x20\x20\x20</scrip
SF:t>\r\n</head>\r\n<body>\r\n</body>\r\n</html>\r\n")%r(X11Probe,6B,"HTTP
SF:/1\.1\x20408\x20Request\x20Timeout\r\nContent-type:\x20text/html\r\nCon
SF:tent-Length:\x200\r\nConnection:\x20close\r\nAuthInfo:\x20\r\n\r\n");
==============NEXT SERVICE FINGERPRINT (SUBMIT INDIVIDUALLY)==============
SF-Port8443-TCP:V=7.94SVN%T=SSL%I=7%D=1/13%Time=6784B9E1%P=x86_64-pc-linux
SF:-gnu%r(GetRequest,74,"HTTP/1\.1\x20302\r\nContent-Length:\x200\r\nLocat
SF:ion:\x20/index\.html\r\n\r\n\0\0\0\0\0\0\0\0\0\0iday\0Sat:Saturday\0\0\
SF:x12\x02\x18\0\x1aC\n\x07workers\x12\n\n\x04jobs\x12\x02\x18#\x12\x0f")%
SF:r(HTTPOptions,36,"HTTP/1\.1\x20404\r\nContent-Length:\x2018\r\n\r\nDocu
SF:ment\x20not\x20found")%r(FourOhFourRequest,36,"HTTP/1\.1\x20404\r\nCont
SF:ent-Length:\x2018\r\n\r\nDocument\x20not\x20found")%r(RTSPRequest,36,"H
SF:TTP/1\.1\x20404\r\nContent-Length:\x2018\r\n\r\nDocument\x20not\x20foun
SF:d")%r(SIPOptions,36,"HTTP/1\.1\x20404\r\nContent-Length:\x2018\r\n\r\nD
SF:ocument\x20not\x20found");
Aggressive OS guesses: Microsoft Windows Server 2019 (95%), Microsoft Windows Server 2016 (93%), Microsoft Windows Server 2012 (92%), Microsoft Windows Vista SP1 (92%), Microsoft Windows 10 1709 - 1909 (92%), Microsoft Windows 10 2004 (90%), Microsoft Windows Longhorn (90%), Microsoft Windows Server 2012 R2 Update 1 (90%), Microsoft Windows 7, Windows Server 2012, or Windows 8.1 Update 1 (90%), Microsoft Windows 7 SP1 (90%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 2 hops
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| smb2-security-mode: 
|   3:1:1: 
|_    Message signing enabled but not required
| smb2-time: 
|   date: 2025-01-13T07:01:29
|_  start_date: N/A

TRACEROUTE (using port 143/tcp)
HOP RTT      ADDRESS
1   59.85 ms 10.10.14.1
2   60.48 ms 10.129.227.77

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 258.83 seconds
```

anonymous ftp
![Pasted image 20250113151659](<0. Attachments/Pasted image 20250113151659.png>)

![Pasted image 20250113152117](<0. Attachments/Pasted image 20250113152117.png>)

![Pasted image 20250113152156](<0. Attachments/Pasted image 20250113152156.png>)

![Pasted image 20250113152341](<0. Attachments/Pasted image 20250113152341.png>)

![Pasted image 20250113152808](<0. Attachments/Pasted image 20250113152808.png>)

![Pasted image 20250113152518](<0. Attachments/Pasted image 20250113152518.png>)

well the other https is useless so we continue with burp
![Pasted image 20250113153117](<0. Attachments/Pasted image 20250113153117.png>)

now we see what works
```
crackmapexec smb 10.129.227.77 -u users -p passwords
```

![Pasted image 20250113153432](<0. Attachments/Pasted image 20250113153432.png>)

using ssh
![Pasted image 20250113153605](<0. Attachments/Pasted image 20250113153605.png>)
![Pasted image 20250113153625](<0. Attachments/Pasted image 20250113153625.png>)
![Pasted image 20250113153739](<0. Attachments/Pasted image 20250113153739.png>)

reading nsclient password, via config or helper
![Pasted image 20250113153932](<0. Attachments/Pasted image 20250113153932.png>)
```
nadine@SERVMON C:\Program Files\NSClient++>nscp web -- password --display
Current password: ew2x6SsGTxjRwXOT
```

BUT WE CANT LOGIN. TO LOGIN WE NEED TO TUNNEL
```
sshpass -p 'L1k3B1gBut7s@W0rk' ssh nadine@10.129.227.77 -L 8443:127.0.0.1:8443
```

HAD TO USE CHROMIUIM
![Pasted image 20250113154704](<0. Attachments/Pasted image 20250113154704.png>)


Priv Esc
![Pasted image 20250113155024](<0. Attachments/Pasted image 20250113155024.png>)

![Pasted image 20250113155250](<0. Attachments/Pasted image 20250113155250.png>)

priv esc
![Pasted image 20250113164924](<0. Attachments/Pasted image 20250113164924.png>)

![Pasted image 20250113165007](<0. Attachments/Pasted image 20250113165007.png>)

![Pasted image 20250113165031](<0. Attachments/Pasted image 20250113165031.png>)

![Pasted image 20250113164939](<0. Attachments/Pasted image 20250113164939.png>)

![Pasted image 20250113164859](<0. Attachments/Pasted image 20250113164859.png>)