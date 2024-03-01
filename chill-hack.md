# [Chill Hack](https://tryhackme.com/room/chillhack)
Easy level CTF. Capture the flags and have fun!

## Task 1 - Investigate

### Question: User Flag
* Begin by running a network scan

```nmap -sV -sC [IP address]```
* Found 3 ports open
  * Anonymous FTP login is allowed
* Using ```ls```, we find a ```note.txt``` file
  * Download the file inside the FTP shell using ```get note.txt``` and view its contents
* We obtain the following information:
  * Two users named Anurodh and Apaar
  * Filtering on strings 
* Let's take a look at the web server
  * We can try to see if there are any interesting directories worth checking

```gobuster dir -u 10.10.24.132 -w /usr/share/wordlists/rockyou.txt```
* The directory ```/secret``` stands out
  * Takes us to page with an input field and a button labeled ```Execute```
    * We can try to run some commands to see what happens
      * Some commands like ```ls``` are being filtered, like the note says
* A reverse shell should work