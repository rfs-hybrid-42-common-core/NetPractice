*This project has been created as part of the 42 curriculum by maaugust.*

<div align="center">
  <img src="https://raw.githubusercontent.com/rfs-hybrid/42-Common-Core/main/assets/covers/cover-net_practice-bonus.png" alt="NetPractice Cover" width="100%" />
</div>

<div align="center">
  <h1>🌐 NetPractice: Discover the basics of networking</h1>
  <img src="https://img.shields.io/badge/Score-100%2F100-success" />
  <img src="https://img.shields.io/badge/Levels-10%2F10-blue" />
</div>

---

## 💡 Description
**NetPractice** is a general practical exercise designed to introduce the foundational basics of computer networking. 

The primary goal of this project is to successfully configure small-scale simulated networks. By completing a series of 10 incremental levels, this project requires you to configure IP addresses, connect devices through routers, and deeply understand the role of a default gateway within a network architecture.

---

## 🧠 Core Concepts

To successfully route the simulated networks in this project, a firm grasp of underlying network theory is required. Below is a breakdown of the fundamental concepts explored in NetPractice.

### 📶 What is a Network & The OSI Model
At its core, a computer network is a group of interconnected devices capable of sharing data and resources. To standardize how these devices communicate across different hardware and software, the **OSI (Open Systems Interconnection) Model** divides networking into 7 conceptual layers:

<div align="center">
  <img src="https://github.com/user-attachments/assets/ed71bbd8-2d80-4675-b9d7-03621c7618c7" alt="OSI vs TCP/IP Model Breakdown" width="650"/>
</div>

1. **Physical Layer:** The raw bit stream over a physical medium (e.g., cables, radio frequencies).
2. **Data Link Layer:** Physical addressing and transferring data between adjacent nodes (e.g., MAC, Ethernet).
3. **Network Layer:** Logical addressing and routing best paths across networks (e.g., IP, ICMP).
4. **Transport Layer:** End-to-end connections, reliability, and flow control (e.g., TCP, UDP).
5. **Session Layer:** Establishes, maintains, and terminates connections between applications.
6. **Presentation Layer:** Data formatting, encryption, and translation (e.g., SSL, JPEG).
7. **Application Layer:** Network applications and end-user processes (e.g., HTTP, FTP).

*NetPractice primarily focuses on mastering two specific layers:*
* **Layer 2 (Data Link Layer):** Where switches operate, moving data frames across a local network using physical hardware addresses.
* **Layer 3 (Network Layer):** Where routers operate, handling logical IP addressing and determining the best path to send packets across multiple networks.

### 🖥️ Network Architectures

<table align="center">
  <tr>
    <th align="center">Client-Server Architecture</th>
    <th align="center">Peer-to-Peer (P2P) Architecture</th>
  </tr>
  <tr>
    <td align="center"><img src="https://github.com/user-attachments/assets/ee8721eb-cbe5-4ed5-8e4f-93ede457571e" alt="Client-Server Architecture Diagram" width="500"/></td>
    <td align="center"><img src="https://github.com/user-attachments/assets/9151e38a-cbb8-4f66-a70f-ddf70ac72f63" alt="Peer-to-Peer Architecture Diagram" width="500"/></td>
  </tr>
</table>

* **Client-Server:** A centralized model where client devices request services or resources from a central server (e.g., loading a webpage from a dedicated web server).
* **Peer-to-Peer (P2P):** A decentralized model where all devices (peers) have equal status and share resources directly with each other without a central server (e.g., BitTorrent).

### 🚦 Transport Protocols: TCP vs. UDP
Data traveling across networks typically uses one of two main Layer 4 protocols:
* **TCP (Transmission Control Protocol):** Connection-oriented and highly reliable. It establishes a handshake, numbers packets, and ensures everything arrives in order without data loss (used for web browsing, emails, file transfers).
* **UDP (User Datagram Protocol):** Connectionless and fast. It fires packets continuously without waiting for acknowledgments or checking for lost data (used for live video streaming, online gaming).

### 📍 IP Addressing
An IP address is the logical identifier for a device on a network.
* **IPv4 vs. IPv6:**
  * **IPv4** uses a 32-bit architecture (e.g., `192.168.1.15`), yielding about 4.3 billion unique addresses—which we have effectively run out of.
  * **IPv6** was introduced using a 128-bit architecture (e.g., `2001:0db8:85a3:0000:0000:8a2e:0370:7334`) to provide a virtually limitless supply of addresses.
* **Public vs. Private Addresses:**
  * **Public IPs:** Globally unique and routable on the open internet (e.g., Google's DNS server `8.8.8.8`).
  * **Private IPs:** Reserved exclusively for internal local area networks (LANs) and cannot connect directly to the internet without a router performing NAT (Network Address Translation). Standard private ranges include:
    * Class A: `10.0.0.0` to `10.255.255.255`
    * Class B: `172.16.0.0` to `172.31.255.255`
    * Class C: `192.168.0.0` to `192.168.255.255`

### 🧮 Subnet Masks & CIDR Notation
Networks are divided into subnets to improve routing efficiency and security.
* **Subnet Mask:** A 32-bit number that masks an IP address, dividing it into a **Network ID** (identifying the specific network) and a **Host ID** (identifying the specific device on that network). For example, a mask of `255.255.255.0` means the first three numbers define the network, and the last number defines the device.
* **CIDR Notation:** "Classless Inter-Domain Routing" is a shorthand method for writing subnet masks. Instead of writing out `255.255.255.0`, CIDR counts the consecutive binary `1`s in the mask, represented as `/24` (e.g., `192.168.1.0/24`).

> ⚠️ **The Golden Rule of IP Assignment:** > When assigning IP addresses to devices (like computers or router interfaces), you can **never** use the very first or very last IP address of a specific subnet block.
> * **The Network Address (First IP):** Used to identify the subnet itself.
> * **The Broadcast Address (Last IP):** Used to broadcast a message to every single device on that subnet.
>
> *Crucial Distinction:* Beginners often assume the network address always ends in `.0` and the broadcast always ends in `.255`. This is **only** true for a `/24` subnet. The actual restricted addresses depend entirely on the block boundaries defined by the CIDR notation:
> * **Example 1 (A `/24` Subnet):** In the subnet `192.168.1.0/24`, the block size is 256. The network address is `.0` and the broadcast is `.255`. Usable IPs: `.1` through `.254`.
> * **Example 2 (A `/26` Subnet):** A `/26` divides the network into blocks of 64. If you are in the second block (`192.168.1.64/26`), the network address is `.64` and the broadcast address is `.127`. Only `.65` through `.126` can be assigned to actual devices!

#### IPv4 CIDR Reference Table
*(Note: "Usable IPs" subtracts 2 from the Total IPs to account for the Network Address and the Broadcast Address).*

| CIDR | Subnet Mask | Total IPs | Usable IPs | Common Use Case |
| :--- | :--- | :--- | :--- | :--- |
| **/8** | `255.0.0.0` | 16,777,216 | 16,777,214 | Massive Enterprise Networks (Class A) |
| **/12** | `255.240.0.0` | 1,048,576 | 1,048,574 | Large Internal Networks |
| **/16** | `255.255.0.0` | 65,536 | 65,534 | Mid-Sized Enterprise Networks (Class B) |
| **/20** | `255.255.240.0` | 4,096 | 4,094 | Corporate Departments |
| **/24** | `255.255.255.0` | 256 | 254 | Standard Home/Small Office (Class C) |
| **/25** | `255.255.255.128` | 128 | 126 | Subdivided LAN |
| **/26** | `255.255.255.192` | 64 | 62 | Subdivided LAN |
| **/27** | `255.255.255.224` | 32 | 30 | Small Subnets / Labs |
| **/28** | `255.255.255.240` | 16 | 14 | Small Subnets / Labs |
| **/29** | `255.255.255.248` | 8 | 6 | Micro Subnets |
| **/30** | `255.255.255.252` | 4 | 2 | Point-to-Point Router Links |
| **/31** | `255.255.255.254` | 2 | 2* | Special Point-to-Point Links (RFC 3021) |
| **/32** | `255.255.255.255` | 1 | 1 | A single specific host/device |

### 🏗️ Network Infrastructure & Interface Elements
To help you map these concepts directly to the NetPractice simulation, here is a reference guide to the visual elements you will interact with during the exercises:

| Interface Element | Component & Definition |
| :---: | :--- |
| <img src="https://github.com/user-attachments/assets/8dcdb16c-4992-44c1-b3d2-36a58d41c3b6" alt="Host Device Icon" width="100"/> | **Host (Client Device):** An end-user machine (like a computer) that generates or receives network traffic. |
| <img src="https://github.com/user-attachments/assets/15fc054c-b68f-4ee8-a5f3-8a41e3ec43ee" alt="Network Switch Icon" width="100"/> | **Switch:** Connects devices within a *single* local network (LAN). It uses MAC addresses to forward data only to the specific device that requested it. |
| <img src="https://github.com/user-attachments/assets/764eb094-c712-490e-b760-3f214af257f4" alt="Network Router Icon" width="100"/> | **Router & Gateway:** Connects *multiple* different networks together (e.g., connecting a home LAN to the internet). It reads IP addresses to route packets to their correct destinations. A **Gateway** is a specific interface on a router that acts as an access point to another network. A "Default Gateway" is where a device sends data when the destination IP is not on its own local subnet. |
| <img src="https://github.com/user-attachments/assets/348ef046-d09d-40be-8f56-02ea23715440" alt="Internet Globe Icon" width="100"/> | **Internet (WAN):** Represents external networks outside of your local topology. To reach this, packets must be routed through the local gateway. |
| <img src="https://github.com/user-attachments/assets/92b14dbf-b3fb-452f-800f-1a8e9698453d" alt="Routing Table Screenshot" width="1000"/> | **Routing Table:** A data table stored in a router or networked computer that lists the routes to particular network destinations, dictating exactly where the hardware should send data packets next. |

---

## 🛠️ Instructions

### 📦 Running the Training Interface
Due to technical design and security constraints on various web browsers, a local web server is required to deliver the NetPractice web interface.

1. Download and extract the project files into a folder of your choice.
2. Run the `run.sh` file in your terminal. This shell script will automatically launch a web server and open your preferred web browser to the dedicated interface.
3. Enter your intranet login in the provided field so the Moulinette knows your specific configuration.

**Manual Fallback:**
If the `run.sh` script does not function properly, you can start the project manually:
```bash
python3 -m http.server 49242
```
Then, navigate to `http://localhost:49242` in your web browser.

### 💾 Exporting Configurations
Once you successfully solve a network topology, you must save your progress. Click the **[Get my config]** button located at the top of the interface to download your specific configuration file for that level. *You will need these files for your final submission*.

### 📤 Submission Requirements
To successfully submit and pass this project:
* You must complete all 10 training levels.
* **10 exported configuration files (one per level) must be placed directly at the repository root**.
* During the defense, you will be required to successfully complete three random levels within a limited timeframe without the use of external tools (excluding a simple calculator like `bc`).

---

## 🏆 Level Solutions

<details>
<summary><b><big>Level 1</big></b></summary>
<br>

<div align="center">
  <img src="https://github.com/user-attachments/assets/393424f9-9bf9-4deb-9d4e-11cfc3ebdf5b" alt="Level 1 Solution" width="100%"/>
</div>

### 🔍 Analysis & Solution
**Goal:** Establish direct communication between two isolated pairs of hosts (A ↔ B and C ↔ D).

Because there are no routers or switches involved, these devices are connected point-to-point. For point-to-point hosts to communicate without a gateway, they **must** belong to the exact same subnet.

**Network 1 (Host A ↔ Host B):**
* **The Constraint:** Host B has a fixed IP of `104.95.23.12` and a fixed Subnet Mask of `255.255.255.0` (a `/24` CIDR).
* **The Math:** A `/24` mask means the first three octets (`104.95.23`) represent the Network ID, and the last octet is for the hosts. The network address is `104.95.23.0` and the broadcast is `104.95.23.255`. 
* **The Solution:** Host A must share the exact same network ID. By assigning it `104.95.23.11`, it is placed perfectly within the usable host range of `.1` to `.254`.

**Network 2 (Host C ↔ Host D):**
* **The Constraint:** Host C has a fixed IP of `211.191.60.75` and a fixed Subnet Mask of `255.255.0.0` (a `/16` CIDR).
* **The Math:** A `/16` mask locks only the first *two* octets (`211.191`) for the Network ID. The network address is `211.191.0.0` and the broadcast is `211.191.255.255`.
* **The Solution:** Host D's IP must start with `211.191`. By assigning it `211.191.60.74`, it perfectly aligns with the required subnet.

### 🔄 Alternative Approaches
Since the subnet masks define a broad range of available addresses, the exact IPs chosen above are just one of many correct possibilities!
* **For Host A:** You could have chosen any number for the final octet (except `.0`, `.12`, or `.255`). For example, `104.95.23.1` or `104.95.23.254` would be equally valid and represent standard network design practices.
* **For Host D:** Because it is a `/16` network, you have a massive pool of 65,534 usable IPs. Matching the third octet (`.60`) keeps things visually organized, but an IP like `211.191.1.1` or `211.191.255.254` would have worked identically.

</details>

<details>
<summary><b><big>Level 2</big></b></summary>
<br>

<div align="center">
  <img src="https://github.com/user-attachments/assets/2fc087fe-ea67-4969-af6f-ead4df374890" alt="Level 2 Solution" width="100%"/>
</div>

### 🔍 Analysis & Solution
**Goal:** Establish direct point-to-point communication between two isolated pairs of hosts (A ↔ B and C ↔ D) while ensuring their subnet ranges do not overlap.

**Network 1 (Host A ↔ Host B):**
* **The Constraint:** Host B has a fixed IP of `192.168.149.222` and a fixed Subnet Mask of `255.255.255.224` (a `/27` CIDR).
* **The Math:** A `/27` mask divides the final octet into blocks of 32 (256 - 224 = 32). Counting by 32s (`0`, `32`, `64`... `192`, `224`), we find that the IP `.222` falls squarely in the `.192` block. The network address is `.192` and the broadcast address is `.223`. 
* **The Solution:** The usable IPs for this specific subnet are `.193` through `.222`. Host A must share this exact subnet. By assigning it `192.168.149.221` and matching the `255.255.255.224` mask, the connection is successfully established.

**Network 2 (Host C ↔ Host D):**
* **The Constraint:** Interface D1 explicitly demands a `/30` subnet. The challenge is to design a tiny 4-IP block that **does not conflict** with the `.192` through `.223` address space already consumed by Network 1.
* **The Math:** A `/30` mask translates to `255.255.255.252` in decimal. To safely avoid Network 1, a block at the very end of the available IP range was calculated: starting at the network address `.252` and ending at the broadcast address `.255`.
* **The Solution:** This specific `/30` block yields exactly **two** usable IPs. By assigning `192.168.149.253` to Host D and `192.168.149.254` to Host C, the point-to-point link is completed flawlessly with zero network overlap.

### 🔄 Alternative Approaches
* **For Network 1 (Host A):** You had plenty of wiggle room here. You could have chosen any IP between `192.168.149.193` and `192.168.149.220` to successfully connect to Host B.
* **For Network 2 (Host C & D):** Because you were designing this subnet from scratch, you had many valid options! Any `/30` block entirely outside of the `.192`–`.223` range would have been correct. For example, using the very first block (`.0` network, `.3` broadcast) would have allowed you to validly assign `.1` and `.2` to these hosts.

</details>

<details>
<summary><b><big>Level 3</big></b></summary>
<br>

<div align="center">
  <img src="https://github.com/user-attachments/assets/d78fa370-94e1-4511-9fcd-247be78c9a13" alt="Level 3 Solution" width="100%"/>
</div>

### 🔍 Analysis & Solution
**Goal:** Establish direct communication between three hosts (A, B, and C) connected through a single switch.

Because switches operate strictly at Layer 2 (Data Link) and do not route traffic between different networks, any device connected to the same switch **must** belong to the exact same subnet to communicate.

**The Local Area Network (Hosts A, B & C):**
* **The Constraints:** Interface C1 has a fixed Subnet Mask of `255.255.255.128` (a `/25` CIDR). Interface A1 has a fixed IP of `104.198.185.125`.
* **The Math:** A `/25` mask divides the final octet into exactly two blocks of 128 (256 - 128 = 128):
  * *Block 1:* `.0` to `.127`
  * *Block 2:* `.128` to `.255`
* **Finding the Subnet:** We must look at Host A's fixed IP (`.125`) to determine which block the network belongs to. Since `.125` falls into the first block, the entire switch's network address is `104.198.185.0`, and its broadcast address is `104.198.185.127`.
* **The Solution:** The usable IP range for this entire switch is `.1` through `.126`. To complete the level, we simply apply the mandatory `255.255.255.128` mask to Hosts A and B, and assign valid, non-overlapping IPs to B and C from the available pool. In this case, Host C is assigned `.124` and Host B is assigned `.126`.

### 🔄 Alternative Approaches
* **For the Subnet Masks:** There are **zero** alternatives. Because the hosts share a Layer 2 switch and Host C's mask is fixed at `/25`, every single device on this switch must adopt the `255.255.255.128` mask.
* **For Host B & Host C IPs:** You had a wide pool of options! Any unique IP between `104.198.185.1` and `104.198.185.126` (excluding A's fixed `.125`) would have worked perfectly. You chose to cluster them neatly at the top of the range (`.124` and `.126`), but you could have just as easily used `.1` and `.2`.

</details>

<details>
<summary><b><big>Level 4</big></b></summary>
<br>

<div align="center">
  <img src="https://github.com/user-attachments/assets/19af61a9-b9d2-4da4-879d-11691ee10226" alt="Level 4 Solution" width="100%"/>
</div>

### 🔍 Analysis & Solution
**Goal:** Establish communication between Hosts A, B, and Router R via the switch. Because a single router is involved, we must adhere to a strict routing rule: **a router cannot have overlapping subnets assigned to its different interfaces**. 

**The Local Area Network (Switch S connecting A1, B1, and R1):**
* **The Constraints:** 
  * Router interface **R2** is fixed at `103.68.118.1` with a `/25` mask (`255.255.255.128`). This claims the entire `103.68.118.0` to `.127` address block.
  * Router interface **R3** is fixed at `103.68.118.244` with a `/26` mask (`255.255.255.192`). This claims the entire `103.68.118.192` to `.255` address block.
  * Interface **A1** has a fixed IP of `103.68.118.132`.
* **The Math:** To avoid overlapping with R2 and R3, the switch's network must fit entirely within the remaining gap: **`.128` through `.191`**. We need to find the most efficient subnet mask for A1 that includes its fixed `.132` IP without spilling out of this safe zone.
* **The Solution:** A mask of `255.255.255.248` (a `/29` CIDR) restricts the network to the absolute bare minimum required for three devices. It divides the network into tiny blocks of 8 (256 - 248 = 8). The block containing `.132` starts at `.128` and ends at `.135`. This perfectly clears the restricted zones with mathematical precision! 
  * Network Address: `.128`
  * Broadcast Address: `.135`
  * Usable IP Range: `.129` through `.134` (6 usable IPs)

By applying the strict `255.255.255.248` mask to A1, B1, and R1, the local network is isolated. The level is solved by assigning B1 and R1 available IPs from that block (in this case, `.131` and `.130`).

### 🔄 Alternative Approaches
* **For the Subnet Masks:** While `/29` proves an elite understanding by locking the network down to its tightest possible configuration (since a `/30` only gives 2 IPs, and you need 3), you had a few broader valid choices. You could have used a `/28` (`255.255.255.240`), a `/27` (`255.255.255.224`), or even maximized the gap with a `/26` (`255.255.255.192`). Any of these would successfully cover `.132` without conflicting with R2 or R3.
* **For R1 & B1 IPs:** Using the chosen `/29` mask, you had exactly 6 usable IPs. You chose `.130` and `.131`, leaving `.129`, `.133`, and `.134` as your only other mathematically valid alternatives.

</details>

<details>
<summary><b><big>Level 5</big></b></summary>
<br>

<div align="center">
  <img src="https://github.com/user-attachments/assets/d32881cd-9b6a-419d-b3d4-539a954dfbda" alt="Level 5 Solution" width="100%"/>
</div>

### 🔍 Analysis & Solution
**Goal:** Establish cross-network communication. This is the first level where hosts reside on completely different subnets, meaning they can no longer communicate point-to-point. They must rely on their routing tables to forward traffic to their respective "Default Gateways" (the router interfaces). 

This solution deliberately tests the absolute mathematical limits of both subnets to demonstrate strict CIDR comprehension.

**Network 1 (Host A ↔ Router R1):**
* **The Constraint:** Router interface **R1** has a fixed IP of `85.15.238.126` and a fixed mask of `255.255.255.128` (a `/25` CIDR).
* **The Math:** A `/25` mask divides the final octet into two blocks of 128. The IP `.126` falls into the first block (Network Address `.0`, Broadcast Address `.127`). The valid range is `.1` to `.126`.
* **The Solution:** To test the lower boundary, Host A is assigned `85.15.238.1` — the very first usable IP in this subnet block. 

**Network 2 (Host B ↔ Router R2):**
* **The Constraint:** Router interface **R2** has a fixed IP of `133.158.128.254` and a fixed mask of `255.255.192.0` (a `/18` CIDR).
* **The Math:** A `/18` mask divides the *third* octet into blocks of 64 (256 - 192 = 64). Counting by 64s (`0`, `64`, `128`, `192`), we see that `.128` is the exact starting point of the third block. 
  * Network Address: `133.158.128.0`
  * Broadcast Address: `133.158.191.255`
* **The Solution:** To test the upper boundary, Host B is assigned `133.158.191.254` — the absolute highest usable IP possible before hitting the broadcast address.

**Routing Tables:**
* **Host B:** The destination is fixed as `default`. A default route acts as a catch-all for any traffic leaving the local network. The "Next Hop" (gateway) must be the router interface connected to this subnet. Thus, the route points to R2: `133.158.128.254`.
* **Host A:** To send packets to Host B, Host A must pass them to its own gateway. The destination is set directly to Host B's IP and subnet (`133.158.191.254/18`), and the gateway is set to R1 (`85.15.238.126`).

### 🔄 Alternative Approaches
* **For Host A & B IPs:** You could have picked any arbitrary numbers in the middle (e.g., `85.15.238.50` and `133.158.130.100`), but pushing the IPs to their absolute minimum and maximum limits (`.1` and `.191.254`) is a fantastic way to prove you fully grasp subnet math to an evaluator.
* **For Host A's Routing Table:** Instead of pointing to the specific destination IP of Host B, you could have simply used the word `default` here just like Host B did. Because Host A only has one path out (via R1), sending *all* unknown traffic to R1 is standard practice. Additionally, writing the strict network ID (`133.158.128.0/18`) instead of the host IP in the destination field would also be perfectly valid.

</details>

<details>
<summary><b><big>Level 6</big></b></summary>
<br>

<div align="center">
  <img src="https://github.com/user-attachments/assets/2a915c88-7b9c-4368-9f1c-87f4a7c00cdb" alt="Level 6 Solution" width="100%"/>
</div>

### 🔍 Analysis & Solution
**Goal:** Route traffic between a local web server (Host A) and an external network ("Somewhere on the Net") via a router, demonstrating how default routes and return path routes function together.

Using `0.0.0.0/0` instead of the `default` keyword explicitly proves that you understand standard CIDR notation for quad-zero default gateway routes.

**The Local Area Network (Host A ↔ Router R1):**
* **The Constraints:** Interface **A1** has a fixed IP of `82.100.104.227`. Interface **R1** has a fixed Subnet Mask of `255.255.255.128` (a `/25` CIDR).
* **The Math:** A `/25` mask splits the final octet into two blocks of 128 (`.0`–`.127` and `.128`–`.255`). 
  * Because Host A's fixed IP is `.227`, the network ID for this LAN is mathematically locked to `82.100.104.128/25`.
  * Usable IP Range: `82.100.104.129` through `82.100.104.254`.
* **The Solution:** Set A1's mask to `255.255.255.128` to match R1. Router interface R1 is assigned `82.100.104.228`, placing it inside Host A's subnet.

**The WAN Link (Router R2 ↔ Internet):**
* **The Constraints:** Interface **R2** is fixed at `163.172.250.12` with a `/28` mask (`255.255.255.240`). Router R's next hop is fixed to `163.172.250.1`.

**Routing Configuration:**
* **Host A Route (`0.0.0.0/0` => `82.100.104.228`):** Host A uses `0.0.0.0/0` (the default route) to forward all outbound internet traffic directly to its local gateway interface (R1).
* **Router R Route (`0.0.0.0/0` => `163.172.250.1`):** Router R uses `0.0.0.0/0` to pass all unknown destination packets out through its WAN port to the Internet gateway.
* **Internet Route (`82.100.104.128/25` => `163.172.250.12`):** For two-way communication to work, the Internet must know where to send response packets. The destination is set to encompass the **entire LAN subnet** (`82.100.104.128/25`), directing traffic back to Router R's public interface R2 (`163.172.250.12`).

### 🔄 Alternative Approaches
* **Default Route Syntax:** You used `0.0.0.0/0` on Host A and Router R, which is standard CIDR notation for a default gateway route. Simply writing `default` in those fields yields the exact same result in NetPractice.
* **Internet Routing Destination:** Instead of specifying the full subnet block (`82.100.104.128/25`), you could have targeted Host A specifically using `82.100.104.227/32` or `82.100.104.227/25`. However, routing the full `/25` subnet block is best networking practice because it allows *any* future host added to that switch to receive return traffic without modifying the Internet's routing table!
* **Router R1 IP:** Any unique IP between `82.100.104.129` and `82.100.104.254` (except `.227`) would have worked for R1.

</details>

<details>
<summary><b><big>Level 7</big></b></summary>
<br>

<div align="center">
  <img src="https://github.com/user-attachments/assets/4475ea6a-e471-42fc-bdb6-773fbd2634fe" alt="Level 7 Solution" width="100%"/>
</div>

### 🔍 Analysis & Solution
**Goal:** Establish multi-hop communication between Host A and Host C across two interconnected routers.

This topology consists exclusively of point-to-point connections (Host-to-Router and Router-to-Router). The most efficient and professional way to handle point-to-point links is by assigning a `/30` subnet mask to every interface, which provides exactly two usable IPs per block and prevents IP waste.

**Network 1 (Host A ↔ Router R1):**
* **The Constraint:** Router interface **R11** has a fixed IP of `108.198.14.1`.
* **The Solution:** Applying a `/30` mask locks this into the `.0` block (Network `.0`, Broadcast `.3`). Since `.1` is taken by R11, Host A is mathematically forced to take `108.198.14.2`.

**Network 2 (Router Link R1 ↔ R2):**
* **The Constraint:** Router interface **R12** has a fixed IP of `108.198.14.254`.
* **The Solution:** Applying a `/30` mask places this in the very last block of the octet (Network `.252`, Broadcast `.255`). With R12 taking `.254`, interface R21 is successfully assigned the other usable address: `108.198.14.253`.

**Network 3 (Host C ↔ Router R2):**
* **The Constraint:** We must design a third `/30` block that does not overlap with the `.0` or `.252` blocks.
* **The Solution:** You selected the `.248` block (Network `.248`, Broadcast `.251`). Interface R22 is assigned `108.198.14.249` and Host C is assigned `108.198.14.250`.

**Routing Tables:**
* **Host A:** Directs traffic destined for Host C's specific subnet (`108.198.14.248/30`) to its local gateway, R11 (`108.198.14.1`).
* **Routers R1 & R2:** Both routers use standard default routes (`0.0.0.0/0`) to continuously forward unknown traffic to each other across their shared `.252/30` link.
* **Host C:** Uses a precise route of `108.198.14.0/30` to send return traffic directly to Host A's specific subnet via its local gateway, R22 (`108.198.14.249`).

### 🔄 Alternative Approaches
* **Network 3 Subnet:** Choosing the `.248/30` block was a great way to keep the IPs clustered near the upper limits, but you had complete freedom here. Any available `/30` block (such as `.4/30`, `.8/30`, or `.12/30`) would have worked flawlessly.
* **Host Routing Tables:** 
  * By explicitly defining the exact destination subnets (`108.198.14.248/30` and `108.198.14.0/30`), you demonstrated a strict and highly secure routing configuration. 
  * Alternatively, because each host only has one single path out of its local network, you could have simply used `default` or `0.0.0.0/0` in both Host A and Host C's routing tables to achieve the same result.

</details>

<details>
<summary><b><big>Level 8</big></b></summary>
<br>

<div align="center">
  <img src="https://github.com/user-attachments/assets/dc28b6d1-95c7-4287-9a04-f4f9ebf766b2" alt="Level 8 Solution" width="100%"/>
</div>

### 🔍 Analysis & Solution
**Goal:** Route traffic from internal hosts (C and D) to each other and to the external Internet via a multi-router setup, adhering to a predefined supernet route. 

This level is a brilliant exercise in **VLSM (Variable Length Subnet Masking)**. You are given a large block of IP addresses and must mathematically carve it up into smaller subnets to satisfy the router constraints.

**The Master Constraint (The `/26` Supernet):** 
* The Internet's routing table dictates that all traffic destined for `155.233.33.0/26` must be sent into our local network. 
* A `/26` subnet spans from `.0` to `.63`. Therefore, every single internal interface under R1 (R13, R21, R22, R23, C1, and D1) **must** be configured using IPs that fall within this `.0` to `.63` range, divided into smaller non-overlapping blocks.

**Network 1 (Router Link R1 ↔ R2):**
* **The Constraint:** Router R2 has a fixed next-hop of `155.233.33.62` for its default route. 
* **The Math:** We need a subnet mask that encompasses `.62` but doesn't consume the entire `/26` supernet. A `/28` mask (`255.255.255.240`) divides the space into blocks of 16. The block from `.48` to `.63` perfectly fits this requirement!
* **The Solution:** Interface R13 is assigned the required `.62`. Interface R21 is assigned `155.233.33.49`. R1's routing table is then updated to forward the `/26` supernet traffic to R21 (`.49`).

**Network 2 (Host D ↔ Router R2):**
* **The Constraint:** Interface D1 has a fixed subnet mask of `255.255.255.240` (`/28`).
* **The Solution:** We assign this network the very first `/28` block of our available supernet: `.0` to `.15`. Host D1 is assigned `155.233.33.1` and its gateway interface (R23) is assigned `155.233.33.14`.

**Network 3 (Host C ↔ Router R2):**
* **The Solution:** We need one more `/28` block for Host C. The `.16` to `.31` block is available, but you strategically chose the `.32` to `.47` block. Host C1 is assigned `155.233.33.33` and its gateway interface (R22) is assigned `155.233.33.46`.

**The WAN Link & Routing:**
* **Internet to R1:** R12 has a fixed IP/Mask of `163.170.250.12/28`. The Internet uses this IP as the next-hop for the `155.233.33.0/26` supernet.
* **R1 to Internet:** Router R1 uses a default route (`0.0.0.0/0`) pointing to `163.170.250.1` (the presumed gateway of the WAN's `.0/28` block) to handle all outbound external traffic.
* **Hosts C & D:** Both hosts use standard default routes (written as either `default` or `0.0.0.0/0`) pointing to their respective local R2 gateway IPs (`.46` and `.14`).

### 🔄 Alternative Approaches
* **Subnetting the Supernet:** Because the `/26` supernet gave you four distinct `/28` blocks to play with (`.0`, `.16`, `.32`, and `.48`), you had flexibility. While the R1-R2 link *had* to be the `.48` block (to include the fixed `.62` constraint), Hosts C and D could have used any of the remaining three blocks. You could have easily placed Host C in the `.16/28` block instead of `.32/28`.
* **Host Routing:** Using `default` on Host D and `0.0.0.0/0` on Host C is a great touch to visually demonstrate to the evaluator that both syntax commands execute the exact same logic within the routing table.

</details>

<details>
<summary><b><big>Level 9</big></b></summary>
<br>

<div align="center">
  <img src="https://github.com/user-attachments/assets/c46720cd-46a3-4a2b-9c80-6d7af77fed1f" alt="Level 9 Solution" width="100%"/>
</div>

### 🔍 Analysis & Solution
**Goal:** Establish multi-way communication across a complex topology involving four hosts (A: *meson*, B: *ion*, C: *cation*, D: *gluon*), two routers (R1: *proton*, R2: *boson*), and an external Internet node. 

Level 9 is widely considered the hardest challenge in NetPractice because it forces you to manage **three completely separate network domains simultaneously** while adhering to strict fixed routes on the Internet node and internal routers.

**Network Domain 1: The Local LAN (Switch S connecting Host A, Host B & R11):**
* **The Constraints:** Interface **R11** has a fixed mask of `255.255.255.128` (`/25`). Interface **R12** on the same router has a fixed IP/Mask of `163.172.250.12/28` (claiming `.0` to `.15`).
* **The Internet Requirement:** The Internet's routing table has a fixed route directing `163.172.250.128/25` to R12 (`163.172.250.12`).
* **The Math:** To satisfy the Internet's fixed route without overlapping with R12's `.0/28` WAN link, interface R11 must sit inside the `163.172.250.128/25` block (`.128` to `.255`).
* **The Solution:** 
  * Apply `255.255.255.128` (`/25`) across R11, A1, and B1.
  * Assign R11 `163.172.250.129` (acting as the default gateway for the switch).
  * Assign Host B (`ion`) `163.172.250.130` and Host A (`meson`) `163.172.250.131`. Both hosts set their default route (`0.0.0.0/0`) to R11 (`163.172.250.129`).

**Network Domain 2: The Router Interconnect (R13 ↔ R21):**
* **The Constraints:** Both **R13** and **R21** have fixed masks of `255.255.255.252` (`/30`).
* **The Solution:** A `/30` mask yields a 4-IP block (2 usable). Selecting the `.16/30` block (`.16` to `.19`):
  * **R13:** Assigned `163.172.250.17`
  * **R21:** Assigned `163.172.250.18`
* **Router R2 Configuration:** Router R2 (`boson`) points its default route (`0.0.0.0/0`) directly to R13 (`163.172.250.17`).

**Network Domain 3: The Supernetting Challenge (Hosts C & D under Router R2):**
* **The Internet Requirements:** The Internet has two additional fixed routes:
  1. `31.168.0.0/18` => `163.172.250.12`
  2. `31.168.192.0/18` => `163.172.250.12`
* **The Subnet Math (`/18` CIDR):** A `/18` mask (`255.255.192.0`) divides the third octet into blocks of 64 (`.0`, `.64`, `.128`, `.192`).
  * **Block A (`31.168.0.0/18`):** Spans `31.168.0.0` to `31.168.63.255`.
  * **Block B (`31.168.192.0/18`):** Spans `31.168.192.0` to `31.168.255.255`.
* **Assigning Subnets to Hosts C & D:**
  * **Host D (`gluon`):** Interface D1 requires a `/18` mask. Placing it in **Block A**, interface D1 is assigned `31.168.0.1` and its gateway interface (R23) is assigned `31.168.45.120`. Host D sets its gateway route to `.45.120`.
  * **Host C (`cation`):** Interface C1 requires a `/18` mask. Placing it in **Block B**, interface R22 is assigned `31.168.192.1` and interface C1 is assigned `31.168.255.254`. Host C sets its default route to R22 (`31.168.192.1`).

**The Grand Routing Table Assembly:**
* **Router R1 (`proton`):** R1 acts as the central traffic hub. It already has its WAN default route (`0.0.0.0/0` => `163.172.250.1`) configured. To route inbound Internet traffic down to Hosts C and D, we add two static routes pointing to R21 (`163.172.250.18`):
  1. `31.168.0.0/18` => `163.172.250.18`
  2. `31.168.192.0/18` => `163.172.250.18`

### 🔄 Alternative Approaches
* **Host C & D Subnet Assignment:** You could have easily swapped the block assignments between Hosts C and D. Assigning Host C to `31.168.0.0/18` and Host D to `31.168.192.0/18` would be 100% mathematically valid, as long as both `/18` ranges are accounted for under Router R2.
* **IP Selection within `/18` Blocks:** Because a `/18` network provides 16,382 usable IP addresses per block, your specific IP choices (like `31.168.45.120` or `31.168.255.254`) leave thousands of valid alternatives. Your choice to pick boundary and arbitrary mid-range IPs proves complete mastery of large-block subnet calculations.

</details>

<details>
<summary><b><big>Level 10</big></b></summary>
<br>

<div align="center">
  <img src="https://github.com/user-attachments/assets/d3a43128-33dc-4036-87bc-28f0990a8f73" alt="Level 10 Solution" width="100%"/>
</div>

### 🔍 Analysis & Solution
**Goal:** Achieve total network interconnectivity across four internal hosts, two routers, and the external Internet in a highly restricted topology where most IPs, subnets, and routes are hardcoded.

The key to solving this final puzzle is working backward from the fixed constraints to deduce the only mathematically valid subnet layouts.

**1. The R1-R2 Router Link (`/30`):**
* **The Constraint:** Interface R21 is hardcoded to `155.84.183.253/30` (Network `.252`, Broadcast `.255`). 
* **The Solution:** Interface R13 has a fixed IP of `155.84.183.254`. By simply updating its mask to match R21 (`255.255.255.252`), the inter-router link is successfully established.

**2. Network 1 (Switch S1 - Hosts 1 & 2):**
* **The Constraint:** Router interface R11 is fixed at `155.84.183.1/25`. This claims the entire first half of the subnet (`.0` to `.127`). Host H11 has a fixed IP of `.2`.
* **The Solution:** 
  * Update Host H11's mask to `/25` (`255.255.255.128`).
  * Configure Host H21 with any available IP in that same block. You selected `155.84.183.126/25`.

**3. Network 2 (Host 4 via R23):**
* **The Constraint:** Host H41 is hardcoded to `155.84.183.131/26`, and its routing table rigidly sets its gateway to `155.84.183.129`. Furthermore, Router R1's routing table has a fixed entry dictating that all traffic for `155.84.183.128/26` must be forwarded to R2.
* **The Solution:** Because H4 demands `.129` as its gateway, Router interface R23 **must** be assigned the IP `155.84.183.129` and the matching `/26` mask (`255.255.255.192`). This perfectly fills the `.128` to `.191` block.

**4. Network 3 (Host 3 via R22) - The Missing Block:**
* **The Constraint:** We need a subnet for Host 3. Looking at what we've used:
  * `.0` – `.127` (Used by Network 1)
  * `.128` – `.191` (Used by Network 2)
  * `.252` – `.255` (Used by Router Link)
  * This leaves a strict gap from **`.192` to `.251`**.
* **The Solution:** You elegantly carved out a `/27` subnet (`255.255.255.224`), which claims `.192` through `.223`. 
  * You updated R1's configurable route to forward `155.84.183.192/27` to R2.
  * You assigned R22 the IP `155.84.183.193/27` and Host H31 the IP `155.84.183.222/27`.
  * Finally, you updated Host H3's next-hop route to point to R22 (`155.84.183.193`).

**5. The Internet Supernet:**
* **The Constraint:** The Internet needs a single destination route to send return traffic to all of these disjointed subnets.
* **The Solution:** Because all of our subnets (`.0/25`, `.128/26`, `.192/27`, and `.252/30`) start with `155.84.183`, they can all be summarized into one massive `/24` supernet. By configuring the Internet's destination to `155.84.183.0/24`, it acts as a master catch-all route, successfully completing the project!

### 🔄 Alternative Approaches
* **Network 3 Subnet Size:** While you chose a `/27` for Network 3 (providing 30 usable IPs), the available gap (`.192` to `.251`) was large enough that you could have technically used a `/26` (which would perfectly claim `.192` to `.255`, though it would overlap with the router link if not careful) or a tighter `/28` (`.192` to `.207`). 
* **Host IP Selection:** Just as in previous levels, your specific IP choices for H21 (`.126`) and H31 (`.222`) were beautifully clustered near the end of their respective broadcast limits, but any valid IP within their specific blocks would have worked.

</details>

---

## 📚 Resources & References

### General Networking Fundamentals
* **[Computer Networking Complete Course (YouTube)](https://www.youtube.com/playlist?list=PLDQaRcbiSnqF5U8ffMgZzS7fq1rHUI3Q8):** A comprehensive video series covering everything from basic network topologies to advanced routing protocols.
* **[Introduction to Networking (Zero To Mastery)](https://zerotomastery.io/blog/introduction-to-networking/):** A beginner-friendly breakdown of what networks are, how the internet works, and core networking terminology.
* **[Basics of Computer Networking (GeeksforGeeks)](https://www.geeksforgeeks.org/computer-networks/basics-computer-networking/):** A quick-reference text guide defining key network devices, types (LAN/WAN), and standard network topologies.
* **[Network Types and Topologies (Microsoft Learn)](https://learn.microsoft.com/en-us/training/modules/network-fundamentals/2-network-types-topologies):** Microsoft's official module on distinguishing between LANs, WANs, and how physical networks are structured.
* **[Network Infrastructure (Microsoft Learn)](https://learn.microsoft.com/en-us/training/modules/network-fundamentals/3-network-infrastructure):** A deep dive into the hardware components of a network, specifically explaining the roles of switches, routers, and gateways.
* **[Network Protocols (Microsoft Learn)](https://learn.microsoft.com/en-us/training/modules/network-fundamentals/4-network-protocols):** A conceptual overview of how data is formatted and transmitted, focusing on the OSI model and standard communication rules.
* **[IP & TCP Basics (Microsoft Learn)](https://learn.microsoft.com/en-us/training/modules/network-fundamentals/5-ip-tcp-basics):** A focused lesson on Layer 3 and Layer 4 routing, detailing how IP addresses and TCP/UDP ports function together.

### NetPractice Specific Guides
* **[NetPractice: An Intro to IP Addresses and Subnets (YouTube)](https://www.youtube.com/watch?v=HQUw0CfQWAM):** A direct, visual walkthrough of the 42 NetPractice training interface and strategies for tackling the routing challenges.
* **[toufa7 - NetPractice Guidelines (Medium)](https://toufa7.medium.com/netpractice-guidelines-6341b8309f38):** A strategic breakdown of the project requirements, including subnetting math and common pitfalls to avoid.
* **[Mohamed Amin Tarza - From Zero to Network Hero: A Practical Guide to NetPractice (Medium)](https://medium.com/@mohamedamintarza/from-zero-to-network-hero-a-practical-guide-to-netpractice-1337-rabat-a2ffb614a928):** A comprehensive guide connecting general networking theory directly to the specific exercises found in the NetPractice module.
* **[imyzf - NetPractice Deep Dive (Medium)](https://medium.com/@imyzf/netpractice-2d2b39b6cf0a):** A detailed exploration of IP addressing, CIDR notation, and network troubleshooting tailored for the 42 curriculum.

---

### 🤖 AI Usage & Transparency
In alignment with the pedagogical guidelines of this curriculum, AI tools were utilized strictly as a learning accelerator and not to bypass problem-solving:

* **Concept Clarification:** AI was used to provide varied technical explanations and analogies for abstract concepts like the OSI model layers and the mathematical breakdown of CIDR notation / subnet masking.
* **Documentation Formatting:** AI assisted in structuring this `README.md` to ensure it met all curriculum requirements while maintaining a clear, professional layout.
* **Zero Solution Generation:** All 10 NetPractice levels were solved manually through trial, error, and peer review. No configurations or network routing tables were generated by AI, ensuring complete responsibility and technical understanding for the defense.
