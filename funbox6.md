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
```

### GOBUSTER

```console
noob2uub@kali:~/Documents/vulnhub/funbox6$ gobuster dir -u http://192.168.1.114 -w /home/noob2uub/Documents/Wordlists/big.txt 
===============================================================
Gobuster v3.1.0
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://192.168.1.114
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /home/noob2uub/Documents/Wordlists/big.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.1.0
[+] Timeout:                 10s
===============================================================
2022/04/22 15:55:20 Starting gobuster in directory enumeration mode
===============================================================
/.htaccess            (Status: 403) [Size: 278]
/.htpasswd            (Status: 403) [Size: 278]
/server-status        (Status: 403) [Size: 278]
/wp-admin             (Status: 301) [Size: 317] [--> http://192.168.1.114/wp-admin/]
/wp-content           (Status: 301) [Size: 319] [--> http://192.168.1.114/wp-content/]
/wp-includes          (Status: 301) [Size: 320] [--> http://192.168.1.114/wp-includes/]
                                                                                       
===============================================================
2022/04/22 15:55:22 Finished
===============================================================
```

we have a wordpress site, lets take a look and run a WPSCAN

### WPSCAN

```console
noob2uub@kali:~/Documents/vulnhub/funbox6$ wpscan --url http://funbox6.box/
_______________________________________________________________
         __          _______   _____
         \ \        / /  __ \ / ____|
          \ \  /\  / /| |__) | (___   ___  __ _ _ __ ®
           \ \/  \/ / |  ___/ \___ \ / __|/ _` | '_ \
            \  /\  /  | |     ____) | (__| (_| | | | |
             \/  \/   |_|    |_____/ \___|\__,_|_| |_|

         WordPress Security Scanner by the WPScan Team
                         Version 3.8.22
       Sponsored by Automattic - https://automattic.com/
       @_WPScan_, @ethicalhack3r, @erwan_lr, @firefart
_______________________________________________________________

[+] URL: http://funbox6.box/ [192.168.1.114]
[+] Started: Fri Apr 22 15:56:49 2022

Interesting Finding(s):

[+] Headers
 | Interesting Entry: Server: Apache/2.4.18 (Ubuntu)
 | Found By: Headers (Passive Detection)
 | Confidence: 100%

[+] XML-RPC seems to be enabled: http://funbox6.box/xmlrpc.php
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 100%
 | References:
 |  - http://codex.wordpress.org/XML-RPC_Pingback_API
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_ghost_scanner/
 |  - https://www.rapid7.com/db/modules/auxiliary/dos/http/wordpress_xmlrpc_dos/
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_xmlrpc_login/
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_pingback_access/

[+] WordPress readme found: http://funbox6.box/readme.html
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 100%

[+] Upload directory has listing enabled: http://funbox6.box/wp-content/uploads/
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 100%

[+] The external WP-Cron seems to be enabled: http://funbox6.box/wp-cron.php
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 60%
 | References:
 |  - https://www.iplocation.net/defend-wordpress-from-ddos
 |  - https://github.com/wpscanteam/wpscan/issues/1299

[+] WordPress version 5.5.1 identified (Insecure, released on 2020-09-01).
 | Found By: Rss Generator (Passive Detection)
 |  - http://funbox6.box/index.php/feed/, <generator>https://wordpress.org/?v=5.5.1</generator>
 |  - http://funbox6.box/index.php/comments/feed/, <generator>https://wordpress.org/?v=5.5.1</generator>

[+] WordPress theme in use: twentyseventeen
 | Location: http://funbox6.box/wp-content/themes/twentyseventeen/
 | Last Updated: 2022-01-25T00:00:00.000Z
 | Readme: http://funbox6.box/wp-content/themes/twentyseventeen/readme.txt
 | [!] The version is out of date, the latest version is 2.9
 | Style URL: http://funbox6.box/wp-content/themes/twentyseventeen/style.css?ver=20190507
 | Style Name: Twenty Seventeen
 | Style URI: https://wordpress.org/themes/twentyseventeen/
 | Description: Twenty Seventeen brings your site to life with header video and immersive featured images. With a fo...
 | Author: the WordPress team
 | Author URI: https://wordpress.org/
 |
 | Found By: Css Style In Homepage (Passive Detection)
 |
 | Version: 2.4 (80% confidence)
 | Found By: Style (Passive Detection)
 |  - http://funbox6.box/wp-content/themes/twentyseventeen/style.css?ver=20190507, Match: 'Version: 2.4'

[+] Enumerating All Plugins (via Passive Methods)

[i] No plugins Found.

[+] Enumerating Config Backups (via Passive and Aggressive Methods)
 Checking Config Backups - Time: 00:00:00 <==========================================================================================================================> (137 / 137) 100.00% Time: 00:00:00

[i] No Config Backups Found.

[!] No WPScan API Token given, as a result vulnerability data has not been output.
[!] You can get a free API token with 25 daily requests by registering at https://wpscan.com/register

[+] Finished: Fri Apr 22 15:56:53 2022
[+] Requests Done: 170
[+] Cached Requests: 5
[+] Data Sent: 41.664 KB
[+] Data Received: 390.085 KB
[+] Memory used: 227.137 MB
[+] Elapsed time: 00:00:04
```

Didn't realize that I need an API key now. 

```console
noob2uub@kali:~/Documents/vulnhub/funbox6$ wpscan --url http://funbox6.box/ --api-token 90UfmPS3wvsRwDOJiEbQXZAuPW5QH3WVBNSGos85HR8
_______________________________________________________________
         __          _______   _____
         \ \        / /  __ \ / ____|
          \ \  /\  / /| |__) | (___   ___  __ _ _ __ ®
           \ \/  \/ / |  ___/ \___ \ / __|/ _` | '_ \
            \  /\  /  | |     ____) | (__| (_| | | | |
             \/  \/   |_|    |_____/ \___|\__,_|_| |_|

         WordPress Security Scanner by the WPScan Team
                         Version 3.8.22
       Sponsored by Automattic - https://automattic.com/
       @_WPScan_, @ethicalhack3r, @erwan_lr, @firefart
_______________________________________________________________

[+] URL: http://funbox6.box/ [192.168.1.114]
[+] Started: Fri Apr 22 16:06:07 2022

Interesting Finding(s):

[+] Headers
 | Interesting Entry: Server: Apache/2.4.18 (Ubuntu)
 | Found By: Headers (Passive Detection)
 | Confidence: 100%

[+] XML-RPC seems to be enabled: http://funbox6.box/xmlrpc.php
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 100%
 | References:
 |  - http://codex.wordpress.org/XML-RPC_Pingback_API
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_ghost_scanner/
 |  - https://www.rapid7.com/db/modules/auxiliary/dos/http/wordpress_xmlrpc_dos/
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_xmlrpc_login/
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_pingback_access/

[+] WordPress readme found: http://funbox6.box/readme.html
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 100%

[+] Upload directory has listing enabled: http://funbox6.box/wp-content/uploads/
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 100%

[+] The external WP-Cron seems to be enabled: http://funbox6.box/wp-cron.php
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 60%
 | References:
 |  - https://www.iplocation.net/defend-wordpress-from-ddos
 |  - https://github.com/wpscanteam/wpscan/issues/1299

[+] WordPress version 5.5.1 identified (Insecure, released on 2020-09-01).
 | Found By: Rss Generator (Passive Detection)
 |  - http://funbox6.box/index.php/feed/, <generator>https://wordpress.org/?v=5.5.1</generator>
 |  - http://funbox6.box/index.php/comments/feed/, <generator>https://wordpress.org/?v=5.5.1</generator>
 |
 | [!] 20 vulnerabilities identified:
 |
 | [!] Title: WordPress < 5.5.2 - Hardening Deserialization Requests
 |     Fixed in: 5.5.2
 |     References:
 |      - https://wpscan.com/vulnerability/f2bd06cf-f4e9-4077-90b0-fba80c3d0969
 |      - https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-28032
 |      - https://wordpress.org/news/2020/10/wordpress-5-5-2-security-and-maintenance-release/
 |      - https://github.com/WordPress/wordpress-develop/commit/add6bedf3a53b647d0ebda2970057912d3cd79d3
 |      - https://blog.wpscan.com/2020/10/30/wordpress-5.5.2-security-release.html
 |      - https://github.com/WordPress/Requests/security/advisories/GHSA-52qp-jpq7-6c54
 |
 | [!] Title: WordPress < 5.5.2 - Disable Spam Embeds from Disabled Sites on a Multisite Network
 |     Fixed in: 5.5.2
 |     References:
 |      - https://wpscan.com/vulnerability/a1941f4f-6adb-41e9-b47f-6eddd6f6a04a
 |      - https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-28033
 |      - https://wordpress.org/news/2020/10/wordpress-5-5-2-security-and-maintenance-release/
 |      - https://blog.wpscan.com/2020/10/30/wordpress-5.5.2-security-release.html
 |
 | [!] Title: WordPress < 5.5.2 - Cross-Site Scripting (XSS) via Global Variables
 |     Fixed in: 5.5.2
 |     References:
 |      - https://wpscan.com/vulnerability/336deb2e-5286-422d-9aa2-6898877d55a9
 |      - https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-28034
 |      - https://wordpress.org/news/2020/10/wordpress-5-5-2-security-and-maintenance-release/
 |      - https://blog.wpscan.com/2020/10/30/wordpress-5.5.2-security-release.html
 |
 | [!] Title: WordPress < 5.5.2 - XML-RPC Privilege Escalation
 |     Fixed in: 5.5.2
 |     References:
 |      - https://wpscan.com/vulnerability/76a05ec0-08f3-459f-8379-3b4865a0813f
 |      - https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-28035
 |      - https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-28036
 |      - https://wordpress.org/news/2020/10/wordpress-5-5-2-security-and-maintenance-release/
 |      - https://github.com/WordPress/wordpress-develop/commit/c9e6b98968025b1629015998d12c3102165a7d32
 |      - https://blog.wpscan.com/2020/10/30/wordpress-5.5.2-security-release.html
 |
 | [!] Title: WordPress < 5.5.2 - Unauthenticated DoS Attack to RCE
 |     Fixed in: 5.5.2
 |     References:
 |      - https://wpscan.com/vulnerability/016774df-5031-4315-a893-a47d99273883
 |      - https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-28037
 |      - https://wordpress.org/news/2020/10/wordpress-5-5-2-security-and-maintenance-release/
 |      - https://github.com/WordPress/wordpress-develop/commit/2ca15d1e5ce70493c5c0c096ca0c76503d6da07c
 |      - https://blog.wpscan.com/2020/10/30/wordpress-5.5.2-security-release.html
 |      - https://threatpost.com/wordpress-patches-rce-bug/160812/
 |
 | [!] Title: WordPress < 5.5.2 - Stored XSS in Post Slugs
 |     Fixed in: 5.5.2
 |     References:
 |      - https://wpscan.com/vulnerability/990cf4ff-0084-4a5c-8fdb-db374ffcb5df
 |      - https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-28038
 |      - https://wordpress.org/news/2020/10/wordpress-5-5-2-security-and-maintenance-release/
 |      - https://blog.wpscan.com/2020/10/30/wordpress-5.5.2-security-release.html
 |
 | [!] Title: WordPress < 5.5.2 - Protected Meta That Could Lead to Arbitrary File Deletion
 |     Fixed in: 5.5.2
 |     References:
 |      - https://wpscan.com/vulnerability/30662254-5a8d-40d0-8a31-eb58b51b3c33
 |      - https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-28039
 |      - https://wordpress.org/news/2020/10/wordpress-5-5-2-security-and-maintenance-release/
 |      - https://github.com/WordPress/wordpress-develop/commit/d5ddd6d4be1bc9fd16b7796842e6fb26315705ad
 |      - https://blog.wpscan.com/2020/10/30/wordpress-5.5.2-security-release.html
 |
 | [!] Title: WordPress < 5.5.2 - Cross-Site Request Forgery (CSRF) to Change Theme Background
 |     Fixed in: 5.5.2
 |     References:
 |      - https://wpscan.com/vulnerability/ebd354db-ab63-4644-891c-4a200e9eef7e
 |      - https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-28040
 |      - https://wordpress.org/news/2020/10/wordpress-5-5-2-security-and-maintenance-release/
 |      - https://github.com/WordPress/wordpress-develop/commit/cbcc595974d5aaa025ca55625bf68ef286bd8b41
 |      - https://blog.wpscan.com/wordpress-5-5-2-security-release/
 |      - https://hackerone.com/reports/881855
 |
 | [!] Title: WordPress 4.7-5.7 - Authenticated Password Protected Pages Exposure
 |     Fixed in: 5.5.4
 |     References:
 |      - https://wpscan.com/vulnerability/6a3ec618-c79e-4b9c-9020-86b157458ac5
 |      - https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-29450
 |      - https://wordpress.org/news/2021/04/wordpress-5-7-1-security-and-maintenance-release/
 |      - https://blog.wpscan.com/2021/04/15/wordpress-571-security-vulnerability-release.html
 |      - https://github.com/WordPress/wordpress-develop/security/advisories/GHSA-pmmh-2f36-wvhq
 |      - https://core.trac.wordpress.org/changeset/50717/
 |      - https://www.youtube.com/watch?v=J2GXmxAdNWs
 |
 | [!] Title: WordPress 3.7 to 5.7.1 - Object Injection in PHPMailer
 |     Fixed in: 5.5.5
 |     References:
 |      - https://wpscan.com/vulnerability/4cd46653-4470-40ff-8aac-318bee2f998d
 |      - https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-36326
 |      - https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2018-19296
 |      - https://github.com/WordPress/WordPress/commit/267061c9595fedd321582d14c21ec9e7da2dcf62
 |      - https://wordpress.org/news/2021/05/wordpress-5-7-2-security-release/
 |      - https://github.com/PHPMailer/PHPMailer/commit/e2e07a355ee8ff36aba21d0242c5950c56e4c6f9
 |      - https://www.wordfence.com/blog/2021/05/wordpress-5-7-2-security-release-what-you-need-to-know/
 |      - https://www.youtube.com/watch?v=HaW15aMzBUM
 |
 | [!] Title: WordPress 5.4 to 5.8 -  Lodash Library Update
 |     Fixed in: 5.5.6
 |     References:
 |      - https://wpscan.com/vulnerability/5d6789db-e320-494b-81bb-e678674f4199
 |      - https://wordpress.org/news/2021/09/wordpress-5-8-1-security-and-maintenance-release/
 |      - https://github.com/lodash/lodash/wiki/Changelog
 |      - https://github.com/WordPress/wordpress-develop/commit/fb7ecd92acef6c813c1fde6d9d24a21e02340689
 |
 | [!] Title: WordPress 5.4 to 5.8 - Authenticated XSS in Block Editor
 |     Fixed in: 5.5.6
 |     References:
 |      - https://wpscan.com/vulnerability/5b754676-20f5-4478-8fd3-6bc383145811
 |      - https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-39201
 |      - https://wordpress.org/news/2021/09/wordpress-5-8-1-security-and-maintenance-release/
 |      - https://github.com/WordPress/wordpress-develop/security/advisories/GHSA-wh69-25hr-h94v
 |
 | [!] Title: WordPress 5.4 to 5.8 - Data Exposure via REST API
 |     Fixed in: 5.5.6
 |     References:
 |      - https://wpscan.com/vulnerability/38dd7e87-9a22-48e2-bab1-dc79448ecdfb
 |      - https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-39200
 |      - https://wordpress.org/news/2021/09/wordpress-5-8-1-security-and-maintenance-release/
 |      - https://github.com/WordPress/wordpress-develop/commit/ca4765c62c65acb732b574a6761bf5fd84595706
 |      - https://github.com/WordPress/wordpress-develop/security/advisories/GHSA-m9hc-7v5q-x8q5
 |
 | [!] Title: WordPress < 5.8.2 - Expired DST Root CA X3 Certificate
 |     Fixed in: 5.5.7
 |     References:
 |      - https://wpscan.com/vulnerability/cc23344a-5c91-414a-91e3-c46db614da8d
 |      - https://wordpress.org/news/2021/11/wordpress-5-8-2-security-and-maintenance-release/
 |      - https://core.trac.wordpress.org/ticket/54207
 |
 | [!] Title: WordPress < 5.8 - Plugin Confusion
 |     Fixed in: 5.8
 |     References:
 |      - https://wpscan.com/vulnerability/95e01006-84e4-4e95-b5d7-68ea7b5aa1a8
 |      - https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-44223
 |      - https://vavkamil.cz/2021/11/25/wordpress-plugin-confusion-update-can-get-you-pwned/
 |
 | [!] Title: WordPress < 5.8.3 - SQL Injection via WP_Query
 |     Fixed in: 5.5.8
 |     References:
 |      - https://wpscan.com/vulnerability/7f768bcf-ed33-4b22-b432-d1e7f95c1317
 |      - https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-21661
 |      - https://github.com/WordPress/wordpress-develop/security/advisories/GHSA-6676-cqfm-gw84
 |      - https://hackerone.com/reports/1378209
 |
 | [!] Title: WordPress < 5.8.3 - Author+ Stored XSS via Post Slugs
 |     Fixed in: 5.5.8
 |     References:
 |      - https://wpscan.com/vulnerability/dc6f04c2-7bf2-4a07-92b5-dd197e4d94c8
 |      - https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-21662
 |      - https://github.com/WordPress/wordpress-develop/security/advisories/GHSA-699q-3hj9-889w
 |      - https://hackerone.com/reports/425342
 |      - https://blog.sonarsource.com/wordpress-stored-xss-vulnerability
 |
 | [!] Title: WordPress 4.1-5.8.2 - SQL Injection via WP_Meta_Query
 |     Fixed in: 5.5.8
 |     References:
 |      - https://wpscan.com/vulnerability/24462ac4-7959-4575-97aa-a6dcceeae722
 |      - https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-21664
 |      - https://github.com/WordPress/wordpress-develop/security/advisories/GHSA-jp3p-gw8h-6x86
 |
 | [!] Title: WordPress < 5.8.3 - Super Admin Object Injection in Multisites
 |     Fixed in: 5.5.8
 |     References:
 |      - https://wpscan.com/vulnerability/008c21ab-3d7e-4d97-b6c3-db9d83f390a7
 |      - https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-21663
 |      - https://github.com/WordPress/wordpress-develop/security/advisories/GHSA-jmmq-m8p8-332h
 |      - https://hackerone.com/reports/541469
 |
 | [!] Title: WordPress < 5.9.2 - Prototype Pollution in jQuery
 |     Fixed in: 5.5.9
 |     References:
 |      - https://wpscan.com/vulnerability/1ac912c1-5e29-41ac-8f76-a062de254c09
 |      - https://wordpress.org/news/2022/03/wordpress-5-9-2-security-maintenance-release/

[+] WordPress theme in use: twentyseventeen
 | Location: http://funbox6.box/wp-content/themes/twentyseventeen/
 | Last Updated: 2022-01-25T00:00:00.000Z
 | Readme: http://funbox6.box/wp-content/themes/twentyseventeen/readme.txt
 | [!] The version is out of date, the latest version is 2.9
 | Style URL: http://funbox6.box/wp-content/themes/twentyseventeen/style.css?ver=20190507
 | Style Name: Twenty Seventeen
 | Style URI: https://wordpress.org/themes/twentyseventeen/
 | Description: Twenty Seventeen brings your site to life with header video and immersive featured images. With a fo...
 | Author: the WordPress team
 | Author URI: https://wordpress.org/
 |
 | Found By: Css Style In Homepage (Passive Detection)
 |
 | Version: 2.4 (80% confidence)
 | Found By: Style (Passive Detection)
 |  - http://funbox6.box/wp-content/themes/twentyseventeen/style.css?ver=20190507, Match: 'Version: 2.4'

[+] Enumerating All Plugins (via Passive Methods)

[i] No plugins Found.

[+] Enumerating Config Backups (via Passive and Aggressive Methods)
 Checking Config Backups - Time: 00:00:00 <==========================================================================================================================> (137 / 137) 100.00% Time: 00:00:00

[i] No Config Backups Found.

[+] WPScan DB API OK
 | Plan: free
 | Requests Done (during the scan): 2
 | Requests Remaining: 23

[+] Finished: Fri Apr 22 16:06:10 2022
[+] Requests Done: 143
[+] Cached Requests: 36
[+] Data Sent: 35.27 KB
[+] Data Received: 35.358 KB
[+] Memory used: 206.969 MB
[+] Elapsed time: 00:00:03
```


### WP-Includes

![Screenshot_2022-04-22_15-57-45](https://user-images.githubusercontent.com/68706090/164815153-1b5746f8-2b73-41ad-83e6-c418c9787fe2.png)

Clicking around for a decase and I noticed that its running some type of cronjob that changes that page every so often so THIS WAS ANNOYING!!!!

When it was open you can go into the blog and then click the date and it brings you to the first flag. 

![Screenshot_2022-04-22_16-34-09](https://user-images.githubusercontent.com/68706090/164817288-ebc41335-e83c-4f74-abff-54e75e7e9407.png)

![Screenshot_2022-04-22_16-34-00](https://user-images.githubusercontent.com/68706090/164817304-50a52922-02fe-488b-af41-5bd24e68d010.png)

Flag: flag{MFSG22LOHJTWC3LCNRSWQYLMNQ3TONY=}

This is a base32 and the results are: 

admin:gamblehall777

VERY ANNOYING YOU HAVE TO WAIT EVEN TO LOGIN!!!

![Screenshot_2022-04-22_17-04-24](https://user-images.githubusercontent.com/68706090/164836339-636cec40-84cd-46aa-8a06-5d104a2cc326.png)

Sooooo yeah I got logged in and the cron job shifted over, so i had to wait another 5 min or so and I was able to check plugins but couldnt find out where to access them. Then once I got in, I checked out themes and I was able to load a reverse shell. 

![Screenshot_2022-04-22_17-04-40](https://user-images.githubusercontent.com/68706090/164836400-ececb970-34c9-44e9-80ff-6a1a629591c7.png)

I did not bother stabolizing my shell because I knew I would get kicked out fast

```console
uid=33(www-data) gid=33(www-data) groups=33(www-data),27(sudo),100(users)
/bin/sh: 0: can't access tty; job control turned off
$ whoami
www-data
$ sudo -l
Matching Defaults entries for www-data on funbox6:
    env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User www-data may run the following commands on funbox6:
    (root) NOPASSWD: ALL
$ sudo su
whoami
root
ls
bin
boot
dev
etc
hint.txt
home
initrd.img
initrd.img.old
lib
lib64
lost+found
media
mnt
opt
proc
root
run
sbin
snap
srv
sys
tmp
usr
var
vmlinuz
vmlinuz.old
cd root
ls
000-default.conf
001-default.conf
gamble.sh
root.flag
sudoers
sudoers2
cat root.flag 
 ___                 _                     
(  _`\              ( )                    
| (_(_)_   _   ___  | |_      _          _ 
|  _) ( ) ( )/' _ `\| '_`\  /'_`\ (`\/')(_)
| |   | (_) || ( ) || |_) )( (_) ) >  <  _ 
(_)   `\___/'(_) (_)(_,__/'`\___/'(_/\_)(_)
 ___                      _      _              _   _         _    _   
(  _`\                   ( )    (_ )           ( ) ( )       (_ ) (_ ) 
| ( (_)   _ _   ___ ___  | |_    | |    __     | |_| |   _ _  | |  | | 
| |___  /'_` )/' _ ` _ `\| '_`\  | |  /'__`\   |  _  | /'_` ) | |  | | 
| (_, )( (_| || ( ) ( ) || |_) ) | | (  ___/   | | | |( (_| | | |  | | 
(____/'`\__,_)(_) (_) (_)(_,__/'(___)`\____)   (_) (_)`\__,_)(___)(___)

Please, share this on twitter: @0815R2d2
```

