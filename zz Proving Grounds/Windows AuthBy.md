```
┌──(kali㉿kali)-[~/PG/authby]
└─$ nmap -p- --min-rate 10000 192.168.140.46                                                               
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-11 02:45 EST
Nmap scan report for 192.168.140.46
Host is up (0.042s latency).
Not shown: 65531 filtered tcp ports (no-response)
PORT     STATE SERVICE
21/tcp   open  ftp
242/tcp  open  direct
3145/tcp open  csi-lfap
3389/tcp open  ms-wbt-server

Nmap done: 1 IP address (1 host up) scanned in 13.58 seconds
                                                                                                                                               
┌──(kali㉿kali)-[~/PG/authby]
└─$ nmap -p 21,242,3145,3389  -sCV 192.168.140.46                                                          
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-11 02:46 EST
Nmap scan report for 192.168.140.46
Host is up (0.041s latency).

PORT     STATE SERVICE       VERSION
21/tcp   open  ftp           zFTPServer 6.0 build 2011-10-17
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
| total 9680
| ----------   1 root     root      5610496 Oct 18  2011 zFTPServer.exe
| ----------   1 root     root           25 Feb 10  2011 UninstallService.bat
| ----------   1 root     root      4284928 Oct 18  2011 Uninstall.exe
| ----------   1 root     root           17 Aug 13  2011 StopService.bat
| ----------   1 root     root           18 Aug 13  2011 StartService.bat
| ----------   1 root     root         8736 Nov 09  2011 Settings.ini
| dr-xr-xr-x   1 root     root          512 Feb 11 15:46 log
| ----------   1 root     root         2275 Aug 09  2011 LICENSE.htm
| ----------   1 root     root           23 Feb 10  2011 InstallService.bat
| dr-xr-xr-x   1 root     root          512 Nov 08  2011 extensions
| dr-xr-xr-x   1 root     root          512 Nov 08  2011 certificates
|_dr-xr-xr-x   1 root     root          512 Aug 03  2024 accounts
242/tcp  open  http          Apache httpd 2.2.21 ((Win32) PHP/5.3.8)
|_http-server-header: Apache/2.2.21 (Win32) PHP/5.3.8
| http-auth: 
| HTTP/1.1 401 Authorization Required\x0D
|_  Basic realm=Qui e nuce nuculeum esse volt, frangit nucem!
|_http-title: 401 Authorization Required
3145/tcp open  zftp-admin    zFTPServer admin
3389/tcp open  ms-wbt-server Microsoft Terminal Service
| ssl-cert: Subject: commonName=LIVDA
| Not valid before: 2024-08-02T13:17:54
|_Not valid after:  2025-02-01T13:17:54
| rdp-ntlm-info: 
|   Target_Name: LIVDA
|   NetBIOS_Domain_Name: LIVDA
|   NetBIOS_Computer_Name: LIVDA
|   DNS_Domain_Name: LIVDA
|   DNS_Computer_Name: LIVDA
|   Product_Version: 6.0.6001
|_  System_Time: 2025-02-11T07:46:54+00:00
|_ssl-date: 2025-02-11T07:46:59+00:00; 0s from scanner time.
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 23.02 seconds
```

![Pasted image 20250211155950](<0. Attachments/Pasted image 20250211155950.png>)

![Pasted image 20250211162615](<0. Attachments/Pasted image 20250211162615.png>)

![Pasted image 20250211162807](<0. Attachments/Pasted image 20250211162807.png>)

![Pasted image 20250211162825](<0. Attachments/Pasted image 20250211162825.png>)

![Pasted image 20250211163043](<0. Attachments/Pasted image 20250211163043.png>)

![Pasted image 20250211163205](<0. Attachments/Pasted image 20250211163205.png>)

![Pasted image 20250211163334](<0. Attachments/Pasted image 20250211163334.png>)

![Pasted image 20250211164051](<0. Attachments/Pasted image 20250211164051.png>)

why did we do this, looking at .htaccess file, it is present in the root also, we can see exactly the same on website. of course more reading is required as to why this works refer to 
[Proving Grounds -Authby (Medium) Windows Box -Walkthrough — A Journey to Offensive Security | by Brian | Medium](https://medium.com/@bdsalazar/proving-grounds-authby-medium-windows-box-walkthrough-a-journey-to-offensive-security-15597c449710#:~:text=In%20this%20blog%20post%2C%20we%20will%20explore%20the,privileges%2C%20and%20achieve%20root%20on%20the%20target%20machine.)

![Pasted image 20250211164637](<0. Attachments/Pasted image 20250211164637.png>)

![Pasted image 20250211164653](<0. Attachments/Pasted image 20250211164653.png>)

https://github.com/abatchy17/WindowsExploits/blob/master/MS11-046/MS11-046.exe

![Pasted image 20250211165453](<0. Attachments/Pasted image 20250211165453.png>)

