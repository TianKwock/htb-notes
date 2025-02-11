# Meow (Very Easy)
- **IP Address:** '10.129.112.32'
- **OS:** Windows/Linux
- **Difficulty:** Very Easy
- **HTB Link:** [Machine Page](https://app.hackthebox.com/starting-point)

---

## Enumeration 

### Nmap Scan

```
nmap -T5 -sV 10.129.112.32
```

### Open Ports & Services
##### Syntax: Port ; Service ; Version

23 ; telnet

---

## Exploitation

Port 23 was open and running telnet, and root login was enabled.

---

## Post-Exploitation

A simple 'ls' revealed a txt file called "flag.txt"

### Flags

flag: b40abdfe23665f766f9c61ecba8a4c19

---

## Lessons Learned

1. Telnet has a root login option that can use a blank password.
2. The -sV tag for nmap shows you the name and description of serives. 

---

Perceived Difficulty: Piece of Cake!  
 
Time Taken: 5 min
