# Active Recon Resources


---
---

# Active Reconnaissance
***To gather intelligence by actively engaging the target.***


In the active reconnaissance phase, we're planning our future phases, like exploitation, by actively collecting information on the target by enumeration, scanning, etc.

Few examples:  
- What targets were found and what ports are open?  
- What software, versions, and configs are we up against?  
- Any sensitive data or services found through fuzzing or crawling?  
- Any hosts/services vulnerable to known exploits?  
- Enumerate users, groups, GPOs, policies, etc
- All while we continue to map the possible network topology.  

---
---

This is a list of tools which use active reconnaissance techniques(E.g., Scanning, Fingerprinting, Enumeration, etc) to gather information on the target.  
&nbsp;  
{{< admonition type=danger title="Exploit Warning!" open=true >}}
Many Active Reconnaissance tools are capable of Executing Exploits!
{{< /admonition>}}

<br>

Regarding my notes:
- The brackets ( ) after each tool will indicate if the tool is:
    1. (Built-in) = Within Kali's repo. If not already installed, run the following:
        
        ```
        sudo apt update && sudo apt install *tool-to-install*
        ```
    1. (External) = Outside Kali's repo. It'll need downloaded then installed.
    1. (Website) = Part of a website.
    1. There's others but they're self-explanatory.
- I'll also try specifying any restrictions I know of.
    1. API access needed.
    1. Paywalls.
    1. etc.

---
---

### Darkweb

1. <a href="https://github.com/s-rah/onionscan" target="_blank">OnionScan</a> - (External)
    * "OnionScan is a free and open source tool for investigating the Dark Web."
    * Scan details at "<a href="https://github.com/s-rah/onionscan/blob/master/doc/what-is-scanned-for.md" target="_blank">What is scanned for</a>".

---
---

### Domains

#### Probe automation

1. <a href="https://github.com/tomnomnom/httprobe" target="_blank">httprobe</a> (External)
    * "Take a list of domains and probe for working http and https servers."
    * Great for automating subdomain discovery prior to [gowitness](#website-screenshots).


#### Subdomains

1. <a href="https://github.com/owasp-amass/amass" target="_blank">Amass by OWASP</a> (Built-in)
    * Open-source for enumerating and discovering subdomains.
    * Active scanning, option `-active`, will attempt to gather TLS certificates, perform web crawling, DNS zone transfer, and NSEC(zone) walking.

---
---

### Fuzzing

#### AIO Fuzzing

1. <a href="https://github.com/ffuf/ffuf" target="_blank">ffuf</a> (Built-in)
    * Fuzzer written in Go.
    * Finds directory, files, V-Host, and GET and POST parameter fuzzing, etc.

1. <a href="https://github.com/OJ/gobuster" target="_blank">GoBuster</a> (Built-in)
    * Fuzzing tool written in Go.
    * Used for Directory/File, DNS, V-Host, open S3 and cloud buckets, and TFTP servers.

1. <a href="https://wfuzz.readthedocs.io/en/latest/" target="_blank">Wfuzz</a> (Built-in)
    * Anything web application fuzzer. E.g., RCE, VHost, etc.
    * Replaces FUZZ reference with specified payload.

#### Web Path Fuzzing

1. <a href="https://github.com/KajanM/DirBuster" target="_blank">DirBuster</a> (Built-in)
    * Multithread GUI/CLI Java app for fuzzing webapp files and directories.

1. <a href="https://github.com/maurosoria/dirsearch" target="_blank">dirsearch</a> (Built-in)
    * An advanced web path brute-forcer for fuzzing directories and files.

1. <a href="https://github.com/epi052/feroxbuster" target="_blank">FeroxBuster</a> (Built-in)
    * "Forced Browsing" rust tool used for enumerating directories and files.


#### Web Object Fuzzing

1. <a href="https://dirb.sourceforge.net/" target="_blank">DIRB</a> (Built-in)
    * Web-Object fuzzer.

---
---

### Scanners

#### Network Scanners

1. <a href="https://nmap.org/book/man.html" target="_blank">Nmap</a> (Built-in)
    * The "goto" network and port scanner with many capabilities beyond scanning, e.g., built-in scripts for vulnerability testing, etc.

#### CMS Scanners

1. <a href="https://github.com/Dionach/CMSmap" target="_blank">CMSmap</a> (External)
    * CMSmap is a python open source CMS scanner that automates the process of detecting security flaws of the most popular CMSs.

1. <a href="https://github.com/wpscanteam/wpscan" target="_blank">WPScan</a> (Built-in)
    * WPScan WordPress security scanner. Written for security professionals and blog maintainers to test the security of their WordPress websites.

1. <a href="https://github.com/OWASP/joomscan" target="_blank">joomscan by OWASP</a> (Built-in)
    * OWASP Joomla Vulnerability Scanner Project.


#### Web Scanners

1. <a href="https://www.tenable.com/downloads/nessus" target="_blank">Nessus</a> (External) - <span style="color:#0b888a">Account creation required. Free for home use but limited to 15 hosts.</span>
    * Proprietary vulnerability scanner by Tenable.
    * Has many additional scanning options like specialized scans, web app scans, etc.

1. <a href="https://github.com/sullo/nikto" target="_blank">nikto</a> (Built-in)
    * Web server vulnerability scanner in perl.

1. <a href="https://openvas.org/" target="_blank">OpenVAS</a> (Built-in) - <span style="color:#0b888a">Account creation required.</span>
    * Commercial and CE editions
    * Component of the Greenbone Vulnerability Management suite.


1. <a href="https://github.com/1N3/Sn1per" target="_blank">Sn1per</a> (External) - <span style="color:#0b888a">Exploitation features tied to premium. API integration available!</span>
    * Open source recon and penetration testing framework.
    * Premium and CE versions available.


#### SNMP Scanners

1. <a href="https://github.com/trailofbits/onesixtyone" target="_blank">onesixtyone</a> (Built-in)
    * SNMP scanner which logs the software running on a device.

#### Specialized Scanners

1. <a href="https://github.com/fullhunt/log4j-scan" target="_blank">log4j-scan</a> (External)
    * A fully automated, accurate, and extensive scanner for finding log4j RCE CVE-2021-44228.
    * Supports lists of URLs, 60+ HTTP headers, Bypass payloads for WAFs(Web Application Firewall), etc.

1. <a href="https://github.com/byt3bl33d3r/ItWasAllADream" target="_blank">ItWasAllADream</a> (External)
    * CVE-2021-34527 (PrintNightmare) RCE python scanner.
    * Scan entire subnets for PrintNightmare RCE(Remote code execution) and export CVS report.
    * Does NOT apply to LPE(Local privilege escalation)! Only RCE!

---
---

### Web *

#### Web App Firewall

1. <a href="https://github.com/EnableSecurity/wafw00f" target="_blank">WAFW00F</a> (Built-in)
    * Identify and fingerprint Web Application Firewall (WAF) products protecting a website.

#### Web App Proxy

1. <a href="https://portswigger.net/burp" target="_blank">BurpSuite</a> (Built-in) - <span style="color:#0b888a">Free version has rate limited brute-forcing. Paid version has many features.</span>
    * AIO web app security testing.
    * Free community extensions can help improve the free version.

1. <a href="https://www.zaproxy.org/" target="_blank">Zed Attack Proxy (ZAP)</a> (Built-in)
    * Free and open-source web app scanner.
    * No limit on brute-force attempts.

1. <a href="https://getfoxyproxy.org/downloads/" target="_blank">Foxy Proxy</a> (Browser Extension)
    * Browser proxy used with ZAP and Burp.

#### Web TechStack

1. <a href="https://www.wappalyzer.com/" target="_blank">Wappalyzer</a> - (Browser Extension)
    * Actively interacts with a website, when browsing to it, to find website's tech stack in realtime.

1. <a href="https://github.com/urbanadventurer/WhatWeb" target="_blank">WhatWeb</a> (Built-in)
    * Default scan uses HTTP requests to identify website's tech stack.
    * Aggression is adjustable.

#### Website Screenshots

1. <a href="https://github.com/sensepost/gowitness" target="_blank">gowitness</a> (External) - <span style="color:#0b888a">Requires chromium to be installed.</span>
    * "gowitness - a golang, web screenshot utility using Chrome Headless."
    * Great for automating external pentests by removing the manual process of visiting each found website.

---
---

### Wireless

1. <a href="https://github.com/aircrack-ng/aircrack-ng" target="_blank">aircrack-ng</a> - (Built-in)
    * AIO wireless security suite.
    * Contains both passive and active recon tools, along with many exploitation tools.

---

> Author: revsh3ll  
> URL: https://PivotTheNet.GitHub.io/active-recon/  

