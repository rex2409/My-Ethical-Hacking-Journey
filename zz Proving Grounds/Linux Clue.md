```
┌──(kali㉿kali)-[~/PG/clue]
└─$ nmap -p- --min-rate 10000 192.168.174.240                                            
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-16 06:23 EST
Nmap scan report for 192.168.174.240
Host is up (0.053s latency).
Not shown: 65529 filtered tcp ports (no-response)
PORT     STATE  SERVICE
22/tcp   open   ssh
80/tcp   open   http
139/tcp  closed netbios-ssn
445/tcp  closed microsoft-ds
3000/tcp open   ppp
8021/tcp open   ftp-proxy

Nmap done: 1 IP address (1 host up) scanned in 13.56 seconds
                                                                                                                                                            
┌──(kali㉿kali)-[~/PG/clue]
└─$ nmap -p 22,80,139,445,3000,8021 -sCV 192.168.174.240                                 
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-16 06:23 EST
Nmap scan report for 192.168.174.240
Host is up (0.049s latency).

PORT     STATE SERVICE          VERSION
22/tcp   open  ssh              OpenSSH 7.9p1 Debian 10+deb10u2 (protocol 2.0)
| ssh-hostkey: 
|   2048 74:ba:20:23:89:92:62:02:9f:e7:3d:3b:83:d4:d9:6c (RSA)
|   256 54:8f:79:55:5a:b0:3a:69:5a:d5:72:39:64:fd:07:4e (ECDSA)
|_  256 7f:5d:10:27:62:ba:75:e9:bc:c8:4f:e2:72:87:d4:e2 (ED25519)
80/tcp   open  http             Apache httpd 2.4.38
|_http-title: 403 Forbidden
|_http-server-header: Apache/2.4.38 (Debian)
139/tcp  open  netbios-ssn      Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
445/tcp  open  netbios-ssn      Samba smbd 4.9.5-Debian (workgroup: WORKGROUP)
3000/tcp open  http             Thin httpd
|_http-server-header: thin
|_http-title: Cassandra Web
8021/tcp open  freeswitch-event FreeSWITCH mod_event_socket
Service Info: Hosts: 127.0.0.1, CLUE; OS: Linux; CPE: cpe:/o:linux:linux_kernel

Host script results:
|_clock-skew: mean: 1h40m01s, deviation: 2h53m15s, median: 0s
| smb2-security-mode: 
|   3:1:1: 
|_    Message signing enabled but not required
| smb2-time: 
|   date: 2025-02-16T11:24:11
|_  start_date: N/A
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
| smb-os-discovery: 
|   OS: Windows 6.1 (Samba 4.9.5-Debian)
|   Computer name: clue
|   NetBIOS computer name: CLUE\x00
|   Domain name: pg
|   FQDN: clue.pg
|_  System time: 2025-02-16T06:24:13-05:00

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 53.30 seconds
```

![Pasted image 20250216192631](<0. Attachments/Pasted image 20250216192631.png>)

https://www.exploit-db.com/exploits/49362

![Pasted image 20250216195112](<0. Attachments/Pasted image 20250216195112.png>)

[How to change FreeSWITCH event socket password? - ASTPP Documentation - Confluence](https://inextrix.atlassian.net/wiki/spaces/ASTPP/pages/5572241/How+to+change+FreeSWITCH+event+socket+password)

![Pasted image 20250216195855](<0. Attachments/Pasted image 20250216195855.png>)

https://www.exploit-db.com/exploits/47799

change passwd in exploit
![Pasted image 20250216200144](<0. Attachments/Pasted image 20250216200144.png>)

![Pasted image 20250216200245](<0. Attachments/Pasted image 20250216200245.png>)

![Pasted image 20250216201003](<0. Attachments/Pasted image 20250216201003.png>)

```
sudo cassandra-web -B 0.0.0.0:4444 -u cassie -p SecondBiteTheApple330
```

another shell as cassie
![Pasted image 20250216201457](<0. Attachments/Pasted image 20250216201457.png>)

![Pasted image 20250216201619](<0. Attachments/Pasted image 20250216201619.png>)

![Pasted image 20250216201943](<0. Attachments/Pasted image 20250216201943.png>)

![Pasted image 20250216203701](<0. Attachments/Pasted image 20250216203701.png>)

![Pasted image 20250216203730](<0. Attachments/Pasted image 20250216203730.png>)

