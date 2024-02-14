# OSI Model


## OSI Layers & PDU

- OSI Model is a 7 abstract layer table that's responsible for explaining the flow of data within a network.
- Experienced individuals will often call out an issue by the culprit layer number. example: "This is a level 3 issue."
- Protocol data unit(PDU) is a name given to the data when passing through each OSI layer. Bits, Frames, etc.

### Physical - Layer 1 - Bits (PDU)

- Bit-by-bit delivery, modulation, start-stop signals, physical network.

- Anything to do with physical transmission of data.
  - From transmission mode(full, half duplex) to pinout of a ethernet connector.
- Some related devices:
  - Ethernet hub, repeater, and physical transmission medium(wire, plug, outlet).


### Data link - Layer 2 - Frames (PDU)

- Encapsulation, frame sync, LLC, and MAC address.

- Provides a link between two devices, via a physical layer, and provides flow control.

- It also detects and corrects errors on layer 1.

- Defines two sublayers:
  1. Media Access Control(MAC) - controls device access and grants permissions for data transit.
  2. Logical link control(LLC) - flow control, handles network layer protocols and error checking/frame sync.

- Some related devices:
  - Switch, bridge, NIC.


### Network - Layer 3 - Packets (PDU)
  
- Controls addressing, routing, and traffic control.

- This layer routes packets between two network nodes by providing cross-network addressing, routing, and updates both routing tables & fragmented packets.

### Transport - Layer 4 - Segments & Datagrams (PDU)

- Reliability, flow control, connection-oriented communications, and multiplexing.
  
- Layer 4 is responsible for segmenting data and relieving congestion by determining the protocol to be used(TCP and UDP, or others), size of window(packet size(MTU)), and order of transmission.

### Session - Layer 5 - Data (PDU)

- Session management(build and control sessions) between two hosts.

- Authentication, Authorization, Session restoration.

- This layer opens, manages, and closes sessions between end-user application processes.

- API, sockets, and WinSock.

### Presentation - Layer 6 - Data (PDU)

- Translation --> data (de)compression --> data (de)encryption.

- This layer converts data (MOV, JPEG, ASCII, etc) to and from the form that the application layer accepts, so it can be sent over the network.


### Application - Layer 7 - Data (PDU)

- Communication protocol and interface methods, used by host processes, to enable network communications.
- In other words, applications handling data through specific protocols which then is sent through layer 6.
  - This would include HTTP(S), IMAP, POP3, SMTP, FTP, SSH, etc.
- Also provides service advertisement on the network.

<br>
<br>

## Detailed Table of OSI & TCP/IP

<font size="-1">
<table>
  <tr>
    <td>Mnemonic</td>
    <td>OSI</td>
    <td>TCP/IP</td>
    <td>PDU</td>
    <td>Devices</td>
    <td>IP Suite</td>
    <td>Functions</td>
  <tr>
    <td>7. <b>A</b>LL</td>
    <td>Application</td>
    <td rowspan="3">Application</td>
    <td rowspan="3">Data</td>
    <td rowspan="3">Gateways, Load Balancers, Firewalls, End-point devices</td>
    <td>HTTP(s), DNS, DHCP, IRC, FTP, TFTP, Telnet, SSH, SMTP, POP, IMAP, NTP, SNMP, TLS/SSL, BGP, RIP, SIP, MIME, and others</td>
    <td> - Applications handle data through specific protocols to present data to user and layer 6.<br>- Provides service advertisement on the network.
  </tr>
  <tr>
    <td>6. <b>P</b>EOPLE</td>
    <td>Presentation</td>
    <td>AFP, ICA, LPP, NCP, NDR, TOX, XDR, PAD</td>
    <td>- Formats, converts, (de/en)crypts, (de)compresses data (MOV, JPEG, ASCII, etc) to and from the form that the application layer accepts, so it can be sent over the network.</td>
  </tr>
  <tr>
    <td>5. <b>S</b>EEM</td>
    <td>Session</td>
    <td>ASP, ADSP, H.245, NetBIOS, RPC, SCP, ZIP, SDP, SOCKS, SMPP, and others</td>
    <td>- Session management (build and control sessions) between two hosts.<br>- Authentication, authorization, session restoration.<br>- This layer opens, manages, and closes sessions between end-user application processes.</td>
  </tr>
  <tr>
    <td>4. <b>T</b>O</td>
    <td>Transport</td>
    <td>Transport</td>
    <td>Segments</td>
    <td>Gateways, Load Balancers, Firewalls</td>
    <td>TCP, UDP, and others</td>
    <td>- Reliability, flow control, connection-oriented communications, and multiplexing.<br>- Segments data and relieves congestion by determining the protocol to be used (TCP and UDP, or others), size of window (packet size(MTU)), and order of transmission.</td>
  </tr>
  <tr>
    <td>3. <b>N</b>EED</td>
    <td>Network</td>
    <td>Internet</td>
    <td>Packets (Datagrams)</td>
    <td>Routers, VPN devices, Multilayer(L3) Switch, WAPs</td>
    <td>IPv4, IPv6, ICMP, ICMPv6, IPSec, OSPF, EIGRP, and others</td>
    <td>- Controls addressing, routing, and traffic control.<br>-  Routes packets between two network nodes by providing cross-network addressing, routing, and updates both routing tables & fragmented packets.</td>
  </tr>
  <tr>
    <td>2. <b>D</b>ATA</td>
    <td>Data Link</td>
    <td rowspan="2">Network Access</td>
    <td>Frames</td>
    <td>Switches, Bridges, NICs, WAPs, Modems</td>
    <td rowspan="2">ARP, Ethernet, CDP, LLDP, HDLC, PPP, DSL, L2TP, 802.11, STP, and others</td>
    <td>- Encapsulation, frame sync, LLC, and MAC address.<br>- Provides a link between two devices, via a physical layer, and provides flow control.<br>- It also detects and corrects errors on layer 1.<br>- Defines both MAC and LLC sublayers.</td>
  <tr>
    <td>1. <b>P</b>ROCESSING</td>
    <td>Physical</td>
    <td>Bits</td>
    <td>Hubs, NICs, Repeaters, Cables, Antennas, Modems, Wireless </td>
    <td>- Bit-by-bit delivery, modulation, start-stop signals, physical network.<br>- Anything to do with physical transmission of data.</td>
</table>
</font>
 


---

> Author: revsh3ll  
> URL: https://PivotTheNet.GitHub.io/osi-model/  

