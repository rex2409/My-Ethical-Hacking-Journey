nmap
```
┌──(kali㉿kali)-[~/HTB/escape-AD]
└─$ nmap -p- --min-rate 10000 10.129.228.253               
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-03 02:09 EST
Nmap scan report for 10.129.228.253
Host is up (0.11s latency).
Not shown: 65516 filtered tcp ports (no-response)
PORT      STATE SERVICE
53/tcp    open  domain
88/tcp    open  kerberos-sec
135/tcp   open  msrpc
139/tcp   open  netbios-ssn
389/tcp   open  ldap
445/tcp   open  microsoft-ds
464/tcp   open  kpasswd5
593/tcp   open  http-rpc-epmap
636/tcp   open  ldapssl
1433/tcp  open  ms-sql-s
3268/tcp  open  globalcatLDAP
3269/tcp  open  globalcatLDAPssl
5985/tcp  open  wsman
9389/tcp  open  adws
49667/tcp open  unknown
49689/tcp open  unknown
49690/tcp open  unknown
49711/tcp open  unknown
49721/tcp open  unknown

Nmap done: 1 IP address (1 host up) scanned in 26.88 seconds
                                                                                                                                 
┌──(kali㉿kali)-[~/HTB/escape-AD]
└─$ nmap -p 53,88,135,139,389,445,464,593,636,1433,3268,3269,5985,9389,49667,49689,49690,49711,49721 -sCV 10.129.228.253
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-03 02:11 EST
Nmap scan report for 10.129.228.253
Host is up (0.047s latency).

PORT      STATE SERVICE       VERSION
53/tcp    open  domain        Simple DNS Plus
88/tcp    open  kerberos-sec  Microsoft Windows Kerberos (server time: 2025-02-03 15:12:00Z)
135/tcp   open  msrpc         Microsoft Windows RPC
139/tcp   open  netbios-ssn   Microsoft Windows netbios-ssn
389/tcp   open  ldap          Microsoft Windows Active Directory LDAP (Domain: sequel.htb0., Site: Default-First-Site-Name)
|_ssl-date: 2025-02-03T15:13:27+00:00; +8h00m01s from scanner time.
| ssl-cert: Subject: 
| Subject Alternative Name: DNS:dc.sequel.htb, DNS:sequel.htb, DNS:sequel
| Not valid before: 2024-01-18T23:03:57
|_Not valid after:  2074-01-05T23:03:57
445/tcp   open  microsoft-ds?
464/tcp   open  kpasswd5?
593/tcp   open  ncacn_http    Microsoft Windows RPC over HTTP 1.0
636/tcp   open  ssl/ldap      Microsoft Windows Active Directory LDAP (Domain: sequel.htb0., Site: Default-First-Site-Name)
|_ssl-date: 2025-02-03T15:13:26+00:00; +8h00m00s from scanner time.
| ssl-cert: Subject: 
| Subject Alternative Name: DNS:dc.sequel.htb, DNS:sequel.htb, DNS:sequel
| Not valid before: 2024-01-18T23:03:57
|_Not valid after:  2074-01-05T23:03:57
1433/tcp  open  ms-sql-s      Microsoft SQL Server 2019 15.00.2000.00; RTM
| ms-sql-ntlm-info: 
|   10.129.228.253:1433: 
|     Target_Name: sequel
|     NetBIOS_Domain_Name: sequel
|     NetBIOS_Computer_Name: DC
|     DNS_Domain_Name: sequel.htb
|     DNS_Computer_Name: dc.sequel.htb
|     DNS_Tree_Name: sequel.htb
|_    Product_Version: 10.0.17763
| ms-sql-info: 
|   10.129.228.253:1433: 
|     Version: 
|       name: Microsoft SQL Server 2019 RTM
|       number: 15.00.2000.00
|       Product: Microsoft SQL Server 2019
|       Service pack level: RTM
|       Post-SP patches applied: false
|_    TCP port: 1433
|_ssl-date: 2025-02-03T15:13:27+00:00; +8h00m01s from scanner time.
| ssl-cert: Subject: commonName=SSL_Self_Signed_Fallback
| Not valid before: 2025-02-03T15:08:18
|_Not valid after:  2055-02-03T15:08:18
3268/tcp  open  ldap          Microsoft Windows Active Directory LDAP (Domain: sequel.htb0., Site: Default-First-Site-Name)
| ssl-cert: Subject: 
| Subject Alternative Name: DNS:dc.sequel.htb, DNS:sequel.htb, DNS:sequel
| Not valid before: 2024-01-18T23:03:57
|_Not valid after:  2074-01-05T23:03:57
|_ssl-date: 2025-02-03T15:13:27+00:00; +8h00m01s from scanner time.
3269/tcp  open  ssl/ldap      Microsoft Windows Active Directory LDAP (Domain: sequel.htb0., Site: Default-First-Site-Name)
|_ssl-date: 2025-02-03T15:13:26+00:00; +8h00m00s from scanner time.
| ssl-cert: Subject: 
| Subject Alternative Name: DNS:dc.sequel.htb, DNS:sequel.htb, DNS:sequel
| Not valid before: 2024-01-18T23:03:57
|_Not valid after:  2074-01-05T23:03:57
5985/tcp  open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-title: Not Found
|_http-server-header: Microsoft-HTTPAPI/2.0
9389/tcp  open  mc-nmf        .NET Message Framing
49667/tcp open  msrpc         Microsoft Windows RPC
49689/tcp open  ncacn_http    Microsoft Windows RPC over HTTP 1.0
49690/tcp open  msrpc         Microsoft Windows RPC
49711/tcp open  msrpc         Microsoft Windows RPC
49721/tcp open  msrpc         Microsoft Windows RPC
Service Info: Host: DC; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| smb2-time: 
|   date: 2025-02-03T15:12:46
|_  start_date: N/A
|_clock-skew: mean: 8h00m00s, deviation: 0s, median: 8h00m00s
| smb2-security-mode: 
|   3:1:1: 
|_    Message signing enabled and required

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 99.28 seconds
```

![Pasted image 20250203154658](<0. Attachments/Pasted image 20250203154658.png>)

![Pasted image 20250204094941](<0. Attachments/Pasted image 20250204094941.png>)

![Pasted image 20250204095108](<0. Attachments/Pasted image 20250204095108.png>)

![Pasted image 20250204111331](<0. Attachments/Pasted image 20250204111331.png>)

![Pasted image 20250204111953](<0. Attachments/Pasted image 20250204111953.png>)

SQL_SVC --> REGGIE1234ronnie

![Pasted image 20250204112138](<0. Attachments/Pasted image 20250204112138.png>)

![Pasted image 20250204112334](<0. Attachments/Pasted image 20250204112334.png>)

![Pasted image 20250204112410](<0. Attachments/Pasted image 20250204112410.png>)

sequel.htb\Ryan.Cooper --> NuclearMosquito3

![Pasted image 20250204112745](<0. Attachments/Pasted image 20250204112745.png>)

![Pasted image 20250204114308](<0. Attachments/Pasted image 20250204114308.png>)

![Pasted image 20250204114621](<0. Attachments/Pasted image 20250204114621.png>)

![Pasted image 20250204114832](<0. Attachments/Pasted image 20250204114832.png>)
![Pasted image 20250204115954](<0. Attachments/Pasted image 20250204115954.png>)

administrator --> A52F78E4C751E5F5E17E1E9F3E58F4EE

![Pasted image 20250204120334](<0. Attachments/Pasted image 20250204120334.png>)

