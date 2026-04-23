# Module 2 – Network Fundamentals

---

## 1. What is Networking ?

- **Networking** is connecting computers and devices to share data and resources.  
- Networks can be **LAN (Local Area Network)**, **WAN (Wide Area Network)**, **PAN (Personal Area Network)**, or **MAN (Metropolitan Area Network)**, depending on geographic scope.  
- **IP (Internet Protocol):** identifies devices on a network  
- **MAC (Media Access Control):** unique hardware address of devices  

### Other Notes
- IPv4 has 4 sections (2^32 addresses, ~4.29 billion total)  
- IPv6 has 8 sections (2^128 addresses, supports over 340 trillion addresses)  
- Each section of an IP address is called an **octet** (0–255)  
- Spoofing MAC addresses could let you access sites you normally don’t have access to  

**Command Used:**  
- `ping <IP>` – check connectivity  

## Screenshots 

### Ping Example
![Ping Example](screenshots/PingExample.png)

> **Personal Note:** I found it interesting how IPv4 and IPv6 addresses differ in size and how MAC addresses are unique to each device. I also liked learning about spoofing MAC addresses and how it could allow access to restricted systems.

---

## 2. Introduction to LAN

- **LAN (Local Area Network):** connects devices within a small area, such as a home, office, or school  
- **Topology:** design or layout of the LAN  

### Common Topologies
- **Star topology:** devices connect to a central switch or hub; robust and most common  
- **Bus topology:** devices share a single backbone cable; single point of failure, prone to bottlenecks  
- **Ring topology:** data passes in a loop; failure of cable stops the network  

> **Personal Note:** I liked how star topology is more robust than bus and ring topologies. Ring topology seems inefficient if a cable fails, which helps me understand why star is preferred today.

### Devices
- **NIC (Network Interface Card):** hardware component that allows a device to connect to a network; each NIC has a unique MAC address  
- **Switch:** connects multiple devices using Ethernet  
- **Router:** connects networks and passes data between them  

> **Personal Note:** I realized that NICs are fundamental because they provide the physical and MAC layer identity for a device. Switches and routers play a huge role in how data flows efficiently.

### Subnetting
- **Subnetting:** splitting a LAN into smaller subnetworks  
  - **Network address:** identifies the start of the subnet  
  - **Host address:** identifies devices within the subnet  
  - **Default gateway:** device responsible for sending data outside the subnet  
- **Subnet mask:** 32 bits, 4 bytes (0–255 each)  
- **Benefits:** efficiency, security, full control  

> **Personal Note:** Subnetting makes a network easier to manage and adds security by controlling broadcast domains. I can see why it’s important for large networks.

### ARP (Address Resolution Protocol)
- Resolves IP addresses to MAC addresses for communication  
- **How it works:**  
  1. Device broadcasts ARP request: “Who owns this IP address?”  
  2. Device with that IP responds with its MAC address (ARP reply)  
  3. Requesting device stores this mapping in **ARP cache**  

> **Personal Note:** Understanding ARP helped me see how devices learn about each other dynamically in a LAN.

### DHCP (Dynamic Host Configuration Protocol)
- IP addresses can be assigned **manually or automatically via DHCP**  
- **How DHCP works:**  
  1. Device sends DHCP Discover  
  2. DHCP server replies with DHCP Offer  
  3. Device confirms with DHCP Request  
  4. DHCP server acknowledges (DHCP ACK) – device can now use the IP  

> **Personal Note:** Practicing DHCP in labs helped me understand how devices automatically get IPs and why this is important for large networks.

## Screenshots

### Star Topology
![Star Topology](screenshots/Star_Topology.png)  
### Bus Topology
![Bus Topology](screenshots/Bus_Topology.png)  
### Ring Topology
![Ring Topology](screenshots/Ring_Topology.png)  
### Router
![Router](screenshots/Router.png)  
### Switch
![Switch](screenshots/Switch.png)  
### Subnetting Example
![Subnetting Example](screenshots/Subnetting.png)  
### ARP Example
![ARP Example](screenshots/ARP.png)

---

## 3. OSI Model

- **OSI model (Open Systems Interconnection Model)**  
  - Consists of seven layers, each with specific responsibilities, arranged from Layer 7 to Layer 1  
  - Encapsulation occurs when data moves down the layers, with headers/footers added  

## Screenshots

### OSI Model
![OSI Model](screenshots/OSI_Model.png) 

### 3.1 Physical Layer
- Transfers raw bits (1s and 0s) over a physical medium  
- Examples: Ethernet cables, hubs, repeaters, NIC (Network Interface Card)  
- **Key Responsibilities:**  
  - Converting data into signals suitable for transmission  
  - Sending and receiving raw bit streams  
  - Defining the physical characteristics of cables, connectors, and signals  

> **Personal Note:** I found it interesting how even at this low level, faulty cables or bad NICs can stop an entire network.

### 3.2 Data Link Layer
- Handles **physical addressing** using **MAC addresses**  
- Creates **frames** and ensures data is delivered to the correct device  
- Key points: NICs, MAC addresses, frames  

> **Personal Note:** I noticed how ARP and MAC addresses are essential for delivering data to the right device within a LAN.

### 3.3 Network Layer
- Responsible for **routing data** from source to destination across networks  
- Uses **IP addresses** to determine where data should go  
- Combines packets into original data at the destination  
- **Layer 3 Devices:** routers  
- **Routing Factors:** shortest path, reliability, speed/connection type  
- **Common Protocols:** OSPF, RIP  

> **Personal Note:** Learning about routing made me understand how data finds the fastest and most reliable path, and why routers are Layer 3 devices.

### 3.4 Transport Layer
- Ensures **reliable delivery** of data  
- Segments data from **Session Layer**  
- **Protocols:**  
  - **TCP (Transmission Control Protocol):** connection-oriented, reliable, error-checked  
  - **UDP (User Datagram Protocol):** connectionless, fast  
- TCP guarantees order and completeness; UDP may lose or reorder data  

> **Personal Note:** It was clear why TCP is used for emails and file transfers, while UDP is better for video streaming where some data loss is acceptable.

### 3.5 Session Layer
- Manages **sessions** between devices: creation, maintenance, termination  
- Includes **checkpoints** so only lost segments are retransmitted  
- Sessions are unique; data cannot cross sessions  
- Examples: remote desktop, video conferencing, database connections  

> **Personal Note:** I liked the idea of checkpoints to save bandwidth when data is lost.

### 3.6 Presentation Layer
- Handles **data translation, formatting, and encryption**  
- Ensures data from the **Application Layer** is understood by the receiving device  
- Examples: emails between different clients, HTTPS, file conversions  

> **Personal Note:** Encryption at this layer really helps with secure web browsing.

### 3.7 Application Layer
- Closest to the **end user**  
- Provides **interfaces and protocols** for applications  
- Protocols: HTTP/HTTPS, FTP, **DNS**  
- **DNS** translates human-readable domain names (like `www.example.com`) into IP addresses (like 192.168.1.1), allowing devices to locate each other on the Internet.
- Examples: web browsing, email, file transfers, resolving domain names to IP addresses  

> **Personal Note:** Seeing how different email clients interpret the same data made me appreciate the importance of standard protocols.

---

## 4. Packets & Frames

### 4.1 What are Packets and Frames

- Packets and frames are small pieces of data that, when combined, form a larger message or piece of information.  
- A **packet** is a piece of data from **Layer 3 (Network Layer)** of the OSI model. It contains information such as an **IP header** and payload.  
- A **frame** is used at **Layer 2 (Data Link Layer)**. It encapsulates the packet and adds additional information, such as **MAC addresses**.  

### Analogy
- Think of sending a letter through the post:  
  - **Envelope = Frame**  
  - **Letter inside = Packet**  
- Encapsulation is the process of wrapping a packet with a frame for transmission. Once the frame is removed, the device sees the original packet.  

### Why Packets & Frames Matter
- Sending data in small pieces is more efficient than sending large messages at once.  
- Example: When loading an image from a website, the image is sent in small packets and reconstructed on your computer.  

### Packet Headers (IP Example)
| Header                  | Description                                                                                     |
|-------------------------|-------------------------------------------------------------------------------------------------|
| **Time to Live (TTL)**  | Prevents packets from circulating forever by setting an expiry timer                            |
| **Checksum**            | Ensures the packet hasn’t been corrupted during transmission                                    |
| **Source Address**      | The IP address of the device sending the packet                                                 |
| **Destination Address** | The IP address of the device that should receive the packet                                     |

> Packets and frames allow networks to efficiently move data between devices without clogging the system.

## 4.2 TCP & the Three-Way Handshake

- **TCP (Transmission Control Protocol)** ensures reliable communication between devices.
- Before sending data, TCP establishes a connection between a **client** and a **server** using a **Three-Way Handshake**.

### TCP Packet Headers
| Header                     | Description                                      |
|----------------------------|--------------------------------------------------|
| **Source Port**            | Port number of the sender                        |
| **Destination Port**       | Port number of the receiver (e.g., 80 for HTTP)  |
| **Source IP**              | IP address of the sender                         |
| **Destination IP**         | IP address of the receiver                       |
| **Sequence Number**        | Initial number for data ordering                 |
| **Acknowledgement Number** | Next expected sequence number                    |
| **Checksum**               | Verifies data integrity                          |
| **Data**                   | The actual information being sent                |
| **Flags**                  | Control communication (SYN, ACK, FIN, RST)       |

### Three-Way Handshake Steps
1. **SYN (Synchronize)** – Client sends initial sequence number to start connection  
2. **SYN/ACK (Synchronize & Acknowledge)** – Server acknowledges client’s SYN and sends its own sequence number  
3. **ACK (Acknowledge)** – Client confirms server’s sequence number; connection is established  

> Once the handshake is complete, data transfer can begin.

### Closing a TCP Connection
- **FIN (Finish)** – initiates graceful connection termination  
- **ACK (Acknowledge)** – confirms closure  
- **RST (Reset)** – forcefully terminates connection if needed  

### Advantages of TCP
- Guarantees data delivery and order  
- Provides error checking and retransmission  
- Synchronizes sender and receiver to prevent flooding  

### Disadvantages of TCP
- Requires more overhead and processing  
- Slower than UDP due to connection setup and reliability features  
- Connection requires resources and can bottleneck slower networks  

### Example
- Client sends **SYN** with ISN = 0  
- Server replies **SYN/ACK** with ISN = 5000, ACK = 1  
- Client sends **ACK** with sequence number = 1

> This ensures both sides know the sequence numbers and can reliably exchange data.

## 4.3 User Datagram Protocol (UDP)

- **UDP (User Datagram Protocol)** is a stateless protocol used for sending data between devices.
- Unlike TCP, UDP does **not** require a constant connection and does **not** use the three-way handshake.
- There is no synchronization or guarantee that data will be received, making it suitable for applications where some data loss is tolerable.

### Use Cases
- Video streaming  
- Voice over IP (VoIP)  
- Device discovery protocols (e.g., ARP, DHCP)  

### Advantages of UDP
- Much faster than TCP.  
- Allows applications to control the sending speed.  
- Does not reserve continuous connections.  

### Disadvantages of UDP
- Does not guarantee delivery.  
- No built-in reliability or error checking.  
- Unstable connections can cause poor user experience.  

> No connection setup or teardown is required. Data is sent “as is.”

### UDP Packet Structure
UDP packets are simpler than TCP packets and have fewer headers, but they share some standard fields:

| Header                 | Description                                                              |
|------------------------|--------------------------------------------------------------------------|
| **Time to Live (TTL)** | Sets an expiry timer so packets do not clog the network if undelivered   |
| **Source Address**     | IP address of the sending device                                         |
| **Destination Address**| IP address of the receiving device                                       |
| **Source Port**        | Randomly chosen port used to send the UDP packet                         |
| **Destination Port**   | Port of the application/service on the remote device (e.g., 80 for HTTP) |
| **Data**               | The actual data (bytes of a file, message, etc.) being transmitted       |

### Key Points
- UDP is **stateless**: no acknowledgments or guarantees.  
- Data is sent in **datagrams**, not streams.  
- Faster but less reliable than TCP.

> Example: A UDP connection between Alice and Bob allows messages to be sent without waiting for acknowledgments, suitable for applications like streaming video or voice chat.

## 4.4 Ports in Networking

- **Ports** are numerical values used to direct data to the correct application on a device.  
- They range from **0 to 65535**.  
- Think of a port like a dock at a harbor: only compatible ships can use it, just like only compatible applications can communicate through a port.

### Why Ports Matter
- Ports ensure that data is delivered to the correct application.  
- Applications, software, and services follow standardized ports for consistency.  
- Example: All web browsers send HTTP traffic over **port 80**. This allows different browsers like Chrome and Firefox to interpret the data consistently.

### Common Ports and Their Protocols
- **FTP (File Transfer Protocol) – Port 21**  
  Used for transferring files on a client-server model.  

- **SSH (Secure Shell) – Port 22**  
  Provides secure login to systems via a text-based interface.  

- **HTTP (HyperText Transfer Protocol) – Port 80**  
  Powers the World Wide Web; used to download web pages such as text, images, and videos.  

- **HTTPS (HTTP Secure) – Port 443**  
  Functions like HTTP but encrypted, ensuring secure communication over the web.  

- **SMB (Server Message Block) – Port 445**  
  Enables sharing of files and devices like printers across a network.  

- **RDP (Remote Desktop Protocol) – Port 3389**  
  Provides a secure graphical login to a remote system.  

### Key Notes
- Ports **0–1024** are commonly known as **well-known ports**.  
- Applications can use non-standard ports (e.g., a web server on **8080**), but users must specify the port explicitly (`example.com:8080`).  
- Standardization ensures that applications can communicate reliably across different devices and platforms.  

> Ports are essential for organizing network traffic and ensuring the right data reaches the correct application.