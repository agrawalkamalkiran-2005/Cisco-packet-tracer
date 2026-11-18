
<div align="center">

# Cisco Packet Tracer – Networking Simulations

![Cisco Packet Tracer](https://img.shields.io/badge/Cisco-Packet%20Tracer-1BA0D7?style=for-the-badge&logo=cisco&logoColor=white)
![Simulations](https://img.shields.io/badge/Simulations-7-00c853?style=for-the-badge)
![Subject](https://img.shields.io/badge/Computer-Networks-7048e8?style=for-the-badge)

### Build it. Ping it. Break it. Fix it.

A collection of seven Cisco Packet Tracer networking simulations covering fundamental networking concepts, router configuration, network services, and static routing.

</div>

---

## Table of Contents

1. [Overview](#overview)
2. [Technologies Used](#technologies-used)
3. [Repository Structure](#repository-structure)
4. [Simulations](#simulations)
5. [Getting Started](#getting-started)
6. [How to Test](#how-to-test)
7. [Author](#author)

---

## Overview

This repository contains practical implementations of computer networking concepts using Cisco Packet Tracer.

The simulations demonstrate how different network topologies operate, how routers and switches communicate, how network services are configured, and how devices exchange data across multiple networks.

The project is intended for students and beginners who want hands-on experience with computer networking and Cisco Packet Tracer.

---

## Technologies Used

- **Cisco Packet Tracer:** Network simulation and configuration.
- **Cisco IOS CLI:** Router configuration and command execution.
- **Networking Protocols:** DHCP, DNS, HTTP, FTP, SMTP, POP3.
- **Routing:** Static routing and multi-router communication.
- **IP Addressing:** IPv4 addressing and subnetting.

---

## Repository Structure

```text
Cisco-Packet-Tracer-Networking/
│
├── simulations/
│   ├── 01-network-topologies.pkt
│   ├── 02-router-configuration.pkt
│   ├── 03-dhcp-server-and-relay.pkt
│   ├── 04-dns-http-ftp-and-dhcp-servers.pkt
│   ├── 05-email-server-smtp-pop3.pkt
│   ├── 06-static-routing-2-routers.pkt
│   └── 07-static-routing-3-routers.pkt
│
└── README.md
```

*Note: The structure above represents the suggested organization of the project files.*

---

## Simulations

### 01. Network Topologies

**Concepts:** Star, Ring, Mesh, Bus and Hybrid Topologies.

This simulation demonstrates five fundamental network topologies in one workspace.

**Components:**
- 19 Switches
- 1 Hub
- 18 PCs

The hybrid topology connects the ring and mesh topologies through an additional switch.

**Testing:**
- Ping devices across the ring topology.
- Disconnect one link in the mesh topology and observe network communication.
- Disconnect one link in the bus topology and observe the resulting connectivity.

---

### 02. Router Configuration

**Concepts:** Router Configuration and IP Addressing.

This simulation demonstrates how routers connect different networks using multiple interfaces.

It includes two independent network setups containing hubs, switches and 23 PCs.

**Sample Router Configuration:**

```bash
enable
configure terminal

interface GigabitEthernet0/0
 ip address 192.168.10.1 255.255.255.0
 no shutdown

interface GigabitEthernet0/1
 ip address 192.168.20.1 255.255.255.0
 no shutdown

interface GigabitEthernet0/2
 ip address 192.168.30.1 255.255.255.0
 no shutdown

end
write memory
```

**Testing:**
- Ping from a `192.168.10.x` PC to a `192.168.20.x` PC.
- Execute `show ip interface brief`.
- Verify that all required interfaces are up.

**Configuration Note:**

The PC named `192.168.30.21` has IP address `192.168.30.20`. Change its IP address to `.21` to avoid the naming and addressing mismatch.

---

### 03. DHCP Server and Relay

**Concepts:** Dynamic Host Configuration Protocol (DHCP) and DHCP Relay Agent.

This simulation demonstrates automatic IP address allocation within the same LAN and across different networks.

Since routers do not forward DHCP broadcasts by default, a DHCP relay agent is required to forward client requests to a remote DHCP server.

**Sample Router Configuration:**

```bash
enable
configure terminal

interface GigabitEthernet0/0/1
 ip address 192.168.1.1 255.255.255.0
 ip helper-address 192.168.2.2
 no shutdown

end
write memory
```

**DHCP Pool Configuration:**

Pool Name: `LAN`

Server: `Server3`

- Network: `192.168.1.0/24`
- Default Gateway: `192.168.1.1`
- Address Range: `192.168.1.10` to `192.168.1.59`

**Testing:**
- Configure PC7 to obtain an IP address through DHCP.
- Verify that the assigned address falls within the configured pool.
- Remove the `ip helper-address` command and observe the DHCP communication failure.

**Configuration Note:**

The DHCP pools on Server1 have a gateway of `0.0.0.0`. Configure the correct gateway to enable communication with external networks.

---

### 04. DNS, HTTP, FTP and DHCP Servers

**Concepts:** DNS, HTTP, FTP and DHCP.

This simulation demonstrates the configuration and interaction of multiple network services using seven servers across two scenarios.

The domain `www.ashu.com` is configured to resolve to the web server in both scenarios.

**Services Covered:**

- **DNS:** Resolves domain names into IP addresses.
- **HTTP:** Provides web page access.
- **FTP:** Supports file transfer.
- **DHCP:** Automatically assigns IP addresses.

**Testing:**

1. Open the web browser on a PC.
2. Visit `http://www.ashu.com`.
3. Execute `ping www.ashu.com` to test DNS resolution.
4. Connect to the FTP server using:

```bash
ftp 192.168.10.4
```

Login credentials:

```text
Username: cisco
```

**Configuration Note:**

In Scenario A, the servers have the gateway `193.168.10.1`, which does not belong to the `192.168.10.0/24` network. Correct the gateway configuration.

---

### 05. Email Server

**Concepts:** SMTP and POP3.

This simulation demonstrates email communication between two users through a centralized mail server.

The mail server is configured for the domain:

```text
ashutosh.com
```

**Protocols:**

- **SMTP:** Used for sending emails.
- **POP3:** Used for retrieving emails from the mail server.

**Testing:**

1. Open Desktop → Email on a PC.
2. Configure the incoming and outgoing mail server addresses as `192.168.10.1`.
3. Send an email from user `u2` to user `u1`.
4. Open the email application on user `u1`.
5. Click Receive to retrieve the message.

---

### 06. Static Routing – 2 Routers

**Concepts:** Static Routing and Inter-Network Communication.

This simulation demonstrates communication between two different LANs connected through two routers.

Static routes are manually configured to tell each router how to reach the remote network.

**Router Configuration:**

Router0:

```bash
ip route 192.168.20.0 255.255.255.0 192.168.30.2
```

Router1:

```bash
ip route 192.168.10.0 255.255.255.0 192.168.30.1
```

**Testing:**

- Ping `192.168.20.12` from a PC with IP `192.168.10.10`.
- Execute `show ip route`.
- Verify that static routes are displayed with the `S` identifier.

---

### 07. Static Routing – 3 Routers

**Concepts:** Multi-Hop Static Routing.

This simulation extends the two-router configuration by introducing a third router between the source and destination networks.

It demonstrates how packets travel through multiple routers to reach a destination network.

**Router Configuration:**

Router0:

```bash
ip route 192.168.20.0 255.255.255.0 192.168.30.2
```

Router2 (Middle Router):

```bash
ip route 192.168.10.0 255.255.255.0 192.168.30.1
ip route 192.168.20.0 255.255.255.0 192.168.40.2
```

Router1:

```bash
ip route 192.168.10.0 255.255.255.0 192.168.40.1
```

**Testing:**

- Execute `tracert 192.168.20.12` from a PC in the source LAN.
- Observe the intermediate router hops.
- Remove a static route from Router2 and observe where packet transmission fails.
- Execute `show ip route` on each router to verify routing entries.

---

## Getting Started

Follow these steps to run the simulations on your computer.

**1. Install Cisco Packet Tracer**

Download and install Cisco Packet Tracer from the official Cisco Networking Academy website.

**2. Clone the Repository**

```bash
git clone https://github.com/agrawalkamalkiran-2005/Cisco-Packet-Tracer-Networking.git
```

**3. Navigate to the Project**

```bash
cd Cisco-Packet-Tracer-Networking
```

**4. Open a Simulation**

Open any `.pkt` file from the `simulations/` directory using Cisco Packet Tracer.

**5. Run the Simulation**

- Switch between Realtime and Simulation modes.
- Use Add Simple PDU to test connectivity.
- Open device CLI windows to inspect configurations.
- Use ping and traceroute commands to troubleshoot connectivity.

---

## How to Test

The following commands are useful when testing the network configurations.

| Command | Purpose |
|---|---|
| `ping <IP>` | Test connectivity |
| `tracert <IP>` | Trace packet route |
| `show ip interface brief` | Check interface status |
| `show ip route` | Display routing table |
| `ipconfig` | Display PC IP configuration |
| `ipconfig /all` | Display detailed network configuration |

---

## Learning Outcomes

Through these simulations, the following networking concepts can be understood practically:

- Different types of network topologies.
- Router and switch configuration.
- IPv4 addressing and subnetting.
- DHCP configuration and relay agents.
- DNS and application-layer services.
- Email communication using SMTP and POP3.
- Static routing between multiple networks.
- Multi-hop packet transmission.
- Network troubleshooting and connectivity testing.

---

## Author

<div align="center">

### Agrawal Kamalkiran

**B.Tech – Computer Science and Engineering**

[![GitHub](https://img.shields.io/badge/GitHub-agrawalkamalkiran--2005-181717?style=for-the-badge&logo=github)](https://github.com/agrawalkamalkiran-2005)

[Visit My GitHub Profile](https://github.com/agrawalkamalkiran-2005)

</div>

---

<div align="center">

**If you find this repository useful, consider giving it a ⭐**

*Learning Computer Networks through practical simulation.*

</div>
