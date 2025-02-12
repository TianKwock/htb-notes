# Redeemer (Very Easy)
- **IP Address:** 10.129.248.14 
- **OS:** Linux
- **Difficulty:** Very Easy
- **HTB Link:** [Machine Page](https://app.hackthebox.com/starting-point)

---

## Enumeration 

### Nmap Scan

```
nmap -sV -p- -T5 10.129.248.14
```
None of the first 1000 ports were open, so I scanned for all ports. 

### Open Ports & Services
#### Syntax: Port ; Service ; Version

6379/tcp ; redis ; Redis key-value store 5.0.7

redis (Remote Dictionary Server)  is an open-source, in-memory data store and database that is used as a cache and message broker.
It is a NoSQL database that stores data in memory instead of on disk. 

---

## Exploitation

```
redis-cli -h 10.129.248.14
```
This command allows us to connect to the redis server.
```
info
```
This will give us important information, such as the Keyspace, and the number of databases. In this case there is only one database, db0.

---

## Post-Exploitation

```
select 0
keys *
```
These two commands will select the db0 database and then list all the keys. We can see that there is one named flag.
```
get flag
```
will retrieve the flag for us.  

There were also 3 other keys that we could have looted.

### [Flags](https://github.com/TianKwock/htb-flags/blob/main/README.md#redeemer.md)

---

## Lessons Learned

1. redis is a key-value database.
2. The default 1000 port nmap scan may not always return what we should be finding.

---

Perceived Difficulty:  Piece of Cake!

Time Taken:  15 min

Date PWNED: 02/12/2025
