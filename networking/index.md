# Networking Basics


---
---

## Basics of Networking

- A network is two or more hosts connected together in order to exchange data.
- There's two network types:
  - WAN (Wide Area Network) - network that connects large geographical areas. 
  - LAN (Local Area Network) - network that is confined within a WAN network.
- These networks use the [OSI Layers](http://pivotthenet.github.io/osi-model/) to exchange data.

---
---

### IP addresses - Part 1/2 of TCP/IP network config (Layer 3)

- IP Addressing provides two functions:
  - Identifies a device's network interface on a network.
  - Gives a network device a network location to enable communications.

---

####  Network and Host IDs

- An IP address is a binary number which is normally shown as a 32-bit decimal number divided, by decimals, into four separate 8-bit sections(octets).

- This number represents two logical sections that determine the network ID and host ID.(more details in [subnet](#subnets) section)
  - Network ID provides the subnet a unique number and specifies the network class(A, B, or C).
  - Host ID gets assigned to the network device and uniquely identifies the host.
  - Example: 192.168.1.1 /24(255.255.255.0)
    - Network ID = 192.168.1 <-- The first three octets specify the subnet's network ID and never changes. This tells the router which subnet to route the packet to.
    - Host ID = 0.0.0.1 <-- The last octet is used for assigning IP addresses to host network devices. This tells the router which host, inside the network ID subnet, to route the packet to.

---

#### IP Address Assignment

- IP addresses are assigned in two different ways:
  1.  Dynamic - The DHCP(Dynamic Host Configuration Protocol) server will assign an IP address to a network device based on the MAC address of the network interface.
  2. Static - DHCP server isn't involved meaning the device network interface must assign its own IP address, MAC address, and Gateway address to a fixed value.

---
---

### Subnets
- As a network grows, it can start to become unmanageable resulting it unwanted effects like the lack of IP addresses and poor security, organization, and performance. A solution to this is to split up the larger network into smaller networks aka subnetting.

- A subnet, or sub-network, is simply a network sitting inside another network defined by a different IP address(network ID).
- When you increase the number of subnets you decrease the number of hosts per subnet.
  - Separating the network improves:
    - Security - by isolation.
    - Performance - by reducing the amount of broadcasts and avoiding routers.
    - Administration - by separating critical network devices and creating redundancies.
  - Traffic going from one subnet to another subnet needs routed(router / gateway).

---
---

### Subnet masks - Part 2/2 of TCP/IP network config (Layer 3)

- Subnet masks are used, in TCP/IP, to specify if the network interface is within the same local subnet or within another subnet.

- Subnet masks are also 32-bit numbers and tell us which part of the IP address represents the Network ID and which part represents the Host ID range.

- When looking at a binary subnet mask, the binary 1's represent Network ID and the binary 0's represent Host ID range.
  - /24 = 255.255.255.0 = CIDR tells you, from left to right, how many 1's the subnet mask has enabled
  - 255.255.255.0(is a decimal representation of the following binary number = 11111111.11111111.11111111.00000000)
  - 11111111.11111111.11111111.00000000 = this is /24 in binary. From left to right, you'll see that 24 1's are enabled.
    -  In each octet section, you can have a maximum of 256 addresses. From left to right, each binary represents this number = 128 - 64 - 32 - 16 - 8 - 4 - 2 - 1 . Add those up and you'll get 256.
    - This explanation of CIDR to decimal to binary also applies to IP addresses.

---
---

### IP Addressing Example

**Simple break down of an IP Address**
  - Line up the binaries for the IP address and subnet mask

  - IP Address = 192.168.123.132, Subnet = /24(CIDR) aka 255.255.255.0
    - 11000000.10101000.01111011.10000100 = Binary representation of IP address 192.168.123.132
    - 11111111.11111111.11111111.00000000 = Binary representation of subnet 255.255.255.0. 1's equal Network ID & 0's equal Host ID range.
        - Look at the first octet section of the subnet mask(starting from the left side). Where we see a 1, we need to carry over the IP address's matching binary value to start building the Network ID. So overall, we need to carry over each binary value of the first three octets of the IP address to the Network ID since the subnet mask binaries are all 1's in those first three octets.
      - When we get to the binary 0's, of the subnet mask, we then copy the matching IP address binary value over to the Host ID.
    - We get the following:
      - **11000000.10101000.01111011**.00000000 - 192.168.123 Network ID
      - 00000000.00000000.00000000.**10000100** - 0.0.0.132 Host ID

---

### Subnetting Example

**Finding the Host ID range, Network ID, and Broadcast IP from only knowing one IP address and it's subnet mask**
- Let's drag down the same IP address from above but change the subnet mask, then work off that.
  - 11111111.11111111.11111111.11|000000 = Subnet mask = /26 = 255.255.255.192
  
  - 11000000.10101000.01111011.10|000100 = IP Address within the subnet = 192.168.123.132
    - Again, the subnet mask tells us which bits, in the IP address, are used for the network ID and which are used for the host ID range.
    - Any enabled bit on the left side of the | is for the network ID. This | sits just to the right of the last enabled bit within the subnet mask. Network ID binaries do not change.
    - Any disabled bit on the right side of the | is for the host IP range.
  
  - **11000000.10101000.01111011.10**|000000 = network ID in bold = 192.168.123.128

  - 11000000.10101000.01111011.**10|000000** through 11000000.10101000.01111011.**10|111111**  = host ID range in bold = 192.168.123.128 through 192.168.123.191
    - Out of the host ID range we get three values:
      - 1. Network ID(lowest number of the Host IP range) = 192.168.123.128
      - 2. Usable Host range = 192.168.123.129 through 192.168.123.190
        - This gives us 62 IP addresses to assign to hosts within the 192.168.123 subnet.
      - 3. Broadcast ID(highest number of the Host IP range) = 192.168.123.191

---
---

### TCP vs UDP (Layer 4)

  - TCP = Transmission Control Protocol
    - Reliable
    - Connection oriented - 3-way handshake SYN > SYN ACK > ACK.
    - Considered reliable since it only sends data once a connection is established.
    - Packets delivered in the same order sent and resent as needed.
    - Dynamically manages congestion
    - Much slower than UDP(higher latency and slower throughput).
    - Uses more resources since more calculations are made. Data taken apart > sent > reconstructed.

  - UDP = User Datagram Protocol
    - Unreliable
    - Connectionless oriented - No handshake
    - Faster than TCP(Low latency with loss-tolerance and faster throughput)
    - Used by real-time apps(video, audio, etc)
    - Error packets are discarded

---
---

### Common Ports and Protocols

  - TCP
    - FTP (21)
    - SSH (22)
    - Telnet (23)
    - SMTP (25)
    - DNS (53)
    - HTTP (80, 8080)
    - Kerberos (88)
    - POP3 (110)
    - RpcBind (111)
    - NNTP (119)
    - NTP (123)
    - RPC (135)
    - SMB (139 + 455)
    - IMAP (143)
    - IRC (194)
    - HTTPS (443, 8443)
  
  - UDP
    - DNS (53)
    - DHCP (67,68)
    - TFTP (69)
    - SNMP (161, 162)

---
---

### DNS (Layer 7)

  - Domain Name System
    - DNS's main task is to associate domain names with their decimal IP addresses.
      - Domain Names help identify services that reside on the internet, like websites.
    - The most common way people interact with DNS is through their browser.
      - Let's start by opening a terminal window and run the following:
        - `nslookup google.com`
      - If you look down in the "Non-authoritative answer:" section, you'll see the "Name: google.com" along with the IP address given to us by a DNS server. In my case, it's "Address: 142.250.191.142"
      - Without DNS, when you type google.com, into a browser, IP protocols wouldn't know what to do with that as it's not a decimal IP address.
      - So to make our lives easier, a DNS server resolves an IP address to connect to and the browser just presents it as "google.com".
      - If you take the google.com associated IP address, in your nslookup command output, and enter that into a browser's address bar, it'll go to google.com without an issue.

> If you ever find yourself having issues resolving a website but you can ping another system... broken DNS may be the cause. DNS is a meme these days since you'll hear people joke about "Did you check DNS" as it's a common issue in IT.  

---

> Author: revsh3ll  
> URL: https://PivotTheNet.GitHub.io/networking/  

