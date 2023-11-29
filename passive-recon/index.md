# Passive Recon Resources


---
---

## Passive Reconnaissance
***To gather intelligence without actively engaging the target.***



In the passive recon phase, we're planning our future steps by passively collecting information on the target by fingerprinting, using OSINT, etc.  

Few examples:  
- Any email formats found?  
- What names can we find related to the target?  
- Sensitive data found on social media? Badges, passwords, or software icons in pics?  
- Any exposed credentials in dumps? Repeat password patterns?  
- What's the business structure. Who holds the keys?  
- Any sensitive information in open website/domain records?  
- All while we continue to map the possible network topology.  

---
---

This is a list of tools which use passive reconnaissance techniques(E.g., OSINT, etc) to gather information on the target.

{{< admonition type=danger title="Warning!" open=true >}}
Some Passive Reconnaissance tools may Actively Engage the Target.
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

### AIO Tools

1. <a href="https://www.aware-online.com/en/osint-tools/" target="_blank">Aware Online</a> - (Website)
    * Resources, tutorials, etc.
    * Company based in Netherlands.

1. <a href="https://github.com/jivoi/awesome-osint" target="_blank">awesome osint</a> - (Website)
    * Awesome OSINT is a large collection of resources dedicated to anything OSINT.
    
1. <a href="https://www.hunch.ly/" target="_blank">Hunchly</a> - (Chrome Extension) - <span style="color:#0b888a"> Trial available</span>
    * Chrome extension for organizing your findings and exporting them. It can auto screenshot as you go.

1. <a href="https://inteltechniques.com/tools/index.html" target="_blank">IntelTechniques</a> - (Website)
    * Great resource for OSINT anything. Tools included.

1. <a href="https://intelx.io/tools" target="_blank">_IntelligenceX</a> - (Website) - <span style="color:#0b888a">Free account required.</span>
    * Tools which can be used for many different OSINT purposes.
    * Email format validation, DNS records, etc

1. <a href="https://www.maltego.com/" target="_blank">Maltego CE</a> - (Built-in) - <span style="color:#0b888a"> APIs aren't needed but can help widen your net.</span>
    * Great link analysis tool for the aggregated data it collects. Helps visualize paths of data points, etc.
    * <a href="https://www.youtube.com/watch?v=ceQhIBKFp2A&list=PLfRX-xJAc2yz6CjQVQuogJeCBoy8HbCOR" target="_blank">Maltego Essentials Youtube Playlist</a> - Youtube playlist for learning Maltego.

1. <a href="https://www.osintcombine.com/tools" target="_blank">OSINT Combine</a> - (Website)
    * AIO site that hosts many useful online tools.
    * E.g., Darkweb, socials, usernames, etc

1. <a href="https://osintframework.com/" target="_blank">OSINT Framework</a> - (Website)
    * Fun interactive site that can help you see the paths of OSINT but, honestly, I've never use it.

1. <a href="https://pentest-tools.com/" target="_blank">Pentest-Tools.com</a> - (Website) - <span style="color:#0b888a">Limited without subscription.</span>
    * Many limited use tools.
    * Access by clicking hamburger menu then Tools.

1. <a href="https://github.com/lanmaster53/recon-ng" target="_blank">recon-ng</a> - (Built-in)
    * "Open Source Intelligence gathering tool aimed at reducing the time spent harvesting information from open sources."
    * Great framework for OSINT gathering. It has a similar feeling to metasploit since it uses modules, "run", etc

---
---

### AIO VM

1. <a href="https://www.tracelabs.org/" target="_blank">Trace Labs Organization</a> - (External - VM VMware & VirtualBox)
    * "Trace Labs is a nonprofit organization whose mission is to accelerate the family reunification of missing persons while training members in the tradecraft of open source intelligence (OSINT)."
    * This VM was created for OSINT. Updated regularly. Privacy focused.
    * <a href="https://github.com/tracelabs/tlosint-vm" target="_blank">Trace Labs Github</a>.
    * <a href="https://github.com/tracelabs/tlosint-vm/releases" target="_blank">Latest Trace Labs OSINT VM</a>.

---
---

### Accounts(Usernames)

1. <a href="https://checkusernames.com/" target="_blank">CheckUserNames</a> - (Website)
    * Website that helps find where a username may be in use, or not in use.

1. <a href="https://github.com/mxrch/GHunt" target="_blank">GHunt</a> - (External & Website)
    * CLI script, and <a href="https://osint.industries/" target="_blank">online now</a>, which can help you dig into anything Google, including accounts.

1. <a href="https://www.idcrawl.com/username" target="_blank">iDCrawl</a> - (Website)
    * Search for usernames across different online platforms.

1. <a href="https://github.com/soxoj/maigret" target="_blank">Maigret</a> - (External)
    * Fork of Sherlock that creates a dossier of a person by username. 

1.  <a href="https://www.namecheckr.com/" target="_blank">NameChecker</a> - (Website)
    * Search for usernames across different online platforms.

1. <a href="https://namecheckup.com/" target="_blank">NameCheckUp</a> - (Website)
    * Search for usernames across different online platforms.

1. <a href="https://github.com/sherlock-project/sherlock" target="_blank">Sherlock</a> - (Built-in)
    * "Hunt down social media accounts by username across social networks"
    * Tool built-in to Kali which allows you to search many different social networks for a username.
    * <a href="https://sherlock-project.github.io/" target="_blank">Sherlock's Github Pages website</a>

1. <a href="https://whatsmyname.app/" target="_blank">WhatsMyName Web</a> - (Website)
    * A very thorough tool that searches the web for usernames and names.

---
---

### Breaches/Dumps

#### Dumps

1. <a href="http://magnet:?xt=urn:btih:7ffbcd8cee06aba2ce6561688cf68ce2addca0a3&dn=BreachCompilation&tr=udp%3A%2F%2Ftracker.openbittorrent.com%3A80&tr=udp%3A%2F%2Ftracker.leechers-paradise.org%3A6969&tr=udp%3A%2F%2Ftracker.coppersurfer.tk%3A6969&tr=udp%3A%2F%2Fglotorrents.pw%3A6969&tr=udp%3A%2F%2Ftracker.opentrackr.org%3A1337" target="_blank">1.4B Breach Compilation</a> - (Torrent Link)

1. <a href="magnet:?xt=urn:btih:JEQMEEFTBXT35RJ3GUTGXU7HP3HBU5P6&dn=rockyou2021.txt%20dictionary%20from%20kys234%20on%20RaidForums&tr=udp%3A%2F%2Ftracker.openbittorrent.com%3A6969%2Fannounce" target="_blank">Rockyou2021.txt - Collection of wordlists combined</a> - (Torrent Link)

1. <a href="https://psbdmp.ws/" target="_blank">psbdmp.ws</a> (Website) - <span style="color:#0b888a">API available.</span>
    * Biggest archive(database) of paste dumps.

#### Search Breaches/Dumps

1. <a href="https://search.0t.rocks/" target="_blank">search.0t.rocks</a> (Website)
    * 14B records to sift through.
    * Older DB.

1. <a href="https://dehashed.com/" target="_blank">DEHASHED</a> (Website & API) - <span style="color:#0b888a">No account required but limited. API available through subscription.</span>
    * Search dumps and chain emails, hashes, and passwords while looking for reuse across different accounts.

1. <a href="https://github.com/hmaverickadams/breach-parse" target="_blank">Breach Parse</a> - (External)
    * A tool for parsing breached passwords.
    * Works well with 1.4B Breach Compilation.

1. <a href="https://haveibeenpwned.com/" target="_blank">haveibeenpwned(HIBP)</a> (Website & API) - <span style="color:#0b888a">API available through subscription.</span>
    * The website allows you to search through a large updated database of data dumps for either emails or passwords. It's active and updated regularly.
    * API subscription available. You send API the first 5 characters of a hash and API responses with a list of hashes matching the sent prefix.

1. <a href="https://haveibeenzuckered.com/" target="_blank">Facebook Data Breach Checker</a> - (Website)
    * Searches through 533 million Facebook accounts for dumped phone number.
    * Uses k-anonymity to ensure privacy.

1. <a href="https://leakcheck.io/" target="_blank">LeakCheck</a> - (Website) - <span style="color:#0b888a"> Account required.</span>
    * Alternative to HIBP and dehashed.

1. <a href="https://snusbase.com/" target="_blank">SnusBase</a> - (Website) - <span style="color:#0b888a"> Account required.</span>
    * Indexes information from websites which had data breaches.

---
---

###  Bucket search engines

#### S3 bucket search
1. <a href="https://grayhatwarfare.com/" target="_blank">GrayHatWarfare</a> (Website) - <span style="color:#0b888a">Free = limited range. Registered = double free range. Premium = unlimited w/ full path search.</span>
    * S3 bucket search engine.

---
---

### Businesses

1. <a href="https://www.aihitdata.com/" target="_blank">AIHIT</a> - (Website) - <span style="color:#0b888a">Account creation and/or subscription may be needed.</span>
    * Company database aggregator.

1. <a href="https://www.bbb.org/" target="_blank">BBB</a> - (Website)
    * Local business search. Find phone numbers, addresses, names, and reviews/complaints.

1. <a href="https://www.bloomberg.com/markets" target="_blank">Bloomberg</a> - (Website) - <span style="color:#0b888a">Account creation and/or subscription may be needed.</span>
    * Find history and news on a company, including public finances.

1. <a href="https://opencorporates.com/" target="_blank">OpenCorporates</a> - (Website)
    * Largest legal-entity database holding copyleft Open Database License.

1. <a href="https://www.linkedin.com/" target="_blank">LinkedIn</a> - (Website)
    * Great place to find badge photos, employee lists, tech stack through job applications, etc.
    * Companies may not share sensitive information but employees do. :smile:

1. <a href="https://www.nerdydata.com/" target="_blank">NerdyData</a> - (Website)
    * Get a list of websites that use certain technologies, plus the company's tech spend data.

---
---

### Code Search

1. <a href="https://grep.app/" target="_blank">grep.app</a> - (Website)
    * Search across a half million git repos.
    * Great place to dig for leaked secrets, etc.

1. <a href="https://codefinder.org/" target="_blank">RepoSearch</a> - (Website)
    * Search for source code across SVN and Github repos.

1. <a href="https://publicwww.com/" target="_blank">PublicWWW</a> - (Website)
    * Search through a web page's HTML, JS, and CSS code.
    * Updated regularly.

1. <a href="https://searchcode.com/" target="_blank">SearchCode</a> - (Website)
    * Searches Bitbucket, CodePlex, Fedora Project, Gitlab, Github, Gitorious, Google Android source codes.

---
---

### Darkweb Search Engines

1. <a href="https://biznar.com" target="_blank">BizNar</a> - (Website)
    * Deep Web search engine.

1. <a href="https://github.com/alecmuffett/real-world-onion-sites#index" target="_blank">real-world-onion-sites</a> - (Website)
    * "This is a list of substantial, commercial-or-social-good mainstream websites which provide onion services."

---
---

### Domains

#### Domain AIO

1. <a href="https://github.com/tomnomnom/assetfinder" target="_blank">assetfinder</a> - (Built-in)
    * Domain and subdomain discovery using passive methods written in golang.

1. <a href="https://centralops.net/co/" target="_blank">CentralOps.net</a> - (Website)
    * Domain & network WHOIS, DNS records, service scan, traceroute, etc.

1. <a href="https://viewdns.info/" target="_blank">ViewDNS.info</a> - (Website)
    * Collection of domain level tools.

#### DNS & Records

1. <a href="https://dnsdumpster.com/" target="_blank">DNS Dumpster</a> - (Website)
    * DNS & Whois recon and research.

1. <a href="https://github.com/fwaeytens/dnsenum" target="_blank">dnsenum</a> (Built-in)
    * Multithreaded perl script that enumerates DNS information and non-contiguous IP blocks.

1. <a href="https://github.com/darkoperator/dnsrecon" target="_blank">DNSRecon</a> (Built-in)
    * Very flexible and effective DNS scanning and enumeration tool.
    * Ability to use external passive means along with local wordlist fuzzing techniques for discovery.

1. <a href="https://github.com/mschwager/fierce" target="_blank">Fierce</a> (Built-in)
    * A DNS reconnaissance tool for locating non-contiguous IP space.

#### Subdomains

1. <a href="https://github.com/owasp-amass" target="_blank">Amass by OWASP</a> - (Built-in)
    * Open-source CLI for enumerating and discovering subdomains.
    * Defaults to passive recon but active is an option.

1. <a href="https://crt.sh/" target="_blank">CRT.sh</a> - (Website)
    * Search digital certificates of subdomains.
    * Great subdomain tool!

1. <a href="https://dnslytics.com/reverse-ip" target="_blank">DNSlytics</a> - (Website)
    * Find domains sharing the same IP or subnet.

1. <a href="https://spyonweb.com/" target="_blank">SpyonWeb.com</a> - (Website)
    * Similar to DNSlytics above.

1. <a href="https://github.com/projectdiscovery/subfinder" target="_blank">Subfinder</a> - (Built-in)- <span style="color:#0b888a">Many API options but not required.</span>
    * Passive subdomain enumeration using golang.
    * Works really well even without APIs. 

1. <a href="https://github.com/aboul3la/Sublist3r" target="_blank">Sublist3r</a> - (Built-in)
    * Python tool for enumerating subdomains via OSINT.
    * Older but still useful in some situations.

#### Was it a Tor Relay

1. <a href="https://metrics.torproject.org/exonerator.html" target="_blank">Exonerator(Tor Project)</a> - (Website)
    * Search IP and/or date to find out if IP was used as Tor relay.

---
---

### Emails

1. <a href="https://clearbit.com/resources/tools/connect" target="_blank">ClearBit</a> (Chrome Extension) - <span style="color:#0b888a">Account required.</span>
    * Confirm and cross reference emails found.

1. <a href="https://dehashed.com/" target="_blank">DEHASHED</a> (Website & API) - <span style="color:#0b888a">No account required but limited. API requires subscription.</span>
    * Chain emails, hashes,  passwords and look for reuse across different accounts.

1. <a href="https://tools.emailhippo.com/" target="_blank">Email Hippo</a> (Website) - <span style="color:#0b888a">No account required.</span>
    * Verify if an email is real or fake.

1. <a href="https://github.com/khast3x/h8mail" target="_blank">h8mail</a> (External) - <span style="color:#0b888a">May require access to various APIs</span>
    * Email OSINT & Password breach hunting tool, locally or using premium services. Supports chasing down related email.
    * Digs through local databases or remote databases for findings.
    * <a href="https://github.com/khast3x/h8mail#package-pip3-install-h8mail" target="_blank">API restrictions</a>. 

1. <a href="https://hunter.io/" target="_blank">hunter.io</a> (Built-in and Website) - <span style="color:#0b888a">Free is limited.</span>
    * Email address search engine/parser.

1. <a href="https://phonebook.cz/" target="_blank">phonebook.cz</a> (Website) - <span style="color:#0b888a">_Intelx account required(free).</span>
    * Email address search engine, plus more.

1. <a href="https://github.com/s0md3v/Zen" target="_blank">Zen</a> (External) - <span style="color:#0b888a">Supports HIBP API.</span>
    * Find emails of Github users.

---
---

### File Search Engines

#### Any File Type Search

1. <a href="https://www.dedigger.com/" target="_blank">dedigger</a> - (Website)
    * Find public files in Google drives.

1. <a href="https://filepursuit.com/" target="_blank">File Pursuit</a> - (Website)
    * "Search the web for files, videos, audios, eBooks & much more."

1. <a href="https://filesearch.link/" target="_blank">FileSearch</a> - (Website)
    * Search archives, programs, videos, music, books, and more.

1. <a href="https://dlldump.com/" target="_blank">DLL Dump</a> - (Website) - <span style="color:#0b888a">Careful downloading DLLs.</span> <span style="color:#eb4034">Malicious warning!</span>
    * Free collection of DLL files free for download.

#### Document & Slide Search

1. <a href="https://www.base-search.net/" target="_blank">BASE</a> - (Website)
    * "BASE is one of the world's most voluminous search engines especially for academic web resources."

1. <a href="https://core.ac.uk/" target="_blank">CORE</a> - (Website)
    * Searches world's largest collection of open access research papers.

1. <a href="https://www.freefullpdf.com/" target="_blank">FreeFullPDF</a> - (Website)
    * "Find free scientific publications in PDF format"

1. <a href="https://scholar.google.com/" target="_blank">Google Scholar</a> - (Website)
    * Google search for anything scholar.

#### Video Search

1. <a href="http://deturl.com/" target="_blank">deturl</a> - (Website)
    * Download any youtube video by adding "pwn" to beginning of youtube video... pwnyoutube.com/watch?v=*********

1. <a href="https://filmot.com/
" target="_blank">filmot</a> - (Website)
    * Search within Youtube Subtitles.

1. <a href="https://citizenevidence.amnestyusa.org/
" target="_blank">Youtube DataViewer</a> - (Website)
    * Quickly extract Youtube video data by providing link.

---
---

### Forums Search

1. <a href="https://boardreader.com/" target="_blank">boardreader</a> - (Website)
    * Searches various forums, blogs, reviews and news via APIs.

1. <a href="https://builtwithflarum.com/" target="_blank">builtwithFlarum</a> - (Website)
    * Discover Flarum made discussion boards.

---
---

### GeoLocation

#### Search GeoLoc

1. <a href="https://www.geocreepy.com/" target="_blank">GeoCreepy</a> - (External)
    * <a href="https://github.com/jkakavas/creepy" target="_blank">Creepy Github</a>
    * A geolocation OSINT tool. Offers geolocation information gathering through social networking platforms.

1. <a href="https://earth.google.com/web/" target="_blank">Google Earth</a> - (Website)
    * Google Earth. Find locations based on GPS coordinates, etc.

1. <a href="https://mattw.io/youtube-geofind/" target="_blank">Youtube GeoFind</a> - (Website)
    * Find GeoLocation information on Youtube channels, etc

#### GeoLoc Practice

1. <a href="https://www.geoguessr.com/" target="_blank">GeoGuessr</a> - (Website & Phone App)
    * Game for everyone. Gamified OSINT through google maps.

---
---

### Images

#### Exif Data

1. <a href="https://exiftool.org/" target="_blank">ExifTool</a> - (Built-in)
    * CLI app for reading and writing exif, GPS, IPTC, XMP, and other meta info in image, audio, PDF, and video.

1. <a href="https://libexif.github.io/" target="_blank">libexif</a> - (External)
    * Library written in portable C.
    * Read and writes exif metadata in image files.

#### Reverse Image Search

1. <a href="https://www.fotoforensics.com/" target="_blank">Foto Forensics</a> - (Website)
    * Provides access to cutting-edge tools for digital photo forensics.
    * Service was retired but then recreated, by 'Hacker Factor' with the goal of providing "...a free service that provides an introduction to photo forensics."
    * <a href="https://www.fotoforensics.com/tutorial.php" target="_blank">Foto Forensics tutorial</a>.

1. <a href="https://www.google.com/imghp?hl=EN" target="_blank">Google Lens</a> - (Website)
    * AI driver reverse image search.
    * Click the little colored camera to open upload feature. Upload image or input image URL.

1. <a href="https://pimeyes.com/en" target="_blank">PimEyes</a> - (Website) - <span style="color:#0b888a">Subscription may be needed. Try page source for found image URL?</span>
    * Reverse image search.
    * For better results turn off safe search but <span style="color:#eb4034">results may become NSFW!</span>

1. <a href="https://tineye.com/" target="_blank">TinyEye</a> - (Website)
    * Image search and recognition company with reverse image search.

#### Stock Images

1. <a href="https://www.freeimages.com/" target="_blank">FreeImages</a> - (Website)
    * Free stock images.

1. <a href="https://freestocks.org/" target="_blank">Free Stocks</a> - (Website)
    * Free stock images.

1. <a href="https://pixabay.com/" target="_blank">pixabay</a> - (Website)
    * Free stock images.

1. <a href="https://unsplash.com/" target="_blank">unsplash</a> - (Website)
    * Free hi-res images. Unique.

---
---

### IoT/Device Search

1. <a href="https://censys.com/" target="_blank">censys</a> - (Website) - <span style="color:#0b888a">Free account required for personal use.</span>
    * <a href="https://support.censys.io/hc/en-us" target="_blank">censys.com How-To Guide</a>

1. <a href="https://app.netlas.io/" target="_blank">Netlas</a> - (Website)
    * Intel apps that provide IP address, domains, websites, web Apps, IoT, and other assets.

1. <a href="https://www.shodan.io/" target="_blank">Shodan.io</a> - (Website) - <span style="color:#0b888a">Free account required. Lifetime subscriptions on sale at random.</span>
    * <a href="https://skerritt.blog/shodan/" target="_blank">Shodan How-To Guide</a>
    * Search IP to do service scans.
    * city:*city* - will show devices in city area.
    * port:*port* - will search for port only.
    * org:*organization* - will search org specified.

---
---

### Leaks

1. <a href="https://offshoreleaks.icij.org/" target="_blank">Offshore Leaks Database</a> - (Website)
    * Search leak databases

---
---

### Online Cameras

1. <a href="http://insecam.org/" target="_blank">Insecam</a> - (Website)  
    * Live camera directory.  
    * Uses Shodan to find cameras then indexes them.

---
---

### Organizations

1. <a href="https://www.tracelabs.org/" target="_blank">Trace Labs Organization</a> - (Website - [VM VMware & VirtualBox](#aio-vm))
    * "Trace Labs is a nonprofit organization whose mission is to accelerate the family reunification of missing persons while training members in the tradecraft of open source intelligence (OSINT)."
    * This VM was created for OSINT. Updated regularly. Privacy focused.

1. <a href="https://www.icij.org/" target="_blank">International Consortium of Investigative Journalists</a> - (Website)
    * Source for <a href="https://www.icij.org/investigations/" target="_blank">investigations</a>, <a href="https://www.icij.org/inside-icij/" target="_blank">news</a>, and host of publicly made [leaks](#leaks)</a>.
    * They also take in leaked data.

1. <a href="https://www.innocentlivesfoundation.org/" target="_blank">Innocent Lives Foundation</a> - (Website)
    * "Identify anonymous child predators and help bring them to justice.

---
---

### Persons

1. <a href="https://www.bop.gov/inmateloc/" target="_blank">Federal Bureau of Prisons</a> - (Website)
    * Searches prisons for inmates by number or name.

1. <a href="https://www.fastbackgroundcheck.com" target="_blank">Fast Background Check</a> - (Website)
    * Searches public records for personal information. It's quick too.

1. <a href="https://www.fastpeoplesearch.com" target="_blank">Fast People Search</a> - (Website)
    * Can find relatives, phone, address, etc.
    * Decent at finding active phone numbers.

1. <a href="https://www.idcrawl.com/" target="_blank">iDCrawl</a> - (Website)
    * Person search engine. Photos, socials, usernames, address, etc.

1. <a href="https://www.judyrecords.com/" target="_blank">Jury Records</a> - (Website)
    * Searches jury cases for linked persons.

1. <a href="https://www.peekyou.com" target="_blank">peekyou</a> - (Website)
    * Uses other site searches to find person information.

1. <a href="https://www.truepeoplesearch.com/" target="_blank">TruePeopleSearch</a> - (Website)
    * Finds address(with google maps), phone, relatives, associates, etc.

1. <a href="https://webmii.com" target="_blank">Webmii</a> - (Website)
    * Person search but includes some social platforms too.

1. <a href="https://www.whitepages.com/" target="_blank">White Pages</a> - (Website)
    * One of the largest person contact and background databases.

---
---

### Phone Numbers

1. <a href="https://calleridtest.com/" target="_blank">CallerID Test</a> - (Website) - <span style="color:#0b888a"> 5 searches a day.</span>
    * Free phone number search. Locates city, state, and phone provider.

1. <a href="https://www.infobel.com/fr/world" target="_blank">infobel</a> - (Website)
    * Phone search across North America, South America, Europe, Asia, Africa, Australia and the Pacific, and the Middle East.
    * USA version called <a href="https://www.us-info.com/en/usa" target="_blank">us-info</a>

1. <a href="https://www.truecaller.com/" target="_blank">true caller</a> - (Website & Phone App) - <span style="color:#0b888a"> Registration required.</span>
    * Searches phones numbers.
    * Many cellular phones have this integrated for caller ID.

---
---

### Social Platforms

#### <a href="https://www.facebook.com/" target="_blank">Facebook</a>

1. <a href="https://github.com/n0kovo/fb_friend_list_scraper" target="_blank">Facebook Friend List Scraper</a> - (External)
    * "OSINT tool to scrape names and usernames from large friend lists on Facebook, without being rate limited."

1. <a href="https://github.com/sqren/fb-sleep-stats" target="_blank">fb-sleep-stats</a> - (External)
    * "Use Facebook to track your friends’ sleeping habits"

1. <a href="https://randomtools.io/" target="_blank">Facebook ID Lookup</a> - (Website)
    * "Facebook ID finder can help you find your or someone’s Facebook numeric user ID easily"

#### <a href="https://www.instagram.com/" target="_blank">Instagram</a>

1. <a href="https://www.codeofaninja.com/tools/" target="_blank">Tools By CodeOfaNinja</a> - (Website)
    * Various tools, including social ID finders.

1. <a href="https://hashtagify.me/" target="_blank">HashTagify</a> - (Website)
    * Search instagram hashtags.

1. <a href="https://github.com/Datalux/Osintgram" target="_blank">Osintgram</a> - (External)
    * "Osintgram is a OSINT tool on Instagram. It offers an interactive shell to perform analysis on Instagram account of any users by its nickname".
    
1. <a href="https://github.com/novitae/sterraxcyl" target="_blank">sterraxcyl</a> - (External)
    * "Instagram OSINT tool to export and analyze followers | following with their details".

1. <a href="https://github.com/megadose/toutatis" target="_blank">Toutatis</a> - (External)
    * "Toutatis is a tool that allows you to extract information from instagram accounts such as e-mails, phone numbers and more".


#### <a href="https://www.linkedin.com/" target="_blank">LinkedIn</a>

1. <a href="https://github.com/gojhonny/InSpy" target="_blank">InSpy</a> - (External)
    * Python based LinkedIn enumeration tool requiring Hunter.io API key.


#### <a href="https://www.pinterest.com/ideas/" target="_blank">Pinterest</a>

1. <a href="https://www.aware-online.com/en/osint-investigation-on-pinterest/" target="_blank">Aware-Online Pinterest OSINT Guide</a> - (Website)


#### <a href="https://www.reddit.com/search" target="_blank">Reddit</a>

1. <a href="http://subreddits.org/" target="_blank">Subreddits</a> - (Website)
    * Discover new subreddits.

1. <a href="https://redditcommentsearch.com/" target="_blank">Reddit Comment Search</a> - (Website)
    * Find all comments posted by user.


#### <a href="https://www.snapchat.com/" target="_blank">Snapchat</a>

1. <a href="https://map.snapchat.com/" target="_blank">Snapchat Map</a> - (Website)
    * Built-in search engine for snapchat, including map.


#### <a href="https://telegram.org/" target="_blank">Telegram</a>

1. <a href="https://github.com/tejado/telegram-nearby-map" target="_blank">Telegram Nearby Map</a> - (External)
    * Discover the location of nearby Telegram users.

#### <a href="https://www.tumblr.com/explore/trending" target="_blank">Tumblr</a>

1. <a href="https://search.0t.rocks/" target="_blank">Tumblr 2013 data breach search</a> - (Website)


#### <a href="https://www.twitter.com/" target="_blank">Twitter</a>

1. <a href="https://nitter.net/" target="_blank">Nitter</a> - (External & Website)
    * Free and open source front-end for searching twitter(x) without an account.
    * <a href="https://github.com/zedeus/nitter" target="_blank">Nitter Github</a>

1. <a href="https://foller.me/" target="_blank">foller.me</a> - (Website)
    * "Twitter analytics shows followers, hashtags, topics, mentions, and other statistics for any public Twitter profile."

---
---

### Threat Intel

1. <a href="https://otx.alienvault.com/browse/global/pulses" target="_blank">AlienVault</a> - (Website)
    * Open Threat Exchange neighborhood watch of the threat intel community.

1. <a href=https://rescure.me/feeds.html target="_blank">Rescure</a> - (Website)
    * Feeds of malicious IPs, domains, and Malware hashes updated every 24hrs.

---
---

### Voter Records

1. <a href="https://voterrecords.com/" target="_blank">Voter Records</a> - (Website)
    * Political research tool which searches public records released by US states.

---
---

### Web

#### Web History

1. <a href="https://archive.org/" target="_blank">Archive.org</a> - (Website)
    * OG Wayback Machine by Internet Archive.

1. <a href="https://archive.is/" target="_blank">Archive.is</a> - (Website)
    * Archive tool which time capsules web pages.

1. <a href="https://visualping.io/" target="_blank">Visual Ping</a> - (Website)
    * Visually look at a webpages for changes.

1. <a href="https://stored.website/" target="_blank">Stored.Website</a> - (Website)
    * Pulls web cache from selected source.

1. <a href="https://github.com/jsvine/waybackpack" target="_blank">waybackpack</a> - (External)
    * "Download the entire Wayback Machine archive for a given URL."

1. <a href="https://github.com/akamhy/waybackpy" target="_blank">waybackpy</a> - (External)
    * API to interface with wayback machine APIs.

#### Web Search Engines

##### <a href="https://www.google.com/" target="_blank">Google</a>

1. <a href="https://www.blackhat.com/presentations/bh-europe-05/BH_EU_05-Long.pdf" target="_blank">Google Hacking for Penetration Testers</a> - (PDF)
    * BlackHat presentation covering "Google Hacking for Penetration Testers".

1. <a href="https://www.google.com/advanced_search" target="_blank">Google Advanced Search</a> - (Website)
    * Helps you run Google operators aka dorks.

1. <a href="https://www.dorksearch.com/" target="_blank">Dork-Search.com</a> - (Website)
    * Google search techniques built into the search bar.

1. <a href="https://www.google-dorking.com/" target="_blank">Google-Dorking</a> - (Website)
    * Site of Google search techniques and tools.

1. <a href="https://www.googleguide.com/print/adv_op_ref.pdf" target="_blank">Google Guide</a> - (Website)
    * Small PDF guide to google search techniques & operators.

1. <a href="https://www.exploit-db.com/google-hacking-database" target="_blank">Google Hacking Database</a> - (Website)
    * Google dorks created by offsec minded individuals.

1. <a href="https://trends.google.com/trends/" target="_blank">Google Trends</a> - (Website)
    * "Google Trends is a website by Google that analyzes the popularity of top search queries in Google Search across various regions and languages. The website uses graphs to compare the search volume of different queries over time." per <a href="https://en.wikipedia.org/wiki/Google_Trends" target="_blank">Wikipedia</a>.

##### Other Search Engines

1. <a href="https://search.aol.com/" target="_blank">Aol</a> - (Website)
    * Aol search engine.

1. <a href="https://www.ask.com/" target="_blank">Ask</a> - (Website)
    * Ask search engine.

1. <a href="https://www.baidu.com/" target="_blank">Baidu</a> - (Website)
    * China's google...

1. <a href="https://www.bing.com/" target="_blank">Bing</a> - (Website)
    * Microsoft search engine.
    * <a href="https://www.bruceclay.com/blog/bing-google-advanced-search-operators/" target="_blank">Bing search guide</a>.
    * <a href="https://support.microsoft.com/en-us/topic/advanced-search-keywords-ea595928-5d63-4a0b-9c6b-0b769865e78a" target="_blank">Advanced Bing search keywords</a>.

1. <a href="https://duckduckgo.com/" target="_blank">DuckDuckGo</a> - (Website)
    * Privacy focused search engine.
    * <a href="https://help.duckduckgo.com/duckduckgo-help-pages/results/syntax/" target="_blank">DuckDuckGo search guide</a>.

1. <a href="https://www.wolframalpha.com/" target="_blank">Wolfram Alpha</a> - (Website)
    * Computational knowledge engine.

1. <a href="https://search.yahoo.com/" target="_blank">Yahoo</a> - (Website)
    * Yahoo search engine.
    * <a href="https://en.wikibooks.org/wiki/How_To_Search/Yahoo" target="_blank">Yahoo search guide</a>.

1. <a href="https://yandex.com/" target="_blank">Yandex</a> - (Website)
    * Russia's google...

#### Web Techstack

1. <a href="https://builtwith.com/" target="_blank">BuiltWith</a> - (Website)
    * Search a websites techstack.

1. <a href="https://sitereport.netcraft.com/" target="_blank">netcraft</a> - (Website)
    * Find infrastructure and techstack.

---
---

### Wireless

1. <a href="https://github.com/aircrack-ng/aircrack-ng" target="_blank">aircrack-ng</a> - (Built-in)
    * AIO wireless security suite.
    * Contains both passive and active recon tools, along with many exploitation tools.

1. <a href="https://wigle.net/" target="_blank">WiGLE</a> - (Website)
    * Wireless Geographic Logging Engine.
    * Searchable central database of world-wide wireless networks.

---
---

### Wordlists

#### Wordlist Creation

1. <a href="https://gist.github.com/superkojiman/11076951" target="_blank">ceWL (Custom Word List Generator)</a> - (Built-in)
    * Ruby based app which crawls URL returns a list of words.

1. <a href="https://gist.github.com/superkojiman/11076951" target="_blank">CUPP (Custom User Passwords Profiler)</a> - (Built-in)
    * After OSINT, takes user input and creates a custom wordlist based off user input like birthday, name, etc.

1. <a href="https://github.com/sc0tfree/mentalist" target="_blank">Mentalist</a> - (External)
    * Wordlist and rules creation tool.

1. <a href="https://gist.github.com/superkojiman/11076951" target="_blank">namemash.py</a> - (External)
    * Takes first and last name as user input and spits out possible combinations.
    * Useful for after finding names via OSINT.

#### Wordlist Downloads

1. <a href="https://github.com/duyet/bruteforce-database" target="_blank">Bruteforce-database repo</a> - (External)
    * Various wordlists in one repo.

1. <a href="https://github.com/InfoSecWarrior" target="_blank">InfoSecWarrior repo</a> - (External)
    * Various wordlists buried inside the repos. 

1. <a href="https://github.com/danielmiessler/SecLists" target="_blank">SecLists repo</a> - (Built-in)
    * Updated collection of wordlists.
    * Located under /usr/share/wordlists/SecLists

---
---

### Additional

#### OSINT Certifications

1. <a href="https://www.mcafeeinstitute.com/products/certified-osint" target="_blank">McAfee Institute</a> - (Website)
    * More info @ <a href="https://niccs.cisa.gov/education-training/catalog/mcafee-institute/certified-open-source-intelligence-cosint" target="_blank">CISA's webpage</a>.
    * "The Certified in Open Source Intelligence (C|OSINT) program is the first and only globally recognized and accredited board certification on open source intelligence."


---

> Author: revsh3ll  
> URL: https://PivotTheNet.GitHub.io/passive-recon/  

