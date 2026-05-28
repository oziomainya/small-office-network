# Small Office Network Build: Complete Networking Fundamentals Lab

> **Category:** Networking
> **Status:** Live
> **Course:** Cisco Networking Basics · Junior Cybersecurity Analyst Career Path
> **Author:** Ozioma Inya         <!-- REPLACE with your name -->
> **Date:** August, 2025              <!-- REPLACE e.g. "February, 2025" -->

---

## Overview

A complete network infrastructure built for a small office (TechCorp) from scratch in Cisco Packet Tracer. Covers network design, wireless configuration, OSI and TCP/IP models, IPv4 addressing and subnetting, IPv6, DHCP, routing, ARP, transport and application layer services, and full network testing.

---

## Objectives

- [x] Design a small office network topology covering wired LAN, wireless, and simulated internet
- [x] Configure a wireless router with SSID, WPA2 security, and DHCP for wireless clients
- [x] Document the OSI and TCP/IP models mapped to real protocols in the topology
- [x] Select and justify appropriate network media for each segment
- [x] Demonstrate Ethernet switching and MAC address table behaviour
- [x] Design and implement a complete IPv4 addressing scheme with subnetting
- [x] Configure IPv6 addresses on router interfaces (dual-stack)
- [x] Configure a DHCP server to automatically assign IPs to wired clients
- [x] Configure inter-network routing and demonstrate ARP and gateway operation
- [x] Analyse TCP and UDP behaviour using simulation mode
- [x] Configure DNS and HTTP services and verify name resolution
- [x] Verify full end-to-end connectivity using ping, traceroute, and show commands

---

## Tools & Technologies

| Tool | Purpose |
|---|---|
| Cisco Packet Tracer | Network simulation -- wired, wireless, routing, and services |
| Cisco IOS CLI | Router and switch configuration |
| Packet Tracer Simulation Mode | Observing packet flow, ARP, TCP, and application traffic |
| ICMP Ping and Traceroute | End-to-end connectivity verification |

---

## Skills Demonstrated

`Network Design` `Network Topology` `Network Types` `Client-Server Model`
`Wireless Configuration` `WPA2 Security` `OSI Model` `TCP/IP Model`
`Network Media` `Ethernet` `MAC Address Table` `IPv4 Addressing`
`Subnetting` `CIDR` `IPv6 Addressing` `Dual-Stack` `DHCP`
`Default Gateway` `Static Routing` `ARP` `TCP` `UDP` `Port Numbers`
`DNS` `HTTP` `Ping` `Traceroute` `Cisco IOS CLI` `Packet Tracer`

---

## Network Topology

```
  [ISP Cloud: 8.8.8.1]
       |
  [ISP Router: 10.0.0.1] ----------- WAN: 10.0.0.0/30
       |
  [R1: S0/0/0: 10.0.0.2 / G0/0: 192.168.1.1]
       |
     [SW1: 192.168.1.2]
    /    |     |     \
  [PC1] [PC2] [Server] [WR1: 192.168.1.50]
  DHCP  DHCP  .100       |
                    [Laptop: 192.168.2.x via DHCP]

  LAN:  192.168.1.0/24
  WLAN: 192.168.2.0/24
  WAN:  10.0.0.0/30
```

### Addressing Table

| Device | Interface | IP Address | Role |
|---|---|---|---|
| R1 | G0/0 | 192.168.1.1 | LAN gateway / DHCP server |
| R1 | S0/0/0 | 10.0.0.2 | WAN uplink to ISP |
| ISP | S0/0/1 | 10.0.0.1 | Simulated ISP router |
| ISP | G0/0 | 8.8.8.1 | Simulated internet |
| SW1 | VLAN 1 | 192.168.1.2 | Access layer switch |
| Server | NIC | 192.168.1.100 | DNS and HTTP server |
| WR1 | LAN | 192.168.1.50 | Wireless access point |
| PC1 | NIC | DHCP (.61) | Wired workstation |
| PC2 | NIC | DHCP (.62) | Wired workstation |
| Laptop | Wireless | DHCP (192.168.2.x) | Wireless client |

---

## Lab Parts

### Part 01: Network Design and Topology Planning

Designed the TechCorp network before touching Packet Tracer. Identified all
required devices and their roles. Documented the network as a client-server
model. PC1, PC2, and Laptop are clients; Server provides services; R1,
SW1, and WR1 are intermediary devices.

```
Device Inventory:
  R1      -- 1941 Router    -- LAN gateway and WAN connection
  SW1     -- 2960 Switch    -- Access layer
  Server  -- Generic Server -- DNS and HTTP
  WR1     -- Wireless Router -- Wireless access
  PC1/PC2 -- Generic PCs   -- Wired workstations
  Laptop  -- Generic Laptop -- Wireless client
  ISP     -- Generic Router -- Simulated internet
```

---

### Part 02: Wireless Network Configuration

```
Wireless Router (WR1):
  LAN IP:     192.168.1.50 / 255.255.255.0
  Gateway:    192.168.1.1
  SSID:       TechCorp-WiFi
  Security:   WPA2-PSK
  Passphrase: TechCorp2024!

DHCP Pool (wireless clients):
  Network:    192.168.2.0 / 255.255.255.0
  Gateway:    192.168.2.1
  DNS:        192.168.1.100
  Range:      192.168.2.100 - 192.168.2.149

Laptop assigned: 192.168.2.100 via DHCP
```

---

### Part 03: OSI and TCP/IP Model Documentation

| OSI Layer | Device/Protocol in Topology |
|---|---|
| Layer 1 -- Physical | UTP cables, wireless radio signal |
| Layer 2 -- Data Link | SW1 -- Ethernet frames, MAC addresses |
| Layer 3 -- Network | R1 -- IP packets, routing |
| Layer 4 -- Transport | TCP (HTTP), UDP (DNS, DHCP) |
| Layer 7 -- Application | HTTP (web), DNS (name resolution) |

TCP/IP Model: Network Access (L1-2) / Internet (L3) / Transport (L4) / Application (L5-7)

---

### Part 04: Network Media Selection

| Segment | Media | Justification |
|---|---|---|
| LAN (wired) | Cat6 UTP straight-through | Gigabit Ethernet, up to 100m, cost-effective |
| WAN | Serial DCE/DTE or Ethernet | Point-to-point link to ISP |
| WLAN | IEEE 802.11 / WPA2-AES | Wireless access for mobile devices |

---

### Part 05: Access Layer and Ethernet Switching

```
-- Before any traffic: MAC table is empty
SW1# show mac address-table
Mac Address Table
------------------------------------------
Vlan  Mac Address       Type    Ports
----  -----------       ------  -----
(no entries)

-- After communication on the network: SW1 learns all MACs
SW1# show mac address-table 
          Mac Address Table
-------------------------------------------

Vlan    Mac Address       Type        Ports
----    -----------       --------    -----

   1    0005.5ea9.eec5    DYNAMIC     Fa0/2
   1    0006.2ad4.d7eb    DYNAMIC     Fa0/3
   1    00e0.a395.9c44    DYNAMIC     Fa0/1
   1    00e0.b019.2101    DYNAMIC     Gig0/1
   1    00e0.f998.ec01    DYNAMIC     Fa0/4
```

---

### Part 06: IPv4 Addressing Scheme

```
DEVICE     INTERFACE    IP ADDRESS       SUBNET MASK       GATEWAY
R1         G0/0         192.168.1.1      255.255.255.0      --
R1         S0/0/0       10.0.0.2         255.255.255.252    --
ISP        S0/0/1       10.0.0.1         255.255.255.252    --
ISP        G0/0         8.8.8.1          255.255.255.0      --
SW1        VLAN 1       192.168.1.2      255.255.255.0      192.168.1.1
Server     NIC          192.168.1.100    255.255.255.0      192.168.1.1
WR1        LAN          192.168.1.50     255.255.255.0      192.168.1.1
PC1/PC2    NIC          DHCP             --                 192.168.1.1
```

---

### Part 07: IPv6 Dual-Stack Configuration

```
R1(config)# ipv6 unicast-routing

R1(config)# interface GigabitEthernet0/0
R1(config-if)# ipv6 address 2001:db8:acad:1::1/64
R1(config-if)# ipv6 address fe80::1 link-local
R1(config-if)# exit

R1(config)# interface Serial0/0/0
R1(config-if)# ipv6 address 2001:db8:acad:a::2/64
R1(config-if)# exit

R1# show ipv6 interface brief
GigabitEthernet0/0         [up/up]
    FE80::1
    2001:DB8:ACAD:1::1
GigabitEthernet0/1         [administratively down/down]
    unassigned
Serial0/0/0                [up/up]
    FE80::2E0:B0FF:FE19:2101
    2001:DB8:ACAD:A::2
Serial0/0/1                [administratively down/down]
    unassigned
Vlan1                      [administratively down/down]
    unassigned
```

---

### Part 08: DHCP Server Configuration

```
R1(config)# ip dhcp excluded-address 192.168.1.1 192.168.1.60

R1(config)# ip dhcp pool LAN_POOL
R1(dhcp-config)# network 192.168.1.0 255.255.255.0
R1(dhcp-config)# default-router 192.168.1.1
R1(dhcp-config)# dns-server 192.168.1.100

R1# show ip dhcp binding
IP address       Client-ID/              Lease expiration        Type
                 Hardware address
192.168.1.61     00E0.A395.9C44           --                     Automatic
192.168.1.62     0005.5EA9.EEC5           --                     Automatic
```

---

### Part 09: Routing, ARP, and Gateway

```
R1(config)# ip route 0.0.0.0 0.0.0.0 10.0.0.1

R1# show ip route
Gateway of last resort is 10.0.0.1 to network 0.0.0.0

     10.0.0.0/8 is variably subnetted, 2 subnets, 2 masks
C       10.0.0.0/30 is directly connected, Serial0/0/0
L       10.0.0.2/32 is directly connected, Serial0/0/0
     192.168.1.0/24 is variably subnetted, 2 subnets, 2 masks
C       192.168.1.0/24 is directly connected, GigabitEthernet0/0
L       192.168.1.1/32 is directly connected, GigabitEthernet0/0
S*   0.0.0.0/0 [1/0] via 10.0.0.1

C:>arp -a
  Internet Address      Physical Address      Type
  192.168.1.1           00e0.b019.2101        dynamic
```

---

### Part 10: Transport Layer Analysis

| Protocol | Type | Port | Used For |
|---|---|---|---|
| TCP | Connection-oriented | 80 | HTTP web traffic |
| TCP | Connection-oriented | 443 | HTTPS |
| UDP | Connectionless | 53 | DNS queries |
| UDP | Connectionless | 67/68 | DHCP |

TCP three-way handshake: SYN > SYN-ACK > ACK (observed in simulation mode)

---

### Part 11: DNS and HTTP Services

```
Server DNS Config:
  Record: www.techcorp.local --> 192.168.1.100 (Type A)

Server HTTP Config:
  Status: ON -- default page served

Verification on PC1:
  C:>nslookup www.techcorp.local

Server: [192.168.1.100]
Address:  192.168.1.100

Non-authoritative answer:
Name:   www.techcorp.local
Address:   192.168.1.10

  Browser: http://www.techcorp.local --> Page loads successfully
```

---

### Part 12: Full Network Verification

```
-- Connectivity matrix from PC1
PC1 -> PC2              SUCCESS
PC1 -> Server           SUCCESS
PC1 -> R1 Fa0/0         SUCCESS
PC1 -> SW1 VLAN 1       SUCCESS
PC1 -> WR1              NAT-BLOCKED
PC1 -> ISP              SUCCESS
PC1 -> 8.8.8.1          SUCCESS
PC1 -> Laptop (WLAN)    NAT-BLOCKED

-- Traceroute from PC1 to internet
C:>tracert 8.8.8.1

Tracing route to 8.8.8.1 over a maximum of 30 hops: 

  1   1 ms      0 ms      14 ms     192.168.1.1
  2   11 ms     1 ms      0 ms      8.8.8.1

Trace complete.
```

---

## Results

| # | Result | Status |
|---|---|---|
| 2 | Full wired and wireless connectivity verified | OK |
| 3 | DHCP assigned addresses to PC1 and PC2 | OK |
| 4 | DNS resolution working. www.techcorp.local resolves correctly | OK |
| 5 | HTTP accessible by hostname from PC1 | OK |
| 6 | Routing to ISP and internet confirmed via traceroute | OK |
| 7 | IPv6 dual-stack configured on R1 | OK |
| 8 | Laptop on WLAN could not reach Server. WR1 gateway missing | WARNING |
| 9 | Fixed by setting WR1 default gateway to 192.168.1.1 | FIXED |
| 10 | DNS resolution failed. Wrong DNS server IP in DHCP pool | WARNING |
| 11 | Fixed by correcting dns-server to 192.168.1.100 in DHCP config | FIXED |

---

## Lessons Learned

**1. Every OSI layer is visible in a real topology**

Mapping the model to actual devices made it concrete. When troubleshooting,
thinking layer by layer immediately narrows down where a problem lives.

**2. DHCP and DNS failures cause the most confusing symptoms**

The device appears connected but nothing works. Always check DHCP bindings
and DNS server assignment early in any troubleshooting workflow.

**3. ARP is invisible until something goes wrong**

Simulation mode made the ARP broadcast and unicast reply visible. ARP
spoofing attacks exploit exactly this process. Understanding it matters
for cybersecurity as much as for networking.

**4. The /30 subnet for WAN links is a standard**

A /30 provides exactly two usable host addresses perfect for a
point-to-point link. This is a real-world standard used consistently
in enterprise networks.

**5. Wireless is a different security problem from wired**

The wired LAN traffic stays on the cable. The wireless signal radiates
outward. WPA2 with a strong passphrase is the minimum acceptable standard.

---

## Repository Structure

```
small-office-network/
|-- index.html                          <- Full project write-up (live via GitHub Pages)
|-- README.md                           <- This file
|-- small-ofice-network.pkt             <- Cisco Packet Tracer project file
|-- topology.png                        <- Full topology in Packet Tracer
|-- SW1-mac-address-table.png           <- SW1 MAC address table output
|-- R1-dhcp-binding.png                 <- show ip dhcp binding output
|-- R1-interface-brief.png              <- show ip interface brief output
|-- R1-ip-route.png                     <- show ip route output
|-- R1-running-config.txt               <- R1 configuration file
|-- SW1-running-confit.txt              <- SW1 configuration file
|-- dns-record.png                      <- nslookup verification
|-- http-access.png                     <- Browser accessing www.techcorp.local
+-- ping-statistics.png                 <- Complete ping matrix results
```

<!-- REMOVE any files from the structure above that you have not added yet -->

---

## Links

- [Full Project Write-up](https://oziomainya.github.io/small-office-network)
- [Portfolio](https://oziomainya.github.io)

<!-- REPLACE [YOUR_GITHUB_USERNAME] and [YOUR_PORTFOLIO_URL] with your real details -->

---

*Ozioma Inya · [LinkedIn ↗](https://linkedin.com/in/ozioma-inya-a46327304) · [Github ↗](https://github.com/oziomainya)*
<!-- REPLACE the placeholders above with your real details -->
