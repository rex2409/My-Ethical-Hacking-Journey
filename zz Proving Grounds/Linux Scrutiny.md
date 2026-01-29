# nmap
```
┌──(kali㉿kali)-[~/PG/scrutiny]
└─$ nmap -p- --min-rate 10000 192.168.207.91
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-26 19:23 EST
Nmap scan report for 192.168.207.91
Host is up (0.055s latency).
Not shown: 65531 filtered tcp ports (no-response)
PORT    STATE  SERVICE
22/tcp  open   ssh
25/tcp  open   smtp
80/tcp  open   http
443/tcp closed https

Nmap done: 1 IP address (1 host up) scanned in 13.59 seconds
                                                                                                                                                 
┌──(kali㉿kali)-[~/PG/scrutiny]
└─$ nmap -p 22,25,80,443 -sCV 192.168.207.91
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-26 19:24 EST
Nmap scan report for 192.168.207.91
Host is up (0.052s latency).

PORT    STATE  SERVICE VERSION
22/tcp  open   ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.11 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 62:36:1a:5c:d3:e3:7b:e1:70:f8:a3:b3:1c:4c:24:38 (RSA)
|   256 ee:25:fc:23:66:05:c0:c1:ec:47:c6:bb:00:c7:4f:53 (ECDSA)
|_  256 83:5c:51:ac:32:e5:3a:21:7c:f6:c2:cd:93:68:58:d8 (ED25519)
25/tcp  open   smtp    Postfix smtpd
|_ssl-date: TLS randomness does not represent time
| ssl-cert: Subject: commonName=onlyrands.com
| Subject Alternative Name: DNS:onlyrands.com
| Not valid before: 2024-06-07T09:33:24
|_Not valid after:  2034-06-05T09:33:24
|_smtp-commands: onlyrands.com, PIPELINING, SIZE 10240000, VRFY, ETRN, STARTTLS, ENHANCEDSTATUSCODES, 8BITMIME, DSN, SMTPUTF8, CHUNKING
80/tcp  open   http    nginx 1.18.0 (Ubuntu)
|_http-title: OnlyRands
|_http-server-header: nginx/1.18.0 (Ubuntu)
443/tcp closed https
Service Info: Host:  onlyrands.com; OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 14.84 seconds
```

# web enum
![Pasted image 20250227082557](<0. Attachments/Pasted image 20250227082557.png>)

# SMTP enum
![Pasted image 20250227083256](<0. Attachments/Pasted image 20250227083256.png>)

adding /etc/hosts files
![Pasted image 20250227083500](<0. Attachments/Pasted image 20250227083500.png>)

![Pasted image 20250227083810](<0. Attachments/Pasted image 20250227083810.png>)

nse scripts
```
┌──(kali㉿kali)-[~/PG/scrutiny]
└─$ nmap -p25 --script smtp-commands 192.168.207.91
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-26 19:40 EST
Nmap scan report for onlyrands.com (192.168.207.91)
Host is up (0.054s latency).

PORT   STATE SERVICE
25/tcp open  smtp
|_smtp-commands: onlyrands.com, PIPELINING, SIZE 10240000, VRFY, ETRN, STARTTLS, ENHANCEDSTATUSCODES, 8BITMIME, DSN, SMTPUTF8, CHUNKING

Nmap done: 1 IP address (1 host up) scanned in 0.72 seconds
                                                                                                                                                 
┌──(kali㉿kali)-[~/PG/scrutiny]
└─$ nmap -p25 --script smtp-open-relay 192.168.207.91 -v
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-26 19:41 EST
NSE: Loaded 1 scripts for scanning.
NSE: Script Pre-scanning.
Initiating NSE at 19:41
Completed NSE at 19:41, 0.00s elapsed
Initiating Ping Scan at 19:41
Scanning 192.168.207.91 [4 ports]
Completed Ping Scan at 19:41, 0.09s elapsed (1 total hosts)
Initiating SYN Stealth Scan at 19:41
Scanning onlyrands.com (192.168.207.91) [1 port]
Discovered open port 25/tcp on 192.168.207.91
Completed SYN Stealth Scan at 19:41, 0.07s elapsed (1 total ports)
NSE: Script scanning 192.168.207.91.
Initiating NSE at 19:41
Completed NSE at 19:41, 20.89s elapsed
Nmap scan report for onlyrands.com (192.168.207.91)
Host is up (0.052s latency).

PORT   STATE SERVICE
25/tcp open  smtp
|_smtp-open-relay: Server doesn't seem to be an open relay, all tests failed

NSE: Script Post-scanning.
Initiating NSE at 19:41
Completed NSE at 19:41, 0.00s elapsed
Read data files from: /usr/share/nmap
Nmap done: 1 IP address (1 host up) scanned in 21.38 seconds
           Raw packets sent: 5 (196B) | Rcvd: 2 (72B)
```

![Pasted image 20250227084735](<0. Attachments/Pasted image 20250227084735.png>)

# back to web enum
forgot to check the page source
![Pasted image 20250227085717](<0. Attachments/Pasted image 20250227085717.png>)

added to /etc/hosts
![Pasted image 20250227085737](<0. Attachments/Pasted image 20250227085737.png>)

![Pasted image 20250227085753](<0. Attachments/Pasted image 20250227085753.png>)

# exploit
https://github.com/yoryio/CVE-2024-27198/blob/main/CVE-2024-27198.py

![Pasted image 20250227094908](<0. Attachments/Pasted image 20250227094908.png>)

![Pasted image 20250227094956](<0. Attachments/Pasted image 20250227094956.png>)

![Pasted image 20250227102805](<0. Attachments/Pasted image 20250227102805.png>)

![Pasted image 20250227102825](<0. Attachments/Pasted image 20250227102825.png>)

saving it
![Pasted image 20250227103215](<0. Attachments/Pasted image 20250227103215.png>)

# cracking hash
![Pasted image 20250227103230](<0. Attachments/Pasted image 20250227103230.png>)

![Pasted image 20250227103444](<0. Attachments/Pasted image 20250227103444.png>)

# initial access
![Pasted image 20250227103516](<0. Attachments/Pasted image 20250227103516.png>)

# local.txt
![Pasted image 20250227103736](<0. Attachments/Pasted image 20250227103736.png>)

# priv esc enum
since we had smtp running we can check its location
![Pasted image 20250227104642](<0. Attachments/Pasted image 20250227104642.png>)

![Pasted image 20250227104803](<0. Attachments/Pasted image 20250227104803.png>)

![Pasted image 20250227104859](<0. Attachments/Pasted image 20250227104859.png>)

IdealismEngineAshen476 --> matthewa
![Pasted image 20250227105353](<0. Attachments/Pasted image 20250227105353.png>)

![Pasted image 20250227105419](<0. Attachments/Pasted image 20250227105419.png>)

![Pasted image 20250227105610](<0. Attachments/Pasted image 20250227105610.png>)

briand --> RefriedScabbedWasting502

![Pasted image 20250227105710](<0. Attachments/Pasted image 20250227105710.png>)

# priv esc

![Pasted image 20250227110422](<0. Attachments/Pasted image 20250227110422.png>)

![Pasted image 20250227110234](<0. Attachments/Pasted image 20250227110234.png>)

# proof.txt
![Pasted image 20250227110338](<0. Attachments/Pasted image 20250227110338.png>)

