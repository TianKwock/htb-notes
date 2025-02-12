# Dancing (Very Easy)
- **IP Address:** 10.129.181.199 
- **OS:** Windows
- **Difficulty:** Very Easy
- **HTB Link:** [Machine Page](https://app.hackthebox.com/starting-point)

---

## Enumeration 

### Nmap Scan

```
nmap -T5 -A 10.129.181.199
```

### Open Ports & Services
#### Syntax: Port ; Service ; Version

135/tcp ;  msrpc ;  Microsoft Windows RPC

139/tcp ; netbios-ssn ; Microsoft Windows netbios-ssn

445/tcp ; microsoft-ds?

### Notes

```
smbclient -L 10.129.181.199
``` 
revealed that there are 4 smb shares.

---

## Exploitation

In the Workshares share, there are 2 directories: Amy.J and James.P

In the Amy.J directrory, there is a worknotes.txt, and in the James.P directory, there is a flag.txt.

worknotes.txt seems to hint at further vulnerabilities.

### Vulnerabiliy Exploited 

```
smbclient \\\\10.129.181.199\\WorkShares
```

One of the shares was poorly configured, allowing us to login without an appropriate password.

---

## Post-Exploitation

### [Flags](https://github.com/TianKwock/htb-flags/blob/main/README.md#dancing.md)

---

## Lessons Learned

1. Server Message Block (SMB) operates on port 445.
2. The -L flag will list the available shares.
3. Shares can allow login without a proper password if misconfigured.

---

Perceived Difficulty:  Piece of Cake!

Time Taken:  15 min

Date PWNED: 02/12/2025
