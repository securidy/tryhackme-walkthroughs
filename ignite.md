# [Ignite](https://tryhackme.com/room/ignite)
A new start-up has a few issues with their web server.

## Task 1 - Root it!

### Question: User.txt
* Scan the network for any open ports

`nmap -sC -sV [IP address]`
* Port 80 is open
  * Let's check out the web server
* Takes us to a web page for `Fuel CMS`, running on `version 1.4`
* Also displays login credentials for an admin account:
  * username: `admin`
  * password: `admin`
  * Doesn't seem hold any important information 
* Let's see if there are any exploits for this application:
 
`searchsploit fuel cms` 
* Found a number of exploits
* Let's use this one:

`fuel CMS 1.4.1 - Remote Code Execution (1) linux/webapps/47138.py`
* Download it and change the target URL and port number
  
`url = "http://[IP address]:[Port number]"`


  
