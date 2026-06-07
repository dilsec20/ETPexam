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
| **Hub** | Layer 1 | Broadcasts to all ports |
| **Switch** | Layer 2 | Forwards using MAC address |
| **Router** | Layer 3 | Routes using IP address |
| **Bridge** | Layer 2 | Connects two LANs |
| **Gateway** | Layer 7 | Protocol translation |
| **Repeater** | Layer 1 | Amplifies signals |

## 2.2 Topologies
| Topology | Key Feature |
|---|---|
| **Bus** | Single backbone; single point of failure |
| **Star** | Central hub/switch; hub failure = network down |
| **Ring** | Circular; one node failure breaks ring |
| **Mesh** | Full: n(n-1)/2 connections; most reliable |
| **Tree** | Hierarchical; scalable |

## 2.3 OSI Model (7 Layers)
| # | Layer | Function | Protocols | Data Unit |
|---|---|---|---|---|
| 7 | Application | User services | HTTP, FTP, SMTP, DNS | Data |
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
| Reliable | Yes (ACK, retransmit) | No |
| Speed | Slower | Faster |
| Header | 20 bytes | 8 bytes |
| Use | HTTP, FTP, Email | DNS, Gaming, VoIP |

**TCP 3-Way Handshake:** SYN → SYN-ACK → ACK

## 2.6 IP Addressing & Subnetting
| Class | Range | Default Mask | Hosts |
|---|---|---|---|
| A | 1-126.x.x.x | /8 (255.0.0.0) | ~16M |
| B | 128-191.x.x.x | /16 (255.255.0.0) | ~65K |
| C | 192-223.x.x.x | /24 (255.255.255.0) | 254 |
| D | 224-239.x.x.x | Multicast | — |

**Private IPs:** 10.x.x.x, 172.16-31.x.x, 192.168.x.x  
**Loopback:** 127.0.0.1  
**Subnet hosts:** 2^h - 2 (h = host bits)

## 2.7 Key Protocols
| Protocol | Port | Function |
|---|---|---|
| HTTP | 80 | Web (unencrypted) |
| HTTPS | 443 | Web (encrypted) |
| FTP | 20/21 | File transfer |
| SSH | 22 | Secure remote login |
| Telnet | 23 | Remote login (insecure) |
| SMTP | 25 | Send email |
| DNS | 53 | Domain → IP |
| DHCP | 67/68 | Auto IP assignment |
| POP3 | 110 | Retrieve email (download & delete) |
| IMAP | 143 | Retrieve email (sync, keep on server) |
| ARP | — | IP → MAC resolution |
| ICMP | — | Ping, error reporting |

---

## MCQ Practice Questions (50+)

---

**Q1.** Which OSI layer handles routing?
A. Transport  B. Data Link  **C. Network ✅**  D. Session

---

**Q2.** Default subnet mask for Class B?
A. 255.0.0.0  **B. 255.255.0.0 ✅**  C. 255.255.255.0  D. 255.255.255.255

---

**Q3.** DNS resolves:
A. MAC to IP  **B. Domain name to IP ✅**  C. IP to MAC  D. Port to IP

---

**Q4.** Which is connectionless?
A. TCP  **B. UDP ✅**  C. HTTP  D. FTP

---

**Q5.** How many OSI layers?
A. 4  B. 5  **C. 7 ✅**  D. 6

---

**Q6.** Router operates at which layer?
A. Layer 1  B. Layer 2  **C. Layer 3 ✅**  D. Layer 4

---

**Q7.** 127.0.0.1 is:
A. Default gateway  B. Broadcast  **C. Loopback (localhost) ✅**  D. Network address

---

**Q8.** Full mesh with n devices needs how many connections?
A. n  B. n²  **C. n(n-1)/2 ✅**  D. 2n

---

**Q9.** TCP uses 3-way handshake:
**A. SYN → SYN-ACK → ACK ✅**  B. ACK → SYN → FIN  C. FIN → ACK → SYN  D. SYN → ACK → FIN

---

**Q10.** SMTP is used for:
**A. Sending email ✅**  B. Receiving email  C. Web browsing  D. File transfer

---

**Q11.** Highest bandwidth cable?
A. Twisted Pair  B. Coaxial  **C. Fiber Optic ✅**  D. Radio

---

**Q12.** ARP resolves:
A. Domain to IP  **B. IP to MAC ✅**  C. MAC to IP  D. Port to MAC

---

**Q13.** In /26 subnet, usable hosts?
A. 64  **B. 62 ✅**  C. 30  D. 126

---

**Q14.** IMAP differs from POP3 because:
A. IMAP deletes emails  **B. IMAP keeps emails on server and syncs ✅**  C. Same  D. IMAP is faster

---

**Q15.** DHCP server port?
A. 80  **B. 67 ✅**  C. 53  D. 443

---

**Q16.** Multicast IP class?
A. Class A  B. Class C  **C. Class D ✅**  D. Class E

---

**Q17.** Which is a private IP?
A. 8.8.8.8  **B. 192.168.1.1 ✅**  C. 172.32.0.1  D. 11.0.0.1

---

**Q18.** Switch sends data to:
A. All ports  **B. Specific port using MAC ✅**  C. Random port  D. Nearest port

---

**Q19.** TCP header size?
**A. 20 bytes ✅**  B. 8 bytes  C. 32 bytes  D. 16 bytes

---

**Q20.** RIP max hop count?
**A. 15 ✅**  B. 16  C. 255  D. 30

---

**Q21.** Which protocol is used by the `ping` command?
A. TCP  B. UDP  **C. ICMP ✅**  D. ARP

---

**Q22.** FTP data transfer uses port:
**A. 20 ✅**  B. 21  C. 22  D. 25

---

**Q23.** FTP control connection uses port:
A. 20  **B. 21 ✅**  C. 22  D. 80

---

**Q24.** Which layer adds MAC address to data?
A. Network  **B. Data Link ✅**  C. Transport  D. Physical

---

**Q25.** Hub operates at which OSI layer?
**A. Physical (Layer 1) ✅**  B. Data Link  C. Network  D. Transport

---

**Q26.** SSH port number?
**A. 22 ✅**  B. 23  C. 25  D. 80

---

**Q27.** Telnet is insecure because:
A. It uses UDP  **B. Data is sent in plaintext (unencrypted) ✅**  C. It is slow  D. It uses wrong port

---

**Q28.** How many layers in TCP/IP model?
A. 3  **B. 4 ✅**  C. 5  D. 7

---

**Q29.** Which protocol auto-assigns IP addresses?
A. DNS  B. ARP  **C. DHCP ✅**  D. HTTP

---

**Q30.** Which topology has a single backbone cable?
**A. Bus ✅**  B. Star  C. Ring  D. Mesh

---

**Q31.** In Star topology, if the central hub fails:
A. Only one node goes down  B. Network slows down  **C. Entire network goes down ✅**  D. Nothing happens

---

**Q32.** Transport layer protocol that provides reliable delivery:
**A. TCP ✅**  B. UDP  C. IP  D. ICMP

---

**Q33.** Presentation layer handles:
A. Routing  **B. Encryption and data format translation ✅**  C. Error detection  D. Session management

---

**Q34.** Session layer is responsible for:
A. Routing  B. Encryption  **C. Establishing, managing, and terminating sessions ✅**  D. Physical transmission

---

**Q35.** IPv4 address is how many bits?
A. 16  **B. 32 ✅**  C. 64  D. 128

---

**Q36.** IPv6 address is how many bits?
A. 32  B. 64  **C. 128 ✅**  D. 256

---

**Q37.** 255.255.255.255 is:
A. Loopback  **B. Broadcast address ✅**  C. Default gateway  D. Network address

---

**Q38.** HTTPS uses which port?
A. 80  **B. 443 ✅**  C. 8080  D. 22

---

**Q39.** Which routing protocol is used between autonomous systems on the Internet?
A. RIP  B. OSPF  **C. BGP ✅**  D. EIGRP

---

**Q40.** OSPF is what type of routing protocol?
A. Distance Vector  **B. Link State ✅**  C. Path Vector  D. Hybrid

---

**Q41.** Data unit at the Transport layer is called:
A. Packet  B. Frame  **C. Segment ✅**  D. Bits

---

**Q42.** Data unit at the Network layer is called:
A. Frame  **B. Packet ✅**  C. Segment  D. Data

---

**Q43.** Data unit at Data Link layer is called:
**A. Frame ✅**  B. Packet  C. Segment  D. Bits

---

**Q44.** Which device connects two different network protocols?
A. Router  B. Switch  **C. Gateway ✅**  D. Bridge

---

**Q45.** A /28 subnet has how many usable hosts?
A. 16  **B. 14 ✅**  C. 30  D. 8

> /28 = 32-28 = 4 host bits → 2⁴ - 2 = 14

---

**Q46.** Class A IP range starts from:
**A. 1.0.0.0 ✅**  B. 128.0.0.0  C. 192.0.0.0  D. 224.0.0.0

---

**Q47.** Which protocol provides error reporting in networks?
A. TCP  B. ARP  **C. ICMP ✅**  D. DNS

---

**Q48.** UDP header size?
A. 20 bytes  **B. 8 bytes ✅**  C. 16 bytes  D. 32 bytes

---

**Q49.** Which device regenerates and amplifies weak signals?
**A. Repeater ✅**  B. Router  C. Switch  D. Gateway

---

**Q50.** DNS uses which transport protocol?
A. TCP only  **B. UDP (primarily), TCP for zone transfers ✅**  C. ICMP  D. ARP

---

## Scenario & One-Line Answer Questions

---

**S1.** A user types www.google.com in the browser. Which protocol converts this to an IP address?
> **DNS** (Domain Name System) resolves the domain name to an IP address.

**S2.** You want to send a file from one computer to another. Which protocol would you use?
> **FTP** (File Transfer Protocol) on ports 20 (data) and 21 (control).

**S3.** An email is stuck in the outbox. Which protocol is likely failing?
> **SMTP** (port 25) — used for sending outgoing emails.

**S4.** You check emails on your phone and laptop and see the same emails on both. Which protocol is being used?
> **IMAP** (port 143) — keeps emails on the server and syncs across multiple devices.

**S5.** A new device joins a network and automatically gets an IP address. Which protocol assigned it?
> **DHCP** (Dynamic Host Configuration Protocol) automatically assigns IP addresses.

**S6.** You run `ping 192.168.1.1` and get a reply. Which protocol is being used?
> **ICMP** (Internet Control Message Protocol) — used by the ping utility.

**S7.** A network has 10 devices in full mesh topology. How many connections are needed?
> **n(n-1)/2 = 10(9)/2 = 45 connections**.

**S8.** What is the difference between a hub and a switch?
> A **hub** broadcasts data to ALL ports (Layer 1). A **switch** sends data only to the SPECIFIC destination port using MAC address table (Layer 2).

**S9.** You have a /27 subnet. How many usable hosts?
> 32 - 27 = 5 host bits → 2⁵ - 2 = **30 usable hosts**.

**S10.** Why is Telnet considered insecure?
> Telnet transmits data (including passwords) in **plaintext** without encryption. SSH is the secure alternative.

**S11.** What is the difference between TCP and UDP in one line?
> TCP is **reliable and connection-oriented** (guarantees delivery); UDP is **fast and connectionless** (no guarantees).

**S12.** What is NAT (Network Address Translation)?
> NAT translates **private IP addresses to a public IP** address, allowing multiple devices on a LAN to share a single public IP for Internet access.

**S13.** What is the subnet mask for a /24 network?
> **255.255.255.0** — 24 bits for network, 8 bits for host.

**S14.** What does ARP do in one line?
> ARP maps a known **IP address to its corresponding MAC address** on a local network.

**S15.** What is the purpose of a default gateway?
> The **default gateway** is the router that a device sends packets to when the destination is **outside the local network**.

---
