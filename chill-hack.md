# [Chill Hack](https://tryhackme.com/room/chillhack)
Easy level CTF. Capture the flags and have fun!

## Task 1 - Investigate

### Question: User Flag
* Begin by running a network scan

```nmap -sV [IP address]```
* Found 3 ports open
  * Let's take a look at the web page hosted at that IP address
* We can try to see if there are any interesting directories worth checking

```gobuster dir -u 10.10.24.132 -w /usr/share/wordlists/rockyou.txt```
* The directory ```/secret``` stands out
  * Takes us to page with an input field and a button labeled ```Execute```
    * We can try to run some commands to see what happens
      * Doesn't seem to like ```ls```, but some other commands are working
      * Running ```sudo -l``` reveals a user named apaar
* A reverse shell should work