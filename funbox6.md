# Enumeration

### NMAP

```console
noob2uub@kali:~/Documents/vulnhub/funbox6$ sudo nmap -sC -sV -sS -Pn -A -p- 192.168.1.114
[sudo] password for noob2uub: 
Starting Nmap 7.92 ( https://nmap.org ) at 2022-04-22 15:52 PDT
Nmap scan report for funbox6.box (192.168.1.114)
Host is up (0.00030s latency).
Not shown: 65533 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.10 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 0e:4f:3c:37:75:8a:a4:4d:bb:17:50:1b:ec:93:02:15 (RSA)
|   256 d7:dc:fc:b1:76:d6:76:13:da:ea:c4:30:04:bc:da:d2 (ECDSA)
|_  256 51:19:47:a6:29:c8:22:10:c2:73:34:ad:de:7f:57:d3 (ED25519)
80/tcp open  http    Apache httpd 2.4.18 ((Ubuntu))
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-generator: WordPress 5.5.1
|_http-title: Funbox: Gamble hall &#8211; OPENED
MAC Address: 08:00:27:50:3A:D9 (Oracle VirtualBox virtual NIC)
Device type: general purpose
Running: Linux 3.X|4.X
OS CPE: cpe:/o:linux:linux_kernel:3 cpe:/o:linux:linux_kernel:4
OS details: Linux 3.2 - 4.9
Network Distance: 1 hop
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE
HOP RTT     ADDRESS
1   0.30 ms funbox6.box (192.168.1.114)

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 10.55 seconds
