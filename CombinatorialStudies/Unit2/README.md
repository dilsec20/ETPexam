# Unit 2: Computer Networking Basics

---

## 2.1 Foundations

**Computer Network:** Collection of interconnected devices that communicate and share resources.

### Network Types:
| Type | Range | Example |
|---|---|---|
| **PAN** | ~10m | Bluetooth |
| **LAN** | Building | Office Wi-Fi |
| **MAN** | City | Cable TV |
| **WAN** | Worldwide | Internet |

### Devices:
| Device | OSI Layer | Function |
|---|---|---|
| **Hub** | Layer 1 | Broadcasts to ALL ports |
| **Switch** | Layer 2 | Forwards using MAC address |
| **Router** | Layer 3 | Routes using IP address |
| **Bridge** | Layer 2 | Connects two LANs |
| **Gateway** | Layer 7 | Protocol translation |
| **Repeater** | Layer 1 | Amplifies/regenerates signals |

---

## 2.2 Topologies
| Topology | Key Feature |
|---|---|
| **Bus** | Single backbone; collision domain |
| **Star** | Central hub; hub failure = network down |
| **Ring** | Circular; token passing |
| **Mesh** | Full: n(n-1)/2 connections; most reliable |
| **Tree** | Hierarchical; scalable |

---

## 2.3 OSI Model (7 Layers)
| # | Layer | Function | Protocols | Data Unit |
|---|---|---|---|---|
| 7 | Application | User services | HTTP, FTP, SMTP, DNS, DHCP | Data |
| 6 | Presentation | Encryption, compression | SSL/TLS, JPEG | Data |
| 5 | Session | Session management | NetBIOS, RPC | Data |
| 4 | Transport | End-to-end delivery | TCP, UDP | Segment |
| 3 | Network | Routing, IP addressing | IP, ICMP, ARP | Packet |
| 2 | Data Link | MAC addressing, framing | Ethernet, PPP | Frame |
| 1 | Physical | Raw bits on medium | Cables, Hubs | Bits |

**Mnemonic (top-down):** All People Seem To Need Data Processing

## 2.4 TCP/IP Model (4 Layers)
| Layer | OSI Equivalent | Protocols |
|---|---|---|
| Application | 7+6+5 | HTTP, FTP, SMTP, DNS |
| Transport | 4 | TCP, UDP |
| Internet | 3 | IP, ICMP, ARP |
| Network Access | 2+1 | Ethernet, Wi-Fi |

## 2.5 TCP vs UDP
| Feature | TCP | UDP |
|---|---|---|
| Connection | Connection-oriented | Connectionless |
| Reliable | Yes | No |
| Speed | Slower | Faster |
| Header | 20 bytes | 8 bytes |
| Use | HTTP, FTP, Email, SSH | DNS, Gaming, VoIP, Multimedia |

**TCP 3-Way Handshake:** SYN → SYN-ACK → ACK

### Transport Layer Protocols for Common Services:
| Service | Protocol |
|---|---|
| **Real-time multimedia** | UDP |
| **File transfer (FTP)** | TCP |
| **DNS** | UDP (queries), TCP (zone transfer) |
| **Email (SMTP)** | TCP |

> **PYQ:** Protocols for multimedia, file transfer, DNS, email = **UDP, TCP, UDP and TCP** ✅

---

## 2.6 IP Addressing & Subnetting

| Class | Range | Default Mask | # Networks | Hosts/Network |
|---|---|---|---|---|
| **A** | 1-126.x.x.x | /8 (255.0.0.0) | 2^7 - 2 = 126 | ~16M |
| **B** | 128-191.x.x.x | /16 (255.255.0.0) | 2^14 = 16384 | ~65K |
| **C** | 192-223.x.x.x | /24 (255.255.255.0) | **2^21** = 2,097,152 | 254 |
| **D** | 224-239.x.x.x | Multicast | — | — |
| **E** | 240-255.x.x.x | Reserved | — | — |

> **PYQ: Number of networks in Class C = 2^21** ✅

### Special Addresses:
- **127.0.0.1** — Loopback (localhost) → can be used as BOTH source and destination IP
- **0.0.0.0** — Default/unspecified
- **255.255.255.255** — Broadcast
- Private: 10.x.x.x, 172.16-31.x.x, 192.168.x.x

> **PYQ: Which IP can be used as both Source and Destination? → 127.0.0.1** ✅

### Subnetting:
- Subnets = 2^n (n = borrowed bits)
- Hosts per subnet = **2^h - 2** (h = host bits; -2 for network & broadcast)
- /26 → 6 host bits → 2^6 - 2 = 62 usable hosts
- /28 → 4 host bits → 2^4 - 2 = 14 usable hosts

---

## 2.7 Token Ring Network Calculations

### 1-Bit Delay Calculation:
```
1-bit delay = distance / propagation speed
```

**PYQ:** Transmission speed = 10^7 bps, propagation = 200 m/μs = 200 × 10^6 m/s
```
Time for 1 bit = 1 / 10^7 = 10^-7 seconds = 0.1 μs
Distance in 0.1 μs = 200 × 10^6 × 10^-7 = 20 metres
```
> **Answer: 20 metres of cable** ✅

### Ethernet Cable Length Calculation:
**PYQ:** 500 Mbps, frames = 10,000 bits, signal speed = 2×10^5 km/s (2×10^8 m/s)
```
Transmission time = Frame size / Data rate = 10000 / (500 × 10^6) = 2 × 10^-5 s
Max cable length = speed × time / 2 = (2 × 10^8 × 2 × 10^-5) / 2 = 2000 m = 2 km
```
> **Answer: 2 km** ✅

---

## 2.8 Key Protocols & Port Numbers

| Protocol | Port | Function |
|---|---|---|
| HTTP | 80 | Web (unencrypted) |
| HTTPS | 443 | Web (encrypted) |
| FTP | 20/21 | File transfer |
| SSH | 22 | Secure remote login |
| Telnet | 23 | Remote login (insecure, plaintext) |
| SMTP | 25 | Send email |
| DNS | 53 | Domain → IP |
| DHCP | 67/68 | Auto IP assignment |
| POP3 | 110 | Retrieve email (download & delete) |
| IMAP | 143 | Retrieve email (sync, keep on server) |
| ARP | — | IP → MAC |
| ICMP | — | Ping, error reporting |

---

## MCQ Practice Questions (50+ PYQ Style)

---

**Q1.** Which of the following can be used as both Source and Destination IP?

a) 198.168.1.255  
b) 10.0.0.1  
**c) 127.0.0.1 ✅**  
d) 255.255.255.255

---

**Q2.** In a token ring network, transmission speed is 10^7 bps and propagation speed is 200 meters/μs. The 1-bit delay is equivalent to:

a) 500 metres  
b) 200 metres  
**c) 20 metres ✅**  
d) 50 metres

---

**Q3.** In IPv4, the number of networks allowed under Class C is:

a) 2^14  
**b) 2^21 ✅**  
c) 2^24  
d) 2^7

---

**Q4.** Transport layer protocols for real-time multimedia, file transfer, DNS, and email respectively are:

a) TCP, UDP, UDP and TCP  
b) UDP, TCP, TCP and UDP  
**c) UDP, TCP, UDP and TCP ✅**  
d) TCP, UDP, TCP and UDP

---

**Q5.** Which OSI layer handles routing?

a) Transport  
b) Data Link  
**c) Network ✅**  
d) Session

---

**Q6.** Default subnet mask for Class B?

a) 255.0.0.0  
**b) 255.255.0.0 ✅**  
c) 255.255.255.0  
d) 255.255.255.255

---

**Q7.** DNS resolves:

a) MAC to IP  
**b) Domain name to IP ✅**  
c) IP to MAC  
d) Port to IP

---

**Q8.** Which is connectionless?

a) TCP  
**b) UDP ✅**  
c) HTTP  
d) FTP

---

**Q9.** How many OSI layers?

a) 4  
b) 5  
**c) 7 ✅**  
d) 6

---

**Q10.** Router operates at which layer?

a) Layer 1  
b) Layer 2  
**c) Layer 3 ✅**  
d) Layer 4

---

**Q11.** Full mesh with n devices needs:

a) n  
b) n²  
**c) n(n-1)/2 ✅**  
d) 2n

---

**Q12.** TCP 3-way handshake:

**a) SYN → SYN-ACK → ACK ✅**  
b) ACK → SYN → FIN  
c) FIN → ACK → SYN  
d) SYN → ACK → FIN

---

**Q13.** SMTP is used for:

**a) Sending email ✅**  
b) Receiving email  
c) Web browsing  
d) File transfer

---

**Q14.** Highest bandwidth cable:

a) Twisted Pair  
b) Coaxial  
**c) Fiber Optic ✅**  
d) Radio

---

**Q15.** ARP resolves:

a) Domain to IP  
**b) IP to MAC ✅**  
c) MAC to IP  
d) Port to MAC

---

**Q16.** In /26 subnet, usable hosts?

a) 64  
**b) 62 ✅**  
c) 30  
d) 126

---

**Q17.** IMAP vs POP3 — IMAP:

a) Deletes emails from server  
**b) Keeps emails on server and syncs ✅**  
c) Same as POP3  
d) Faster than POP3

---

**Q18.** DHCP server port?

a) 80  
**b) 67 ✅**  
c) 53  
d) 443

---

**Q19.** Multicast IP class?

a) Class A  
b) Class C  
**c) Class D ✅**  
d) Class E

---

**Q20.** Which is a private IP?

a) 8.8.8.8  
**b) 192.168.1.1 ✅**  
c) 172.32.0.1  
d) 11.0.0.1

---

**Q21.** Switch sends data to:

a) All ports  
**b) Specific port using MAC address ✅**  
c) Random port  
d) Nearest port

---

**Q22.** TCP header size:

**a) 20 bytes ✅**  
b) 8 bytes  
c) 32 bytes  
d) 16 bytes

---

**Q23.** RIP max hop count:

**a) 15 ✅**  
b) 16  
c) 255  
d) 30

---

**Q24.** `ping` command uses:

a) TCP  
b) UDP  
**c) ICMP ✅**  
d) ARP

---

**Q25.** FTP data port:

**a) 20 ✅**  
b) 21  
c) 22  
d) 25

---

**Q26.** FTP control port:

a) 20  
**b) 21 ✅**  
c) 22  
d) 80

---

**Q27.** Data Link layer adds:

a) IP address  
**b) MAC address ✅**  
c) Port number  
d) Domain name

---

**Q28.** Hub operates at:

**a) Physical (Layer 1) ✅**  
b) Data Link  
c) Network  
d) Transport

---

**Q29.** SSH port:

**a) 22 ✅**  
b) 23  
c) 25  
d) 80

---

**Q30.** Telnet is insecure because:

a) Uses UDP  
**b) Data sent in plaintext ✅**  
c) Slow  
d) Wrong port

---

**Q31.** How many TCP/IP layers?

a) 3  
**b) 4 ✅**  
c) 5  
d) 7

---

**Q32.** DHCP auto-assigns:

a) MAC addresses  
**b) IP addresses ✅**  
c) Domain names  
d) Ports

---

**Q33.** Star topology: if hub fails:

a) One node down  
**b) Entire network down ✅**  
c) Network slows  
d) Nothing

---

**Q34.** IPv4 is __ bits; IPv6 is __ bits:

a) 16, 64  
**b) 32, 128 ✅**  
c) 64, 128  
d) 32, 256

---

**Q35.** 255.255.255.255 is:

a) Loopback  
**b) Broadcast address ✅**  
c) Default gateway  
d) Network address

---

**Q36.** HTTPS uses port:

a) 80  
**b) 443 ✅**  
c) 8080  
d) 22

---

**Q37.** BGP is used:

a) Within a LAN  
**b) Between autonomous systems (Internet backbone) ✅**  
c) For DNS  
d) For email

---

**Q38.** OSPF is what type?

a) Distance Vector  
**b) Link State ✅**  
c) Path Vector  
d) Hybrid

---

**Q39.** Data unit at Transport layer:

a) Packet  
b) Frame  
**c) Segment ✅**  
d) Bits

---

**Q40.** Data unit at Network layer:

a) Frame  
**b) Packet ✅**  
c) Segment  
d) Data

---

**Q41.** Data unit at Data Link layer:

**a) Frame ✅**  
b) Packet  
c) Segment  
d) Bits

---

**Q42.** Gateway connects different:

a) Cables  
**b) Network protocols ✅**  
c) Switches  
d) Hubs

---

**Q43.** /28 subnet usable hosts:

a) 16  
**b) 14 ✅**  
c) 30  
d) 8

---

**Q44.** Class A range starts from:

**a) 1.0.0.0 ✅**  
b) 128.0.0.0  
c) 192.0.0.0  
d) 0.0.0.0

---

**Q45.** ICMP provides:

a) Routing  
**b) Error reporting ✅**  
c) File transfer  
d) Email

---

**Q46.** UDP header size:

a) 20 bytes  
**b) 8 bytes ✅**  
c) 16 bytes  
d) 32 bytes

---

**Q47.** Repeater does:

**a) Regenerates/amplifies weak signals ✅**  
b) Routes packets  
c) Switches frames  
d) Translates protocols

---

**Q48.** DNS primarily uses:

a) TCP only  
**b) UDP (queries), TCP (zone transfers) ✅**  
c) ICMP  
d) ARP

---

**Q49.** Determine max cable length (km) for Ethernet LAN: data rate 500 Mbps, frame size 10,000 bits, signal speed 2,00,000 km/s:

a) 1  
**b) 2 ✅**  
c) 2.5  
d) 5

---

**Q50.** Which environment variable sets the Java path?

a) MAVEN_Path  
b) JavaPATH  
c) JAVA  
**d) JAVA_HOME ✅**

---

## Scenario / One-Line Answers

**S1.** Token ring 1-bit delay = distance / propagation speed. Calculate distance for given speed.  
**S2.** Class C has 21 bits for network portion → 2^21 networks possible.  
**S3.** 127.0.0.1 is loopback — can be both source and destination (used for self-testing).  
**S4.** Multimedia uses UDP (speed > reliability); FTP uses TCP; DNS uses UDP; Email uses TCP.  
**S5.** Ethernet max cable length = (signal speed × frame transmission time) / 2.  
**S6.** NAT translates private IPs to a public IP for internet access.  
**S7.** Subnet hosts = 2^(host bits) - 2. The -2 is for network address and broadcast address.

---
