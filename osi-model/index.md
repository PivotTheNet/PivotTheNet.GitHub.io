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



---

> Author: revsh3ll  
> URL: https://PivotTheNet.GitHub.io/osi-model/  

