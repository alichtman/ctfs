# Resolute (`10.10.10.169`)

## `/etc/hosts`

I begin by adding an entry in `/etc/hosts` to resolve `resolute.htb` to `10.10.10.169`. I use this later in my report.

## Enumeration

I start a portscan of all ports (`-p-`), running OS, service version, and vulnerability scripts (`-A`), skipping host discovery (`-Pn`), with verbose logging (`-v`) and output to a file (`-oN`).

```bash
$ nmap -A -v -p- -Pn -oN allports resolute.htb
# Nmap 7.91 scan initiated Wed Jan  6 23:56:07 2021 as: nmap -A -v -p- -Pn -oN allports resolute.htb
Nmap scan report for resolute.htb (10.10.10.169)
Host is up (0.042s latency).
Not shown: 65515 closed ports
PORT      STATE SERVICE      VERSION
53/tcp   open  domain?      syn-ack
| fingerprint-strings:
|   DNSVersionBindReqTCP:
|     version
|_    bind
88/tcp    open  kerberos-sec Microsoft Windows Kerberos (server time: 2021-01-07 05:12:45Z)
135/tcp   open  msrpc        Microsoft Windows RPC
139/tcp   open  netbios-ssn  Microsoft Windows netbios-ssn
389/tcp   open  ldap         Microsoft Windows Active Directory LDAP (Domain: megabank.local, Site: Default-First-Site-Name)
445/tcp   open  microsoft-ds Windows Server 2016 Standard 14393 microsoft-ds (workgroup: MEGABANK)
464/tcp   open  kpasswd5?
593/tcp   open  ncacn_http   Microsoft Windows RPC over HTTP 1.0
636/tcp   open  tcpwrapped
3269/tcp  open  tcpwrapped
5985/tcp  open  http         Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
9389/tcp  open  mc-nmf       .NET Message Framing
47001/tcp open  http         Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
49664/tcp open  msrpc        Microsoft Windows RPC
49665/tcp open  msrpc        Microsoft Windows RPC
49666/tcp open  msrpc        Microsoft Windows RPC
49667/tcp open  msrpc        Microsoft Windows RPC
49671/tcp open  msrpc        Microsoft Windows RPC
49676/tcp open  ncacn_http   Microsoft Windows RPC over HTTP 1.0
49677/tcp open  msrpc        Microsoft Windows RPC
49707/tcp open  unknown
No exact OS matches for host (If you know what OS is running on it, see https://nmap.org/submit/ ).
TCP/IP fingerprint:
OS:SCAN(V=7.91%E=4%D=1/6%OT=88%CT=1%CU=35833%PV=Y%DS=2%DC=T%G=Y%TM=5FF69500
OS:%P=x86_64-pc-linux-gnu)SEQ(SP=102%GCD=1%ISR=105%TI=I%CI=I%II=I%TS=A)SEQ(
OS:SP=102%GCD=1%ISR=105%CI=I%II=I%TS=A)SEQ(SP=102%GCD=1%ISR=105%TI=I%CI=I%I
OS:I=I%SS=S%TS=A)OPS(O1=M54DNW8ST11%O2=M54DNW8ST11%O3=M54DNW8NNT11%O4=M54DN
OS:W8ST11%O5=M54DNW8ST11%O6=M54DST11)WIN(W1=2000%W2=2000%W3=2000%W4=2000%W5
OS:=2000%W6=2000)ECN(R=Y%DF=Y%T=80%W=2000%O=M54DNW8NNS%CC=Y%Q=)T1(R=Y%DF=Y%
OS:T=80%S=O%A=S+%F=AS%RD=0%Q=)T2(R=Y%DF=Y%T=80%W=0%S=Z%A=S%F=AR%O=%RD=0%Q=)
OS:T3(R=Y%DF=Y%T=80%W=0%S=Z%A=O%F=AR%O=%RD=0%Q=)T4(R=Y%DF=Y%T=80%W=0%S=A%A=
OS:O%F=R%O=%RD=0%Q=)T5(R=Y%DF=Y%T=80%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)T6(R=Y%DF
OS:=Y%T=80%W=0%S=A%A=O%F=R%O=%RD=0%Q=)T7(R=Y%DF=Y%T=80%W=0%S=Z%A=S+%F=AR%O=
OS:%RD=0%Q=)U1(R=Y%DF=N%T=80%IPL=164%UN=0%RIPL=G%RID=G%RIPCK=G%RUCK=G%RUD=G
OS:)U1(R=N)IE(R=Y%DFI=N%T=80%CD=Z)

Uptime guess: 0.002 days (since Wed Jan  6 23:55:41 2021)
Network Distance: 2 hops
TCP Sequence Prediction: Difficulty=258 (Good luck!)
IP ID Sequence Generation: Incremental
Service Info: Host: RESOLUTE; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
|_clock-skew: mean: 2h55m15s, deviation: 4h37m09s, median: 15m14s
| smb-os-discovery: 
|   OS: Windows Server 2016 Standard 14393 (Windows Server 2016 Standard 6.3)
|   Computer name: Resolute
|   NetBIOS computer name: RESOLUTE\x00
|   Domain name: megabank.local
|   Forest name: megabank.local
|   FQDN: Resolute.megabank.local
|_  System time: 2021-01-06T21:13:46-08:00
| smb-security-mode: 
|   account_used: <blank>
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: required
| smb2-security-mode: 
|   2.02: 
|_    Message signing enabled and required
| smb2-time: 
|   date: 2021-01-07T05:13:47
|_  start_date: 2021-01-07T05:11:13

TRACEROUTE (using port 1720/tcp)
HOP RTT      ADDRESS
1   39.48 ms 10.10.14.1
2   39.50 ms resolute.htb (10.10.10.169)

Read data files from: /usr/bin/../share/nmap
OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Wed Jan  6 23:58:40 2021 -- 1 IP address (1 host up) scanned in 153.08 seconds
```

The FQDN is `Resolute.megabank.local`, Domain name is `megabank.local`. I add these to `/etc/hosts`.

## Shell as `melanie`

I use `rpcclient` to enumerate domain users over SMB. I am allowed to login and run the query with empty authentication.

```bash
$ rpcclient -U "" -N resolute.htb
rpcclient $> enumdomusers
user:[Administrator] rid:[0x1f4]
user:[Guest] rid:[0x1f5]
user:[krbtgt] rid:[0x1f6]
user:[DefaultAccount] rid:[0x1f7]
user:[ryan] rid:[0x451]
user:[marko] rid:[0x457]
user:[sunita] rid:[0x19c9]
user:[abigail] rid:[0x19ca]
user:[marcus] rid:[0x19cb]
user:[sally] rid:[0x19cc]
user:[fred] rid:[0x19cd]
user:[angela] rid:[0x19ce]
user:[felicia] rid:[0x19cf]
user:[gustavo] rid:[0x19d0]
user:[ulf] rid:[0x19d1]
user:[stevie] rid:[0x19d2]
user:[claire] rid:[0x19d3]
user:[paulo] rid:[0x19d4]
user:[steve] rid:[0x19d5]
user:[annette] rid:[0x19d6]
user:[annika] rid:[0x19d7]
user:[per] rid:[0x19d8]
user:[claude] rid:[0x19d9]
user:[melanie] rid:[0x2775]
user:[zach] rid:[0x2776]
user:[simon] rid:[0x2777]
user:[naoki] rid:[0x2778]
```

I reformat the list of users into something more easily usable.

![](img/2021-01-08-05-47-34.png)

I check the password policy, to see if I can brute force the accounts, and it looks like there is no Account Lockout Threshold, so I can.

![](img/2021-01-07-22-11-41.png)

I find a comment saying the default account password was set to `Welcome123!`.

![](img/2021-01-07-22-13-59.png)

I try it for all users I found above. It works for `melanie`.

![](img/2021-01-08-05-51-46.png)

I check if I can login to Windows Remote Manager and see that I can.

![](img/2021-01-08-05-53-16.png)

I spawn a shell with `evil-winrm`.

![](img/2021-01-08-05-53-51.png)

## Privilege Escalation to `ryan`

![](img/2021-01-08-06-05-09.png)

![](img/2021-01-08-06-06-07.png)

![](img/2021-01-08-06-07-38.png)

## Privilege Escalation to `root`

I see he is a part of the `DnsAdmins` group, which is vulnerable to this privilege escalation attack: https://medium.com/techzap/dns-admin-privesc-in-active-directory-ad-windows-ecc7ed5a21a2

![](img/2021-01-08-06-08-01.png)

I generate a payload.

![](img/2021-01-08-06-09-19.png)

I host an `SMB` server.

![](img/2021-01-08-06-10-14.png)

I start a `nc` listener.

![](img/2021-01-08-06-10-33.png)

I run the exploit.

![](img/2021-01-08-06-11-02.png)

And get a shell as `nt authority\system`.

![](img/2021-01-08-06-11-38.png)