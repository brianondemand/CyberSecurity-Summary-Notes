
## ENUMERATION

We start the attack by finding the IP of the victim machine by using the netdiscover command run as root or use sudo:

```
netdiscover

```
image: 1

- Now that we know our target IP, let's start by scanning the ports and try to get more information about it:


```
nmap -sC -sV -Pn -p- -T4 -oN full_scan.txt 192.168.1.58

```

-sC: Run default Nmap scripts
-sV: Determine service/version info
-Pn: Treat all hosts as online -- skip host discovery
-p-: Scan all ports
-T4: Set timing template (higher is faster)
-oN: Output scan in normal

image: 2

The port 8080 is open so I started enumeration from port 80/HTTP and I found a website related to the Shuriken Company. 

In the navigation bar, I found Log in page any tried some common credentials but that didn't work. 

image: 3

Next I thought to go for directory brute force and found some useful directories.

```
gobuster dir -u http://192.168.1.58:8080 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
                        

```

image: 4

Check the Session Id provided by the server

```
eyJ1c2VybmFtZSI6Ikd1ZXN0IiwiaXNHdWVzdCI6dHJ1ZSwiZW5jb2RpbmciOiAidXRmLTgifQ%3D%3D

```

Session_Id image 

Session_Id_decode Image

Here, to make a modification using `Cyberchef`, we are changing the value of ‘Guest’ within the cookie to ‘Admin’. The server processes this and updates the greeting from ‘Welcome, Guest’ to ‘Welcome, Admin’. 

cookie_change 1 image

cookie_change 2 image


When we see text reflected on the front-end, we may immediately think of an XSS and SSTI attack. As a check, instead of changing the value to ‘admin’, we modify it to ‘${7*7}’.

cookie_change 3 image

cookie_change 4 image

I swapped my cookie and I got error.

cookie_change error image

Error tells many things that can really help you. If you see the third line of the error, you will notice it’s serializing and unserializing the cookie object.

Finally I went to google to find a way to exploit this serialization.
