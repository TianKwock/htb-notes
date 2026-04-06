# Crocodile (Very Easy)
- **IP Address:** '10.129.88.161'
- **OS:** Linux
- **Difficulty:** Very Easy
- **HTB Link:** [Machine Page](https://app.hackthebox.com/machines/crocodile)

---

## Enumeration 

### Nmap Scan

```
nmap -sC -sV -T5 -vv 10.129.88.161
```

### Open Ports & Services
#### Syntax: Port ; Service ; Version

21 ; ftp ; vsftpd 3.0.3

80 ; http ; Apache httpd 2.4.41 ((Ubuntu))

FTP anonymous loin is enabled

---

## Exploitation

Logged in anonymously to ftp with ```ftp 10.129.88.161``` and the user ```anonymous```, and extracted the allowed.userlist and allowed.userlist.passwd files. 

Used gobuster ```gobuster dir --url http://10.129.88.161/ --wordlist /usr/share/wordlists/dirbuster/directory-list-2.3-small.txt``` to find interesting directories.


### Credential Discovery

There were credentials stored in files in the ftp server.

---

## Privilege Escalation

Used the credentials found in the ftp server to escalate to admin privileges in the web app. 

---

### [Flags](https://github.com/TianKwock/htb-flags/blob/main/README.md#crocodile.md)

---

## Lessons Learned

Use the ```-x``` switch in gobuster to filter for file extension type

---

Perceived Difficulty: Piece of Cake! 

Time Taken: 10 min 

Date PWNED: 4/6/2026 
