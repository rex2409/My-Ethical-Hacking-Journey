```
┌──(kali㉿kali)-[~/PG/algernon]
└─$ nmap -p- --min-rate 10000 192.168.140.65
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-10 23:34 EST
Warning: 192.168.140.65 giving up on port because retransmission cap hit (10).
Nmap scan report for 192.168.140.65
Host is up (0.041s latency).
Not shown: 64338 closed tcp ports (reset), 1182 filtered tcp ports (no-response)
PORT      STATE SERVICE
21/tcp    open  ftp
80/tcp    open  http
135/tcp   open  msrpc
139/tcp   open  netbios-ssn
445/tcp   open  microsoft-ds
5040/tcp  open  unknown
7680/tcp  open  pando-pub
9998/tcp  open  distinct32
17001/tcp open  unknown
49664/tcp open  unknown
49665/tcp open  unknown
49666/tcp open  unknown
49667/tcp open  unknown
49668/tcp open  unknown
49669/tcp open  unknown

Nmap done: 1 IP address (1 host up) scanned in 15.98 seconds
                                                                                                                                               
┌──(kali㉿kali)-[~/PG/algernon]
└─$ nmap -p 21,80,135,139,445,5040,7680,9998,17001,49664,49665,49666,49667,49668,49669  -sCV 192.168.140.65
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-10 23:36 EST
Nmap scan report for 192.168.140.65
Host is up (0.041s latency).

PORT      STATE SERVICE       VERSION
21/tcp    open  ftp           Microsoft ftpd
| ftp-syst: 
|_  SYST: Windows_NT
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
| 04-29-20  09:31PM       <DIR>          ImapRetrieval
| 02-10-25  08:34PM       <DIR>          Logs
| 04-29-20  09:31PM       <DIR>          PopRetrieval
|_04-29-20  09:32PM       <DIR>          Spool
80/tcp    open  http          Microsoft IIS httpd 10.0
|_http-server-header: Microsoft-IIS/10.0
|_http-title: IIS Windows
| http-methods: 
|_  Potentially risky methods: TRACE
135/tcp   open  msrpc         Microsoft Windows RPC
139/tcp   open  netbios-ssn   Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds?
5040/tcp  open  unknown
7680/tcp  open  pando-pub?
9998/tcp  open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-IIS/10.0
| uptime-agent-info: HTTP/1.1 400 Bad Request\x0D
| Content-Type: text/html; charset=us-ascii\x0D
| Server: Microsoft-HTTPAPI/2.0\x0D
| Date: Tue, 11 Feb 2025 04:39:06 GMT\x0D
| Connection: close\x0D
| Content-Length: 326\x0D
| \x0D
| <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN""http://www.w3.org/TR/html4/strict.dtd">\x0D
| <HTML><HEAD><TITLE>Bad Request</TITLE>\x0D
| <META HTTP-EQUIV="Content-Type" Content="text/html; charset=us-ascii"></HEAD>\x0D
| <BODY><h2>Bad Request - Invalid Verb</h2>\x0D
| <hr><p>HTTP Error 400. The request verb is invalid.</p>\x0D
|_</BODY></HTML>\x0D
17001/tcp open  remoting      MS .NET Remoting services
49664/tcp open  msrpc         Microsoft Windows RPC
49665/tcp open  msrpc         Microsoft Windows RPC
49666/tcp open  msrpc         Microsoft Windows RPC
49667/tcp open  msrpc         Microsoft Windows RPC
49668/tcp open  msrpc         Microsoft Windows RPC
49669/tcp open  msrpc         Microsoft Windows RPC
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| smb2-time: 
|   date: 2025-02-11T04:39:00
|_  start_date: N/A
| smb2-security-mode: 
|   3:1:1: 
|_    Message signing enabled but not required

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 178.56 seconds
```

![Pasted image 20250211124741](<0. Attachments/Pasted image 20250211124741.png>)

![Pasted image 20250211123920](<0. Attachments/Pasted image 20250211123920.png>)

![Pasted image 20250211124802](<0. Attachments/Pasted image 20250211124802.png>)

![Pasted image 20250211124824](<0. Attachments/Pasted image 20250211124824.png>)

https://www.exploit-db.com/exploits/49216

![Pasted image 20250211125829](<0. Attachments/Pasted image 20250211125829.png>)

![Pasted image 20250211125846](<0. Attachments/Pasted image 20250211125846.png>)
