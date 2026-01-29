# nmap
```
┌──(kali㉿kali)-[~/PG/fired]
└─$ nmap -p- --min-rate 10000 192.168.135.96 
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-24 20:31 EST
Nmap scan report for 192.168.135.96
Host is up (0.052s latency).
Not shown: 65532 filtered tcp ports (no-response)
PORT     STATE SERVICE
22/tcp   open  ssh
9090/tcp open  zeus-admin
9091/tcp open  xmltec-xmlmail

Nmap done: 1 IP address (1 host up) scanned in 13.57 seconds
                                                                                                                                                   
┌──(kali㉿kali)-[~/PG/fired]
└─$ nmap -p 22,9090,9091 -sCV 192.168.135.96
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-24 20:32 EST
Nmap scan report for 192.168.135.96
Host is up (0.048s latency).

PORT     STATE SERVICE                VERSION
22/tcp   open  ssh                    OpenSSH 8.2p1 Ubuntu 4ubuntu0.11 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 51:56:a7:34:16:8e:3d:47:17:c8:96:d5:e6:94:46:46 (RSA)
|   256 fe:76:e3:4c:2b:f6:f5:21:a2:4d:9f:59:52:39:b9:16 (ECDSA)
|_  256 2c:dd:62:7d:d6:1c:f4:fd:a1:e4:c8:aa:11:ae:d6:1f (ED25519)
9090/tcp open  hadoop-tasktracker     Apache Hadoop
| hadoop-tasktracker-info: 
|_  Logs: jive-ibtn jive-btn-gradient
|_http-title: Site doesn't have a title (text/html).
| hadoop-datanode-info: 
|_  Logs: jive-ibtn jive-btn-gradient
9091/tcp open  ssl/hadoop-tasktracker Apache Hadoop
|_ssl-date: TLS randomness does not represent time
| hadoop-tasktracker-info: 
|_  Logs: jive-ibtn jive-btn-gradient
|_http-title: Site doesn't have a title (text/html).
| ssl-cert: Subject: commonName=localhost
| Subject Alternative Name: DNS:localhost, DNS:*.localhost
| Not valid before: 2024-06-28T07:02:39
|_Not valid after:  2029-06-27T07:02:39
| hadoop-datanode-info: 
|_  Logs: jive-ibtn jive-btn-gradient
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 33.21 seconds
```
![Pasted image 20250225093310](<0. Attachments/Pasted image 20250225093310.png>)

# web enum
![Pasted image 20250225093404](<0. Attachments/Pasted image 20250225093404.png>)

# exploit
https://github.com/K3ysTr0K3R/CVE-2023-32315-EXPLOIT

![Pasted image 20250225094117](<0. Attachments/Pasted image 20250225094117.png>)

trying to login with it - took alot of time

![Pasted image 20250225094710](<0. Attachments/Pasted image 20250225094710.png>)

# openfire enum

![Pasted image 20250225095255](<0. Attachments/Pasted image 20250225095255.png>)

https://github.com/miko550/CVE-2023-32315 - another exploit with a plugin upload capability

![Pasted image 20250225095313](<0. Attachments/Pasted image 20250225095313.png>)

# webshell access
![Pasted image 20250225095743](<0. Attachments/Pasted image 20250225095743.png>)

![Pasted image 20250225095839](<0. Attachments/Pasted image 20250225095839.png>)

![Pasted image 20250225095904](<0. Attachments/Pasted image 20250225095904.png>)

# initial access
![Pasted image 20250225100045](<0. Attachments/Pasted image 20250225100045.png>)

![Pasted image 20250225100103](<0. Attachments/Pasted image 20250225100103.png>)

# local.txt
![Pasted image 20250225100330](<0. Attachments/Pasted image 20250225100330.png>)

# priv esc enum
getting linpeas
![Pasted image 20250225100511](<0. Attachments/Pasted image 20250225100511.png>)

interesting but difficult find
![Pasted image 20250225102500](<0. Attachments/Pasted image 20250225102500.png>)

![Pasted image 20250225102749](<0. Attachments/Pasted image 20250225102749.png>)

requires very thorough reading
![Pasted image 20250225102825](<0. Attachments/Pasted image 20250225102825.png>)

# priv esc and root.txt
root - OpenFireAtEveryone
![Pasted image 20250225103000](<0. Attachments/Pasted image 20250225103000.png>)
