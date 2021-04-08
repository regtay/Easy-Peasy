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

On the hunt now, after using *The Cyber Swiss Army Knife* no Luck.

Now on to my backup tool *md5hashing.net* Well lets just say that *Swiss Army Knife was dull*

Crack the hash with easypeasy.txt, What is the flag 3?

Don't truly understand why I would need to crack flag 3 stumbled across this sitting in plain
view on one of the pages --.--.---.---:-----

* But I thought it would be fun if I tried it anyway, nothing. I think this was a typo intended
for another question.

What is the hidden directory?

Any time I visit a page, I find it to be good practice to always view the page source
```
page source --.--.---.---:-----

<div class="main_page">
      <div class="page_header floating_element">
        <img src="/icons/openlogo-75.png" alt="Debian Logo" class="floating_element"/>
        <span class="floating_element">
          Apache 2 It Works For Me
	<p hidden>its encoded with ba....:O----------------------u</p>
        </span>
      </div>
```

So I had to sharpen my *Cyber Swiss Army Knife* comes to find out it decided to cut away

at this base62 string O----------------------u

/n---------------r is what it came with, what do I do with this now.

Using the wordlist that provided to you in this task crack the hash

After locating hidden directory, navigate to

--.--.---.---:/n---------------r

```
view page source

</style>
</head>
<body>
<center>
<img src="b-----------------.jpg" width="140px" height="140px"/>
<p>940d---------------f8ab8---------------186a66---------------fd81</p>
</center>
</body>
</html>
```
echo "940d---------------f8ab8---------------186a66---------------fd81" > <filename>

using hashcat and the hint combo

hashcat -a 0 -m 6900 <filename> easypeasy.txt **Must be run as sudo**

*-a attack mode

*0 MD5

*-m hash type

*6900 GOST R 34.11-94
```
sudo hashcat -a 0 -m 6900 hash.txt ~/Downloads/easypeasy.txt                                                                                                                                                              2 ⚙
hashcat (v6.1.1) starting...

/usr/share/hashcat/OpenCL/m06900_a0-optimized.cl: Pure kernel not found, falling back to optimized kernel
OpenCL API (OpenCL 1.2 pocl 1.6, None+Asserts, LLVM 9.0.1, RELOC, SLEEF, DISTRO, POCL_DEBUG) - Platform #1 [The pocl project]
=============================================================================================================================
* Device #1: pthread-Intel(R) Xeon(R) CPU E5-4640 0 @ 2.40GHz, 13895/13959 MB (4096 MB allocatable), 8MCU

/usr/share/hashcat/OpenCL/m06900_a0-optimized.cl: Pure kernel not found, falling back to optimized kernel
Minimum password length supported by kernel: 0
Maximum password length supported by kernel: 32

Hashes: 1 digests; 1 unique digests, 1 unique salts
Bitmaps: 16 bits, 65536 entries, 0x0000ffff mask, 262144 bytes, 5/13 rotates
Rules: 1

Applicable optimizers applied:
* Optimized-Kernel
* Zero-Byte
* Not-Iterated
* Single-Hash
* Single-Salt

Watchdog: Hardware monitoring interface not found on your system.
Watchdog: Temperature abort trigger disabled.

Host memory required for this attack: 66 MB

Dictionary cache built:
* Filename..: /home/------/Downloads/easypeasy.txt
* Passwords.: 5141
* Bytes.....: 48857
* Keyspace..: 5141
* Runtime...: 0 secs

Approaching final keyspace - workload adjusted.  

940d---------------f8ab8---------------186a66---------------fd81:m------------------b

Session..........: hashcat
Status...........: Cracked
Hash.Name........: GOST R 34.11-94
Hash.Target......: 940d---------------f8ab8---------------186a66---------------fd81
Time.Started.....: Thu Apr  8 01:38:43 2021 (1 sec)
Time.Estimated...: Thu Apr  8 01:38:44 2021 (0 secs)
Guess.Base.......: File (/home/------/Downloads/easypeasy.txt)
Guess.Queue......: 1/1 (100.00%)
Speed.#1.........:    34990 H/s (6.89ms) @ Accel:256 Loops:1 Thr:1 Vec:8
Recovered........: 1/1 (100.00%) Digests
Progress.........: 4097/5141 (79.69%)
Rejected.........: 1/4097 (0.02%)
Restore.Point....: 2048/5141 (39.84%)
Restore.Sub.#1...: Salt:0 Amplifier:0-1 Iteration:0-1
Candidates.#1....: fantasy14 -> flash72

Started: Thu Apr  8 01:36:30 2021
Stopped: Thu Apr  8 01:38:45 2021
```
what is the password?

What is the password to login to the machine via SSH?

What is the user flag?

What is the root flag?
