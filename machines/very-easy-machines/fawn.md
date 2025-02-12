# Fawn (Very Easy)
- **IP Address:** '10.129.29.96'
- **OS:** Linux
- **Difficulty:** Very Easy
- **HTB Link:** [Machine Page](https://app.hackthebox.com/starting-point)

---

## Enumeration 

### Nmap Scan

```
nmap -T5 -A 10.129.29.96
```

The nmap scan revealed that there is a flag.txt file on the ftp server.

### Open Ports & Services
#### Syntax: Port ; Service ; Version

21 ; ftp ; vsftpd 3.0.3

---

## Exploitation

### Vulnerabiliy Exploited 

```
ftp 10.129.29.96
get flag.txt
```

Anonymous login was enabled for ftp. 

---

## Post-Exploitation

### [Flags](https://github.com/TianKwock/htb-flags/blob/main/README.md#fawn.md)

---

## Lessons Learned

1. Anonymous login on ftp allows you to login with any password.

---

Perceived Difficulty: Piece of Cake!

Time Taken: 5 min

Date PWNED: 02/11/2025
