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
![DVWA Setup]()

## Objective

## Tools Used

## Scanning Methodology

## Importance

## Findings

## Lessons Learned
