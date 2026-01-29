```
┌──(kali㉿kali)-[~/PG/pelican]
└─$ nmap -p- --min-rate 10000 192.168.202.98 
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-10 03:10 EST
Nmap scan report for 192.168.202.98
Host is up (0.084s latency).
Not shown: 65526 closed tcp ports (reset)
PORT      STATE SERVICE
22/tcp    open  ssh
139/tcp   open  netbios-ssn
445/tcp   open  microsoft-ds
631/tcp   open  ipp
2181/tcp  open  eforward
2222/tcp  open  EtherNetIP-1
8080/tcp  open  http-proxy
8081/tcp  open  blackice-icecap
39605/tcp open  unknown

Nmap done: 1 IP address (1 host up) scanned in 10.48 seconds
                                                                                                                                                            
┌──(kali㉿kali)-[~/PG/pelican]
└─$ nmap -p 22,139,445,631,2181,2222,8080,8081,39605  -sCV 192.168.202.98
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-10 03:11 EST
Nmap scan report for 192.168.202.98
Host is up (0.042s latency).

PORT      STATE SERVICE     VERSION
22/tcp    open  ssh         OpenSSH 7.9p1 Debian 10+deb10u2 (protocol 2.0)
| ssh-hostkey: 
|   2048 a8:e1:60:68:be:f5:8e:70:70:54:b4:27:ee:9a:7e:7f (RSA)
|   256 bb:99:9a:45:3f:35:0b:b3:49:e6:cf:11:49:87:8d:94 (ECDSA)
|_  256 f2:eb:fc:45:d7:e9:80:77:66:a3:93:53:de:00:57:9c (ED25519)
139/tcp   open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
445/tcp   open  netbios-ssn Samba smbd 4.9.5-Debian (workgroup: WORKGROUP)
631/tcp   open  ipp         CUPS 2.2
|_http-title: Forbidden - CUPS v2.2.10
| http-methods: 
|_  Potentially risky methods: PUT
|_http-server-header: CUPS/2.2 IPP/2.1
2181/tcp  open  zookeeper   Zookeeper 3.4.6-1569965 (Built on 02/20/2014)
2222/tcp  open  ssh         OpenSSH 7.9p1 Debian 10+deb10u2 (protocol 2.0)
| ssh-hostkey: 
|   2048 a8:e1:60:68:be:f5:8e:70:70:54:b4:27:ee:9a:7e:7f (RSA)
|   256 bb:99:9a:45:3f:35:0b:b3:49:e6:cf:11:49:87:8d:94 (ECDSA)
|_  256 f2:eb:fc:45:d7:e9:80:77:66:a3:93:53:de:00:57:9c (ED25519)
8080/tcp  open  http        Jetty 1.0
|_http-server-header: Jetty(1.0)
|_http-title: Error 404 Not Found
8081/tcp  open  http        nginx 1.14.2
|_http-server-header: nginx/1.14.2
|_http-title: Did not follow redirect to http://192.168.202.98:8080/exhibitor/v1/ui/index.html
39605/tcp open  java-rmi    Java RMI
Service Info: Host: PELICAN; OS: Linux; CPE: cpe:/o:linux:linux_kernel

Host script results:
| smb2-time: 
|   date: 2025-02-10T08:11:40
|_  start_date: N/A
|_clock-skew: mean: 1h40m02s, deviation: 2h53m12s, median: 1s
| smb2-security-mode: 
|   3:1:1: 
|_    Message signing enabled but not required
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
| smb-os-discovery: 
|   OS: Windows 6.1 (Samba 4.9.5-Debian)
|   Computer name: pelican
|   NetBIOS computer name: PELICAN\x00
|   Domain name: \x00
|   FQDN: pelican
|_  System time: 2025-02-10T03:11:41-05:00

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 20.58 seconds

┌──(kali㉿kali)-[~/PG/pelican]
└─$ sudo nmap -Pn -sU -p- 192.168.202.98 --min-rate 10000 -T5
[sudo] password for kali: 
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-10 03:19 EST
Warning: 192.168.202.98 giving up on port because retransmission cap hit (2).
Nmap scan report for 192.168.202.98
Host is up (0.084s latency).
Not shown: 65509 open|filtered udp ports (no-response)
PORT      STATE  SERVICE
1672/udp  closed netview-aix-12
4300/udp  closed corelccam
4463/udp  closed unknown
5353/udp  open   zeroconf
5830/udp  closed unknown
7845/udp  closed apc-7845
13135/udp closed unknown
16624/udp closed unknown
16776/udp closed unknown
18666/udp closed unknown
30934/udp closed unknown
33863/udp closed unknown
39160/udp closed unknown
39566/udp closed unknown
39600/udp closed unknown
39923/udp closed unknown
41441/udp closed unknown
42561/udp closed unknown
43584/udp closed unknown
44662/udp closed unknown
45269/udp closed unknown
48266/udp closed unknown
48286/udp closed unknown
48812/udp closed unknown
52588/udp closed unknown
61810/udp closed unknown

Nmap done: 1 IP address (1 host up) scanned in 20.17 seconds
```

![Pasted image 20250210161404](<0. Attachments/Pasted image 20250210161404.png>)

https://www.exploit-db.com/exploits/48654

![Pasted image 20250210163925](<0. Attachments/Pasted image 20250210163925.png>)

click commit > All At Once > OK

![Pasted image 20250210163906](<0. Attachments/Pasted image 20250210163906.png>)

![Pasted image 20250210164036](<0. Attachments/Pasted image 20250210164036.png>)

![Pasted image 20250210164639](<0. Attachments/Pasted image 20250210164639.png>)

![Pasted image 20250210164653](<0. Attachments/Pasted image 20250210164653.png>)

![Pasted image 20250210165452](<0. Attachments/Pasted image 20250210165452.png>)

![Pasted image 20250210165519](<0. Attachments/Pasted image 20250210165519.png>)

![Pasted image 20250210165538](<0. Attachments/Pasted image 20250210165538.png>)

