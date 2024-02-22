# [Simple CTF](https://tryhackme.com/room/easyctf)
Beginner level ctf.

## Task 1 - Simple CTF

### Question: How many services are running under port 1000?
* Run a network scan to discover any active services

```nmap -sV [IP address]```
```
Answer: 2
```
---
### Question: What is running on the higher port?
```
Answer: ssh
```
---
### Question: What's the CVE you're using against the application?
* Search for any directories

```gobuster dir -u 10.10.213.243 -w /usr/share/wordlists/rockyou.txt ```
* Found the directory ```/simple/``` that looks interesting
  * Looking around the page, we find the website running ```CMS Made Simple version 2.2.8```
  * Under News, it shows that a news module was installed
* Search for this in a CVE database
```
Answer: CVE-2019-9053
```
---
### Question: To what kind of vulnerability is the application vulnerable?
```
Answer: SQLi
```
---
### Question: What's the password?
* We can use the information about the CVE to find and download the appropriate exploit on ```exploit-db.com```
  * ```CMS Made Simple < 2.2.10 - SQL Injection``` 
* 
