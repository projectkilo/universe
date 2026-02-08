
The following is written by Chat GPT. While I do intend to change it and build on it, as a somewhat newb, I'm using this for starting reference.

# Network Topology

This document describes the logical network model used in the Project
Kilo homelab, including segmentation, trust boundaries, and design
intent.

Specific IP addresses may be representative rather than exact.

---

## Design Goals

The network is designed to:

- Isolate critical infrastructure from user and IoT devices
- Minimize lateral movement between segments
- Support experimentation without risking core services
- Remain understandable and debuggable

Security is achieved through *segmentation and policy*, not obscurity.

---

## Logical Segments

The network is divided into multiple logical segments using VLANs.
Each segment has a clearly defined purpose and trust level.

### Management
- Infrastructure management interfaces
- Hypervisors, switches, and network devices
- Access is tightly restricted

### Servers
- Virtual machines and containers hosting services
- Controlled access from trusted segments only

### Trusted Clients
- Personal devices used for administration and daily access
- Allowed to initiate connections to servers

### IoT / Untrusted
- Devices with limited trust (TVs, assistants, appliances)
- Internet access only by default

### Guest / Wi-Fi
- Temporary or untrusted user devices
- No access to internal resources

---

## Routing and Firewall Model

A dedicated edge router performs:

- Inter-VLAN routing
- Stateful firewalling
- Default-deny policies between segments

Firewall rules are written explicitly to allow required flows and deny
everything else.

Example principles:
- Trusted → Servers: allowed
- IoT → Servers: denied
- Guest → LAN: denied
- Management → All: restricted and logged

---

## Addressing Strategy

- Private IPv4 addressing is used internally
- Subnets are aligned with VLAN boundaries
- Addressing is structured for readability and expansion

IPv6 may be present on some segments but is not relied upon for core
functionality.

---

## Switching Layer

The switching layer supports:

- VLAN tagging and access ports
- Segmentation between wired and wireless devices
- Expansion without readdressing

Ports are assigned based on device role, not convenience.

---

## Wireless Integration

Wireless access points are treated as extensions of the wired network.

- SSIDs map directly to VLANs
- Client isolation is enforced where appropriate
- Wi-Fi does not bypass segmentation rules

---

## Failure Domains

The network is designed so that:

- A misbehaving IoT device cannot impact servers
- A test VM cannot affect infrastructure management
- Wireless issues do not disrupt wired services

This reduces the impact of mistakes during experimentation.
