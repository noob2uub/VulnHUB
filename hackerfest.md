# Enumeration

### NMAP

```console
noob2uub@kali:~/Documents/vulnhub/hackerfest$ sudo nmap -sC -sV -sS -Pn -A -p- 192.168.1.24
[sudo] password for noob2uub: 
Starting Nmap 7.92 ( https://nmap.org ) at 2022-04-22 15:01 PDT
Nmap scan report for 192.168.1.24
Host is up (0.00031s latency).
Not shown: 65531 closed tcp ports (reset)
PORT      STATE SERVICE  VERSION
21/tcp    open  ftp      vsftpd 3.0.3
| ftp-syst: 
|   STAT: 
| FTP server status:
|      Connected to 192.168.1.166
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
| -rw-rw-r--    1 ftp      ftp           420 Nov 30  2017 index.php
| -rw-rw-r--    1 ftp      ftp         19935 Sep 05  2019 license.txt
| -rw-rw-r--    1 ftp      ftp          7447 Sep 05  2019 readme.html
| -rw-rw-r--    1 ftp      ftp          6919 Jan 12  2019 wp-activate.php
| drwxrwxr-x    9 ftp      ftp          4096 Sep 05  2019 wp-admin
| -rw-rw-r--    1 ftp      ftp           369 Nov 30  2017 wp-blog-header.php
| -rw-rw-r--    1 ftp      ftp          2283 Jan 21  2019 wp-comments-post.php
| -rw-rw-r--    1 ftp      ftp          3255 Sep 27  2019 wp-config.php
| drwxrwxr-x    8 ftp      ftp          4096 Sep 29  2019 wp-content
| -rw-rw-r--    1 ftp      ftp          3847 Jan 09  2019 wp-cron.php
| drwxrwxr-x   20 ftp      ftp         12288 Sep 05  2019 wp-includes
| -rw-rw-r--    1 ftp      ftp          2502 Jan 16  2019 wp-links-opml.php
| -rw-rw-r--    1 ftp      ftp          3306 Nov 30  2017 wp-load.php
| -rw-rw-r--    1 ftp      ftp         39551 Jun 10  2019 wp-login.php
| -rw-rw-r--    1 ftp      ftp          8403 Nov 30  2017 wp-mail.php
| -rw-rw-r--    1 ftp      ftp         18962 Mar 28  2019 wp-settings.php
| -rw-rw-r--    1 ftp      ftp         31085 Jan 16  2019 wp-signup.php
| -rw-rw-r--    1 ftp      ftp          4764 Nov 30  2017 wp-trackback.php
|_-rw-rw-r--    1 ftp      ftp          3068 Aug 17  2018 xmlrpc.php
22/tcp    open  ssh      OpenSSH 7.4p1 Debian 10+deb9u7 (protocol 2.0)
| ssh-hostkey: 
|   2048 b7:2e:8f:cb:12:e4:e8:cd:93:1e:73:0f:51:ce:48:6c (RSA)
|   256 70:f4:44:eb:a8:55:54:38:2d:6d:75:89:bb:ec:7e:e7 (ECDSA)
|_  256 7c:0e:ab:fe:53:7e:87:22:f8:5a:df:c9:da:7f:90:79 (ED25519)
80/tcp    open  http     Apache httpd 2.4.25 ((Debian))
|_http-server-header: Apache/2.4.25 (Debian)
|_http-title: Tata intranet &#8211; Just another WordPress site
|_http-generator: WordPress 5.2.3
10000/tcp open  ssl/http MiniServ 1.890 (Webmin httpd)
|_http-title: Login to Webmin
|_ssl-date: TLS randomness does not represent time
| ssl-cert: Subject: commonName=*/organizationName=Webmin Webserver on Linux-Debian
| Not valid before: 2019-09-09T13:32:42
|_Not valid after:  2024-09-07T13:32:42
| http-robots.txt: 1 disallowed entry 
|_/
MAC Address: 08:00:27:9D:DF:56 (Oracle VirtualBox virtual NIC)
Device type: general purpose
Running: Linux 3.X|4.X
OS CPE: cpe:/o:linux:linux_kernel:3 cpe:/o:linux:linux_kernel:4
OS details: Linux 3.2 - 4.9
Network Distance: 1 hop
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE
HOP RTT     ADDRESS
1   0.31 ms 192.168.1.24

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 46.54 seconds
```
