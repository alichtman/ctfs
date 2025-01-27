# Monteverde

## IP: 10.10.10.172

First, add `10.10.10.172` to `/etc/hosts` file as `monteverde.htb`.

```bash
$ nmap -vvv -sCV -oN monteverde.nmap monteverde.htb -Pn
# Nmap 7.80 scan initiated Tue Apr 14 14:58:44 2020 as: nmap -vvv -sCV -oN monteverde.nmap -Pn monteverde.htb
Nmap scan report for monteverde.htb (10.10.10.172)
Host is up, received user-set (0.053s latency).
Scanned at 2020-04-14 14:58:44 CDT for 312s
Not shown: 989 filtered ports
Reason: 989 no-responses
PORT     STATE SERVICE       REASON  VERSION
53/tcp   open  domain?       syn-ack
| fingerprint-strings: 
|   DNSVersionBindReqTCP: 
|     version
|_    bind
88/tcp   open  kerberos-sec  syn-ack Microsoft Windows Kerberos (server time: 2020-04-14 19:11:42Z)
135/tcp  open  msrpc         syn-ack Microsoft Windows RPC
139/tcp  open  netbios-ssn   syn-ack Microsoft Windows netbios-ssn
389/tcp  open  ldap          syn-ack Microsoft Windows Active Directory LDAP (Domain: MEGABANK.LOCAL0., Site: Default-First-Site-Name)
445/tcp  open  microsoft-ds? syn-ack
464/tcp  open  kpasswd5?     syn-ack
593/tcp  open  ncacn_http    syn-ack Microsoft Windows RPC over HTTP 1.0
636/tcp  open  tcpwrapped    syn-ack
3268/tcp open  ldap          syn-ack Microsoft Windows Active Directory LDAP (Domain: MEGABANK.LOCAL0., Site: Default-First-Site-Name)
3269/tcp open  tcpwrapped    syn-ack
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port53-TCP:V=7.80%I=7%D=4/14%Time=5E961608%P=x86_64-pc-linux-gnu%r(DNSV
SF:ersionBindReqTCP,20,"\0\x1e\0\x06\x81\x04\0\x01\0\0\0\0\0\0\x07version\
SF:x04bind\0\0\x10\0\x03");
Service Info: Host: MONTEVERDE; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
|_clock-skew: -47m17s
| p2p-conficker: 
|   Checking for Conficker.C or higher...
|   Check 1 (port 10664/tcp): CLEAN (Timeout)
|   Check 2 (port 2859/tcp): CLEAN (Timeout)
|   Check 3 (port 47166/udp): CLEAN (Timeout)
|   Check 4 (port 52319/udp): CLEAN (Timeout)
|_  0/4 checks are positive: Host is CLEAN or ports are blocked
| smb2-security-mode: 
|   2.02: 
|_    Message signing enabled and required
| smb2-time: 
|   date: 2020-04-14T19:14:02
|_  start_date: N/A

Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Tue Apr 14 15:03:56 2020 -- 1 IP address (1 host up) scanned in 311.87 seconds
```

We note the following `LDAP` domain: `MEGABANK.LOCAL0.`
