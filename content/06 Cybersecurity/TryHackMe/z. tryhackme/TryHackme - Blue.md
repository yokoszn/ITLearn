___
**Tags:** #hacking #Learning #practice-exercises [[Windows]] [[Nmap]]

**Links:** 

---
nmap -sS -vv <ip_address>
```
PORT      STATE SERVICE       REASON
135/tcp   open  msrpc         syn-ack ttl 128
139/tcp   open  netbios-ssn   syn-ack ttl 128
445/tcp   open  microsoft-ds  syn-ack ttl 128
3389/tcp  open  ms-wbt-server syn-ack ttl 128
49152/tcp open  unknown       syn-ack ttl 128
49153/tcp open  unknown       syn-ack ttl 128
49154/tcp open  unknown       syn-ack ttl 128
49158/tcp open  unknown       syn-ack ttl 128
49160/tcp open  unknown       syn-ack ttl 128
MAC Address: 02:F7:E0:20:0E:23 (Unknown)

Read data files from: /usr/bin/../share/nmap
Nmap done: 1 IP address (1 host up) scanned in 55.44 seconds
           Raw packets sent: 1868 (82.176KB) | Rcvd: 1269 (50.800KB)

```

-sC -- Common Scripts

-script vuln -- scan vulnerabilities

less / more or any other reader


start metasploit 
search for ms17-010 CVE

CVE-2017-0144

exploit/windows/smb/ms17_010_eternalblue

meterpreter

ps

Migrate to this process using the 'migrate PROCESS_ID' command where the process id is the one you just wrote down in the previous step. This may take several attempts, migrating processes is not very stable. If this fails, you may need to re-run the conversion process or reboot the machine and start once again. If this happens, try a different process next time.
