
<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=gradient&customColorList=12,14,18&height=220&section=header&text=Packet%20Tracer%20Networking%20Simulations&fontSize=36&fontColor=ffffff&animation=fadeIn&fontAlignY=38&desc=Build%20it.%20Ping%20it.%20Break%20it.%20Fix%20it.&descAlignY=60&descSize=18" alt="header" />

![Cisco Packet Tracer](https://img.shields.io/badge/Cisco-Packet%20Tracer%209.0-1BA0D7?style=for-the-badge&logo=cisco&logoColor=white)
![Simulations](https://img.shields.io/badge/Simulations-7-00c853?style=for-the-badge)
![Subject](https://img.shields.io/badge/Computer-Networks-7048e8?style=for-the-badge)

**Seven simulations, from a single router to a multi-router network.**

**Developed and maintained by [@agrawalkamal-2005](https://github.com/agrawalkamal-2005)**

</div>

---

## 🌠 Simulations

| | Simulation | Covers |
|:-:|---|---|
| 🕸️ | [01 · Network Topologies](#-01--network-topologies) | Star, ring, mesh, bus, hybrid |
| 🕸️ | [02 · Router Configuration](#-02--router-configuration) | Router setup, IP addressing |
| 🕸️ | [03 · DHCP Server and Relay](#-03--dhcp-server-and-relay) | DHCP, relay agent |
| 🕸️ | [04 · DNS, HTTP, FTP and DHCP Servers](#-04--dns-http-ftp-and-dhcp-servers) | Server services |
| 🕸️ | [05 · Email Server](#-05--email-server) | SMTP, POP3 |
| 🕸️ | [06 · Static Routing, 2 Routers](#-06--static-routing-2-routers) | Static routes |
| 🕸️ | [07 · Static Routing, 3 Routers](#-07--static-routing-3-routers) | Multi-hop routes |

---

## ♨️ Quick Start

1. Install **Cisco Packet Tracer 9.0** or newer.
2. Clone this repository:

   ```bash
   git clone https://github.com/agrawalkamal-2005/packet-tracer-networking-simulations.git
   ```

3. Open any file in `simulations/`.
4. Switch to **Simulation mode** and send a PDU to watch packets hop.

---

## 🕸️ 01 · Network Topologies

`Star · Ring · Mesh · Bus · Hybrid`

All five topologies in one workspace: 19 switches, 1 hub and 18 PCs. The hybrid joins the ring and the mesh through one extra switch.

<img src="assets/01-network-topologies.svg" alt="Network topologies diagram" width="100%" />

<details>
<summary> 🏴‍☠️ <b>Test steps</b></summary>

- [ ] Ping across the ring in Simulation mode and note the path.
- [ ] Cut one link in the mesh; traffic still flows.
- [ ] Cut one link in the bus and see what is isolated.

</details>

---

## 🕸️ 02 · Router Configuration

`Router Configuration · IP Addressing`

Routers join separate networks. Two independent setups with hubs, switches and 23 PCs.

<img src="assets/02-router-configuration.svg" alt="Router configuration diagram" width="100%" />

<details>
<summary> ❄️ <b>Config and test steps</b></summary>

```cisco
interface GigabitEthernet0/0
 ip address 192.168.10.1 255.255.255.0
 no shutdown

interface GigabitEthernet0/1
 ip address 192.168.20.1 255.255.255.0
 no shutdown

interface GigabitEthernet0/2
 ip address 192.168.30.1 255.255.255.0
 no shutdown
```

- [ ] Ping from a `192.168.10.x` PC to a `192.168.20.x` PC.
- [ ] `show ip interface brief` shows every port `up`.

⚠️ The PC named `192.168.30.21` has IP `192.168.30.20`, a duplicate. Change it to `.21`.

</details>

---

## 🕸️ 03 · DHCP Server and Relay

`DHCP · DHCP Relay`

DHCP on the same LAN, and across a router. Routers drop broadcasts, so the relay forwards requests to the server.

<img src="assets/03-dhcp-server-and-relay.svg" alt="DHCP and relay diagram" width="100%" />

<details>
<summary> ❄️ <b>Config and test steps</b></summary>

```cisco
interface GigabitEthernet0/0/1
 ip address 192.168.1.1 255.255.255.0
 ip helper-address 192.168.2.2
 no shutdown
```

Pool `LAN` on `Server3`: `192.168.1.0/24`, gateway `192.168.1.1`, range `.10` to `.59`.

- [ ] Set `PC7` to **DHCP** and confirm it gets `192.168.1.10` to `.59`.
- [ ] Remove the `ip helper-address` line and watch DHCP fail.

⚠️ Pools on `Server1` have gateway `0.0.0.0`, so those clients get no gateway.

</details>

---

## 🕸️ 04 · DNS, HTTP, FTP and DHCP Servers

`DNS · HTTP · FTP · DHCP`

Seven servers in two scenarios. `www.ashu.com` resolves to the web server in both.

<img src="assets/04-dns-http-ftp-dhcp-servers.svg" alt="Servers diagram" width="100%" />

<details>
<summary> ⚓ <b>Test steps</b></summary>

- [ ] Open `http://www.ashu.com` in a PC browser.
- [ ] `ping www.ashu.com` resolves.
- [ ] `ftp 192.168.10.4` (login `cisco`).

⚠️ In Scenario A the servers list gateway `193.168.10.1`, which is not on `192.168.10.0/24`. Clear or correct it.

</details>

---

## 🕸️ 05 · Email Server

`SMTP · POP3`

One mail server for `ashutosh.com` with two users on a single switch.

<img src="assets/05-email-server-smtp-pop3.svg" alt="Email server diagram" width="100%" />

<details>
<summary> ⚓ <b>Test steps</b></summary>

- [ ] On a PC open *Desktop → Email*, both servers point to `192.168.10.1`.
- [ ] Send a mail from `u2` to `u1`.
- [ ] Press **Receive** on `u1`.

</details>

---

## 🕸️ 06 · Static Routing, 2 Routers

`Static Routing`

Routers only know their own networks, so each one is told where the other LAN lives.

<img src="assets/06-static-routing-2-routers.svg" alt="Static routing with 2 routers diagram" width="100%" />

<details>
<summary> ❄️ <b>Config and test steps</b></summary>

```cisco
! Router0
ip route 192.168.20.0 255.255.255.0 192.168.30.2

! Router1
ip route 192.168.10.0 255.255.255.0 192.168.30.1
```

- [ ] Ping `192.168.20.12` from `192.168.10.10`.
- [ ] `show ip route` lists the `S` entries.

</details>

---

## 🕸️ 07 · Static Routing, 3 Routers

`Multi-hop Static Routing`

Same two LANs, but traffic now crosses a middle router.

<img src="assets/07-static-routing-3-routers.svg" alt="Static routing with 3 routers diagram" width="100%" />

<details>
<summary> ❄️ <b>Config and test steps</b></summary>

```cisco
! Router0
ip route 192.168.20.0 255.255.255.0 192.168.30.2

! Router2 (middle)
ip route 192.168.10.0 255.255.255.0 192.168.30.1
ip route 192.168.20.0 255.255.255.0 192.168.40.2

! Router1
ip route 192.168.10.0 255.255.255.0 192.168.40.1
```

- [ ] `tracert 192.168.20.12` from a LAN 10 PC shows every hop.
- [ ] Remove a route on `Router2` and see where the trace stops.

</details>

---

<div align="center">

## 👨‍💻 Author

**Kamal Kiran Agrawal**

B.Tech | Computer Science and Engineering

[![GitHub](https://img.shields.io/badge/GitHub-@agrawalkamal--2005-181717?style=for-the-badge&logo=github)](https://github.com/agrawalkamal-2005)

If you find this repository useful, consider giving it a ⭐!

<img src="https://capsule-render.vercel.app/api?type=waving&color=gradient&customColorList=12,14,18&height=100&section=footer" alt="footer" />

</div>

