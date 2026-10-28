# Network Services Labs — DHCP, DNS, FTP/TFTP, Mail, SNMP & Packet Analysis

A set of hands-on labs covering the core services every enterprise network relies on: automatic addressing, name resolution, file transfer, e-mail, network management with SNMP, and packet-level analysis with Wireshark.

> Academic labs — Network Administration module, ENSA Fez (GSCSI), 2024–2025.

![Cisco Packet Tracer](https://img.shields.io/badge/Cisco-Packet%20Tracer-1BA0D7) ![SNMP](https://img.shields.io/badge/SNMP-v2c-green) ![Wireshark](https://img.shields.io/badge/Wireshark-ICMP%20%7C%20ARP-blue) ![VMware](https://img.shields.io/badge/VMware-VMs-grey)

---

## Overview

| Lab | Environment | Main topics |
|---|---|---|
| [DHCPv4 & DHCP relay](#1-dhcpv4-with-dynamic-routing-and-dhcp-relay) | Cisco Packet Tracer, 3 routers | DHCP server on a router, DHCP relay, dynamic routing |
| [Network services](#2-network-services-dhcp-dns-ftptftp-mail) | Cisco Packet Tracer | DHCP pools & exclusions, DNS, FTP/TFTP, SMTP/POP3 |
| [Enterprise network design & packet analysis](#3-enterprise-network-design-and-packet-analysis) | Packet Tracer, VMs, Wireshark | Requirements, IP addressing plan, DHCP pools, ICMP & ARP captures |
| [SNMP monitoring](#4-snmp-agent-manager-and-traps) | Two Windows VMs (VMware) | SNMP agent/manager, MIB browsing, communities, traps |

---

## 1. DHCPv4 with dynamic routing and DHCP relay

- Built a three-router topology (R1, R2, R3) with hosts, addressed all interfaces and configured **dynamic routing**.
- Configured a router as the **DHCP server** and a **DHCP relay** (`ip helper-address`) so remote subnets also receive addresses.
- Verified address distribution and end-to-end connectivity.

## 2. Network services: DHCP, DNS, FTP/TFTP, Mail

| Service | What I configured | How it was validated |
|---|---|---|
| **DHCP** | Two pools (`serverPool`, `ensafPool`), exclusion of the servers' static addresses, router R1 as **DHCP relay** | Automatic addressing on every client (`ipconfig`) |
| **DNS** | DNS service and an **A record** for the domain `tp2-ensaf.ma`, DNS server distributed to clients | `nslookup` |
| **FTP / TFTP** | FTP accounts with different permissions (full rights for Admin, restricted for others); TFTP server | File upload, read and rename by an authorised user; **router configuration restored from TFTP** |
| **Mail** | SMTP / POP3 server for `tp2-ensaf.ma`, user mailboxes and mail clients | Messages sent and received between clients |

Traffic for each service was then observed in Packet Tracer's **simulation mode**.

| | FTP | TFTP |
|---|---|---|
| Transport | TCP (21 control, 20 data) | UDP 69 |
| Authentication | Yes | No |
| Typical use | Managed file transfer | Device configs / firmware |

## 3. Enterprise network design and packet analysis

- Wrote a **functional and technical requirements specification** for a company network: services, subnets, security, equipment choice (routers, switches, access points), performance and availability needs.
- Built the **IP addressing plan** and the DHCP pools with exclusions.
- Connected two virtual machines and captured traffic with **Wireshark**:
  - **ICMP** — echo request / echo reply exchanged by `ping`;
  - **ARP** — cache manipulation (`arp -a`, clearing entries), broadcast request and unicast reply.

## 4. SNMP: agent, manager and traps

| Step | Details |
|---|---|
| Agent | SNMP service installed and configured on the Windows server (contact, location, services) |
| Manager | **iReasoning MIB Browser** on the client: `get`, `get next` and MIB tree browsing (system information, server resources) |
| Securing access | Default `public` community **disabled**; custom **read-only** and **read-write** communities created |
| Traps | Trap destination configured; an access attempt with a **wrong community** generated an **authentication failure** trap, received on the trap console |
| Capture | SNMP packets captured and analysed |

## Skills demonstrated

DHCP · DHCP relay · DNS · FTP/TFTP · SMTP/POP3 · IP addressing & subnetting · network design · SNMP (MIB, communities, traps) · Wireshark · ICMP · ARP · Cisco Packet Tracer · VMware

## Documentation (French)

- [DHCPv4 & DHCP relay](docs/lab-dhcpv4-relay.pdf)
- [DHCP, DNS, FTP/TFTP & Mail](docs/lab-dhcp-dns-ftp-mail.pdf)
- [Enterprise network design & Wireshark analysis](docs/lab-enterprise-design-wireshark.pdf)
- [SNMP under Windows](docs/lab-snmp-windows.pdf)

---

**Author:** Khaoula Belhaj — final-year engineering student, Communicating Systems & Computer Security, ENSA Fez · [LinkedIn](https://linkedin.com/in/khaoula-belhaj-1999163a6)
