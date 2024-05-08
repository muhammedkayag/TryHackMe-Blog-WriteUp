![](pics/b2.png)



[Link to room on TryHackMe.com](https://tryhackme.com/room/blog)

Welcome to my TryHacMe-Blog-WriteUp! first we add machines ip adress on our /etc/hosts file as blog.thm: 



```
echo "10.10.153.19 blog.thm" >> /etc/hosts
```



after that we start enumeration with rustscan and nmap:



```
┌─[✗]─[root@parrot]─[/home/parrot]
└──╼ #rustscan -a blog.thm
.----. .-. .-. .----..---.  .----. .---.   .--.  .-. .-.
| {}  }| { } |{ {__ {_   _}{ {__  /  ___} / {} \ |  `| |
| .-. \| {_} |.-._} } | |  .-._} }\     }/  /\  \| |\  |
`-' `-'`-----'`----'  `-'  `----'  `---' `-'  `-'`-' `-'
The Modern Day Port Scanner.
________________________________________
: http://discord.skerritt.blog         :
: https://github.com/RustScan/RustScan :
 --------------------------------------
You miss 100% of the ports you don't scan. - RustScan

[~] The config file is expected to be at "/root/.rustscan.toml"
[!] File limit is lower than default batch size. Consider upping with --ulimit. May cause harm to sensitive servers
[!] Your file limit is very small, which negatively impacts RustScan's speed. Use the Docker image, or up the Ulimit with '--ulimit 5000'. 
Open 10.10.153.19:22
Open 10.10.153.19:80
[~] Starting Script(s)
[~] Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-05-07 17:36 +03
Initiating Ping Scan at 17:36
Scanning 10.10.153.19 [4 ports]
Completed Ping Scan at 17:36, 0.37s elapsed (1 total hosts)
Initiating SYN Stealth Scan at 17:36
Scanning blog.thm (10.10.153.19) [2 ports]
Discovered open port 80/tcp on 10.10.153.19
Discovered open port 22/tcp on 10.10.153.19
Completed SYN Stealth Scan at 17:36, 0.41s elapsed (2 total ports)
Nmap scan report for blog.thm (10.10.153.19)
Host is up, received reset ttl 60 (0.35s latency).
Scanned at 2024-05-07 17:36:34 +03 for 0s

PORT   STATE SERVICE REASON
22/tcp open  ssh     syn-ack ttl 60
80/tcp open  http    syn-ack ttl 60

Read data files from: /usr/bin/../share/nmap
Nmap done: 1 IP address (1 host up) scanned in 0.87 seconds
           Raw packets sent: 6 (240B) | Rcvd: 3 (128B)
```

```
┌─[root@parrot]─[/home/parrot]
└──╼ #nmap -sC -sV -A -Pn blog.thm -p 22,80
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-05-07 17:38 +03
Nmap scan report for blog.thm (10.10.153.19)
Host is up (0.36s latency).

PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 57:8a:da:90:ba:ed:3a:47:0c:05:a3:f7:a8:0a:8d:78 (RSA)
|   256 c2:64:ef:ab:b1:9a:1c:87:58:7c:4b:d5:0f:20:46:26 (ECDSA)
|_  256 5a:f2:62:92:11:8e:ad:8a:9b:23:82:2d:ad:53:bc:16 (ED25519)
80/tcp open  http    Apache httpd 2.4.29 ((Ubuntu))
|_http-server-header: Apache/2.4.29 (Ubuntu)
| http-robots.txt: 1 disallowed entry 
|_/wp-admin/
|_http-title: Billy Joel&#039;s IT Blog &#8211; The IT blog
|_http-generator: WordPress 5.0
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Aggressive OS guesses: Linux 3.1 (95%), Linux 3.2 (95%), AXIS 210A or 211 Network Camera (Linux 2.6.17) (95%), ASUS RT-N56U WAP (Linux 3.4) (93%), Linux 3.16 (93%), Linux 2.6.32 (93%), Linux 2.6.39 - 3.2 (93%), Linux 3.1 - 3.2 (93%), Linux 3.2 - 4.9 (93%), Linux 3.7 - 3.10 (93%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 5 hops
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE (using port 22/tcp)
HOP RTT       ADDRESS
1   232.47 ms 10.17.0.1
2   ... 4
5   354.48 ms blog.thm (10.10.153.19)

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 43.92 seconds
```
