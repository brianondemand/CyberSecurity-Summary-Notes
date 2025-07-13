## DEATHNOTE WALKTHROUGH


- write short notes

- take screenshots

- dont clear terminal use `CTRL + L`

- use ssh to connect to target

- aim to get root.txt file


Step 1 : Find VM IP on the network

> `angry-ip scanner` (open ports)

> `netdiscover`  (look for PCS Systemtechnik GmbH)


 
Step 2 : Nmap scan

> `nmap -A 192.168.1.78`

> `nmap -Pn -v 10.10.10.2`

-  i discovered that ports 80(HTTP) and 22(SSH) are open.




Step 3: Host File

- i open the website using our browser. We type in 10.10.10.2 ( If an error shows up, add the ip address to the hosts file in /etc). 




Step 4: Explore

- i found a hint button. Let’s click on that.

- It is asking us to locate a notes.txt file. Let’s see if we can find something out by viewing the pages source code.

- i found the Notes.txt file already! There is also a user.txt file. Let’s look into their contents.


A robots.txt file is a text file that provides instructions to web crawlers, like those used by search engines, on which parts of a website they can or cannot access. It's located in the root directory of a website (e.g., https://www.example.com/robots.txt). 


- Light’s Dad added a hint in the important.jpg file lets look at it.

- I used curl to return the data from the image.

> `curl http://deathnote.vuln/important.jpg`
``
- There is some content hidden there


- This confirms that user.txt can be used as a wordlist for usernames and notes.txt can be used for passwords.


Step 5: Bruteforce Users


- I will be Using hydra to bruteforce login into the target machine.

> `hydra -L users.txt -P notes.txt ssh://192.168.1.78`


- I found the credentials `user : l` `password: death4me`.


> `ssh l@192.168.1.78`  `passwd : death4me `


- Run this for enumeration.

> `whoami`

> `id`

> `pwd`

> `ls -la`


Step 6: User.txt File Decode

- I found user.txt file which has hidden content.



> (ChatGPT) 

- The code you’ve shared is not a cryptographic method—instead, it is a program written in an esoteric programming language called Brainfuck.

- Brainfuck is a minimalist, Turing-complete programming language created for fun and obfuscation. It uses only 8 characters:

`+ - < > [ ] . ,`

- Each character performs a very low-level operation on an array of memory cells, similar to how a Turing machine works.


- (our user.txt file) This is a Brainfuck program that, when run, produces a human-readable message (like ASCII text). It’s not encrypted, but obfuscated through Brainfuck’s obscure syntax.


- to decode i can use

> Online Tools:

`https://copy.sh/brainfuck/`


`https://www.dcode.fr/brainfuck-language`


Just paste your code into the interpreter, and it will print the hidden message.



- on the /home i see another user `kira` noted (bruteforce using hydra)



Step 7: OPT Directory

- The /opt directory in Linux is primarily used for installing add-on application software packages that are not part of the base system.

- I found a folder called `L` cd into it and find other two : `fake-notebook-rule`  `kira-case`

- Start with kira-case folder i got a case file which had a message.


- Go to fake-notebook-rule folder.

- Found two file : `case.wav` &  `hint`

- The hint file is saying we use `cyberchef` (online decoder/encoder).

- The case.wav is a hexadecimal representation of ASCII characters lets decode it. After decoding it i got a base64 encoded text.

> cyberchef - From Hex + From Base64


- After decoding i get a text : `passwd : kiraisevil `


Step 8: Switch to Kira


> `ssh kira@192.168.1.78`  `passwd : kiraisevil `


- Created after L based on user id

- I found a `kira.txt` file which had some Base64 encoded text.

- After decoding from Base64 i got :

`please protect one of the following 
1. L (/opt)
2. Misa (/var)
`

Interesting. As i already explored the /opt directory we explore the /var directory now.



Step 9: VAR Directory


> `cd /var`

> `ls -la`


- i can see the `misa` file belongs to the root user and group so i viewed the content in the file. I learn that misa cannot be saved.


Step 10: Becoming Root



- We i run the `id` command `Kira` was in `sudo` group.


> `sudo cat /etc/sudoers`



> `sudo /bin/bash` to switch to root user so i can visit the `/` (root directory)


- Yes i can lets vist the `/root` directory and see what there


- I get a `root.txt` file which contains a flag.




`https://medium.com/@satyamgarg_94325/deathnote-1-vulnhub-walkthrough-c2c1c793e128` Walkthough