# *CyberReg* [THM] EASY-PEASY
## Task 1 ##
**Enumeration Through Nmap**

How many ports are open?

https://github.com/regtay/Easy-Peasy/blob/main/screenshots/nmapscan.png

* nmap -A -p- < ipaddress >

*-A (Aggressive scan options)*

*-p- (port ranges)*

What is the version of nginx?

* nginx version was shown in nmap scan

What is running on the highest port?

* The higest port is 11 away for the total number of networking ports (65535)

## Task 2 ##

**Compromising the machine**

Using GoBuster, find flag 1.

https://github.com/regtay/Easy-Peasy/blob/main/screenshots/gobuster.png

gobuster dir -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -u <url location>

This is the command used to find the first flag, flag was located
* < url/h-----/w------- >

Once I was on this page, I decided to view the sourcepages.

* Noticed a base64 string

* echo "base64 string" > < filename >

* base64 -d < filename > to decode string

-d decode data

"WALAH" there goes the first flag

Taking a bow I Easy Peasy lemon squeezy

Further enumerate the machine, what is flag 2?

Crack the hash with easypeasy.txt, What is the flag 3?

What is the hidden directory?

Using the wordlist that provided to you in this task crack the hash
what is the password?

What is the password to login to the machine via SSH?

What is the user flag?

What is the root flag?
