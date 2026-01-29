nmap
```
┌──(kali㉿kali)-[~/HTB/shocker]
└─$ sudo nmap -T5 -p- -A -oN nmap 10.129.251.11           
[sudo] password for kali: 
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-12-25 01:12 EST
Warning: 10.129.251.11 giving up on port because retransmission cap hit (2).
Nmap scan report for 10.129.251.11
Host is up (0.086s latency).
Not shown: 65308 closed tcp ports (reset), 225 filtered tcp ports (no-response)
PORT     STATE SERVICE VERSION
80/tcp   open  http    Apache httpd 2.4.18 ((Ubuntu))
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-title: Site doesn't have a title (text/html).
2222/tcp open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.2 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 c4:f8:ad:e8:f8:04:77:de:cf:15:0d:63:0a:18:7e:49 (RSA)
|   256 22:8f:b1:97:bf:0f:17:08:fc:7e:2c:8f:e9:77:3a:48 (ECDSA)
|_  256 e6:ac:27:a3:b5:a9:f1:12:3c:34:a5:5d:5b:eb:3d:e9 (ED25519)
Aggressive OS guesses: Linux 3.12 (96%), Linux 3.13 (96%), Linux 3.16 (96%), Linux 3.18 (96%), Linux 3.2 - 4.9 (96%), Linux 3.8 - 3.11 (96%), Linux 4.8 (96%), Linux 4.4 (95%), Linux 4.2 (95%), ASUS RT-N56U WAP (Linux 3.4) (95%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 2 hops
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE (using port 110/tcp)
HOP RTT      ADDRESS
1   80.22 ms 10.10.14.1
2   81.02 ms 10.129.251.11

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 419.98 seconds
```

during web crawling changing some extensions are necessary.
```
┌──(kali㉿kali)-[~/HTB/shocker]
└─$ dirb http://10.129.244.182/cgi-bin -X .sh

-----------------
DIRB v2.22    
By The Dark Raver
-----------------

START_TIME: Tue Dec 31 23:10:03 2024
URL_BASE: http://10.129.244.182/cgi-bin/
WORDLIST_FILES: /usr/share/dirb/wordlists/common.txt
EXTENSIONS_LIST: (.sh) | (.sh) [NUM = 1]

-----------------

GENERATED WORDS: 4612                                                          

---- Scanning URL: http://10.129.244.182/cgi-bin/ ----
+ http://10.129.244.182/cgi-bin/user.sh (CODE:200|SIZE:119)                                                          
                                                                                                                     
-----------------
END_TIME: Tue Dec 31 23:17:17 2024
DOWNLOADED: 4612 - FOUND: 1
```

checking if vulnerable to shellshock

```
┌──(kali㉿kali)-[~/HTB/shocker]
└─$ nmap 10.129.244.182 -p 80 --script http-shellshock --script-args uri=/cgi-bin/user.sh
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-12-31 23:46 EST
Nmap scan report for 10.129.244.182
Host is up (0.085s latency).

PORT   STATE SERVICE
80/tcp open  http
| http-shellshock: 
|   VULNERABLE:
|   HTTP Shellshock vulnerability
|     State: VULNERABLE (Exploitable)
|     IDs:  CVE:CVE-2014-6271
|       This web application might be affected by the vulnerability known
|       as Shellshock. It seems the server is executing commands injected
|       via malicious HTTP headers.
|             
|     Disclosure date: 2014-09-24
|     References:
|       http://www.openwall.com/lists/oss-security/2014/09/24/10
|       http://seclists.org/oss-sec/2014/q3/685
|       https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2014-7169
|_      https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2014-6271

Nmap done: 1 IP address (1 host up) scanned in 1.17 seconds
```

![Pasted image 20250101125137](<0. Attachments/Pasted image 20250101125137.png>)

![Pasted image 20250101125506](<0. Attachments/Pasted image 20250101125506.png>)

![Pasted image 20250101125754](<0. Attachments/Pasted image 20250101125754.png>)

![Pasted image 20250101125737](<0. Attachments/Pasted image 20250101125737.png>)

