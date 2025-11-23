# dvwa-web-enum-personal-project3

This is a personal project that demonstrates highlights critical flaws of target that lacks propper security measures through the process of web enumeration using a variety of tools which include ffuf, nmap, gobuster, and nikto. It gives insights on how different tools and wordlists yield different results and directories while elaborating on how an attacker can use these vulnerabilities to gain access.

## Overview 

In this personal project I will be going into depth regarding web enumeration in my homelab, a safe environment isolated from the internet to shed light on the importance of finding hidden directories. I used kali linux and an intentionally vulnerable webserver known as damn vulnerable web app (dvwa).  I use a number of tools inlcuding gobuster, nikto, nmap, and ffuf which are very essential for web enumeration to showcase how these hidden directories can contain crucial information about a webserver or website resulting in an attacker gaining access, recovering crucial information such as credentials and configurations, and ssh keys.

## MITRE ATT&CK Mapping

This project aligns the following MITRE ATT&CK techniques:

• TA0043 - Reconnaissance, identifying the victim's environment before attacking
• T1595 - Scanning the target to identify weaknesses, architecture, and attack surfaces
• T1595.001 - Scanning for Vulnerable or Exposed Web Directories (The main technique of this project)
• T1594 - Search Victim-Owned Websites

## Architecture

 I used only my Kali Machine which was set up on a NAT Network called "labnet". Labnet is completely isolated from the internet which makes it perfect for pentesting. I had 2 terminals open, 1 for the dvwa webserver which is running in a docker container, and another terminal used to scan dvwa. 
 
![DVWA Setup](dvwa-homelab-setup.png)
![Kali Settings](Kali.png)



## Objective
• Discover hidden directories within a webserver
• Highlight how hidden directories can contain useful information to gain access
• To build a portfolio of hands on pentesting projects as well as attacking methodlogies
•

## Tools Used
• nmap 
• ffuf
• gobuster
• nikto

## Scanning Methodology 
• ffuf -u http://(dvwa-ip)/FUZZ -w /usr/share/wordlists/dirb/common.txt -mc 200
![ffuf scan filtering only for 200 status codes](ffuf-mc200-scan.png)
• ffuf -u http://(dvwa-ip)/FUZZ -w /usr/share/wordlists/dirbuster/directory-list-2.3.txt
![ffuf regular scan](ffuf-regular-scan.png)
• gobuster dir -u http://(dvwa-ip) -w /usr/share/wordlists/dirb/common.txt 
![Regular gobutser scan](gobuster-scan.png)
• gobuster dir -u http://(dvwa-ip) -w /usr/share/wordlists/dirbuster/directory-list-2.3.txt
![Gobuster scan with the dirbuster wordlist](gobuster-dirbuster-scan.png)

• gobuster dir -u http://(dvwa-ip) -w /usr/share/wordlists/dirb/common.txt -x txt,php,js,asp,aspx,html,log,bak,conf,config,admin,old,login
![](gobuster-extension-scan.png)

• gobuster dir -u http://(dvwa-ip) -w /usr/share/wordlists/dirb/common.txt -x txt,php,js,asp,aspx,html,log,bak,conf,config,admin,old,login
![](gobuster-extension-scan2.png)

• gobuster dir -u http://(dvwa-ip) -w /usr/share/wordlists/dirb/common.txt -x txt,php,js,asp,aspx,html,log,bak,conf,config,admin,old,login -b 403, 404 -r 
![](gobuster-exclude403.png)

• gobuster dir -u http://(dvwa-ip) -w /usr/share/wordlists/dirb/common.txt -x txt,php,js,asp,aspx,html,log,bak,conf,config,admin,old,login
![](gobuster-extension-scan3.png)

• gobuster dir -u http://(dvwa-ip) -w /usr/share/wordlists/dirb/common.txt -r
![](.png)

• gobuster dir -u http://(dvwa-ip) -w /usr/share/wordlists/seclists/Web-Content/raft-large-directories -x txt,php,js,asp,aspx,html,log,bak,conf,config,admin,old,login
![](gobuster-Seclist-scan.png)

• nmap -p 80 --script http-enum (dvwa-ip)
• nmap -p 80 --script http-title (dvwa-ip)
![A scan against dvwa using nmaps http scripts](http-scripts.png)

• nmap -A -p 80 (dvwa-ip)
![Running an aggressive scan against dvwa](nmap-A-scan.png)

• nikto -h (dvwa-ip) -C all
![](nikto-scan1.png)
![Running a nikto scan to see if there's any difference in results](nikto-scan2.png)



## Importance

## Findings

## Lessons Learned
