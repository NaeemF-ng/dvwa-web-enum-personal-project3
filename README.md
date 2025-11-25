# dvwa-web-enum-personal-project3

### Table of Contents

[Overview](##Overview)
[MITRE ATT&CK Mapping](##MITRE-ATT&CK-Mapping)
[Objective](##Objective)
[Tools Used](##Tools-Used)
[Scanning Methodology / Wordlists used](##Scanning Methodology / Wordlists used)
[Importance](##Importance)
[Findings](##Findings)
[Lessons Learned](##Lessons Learned)


This is a personal project that demonstrates highlights critical flaws of target that lacks propper security measures through the process of web enumeration using a variety of tools which include ffuf, nmap, gobuster, and nikto. It gives insights on how different tools and wordlists yield different results and directories while elaborating on how an attacker can use these vulnerabilities to gain access.

## Overview 

In this personal project I will be going into depth regarding web enumeration in my homelab, a safe environment isolated from the internet. The main focus is to discover hidden directories, understand their purpose, and show how attackers build an initial foothold during a web application penetration test. 

This project demonstrates:

• Understanding of reconnaissance & enumeration, and pentesting skills
• Ability to use multiple enumeration tools
• Interpreting scan results and identifying exposed or unnecessary directories

## MITRE-ATT&CK-Mapping

This project aligns the following MITRE ATT&CK techniques:

• TA0043 - Reconnaissance, identifying the victim's environment before attacking
• T1595 - Scanning the target to identify weaknesses, architecture, and attack surfaces
• T1595.001 - Scanning for Vulnerable or Exposed Web Directories (The main technique of this project)
• T1594 - Search Victim-Owned Websites

## Architecture

• Attacker Machine: Kali Linux
• Target Machine: DVWA running in docker
• Network: Virtualbox NAT-Network (Labnet)
• DVWA Access: dvwa-ip (has been redacted as a security measure)

![Kali Settings](Kali.png)
![DVWA Setup](dvwa-homelab-setup.png)


## Objective
Discover hidden and sensitive directories on a vulnerable web application (DVWA) using common enumeration tools to replicate an attackers behavior.

Hidden directories may include:
• Backup files
• Developer notes
• Sensitive config files
• Old versions
• Upload directories
These can often leads to full compromise and information being leaked.

• To build a portfolio of hands on pentesting projects as well as attacking methodlogies

## Tools-Used
• nmap 
• ffuf
• gobuster
• nikto

## Scanning Methodology / Wordlists used
• ffuf -u http://(dvwa-ip)/FUZZ -w /usr/share/wordlists/dirb/common.txt -mc 200
![ffuf scan filtering only for 200 status codes](ffuf-mc200-scan.png)
• ffuf -u http://(dvwa-ip)/FUZZ -w /usr/share/wordlists/dirbuster/directory-list-2.3.txt
![ffuf regular scan](ffuf-regular-scan.png)
![ffuf regular scan](ffuf-regular-scan2.png)
• gobuster dir -u http://(dvwa-ip) -w /usr/share/wordlists/dirb/common.txt 
![Regular gobuster scan ](gobuster-scan.png)
• gobuster dir -u http://(dvwa-ip) -w /usr/share/wordlists/dirb/common.txt -r
![Regular gobuster scan and another one for redirects](gobuster-scanr2.png)


• gobuster dir -u http://(dvwa-ip) -w /usr/share/wordlists/dirbuster/directory-list-2.3.txt
![Gobuster scan with the dirbuster wordlist](gobuster-dirbuster-scan.png)

• gobuster dir -u http://(dvwa-ip) -w /usr/share/wordlists/dirb/common.txt -x txt,php,js,asp,aspx,html,log,bak,conf,config,admin,old,login
![Gobuster scan for extensions](gobuster-extension-scan.png)
![](gobuster-extension-scan2.png)
![](gobuster-extension-scan3.png)


• gobuster dir -u http://(dvwa-ip) -w /usr/share/wordlists/dirb/common.txt -x txt,php,js,asp,aspx,html,log,bak,conf,config,admin,old,login -b 403, 404 -r 
![](gobuster-exclude403.png)
![](gobuster-exclude403-2.png)


• gobuster dir -u http://(dvwa-ip) -w /usr/share/wordlists/seclists/Discovery/Web-Content/raft-large-directories -x txt,php,js,asp,aspx,html,log,bak,conf,config,admin,old,login
![](gobuster-Seclist-scan.png)
![](gobuster-Seclist-scan2.png)


• nmap -p 80 --script http-enum (dvwa-ip)
• nmap -p 80 --script http-title (dvwa-ip)
![A scan against dvwa using nmaps http scripts](http-scripts.png)

• nmap -A -p 80 (dvwa-ip)
![Running an aggressive scan against dvwa](nmap-A-scan.png)
• The title of the application was found

• nikto -h (dvwa-ip) -C all
![Running a nikto scan to see if there's any difference in results](nikto-scan1.png)
![](nikto-scan2.png)


## Importance

• Finding hidden directories is very important as they can contain crucial information about a webserver or website resulting in an attacker gaining access. Things that shouldn't be public rely within these directories such as admin portals, backup pages, config files, admin panels, and database configuration. 

• I wanted to highlight how important it is to use the multiple wordlists. As you'll see in the screenshots within my findings you'll see that I discover the same directories with default wordlists, but when I use one of the wordlists from seclists I discover a new listing, "COPYING.txt". This is so important because that new directory may just be an attack surface that allows you to gain access to the target
![](gobuster-Seclist-scan2-copy.png)
It lead to a liscensing page however, it won't always lead to this.
![](Copyingtxt.png)


## Findings

![](page-surf.png)
Here is the config page for dvwa, it contained a directory listing. I clicked on each php file and there wasn't anything in it.
![](page-surf2.png)
![](page-surf2findings.png)
I found the documentation for dvwa which goes into depth regarding how the webserver (architecture) is setup
![](page-surf3.png)
The nikto scan provided me with the "/" directory also knownn as the root directory which was an admin login page which isn't supposed to be accessible to the public, which is displayed in the next screenshot
![](page-surf3-findings.png)
I visited the robots.txt directory which is commonly targeted by attackers due to the fact that developers put sensitive paths within here, it also led me to the admin page
![](page-surf-4.png)
![](page-surf-4]54.png)



## Lessons Learned
• How to discover hidden directories within a vulnerable web server leading to potential attack surfaces
• Fuzzing with the ffuf tool 
• The importance of using different wordlists and how it affects what can be found
• Some directories can lead to critical vulnerabilities
• Why mitigation is so essential to prevent sensitive information from being leaked


