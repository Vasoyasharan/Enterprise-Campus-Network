# **Enterprise Multi-Floor, Multi-Department Network Infrastructure**

**Technologies: VLAN | OSPF | Inter-VLAN Routing | EtherChannel | Site-to-Site IPsec VPN | NAT | L3 Switching**

---

## 📌 **Overview**

This project implements a complete **enterprise-grade network architecture** across multiple floors and departments.
The design includes:

* Segmented VLAN infrastructure
* Layer-3 switching
* Redundant OSPF-based core
* EtherChannel trunk aggregation
* Site-to-Site IPsec VPN
* Centralized services (Data Center, Admin, Accounting, Finance, Logistics, Research, Customer Service, Marketing, Guest WiFi)

The goal is to simulate a scalable, secure, and high-availability network similar to what real organizations use.

---

![image](https://github.com/avadh-150/Multi-floor-Enterprise-Design-Network/blob/main/image/Screenshot%20from%202025-12-04%2022-49-36.png?raw=true)

---

## 🗺️ **Network Topology**

The topology includes:

* **Four floors** each with their own distribution switches
* A **core network** consisting of four L3 routers connected in a mesh
* Dedicated **access layer switches** per department
* **Wireless + Printer integration**
* A secure **Data Center network**
* **WAN connectivity + IPsec VPN tunnel** to external sites
* **Redundant links using EtherChannel**

*(Insert your exported topology image here using GitHub upload once repo is created.)*

---

## 🧱 **VLAN Architecture**

| VLAN | Name                      | Subnet            |
| ---- | ------------------------- | ----------------- |
| 10   | Management                | 192.168.10.0/25   |
| 20   | Admin                     | 192.168.12.0/25   |
| 30   | Marketing                 | 192.168.20.0/25   |
| 40   | HR                        | 192.168.21.0/25   |
| 50   | Research                  | 192.168.30.0/25   |
| 60   | Accounting                | 192.168.40.128/25 |
| 70   | Finance                   | 192.168.40.0/25   |
| 80   | Customer Service          | 192.168.31.128/25 |
| 90   | Logistics                 | 192.168.50.0/25   |
| 100  | SDC (Service Data Center) | 192.168.6.0/25    |
| 120  | Guest                     | 192.168.6.128/25  |

Each VLAN is routed at the **L3 distribution layer**, using SVIs for gateway and OSPF redistribution.

---

## ⚙️ **Core Network (OSPF + Redundancy)**

Core consists of:

* Core1, Core2, Core3, Core4
* Full mesh OSPF adjacency
* Redundant 1Gbps and 10Gbps backbone links
* All SVIs redistributed into OSPF
* No single point of failure in routing

**OSPF Areas:**

* **Area 0** – Backbone
* All distribution switches advertise their VLAN networks into Area 0.

---

## 🔗 **EtherChannel (LACP)**

EtherChannel used between:

* Distribution ↔ Core
* Server-farm switches
* Floor access switches

**Mode:** LACP (active/active)
**Purpose:**

* Bandwidth aggregation
* Link redundancy
* Faster convergence compared to STP-only environments

---

## 🌐 **Inter-VLAN Routing**

Performed at the **L3 switches** using:

```
ip routing
interface vlan XX
 ip address <gateway>
```

All VLANs have Layer-3 gateways configured on distribution switches, not on access switches.

---

## 🧱 **Access Layer Design**

Each department features:

* PC hosts
* Printers
* Wireless access points
* One or more 2960 switches
* VLAN tagging on trunk uplinks
* DHCP services (via central DHCP or router DHCP pools depending on design)

---

## 🏢 **Server/Data Center Network**

Includes VLAN 100 (SDC) with:

* Admin PC
* Servers
* Printers
* AP
* Management VLAN for switch control

All connections aggregated via EtherChannel for redundancy and performance.

---

## 📡 **Wireless Integration**

* Each floor has separate APs bound to corresponding VLANs
* Guest Wi-Fi isolated using VLAN 120
* ACLs restrict inter-department access where required

---

## ✔️ **What This Project Demonstrates**

* Professional multi-layer enterprise network architecture
* Complete VLAN segmentation & routing
* Fully working OSPF backbone
* Layer-2 link aggregation using LACP
* Secure branch connectivity with IPsec
* NAT + DHCP + Printer + WiFi integration
* Real-world scalable and secure design

---

## 🧑‍💻 **Author**

Designed and implemented as a practical enterprise-level networking project demonstrating advanced switching, routing, security, and WAN technologies.
