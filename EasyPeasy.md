# *CyberReg* [THM] EASY-PEASY
## Task 1 ##
**Enumeration Through Nmap**

How many ports are open?

```
Nmap scan report for --.--.---.---
Host is up (0.13s latency).
Not shown: 65532 closed ports
PORT      STATE SERVICE VERSION
--/tcp    open  http    nginx -.--.-
| http-robots.txt: 1 disallowed entry
|_/
|_http-server-header: nginx/-.--.-
|_http-title: Welcome to nginx!
----/tcp  open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey:
|   2048 30:4a:2b:22:ac:d9:56:09:f2:da:12:20:57:f4:6c:d4 (RSA)
|   256 bf:86:c9:c7:b7:ef:8c:8b:b9:94:ae:01:88:c0:85:4d (ECDSA)
|_  256 a1:72:ef:6c:81:29:13:ef:5a:6c:24:03:4c:fe:3d:0b (ED25519)
-----/tcp open  http    Apache httpd 2.4.43 ((Ubuntu))
| http-robots.txt: 1 disallowed entry
|_/
|_http-server-header: Apache/2.4.43 (Ubuntu)
|_http-title: Apache2 Debian Default Page: It works
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 1552.77 seconds
```

* nmap -A -p- < ipaddress >

*-A (Aggressive scan options)*

*-p- (port ranges)*

What is the version of nginx?

* nginx version was shown in nmap scan

What is running on the highest port?

* The highest port is 11 away for the total number of networking ports (65535)

## Task 2 ##

**Compromising the machine**

Using GoBuster, find flag 1.

```
dirbuster -H -u http://--.--.---.--- -l /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -t 200

Picked up _JAVA_OPTIONS: -Dawt.useSystemAAFontSettings=on -Dswing.aatext=true
Starting OWASP DirBuster 1.0-RC1
Starting dir/file list based brute forcing
Dir found: / - 200
Dir found: /------/ - 200
Dir found: /------/--------/ - 200

Unfortunately I was unable to get this to work without the GUI
```

This is the command used to find the first flag, flag was located

* < --.--.---.---/h-----/w------- >

Once I was on this page, I decided to view the sourcepages.

* Noticed a base64 string

* echo "base64 string" > < filename >

* base64 -d < filename > to decode string

*-d decode data*

"WALAH" there goes the first flag

Taking a bow Easy Peasy lemon squeezy

Further enumerate the machine, what is flag 2?

From earlier notes I noticed a file *------.txt*
I didn't think it would hurt to check it out at some point once I did
*Wamb Bamb Money Gram*

```
User-Agent:*
Disallow:/
Robots Not Allowed
User-Agent:a------------------------------0
Allow:/
This Flag Can Enter But Only This Flag No More Exceptions
```
hash-identifier I thought would be a good tool for this guy it pointed me in the right

direction but no *Chicken Dinner*

On the hunt now, after using *The Cyber Swiss Army Knife*

Now on to my backup tool *md5hashing.net* Well lets just say that *Swiss Army Knife was dull*

Crack the hash with easypeasy.txt, What is the flag 3?

Don't truly understand why I would need to crack flag 3 stumbled across this sitting in plain
view on one of the pages --.--.---.---:-----

What is the hidden directory?


Using the wordlist that provided to you in this task crack the hash
what is the password?

What is the password to login to the machine via SSH?

What is the user flag?

What is the root flag?
