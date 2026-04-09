# Oopsie (Very Easy)
- **IP Address:** '10.129.95.191'
- **OS:** Linux
- **Difficulty:** Very Easy
- **HTB Link:** [Machine Page](https://app.hackthebox.com/machines/oopsie)

---

## Enumeration 
### Nmap Scan

```
nmap -sC -sV -p 22,80 -T5 10.129.95.191
```

| Port | Service | Version |
|------|---------|---------|
| 22 | ssh | OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0) |
| 80 | http | Apache httpd 2.4.29 ((Ubuntu)) |

### Further Enumeration

Used burpsuite to intercept the request for the page, then under target -> sitemap, saw where the login page was stored

Then I log in as guest

---

## Exploitation
### Vulnerabiliy Identified

IDOR allowed me to change my id from 2 to 1 in the url, which was the admin ID, 34322

### Exploitation Steps

```
I then visited the uploads page and changed my cookie value to the admin cookie value

I then uploaded /usr/share/webshells/php/php-reverse-shell.php and started a nc listener on my kali.

Finally I upgraded to a bash shell using ```python3 -c 'import pty;pty.spawn("/bin/bash")'```
```

### Initial Foothold

I now have a bash shell with the www-data user

---

## Privilege Escalation
### PrivEsc Enumeration 

In /home/robert, I found the user flag

In /var/www/html/cdn-cgi/login, I ran ```cat * | grep passw*```, which returned admin:MEGACORP_4dm1n!!

Also, the db.php file had robert:M3g4C0rpUs3r!

I switched to the robert user and checked his groups, one of which was bugtracker 

I ran ```find / -group bugtracker 2>/dev/null``` to find binaries, which returned /usr/bin/bugtracker, which has the suid bit set

When i ran the executable, it appeared to try to read a file using 'cat', so I tried to path hijack the cat binary

### Root Exploitation

```
Created a file named cat in /tmp, which contained ```/bin/sh```, and gave it execute perms

Then I ran ```export PATH=/tmp:$PATH``` to make sure it sees my cat binary first, then re-ran the executable, and got a root shell

The root flag was found in /root
```

---

### [Flags](https://github.com/TianKwock/htb-flags/blob/main/README.md#X)

---

## Lessons Learned

burpsuites target sitemap can be a useful tool

Look for binaries that are related to the group of a user you control

Look for insecure uses of standard binaries for path hijacking opportunities 

---

Perceived Difficulty: Easy 

Time Taken: 45 min 

Date PWNED: 4/9/2026 
