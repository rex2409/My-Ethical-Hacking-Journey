nmap
```
┌──(kali㉿kali)-[~/HTB/bashed]
└─$ sudo nmap -T5 -p- -A -oN nmap 10.129.249.94                                                                                       
[sudo] password for kali: 
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-12-18 21:50 EST
Warning: 10.129.249.94 giving up on port because retransmission cap hit (2).
Nmap scan report for 10.129.249.94
Host is up (0.082s latency).
Not shown: 65397 closed tcp ports (reset), 137 filtered tcp ports (no-response)
PORT   STATE SERVICE VERSION
80/tcp open  http    Apache httpd 2.4.18 ((Ubuntu))
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-title: Arrexel's Development Site
Aggressive OS guesses: Linux 3.13 (96%), Linux 3.16 (96%), Linux 3.18 (96%), Linux 3.2 - 4.9 (96%), Linux 4.2 (96%), Linux 3.12 (95%), Linux 3.8 - 3.11 (95%), Linux 4.8 (95%), ASUS RT-N56U WAP (Linux 3.4) (95%), Linux 3.1 (95%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 2 hops

TRACEROUTE (using port 110/tcp)
HOP RTT      ADDRESS
1   88.40 ms 10.10.14.1
2   85.69 ms 10.129.249.94

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 233.95 seconds
```

![Pasted image 20241219105112](<0. Attachments/Pasted image 20241219105112.png>)

dirsearch

```
# Dirsearch started Wed Dec 18 20:14:59 2024 as: /usr/lib/python3/dist-packages/dirsearch/dirsearch.py -u http://10.129.249.42 -x 400-599

301   312B   http://10.129.249.42/php    -> REDIRECTS TO: http://10.129.249.42/php/
301   311B   http://10.129.249.42/js    -> REDIRECTS TO: http://10.129.249.42/js/
200     2KB  http://10.129.249.42/about.html
200     0B   http://10.129.249.42/config.php
200     2KB  http://10.129.249.42/contact.html
301   312B   http://10.129.249.42/css    -> REDIRECTS TO: http://10.129.249.42/css/
301   312B   http://10.129.249.42/dev    -> REDIRECTS TO: http://10.129.249.42/dev/
200   484B   http://10.129.249.42/dev/
301   314B   http://10.129.249.42/fonts    -> REDIRECTS TO: http://10.129.249.42/fonts/
200   516B   http://10.129.249.42/images/
301   315B   http://10.129.249.42/images    -> REDIRECTS TO: http://10.129.249.42/images/
200   664B   http://10.129.249.42/js/
200   458B   http://10.129.249.42/php/
200    14B   http://10.129.249.42/uploads/
301   316B   http://10.129.249.42/uploads    -> REDIRECTS TO: http://10.129.249.42/uploads/
```

to get a bash
```
python -c "import pty; pty.spawn('/bin/bash');"
```

![Pasted image 20241219105303](<0. Attachments/Pasted image 20241219105303.png>)

![Pasted image 20241219105318](<0. Attachments/Pasted image 20241219105318.png>)

![Pasted image 20241219105358](<0. Attachments/Pasted image 20241219105358.png>)

![Pasted image 20241219105414](<0. Attachments/Pasted image 20241219105414.png>)
