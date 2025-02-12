# Appointment (Very Easy)
- **IP Address:** 10.129.245.197
- **OS:** Linux
- **Difficulty:** Very Easy
- **HTB Link:** [Machine Page](https://app.hackthebox.com/starting-point)

---

## Enumeration 

### Nmap Scan

```
nmap -T5 -sV 10.129.245.197
```

### Open Ports & Services
#### Syntax: Port ; Service ; Version

80/tcp ; http ; Apache2 http 2.4.38 (Debian)

9003/tcp ; Unknown

---

## Exploitation

When visiting the target IP on a web browser, we are presented with a login page.

```
admin' #
```

allows us to comment out the rest of the SQL query


### Vulnerabiliy Exploited 

This website did not sanitize login input, allowing us to perform an SQL injection.

---

### [Flags](https://github.com/TianKwock/htb-flags/blob/main/README.md#appointment.md)

---

## Lessons Learned

1. An example SQL query looks like this: SELECT * FROM users WHERE username = 'admin' AND password = 'password';
2. We can comment out the rest of the line after 'admin' when input is not sanitized. 

---

Perceived Difficulty:  Very Easy 

Time Taken:  15 min

Date PWNED: 02/12/2025
