# Silo (`10.10.10.82`)

## Summary

I find an Oracle database that I can log into with default credentials. I upload a reverse shell and execute it, and I am root. 

## Enumeration

I start a portscan of all ports (`-p-`), running OS, service version, and vulnerability scripts (`-A`), skipping host discovery (`-Pn`), with verbose logging (`-v`) and output to a file (`-oN`).

```bash
$ nmap -A -v -p- -Pn -oN allports silo.htb
Nmap scan report for silo.htb (10.10.10.82)
Host is up (0.13s latency).
Not shown: 65488 closed ports
PORT      STATE    SERVICE        VERSION
80/tcp    open     http           Microsoft IIS httpd 8.5
| http-methods:
|   Supported Methods: OPTIONS TRACE GET HEAD POST
|_  Potentially risky methods: TRACE
|_http-server-header: Microsoft-IIS/8.5
|_http-title: IIS Windows Server
135/tcp   open     msrpc          Microsoft Windows RPC
139/tcp   open     netbios-ssn    Microsoft Windows netbios-ssn
445/tcp   open     microsoft-ds   Microsoft Windows Server 2008 R2 - 2012 microsoft-ds
1198/tcp  filtered cajo-discovery
1521/tcp  open     oracle-tns     Oracle TNS listener 11.2.0.2.0 (unauthorized)
1682/tcp  filtered lanyon-lantern
1987/tcp  filtered tr-rsrb-p1
3453/tcp  filtered pscupd
5985/tcp  open     http           Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
6053/tcp  filtered x11
7257/tcp  filtered unknown
9787/tcp  filtered unknown
9858/tcp  filtered unknown
9902/tcp  filtered unknown
9963/tcp  filtered unknown
10315/tcp filtered unknown
10652/tcp filtered unknown
13092/tcp filtered unknown
14000/tcp filtered scotty-ft
19058/tcp filtered unknown
19148/tcp filtered unknown
22375/tcp filtered unknown
32851/tcp filtered unknown
36315/tcp filtered unknown
38821/tcp filtered unknown
40831/tcp filtered unknown
43984/tcp filtered unknown
47001/tcp open     http           Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
49152/tcp open     msrpc          Microsoft Windows RPC
49153/tcp open     msrpc          Microsoft Windows RPC
49154/tcp open     msrpc          Microsoft Windows RPC
49155/tcp open     msrpc          Microsoft Windows RPC
49159/tcp open     oracle-tns     Oracle TNS listener (requires service name)
49160/tcp open     msrpc          Microsoft Windows RPC
49161/tcp open     msrpc          Microsoft Windows RPC
49162/tcp open     msrpc          Microsoft Windows RPC
49740/tcp filtered unknown
53762/tcp filtered unknown
54603/tcp filtered unknown
55225/tcp filtered unknown
56906/tcp filtered unknown
59089/tcp filtered unknown
59580/tcp filtered unknown
61721/tcp filtered unknown
62296/tcp filtered unknown
64811/tcp filtered unknown
No exact OS matches for host (If you know what OS is running on it, see https://nmap.org/submit/ ).
TCP/IP fingerprint:
OS:SCAN(V=7.80%E=4%D=11/2%OT=80%CT=1%CU=31007%PV=Y%DS=2%DC=T%G=Y%TM=5FA0EF6
OS:6%P=x86_64-pc-linux-gnu)SEQ(SP=FA%GCD=1%ISR=FF%TI=I%CI=I%II=I%SS=S%TS=7)
OS:SEQ(SP=FA%GCD=1%ISR=FF%TI=I%CI=I%TS=7)OPS(O1=M54DNW8ST11%O2=M54DNW8ST11%
OS:O3=M54DNW8NNT11%O4=M54DNW8ST11%O5=M54DNW8ST11%O6=M54DST11)WIN(W1=2000%W2
OS:=2000%W3=2000%W4=2000%W5=2000%W6=2000)ECN(R=Y%DF=Y%T=80%W=2000%O=M54DNW8
OS:NNS%CC=Y%Q=)T1(R=Y%DF=Y%T=80%S=O%A=S+%F=AS%RD=0%Q=)T2(R=Y%DF=Y%T=80%W=0%
OS:S=Z%A=S%F=AR%O=%RD=0%Q=)T3(R=Y%DF=Y%T=80%W=0%S=Z%A=O%F=AR%O=%RD=0%Q=)T4(
OS:R=Y%DF=Y%T=80%W=0%S=A%A=O%F=R%O=%RD=0%Q=)T5(R=Y%DF=Y%T=80%W=0%S=Z%A=S+%F
OS:=AR%O=%RD=0%Q=)T6(R=Y%DF=Y%T=80%W=0%S=A%A=O%F=R%O=%RD=0%Q=)T7(R=Y%DF=Y%T
OS:=80%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)U1(R=Y%DF=N%T=80%IPL=164%UN=0%RIPL=G%RI
OS:D=G%RIPCK=G%RUCK=G%RUD=G)IE(R=Y%DFI=N%T=80%CD=Z)

Uptime guess: 0.247 days (since Mon Nov  2 17:53:49 2020)
Network Distance: 2 hops
TCP Sequence Prediction: Difficulty=250 (Good luck!)
IP ID Sequence Generation: Incremental
Service Info: OSs: Windows, Windows Server 2008 R2 - 2012; CPE: cpe:/o:microsoft:windows

Host script results:
|_clock-skew: mean: 7m03s, deviation: 0s, median: 7m02s
|_smb-os-discovery: ERROR: Script execution failed (use -d to debug)
| smb-security-mode:
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: supported
| smb2-security-mode:
|   2.02:
|_    Message signing enabled but not required
| smb2-time:
|   date: 2020-11-03T05:56:26
|_  start_date: 2020-11-03T00:01:06

TRACEROUTE (using port 22/tcp)
HOP RTT       ADDRESS
1   87.92 ms  10.10.14.1
2   170.94 ms silo.htb (10.10.10.82)

NSE: Script Post-scanning.
Initiating NSE at 23:49
Completed NSE at 23:49, 0.00s elapsed
Initiating NSE at 23:49
Completed NSE at 23:49, 0.00s elapsed
Initiating NSE at 23:49
Completed NSE at 23:49, 0.00s elapsed
Read data files from: /usr/bin/../share/nmap
OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 21295.49 seconds
           Raw packets sent: 70307 (3.099MB) | Rcvd: 299047 (26.293MB)
```

### Oracle TNS Listener

I use `odat.py` to enumerate the Oracle databases.

```bash
$ python3 odat.py sidguesser -s 10.10.10.82

[1] (10.10.10.82:1521): Searching valid SIDs
[1.1] Searching valid SIDs thanks to a well known SID list on the 10.10.10.82:1521 server
[+] 'XE' is a valid SID. Continue...                              ####################################################################  | ETA:  00:00:00
[+] 'XEXDB' is a valid SID. Continue...
100% |##################################################################################################################################| Time: 00:01:40
[1.2] Searching valid SIDs thanks to a brute-force attack on 1 chars now (10.10.10.82:1521)
100% |##################################################################################################################################| Time: 00:00:02
[1.3] Searching valid SIDs thanks to a brute-force attack on 2 chars now (10.10.10.82:1521)
[+] 'XE' is a valid SID. Continue...                              #######################################################               | ETA:  00:00:07
100% |##################################################################################################################################| Time: 00:01:06
[+] SIDs found on the 10.10.10.82:1521 server: XE,XEXDB
```

It finds two valid SIDS: `XE` and `XEXDB`.

Using the `passwordguesser` module in `odat`, I find the credentials: `scott:tiger`. These are default Oracle credentials.

![](img/2020-11-04-00-13-45.png)

## Reverse Shell

I generate a reverse shell with `msfvenom`.

![](img/2020-11-04-02-55-47.png)

I upload it to the target, guessing the `C:\temp\shell.exe` path will work. It does.

![](img/2020-11-04-02-56-07.png)

I execute the shell after starting a `nc` listener, and get a root shell.

![](img/2020-11-04-02-58-01.png)

![](img/2020-11-04-02-58-15.png)