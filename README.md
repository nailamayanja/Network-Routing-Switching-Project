Excel-Tec Inc — Network Transformation & Routing Design

Cisco Packet Tracer project redesigning a 4-site enterprise network to resolve efficiency, security and resilience issues in the existing infrastructure. University module project (Network Routing) — **First-class, 75%**.

![Network toplogy](topology.png)


Scenario

Excel-Tec Inc, a multi-site organisation with sites in London, Leicester, Leeds and Liverpool, needed a redesigned network to address performance, scalability and security limitations in its existing infrastructure. The brief called for a routed, segmented, and secured topology suitable for presentation to non-technical board members — the deliverable was a technical report justifying each design decision.

Topology overview

- **4 sites:** London, Leicester, Leeds, Liverpool
- **4 routers** (Cisco 2911), one per site, interconnected in a partial-mesh/ring — London-Leicester, Leeds-Liverpool, London-Leeds, Leicester-Liverpool — so no single WAN link failure isolates a site
- **2 switches per site** (Cisco 2960-24TT), 8 total
- **3 end devices per site** (Finance, Executive, Employees), representing the three departmental VLANs required at every location
- **DMZ server** hosted off London Switch 1, for externally facing services
- **WAN/internet edge** via a Cloud (Cloud-PT) connection at London Router 1

Design

Routing (40%)
- **IP addressing:** VLSM used throughout to size each subnet to its actual host count rather than a flat scheme, avoiding address waste across sites of different sizes.
- **Routing protocol:** OSPF configured across all four sites for dynamic routing, replacing a static-only approach so the network converges automatically around link failures — directly addressing the brief's reliability requirement.

Switching (40%)
- **VLANs:** Three VLANs per site (Finance, Executive, Employees), configured with access ports for end devices and trunk ports between switches and to the router, using router-on-a-stick / inter-VLAN routing to allow controlled communication between departments.
- **DHCP:** Enabled per site so all end devices receive addressing automatically rather than via static configuration.

Access control & security (10%)

- **DMZ:** London hosts a DMZ server, isolating externally facing services from the internal network.
- **ACLs:** Applied at branch routers to restrict unwanted internet-bound traffic while permitting legitimate business traffic.
- **Device hardening:** Password encryption enabled, Telnet disabled in favour of SSH, and console/VTY ports secured on all routers and switches.

Testing & troubleshooting

Connectivity was verified end-to-end using ping and traceroute across all site pairs. During testing:
- **Inter-site communication failure:** [describe the specific fault you traced — e.g. missing/incorrect OSPF network statement, area mismatch, wildcard mask error] — diagnosed via `show ip ospf neighbor` and route table inspection, then resolved.
- **ACL/DMZ misconfiguration:** an overly restrictive ACL was blocking legitimate traffic to the DMZ server; corrected by refining the ACL to permit only the required service ports.

Repository contents

| File | Description |
|---|---|
| `Excel-Tec-Network.pkt` | Full Packet Tracer topology file |
| `topology.png` | Network diagram |
| `configs/` | Exported `show running-config` output from each router and switch |
| `README.md` | This file |

## Result

Achieved **75% (First-class)** against a marking scheme weighted on routing (40%), switching (40%), access control & security (10%) and report presentation (10%).
