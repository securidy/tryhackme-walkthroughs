# [Agent Sudo](https://tryhackme.com/room/agentsudoctf)
You found a secret server located under the deep sea. Your task is to hack inside the server and reveal the truth.

## Task 1 - Author note

### Question: Deploy the machine
```
Answer: No answer needed
```

## Task 2 - Enumerate

### Question: How many open ports?
* Scan the network

`nmap -sV -sC [IP address]`
```
Answer: 3
```
### Question: How you redirect yourself to a secret page?
* As the web server states, we need to change the `User-Agent` to the codename (probably Agent R) to access the site
```
Answer: user-agent
```
### Question: What is the agent name?
* Launch Burp Suite and intercept the server request to modify the `User-Agent` field
* Changing it to `Agent R` doesn't do anything
  * Changing it to just `R` prints a new message on the web page
* It's likely that the agents are using letters as their codename
  * We can try to attempt different letters to see if we find a match
* `C` turns out to be the codename for `chris`
  * It also redirects us to another page

`/agent_C_attention.php`
```
Answer: chris
```

## Task 3 - Hash cracking and brute-force

### Question: FTP password
* Now that we have the name of the agent, we can attempt to brute-force the password using Hydra
  * We know it's weak based off the message on the web page we found earlier

`hydra -l chris -P /usr/share/wordlists/rockyou.txt ftp://[IP address]:21`
```
Answer: crystal
```
### Question: Zip file password
* We can use the login credentials to FTP into the server

`ftp chris@10.10.42.62 `
 
