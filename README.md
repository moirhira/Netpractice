# 🌐 Netpractice — Networking Fundamentals

> A comprehensive reference guide covering networking concepts from the ground up: interfaces, IP addressing, subnetting, OSI layers, and more.

---

## 📋 Table of Contents

- [Core Concepts](#core-concepts)
- [IP Addressing](#ip-addressing)
- [Subnetting](#subnetting)
- [Network Devices](#network-devices)
- [OSI Model](#osi-model)
- [IPv4 vs IPv6](#ipv4-vs-ipv6)
- [Transmission Types](#transmission-types)
- [Routing & Gateways](#routing--gateways)
- [Practice Hints](#practice-hints)

---

## Core Concepts

### Interface
An **interface** is a point of interaction between components or objects that enables communication and data sharing — like a CLI (`$`, `>`) or GUI.

| Interface Type | Description |
|----------------|-------------|
| **CLI** | Command-line interface for communicating with computers via commands |
| **GUI** | Graphical interface using mouse and windows (less control) |

### NIC (Network Interface Card)
- A **NIC** is a hardware component (or software interface) connecting a device to a network
- Each NIC has a unique **MAC address** (48-bit physical address)
- Used in the **Data Link layer** of the OSI model

---

## IP Addressing

### Structure
- An IP address is a **unique identifier** for a device on a network
- Contains **two parts**: network bits + host bits
- Each IP address has a corresponding **subnet mask**
- Length: **32 bits** (IPv4)

### Example

```
192.168.255.0
192.168.255.255  (inclusive range)
192.168.0.0/16   → 1 network address + host addresses
```

### Key Terms

| Term | Meaning |
|------|---------|
| **Network Address** | First IP in a subnet (identifies the network) |
| **Broadcast Address** | Last IP in a subnet (sends to all hosts) |
| **Host Address** | Any IP between network and broadcast |
| **Prefix Length** | `/24`, `/16`, etc. — number of network bits |

---

## Subnetting

Subnetting = **taking one network and dividing it into Sub-networks.**

### Attributes of a Subnet

1. **Network IP** — First IP in each sub-network  
2. **Broadcast IP** — Last IP after the network address  
3. **Last host IP** — IP address before broadcast  
4. **First host IP** — IP address after the network address  
5. **Next Sub-network** — IP address before broadcast + 1  
6. **# of IP addresses** — depends on subnet size  

### CIDR/Subnet Conversion

```
converting between subnet mask/CIDR
```

### Calculating Subnets

```bash
# Example: 192.0.0/16
# subnet is a multiple of 2
# sub not in range of 200 → the result 2^n ≥ 200
# so 2^8 = 256 → mask = /24 → 192.0.0.0/24

# network address: change host bits to 0
# prefix length → go to host bits → change to 0 → convert to decimal
# example: 192.168.1.0 → /24 → mask = 255.255.255.0
```

### Number of Hosts per Subnet

```
2^(host bits) - 2 = usable hosts
e.g., /24 → 2^8 - 2 = 254 hosts
```

---

## Network Devices

### Hub
- Connects devices in a **LAN (wired)**
- Sends data to **all** connected devices (broadcast)
- Operates at **Physical layer**

### Switch
- Connects devices also in a **LAN**
- Sends data to the **exact destination** using MAC address
- **Smarter** than a hub — stores a MAC address table

### Router
- Connects **internal network** to **outside/internet**
- Has a **local (private) IP** and a **public IP**
- Routes packets using IP addresses and a **routing table**

### Gateway
- The **gateway is always the first interface** of the router
- Has its **own local interface IP**
- Routes outbound traffic toward the correct network

---

## OSI Model

The OSI model has **7 layers**, activated by the IEEE to make communication smooth. The difference between layers is the **unit of data**.

| Layer | Name | Function |
|-------|------|----------|
| 7 | **Application** | Indicates the protocol to use (HTTP, FTP, SMTP) |
| 6 | **Presentation** | Takes data, formats, encrypts using TLS, compresses |
| 5 | **Session** | Handles transmission order and manages the session |
| 4 | **Transport** | Segments data, assigns port number, determines protocol (TCP/UDP) |
| 3 | **Network** | Logical addressing — adds receiver/sender IP, handles routing |
| 2 | **Data Link** | Frames data, adds MAC address, error detection & correction |
| 1 | **Physical** | Transforms frames into physical signals (electrical, fiber, radio) |

### Transport Layer — TCP vs UDP

```
TCP  → connection-oriented, reliable, slower
UDP  → connectionless, faster, no guarantee
```

---

## IPv4 vs IPv6

### Global IPv4 Summary

- **Public IPs are unique worldwide** — no two devices share the same public IP globally
- Managed by **IANA** (Internet Assigned Numbers Authority) and **RIRs** (ARIN, RIPE, etc.)
- **ISPs** assign IP blocks from RIRs and allocate IPs to customers
- IPs are **free** — only ISPs pay for large allocations

### Getting a Public IP

When a company/ISP wants internet access, they request an IP block from their RIR.
> Example: `151.36.125.0/24` → 254 usable IPs assigned to the ISP

### Creating Subnetworks
Each subnet one company uses becomes a smaller block within the larger allocation.

### Devices Connecting to the Internet

```
[Internal]
Private IP (e.g., 192.168.22) → Assigned by ISP or RIR

[Router]
1. Public IP  (e.g., 212.93.22) → Assigned by ISP or RIR
```

### NAT (Network Address Translation)
- When a device makes an internet request, the router translates its **private IP → public IP**
- There is **one way** to do NAT, but it is the most used and supported approach:
  - All devices request with different **port numbers**

---

## Transmission Types

| Type | Description |
|------|-------------|
| **Unicast** | One-to-one |
| **Multicast** | One-to-many (specific group) |
| **Broadcast** | One-to-all |
| **Peer-to-peer** | No centralized device — devices can be client & server simultaneously |
| **Unidirectional** | Data flows one direction at a time |
| **Bidirectional** | Data flows in both directions simultaneously |

### Full-duplex vs Half-duplex

```
Full-duplex   → both directions at same time
Half-duplex   → one direction at a time (e.g., walkie-talkie)
Client/Server → one server provides services to multiple clients
```

---

## Routing & Gateways

### How Routing Works

1. A packet arrives at a router
2. Router checks the **destination IP**
3. Looks up its **routing table** to find the best route
4. Forwards the packet to the next hop

### Default Route

```
0.0.0.0/0  →  sends all unknown traffic to this gateway
```

### Routing Table Fields

| Field | Description |
|-------|-------------|
| Destination | Target network/host |
| Gateway | Next hop address |
| Interface | Which interface to use |
| Metric | Cost/priority of the route |

---

## Practice Hints

### Level 10
> Take the R2 IP and submit it into all the networks with `/28`.

### Level 1
> Take the R2 IP and submit it into all the other networks with `/28`.

### Level 9
> Take the IP for `rT1`, find the host and a point to point R2 and enable a new network in `c1` LAN.

---

## 🗺️ Network Topology Types

| Topology | Description |
|----------|-------------|
| **Bus** | All devices share one line |
| **Ring** | Devices connected in a circle |
| **Star** | All devices connect to a central switch |
| **Mesh** | Every device connects to every other |
| **Tree** | Hierarchical star topology |
| **Hybrid** | Combination of topologies |
| **Daisy chain** | Devices connected in sequence (common use: switch) |

---

## 📡 DHCP

> A server that provides the service of assigning IP addresses to devices connected to the network. The router is usually the DHCP server. When a device connects to the network, the DHCP server assigns it a private address for the local LAN.

---

## DNS

> The translation between the user and the computer — the browser translates **domain names → IP addresses**.  
> The user enters the domain name → DNS resolves it to an IP at the physical layer (bottom of OSI model).

---

## Resources

- [Subnetting Practice](https://subnettingpractice.com)
- [Visual Subnet Calculator](https://www.davidc.net/sites/default/subnets/subnets.html)
- [OSI Model Reference](https://www.cloudflare.com/learning/ddos/glossary/open-systems-interconnection-model-osi/)
- [IPv4 vs IPv6 Explained](https://www.avast.com/c-ipv4-vs-ipv6-addresses)
