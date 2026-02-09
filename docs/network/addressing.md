
The following is written by Chat GPT. While I do intend on changing it in the future and building on top of it, for now I'm using it as a starting point.


# Network Addressing

This document describes the internal IP addressing strategy used in the
Project Kilo homelab.

The goal of this addressing model is clarity, scalability, and alignment
with logical network segmentation rather than convenience.

---

## Design Principles

The addressing scheme follows these principles:

- One subnet per logical segment (VLAN)
- Predictable, human-readable structure
- Room for expansion without renumbering
- Clear separation between infrastructure and clients

Addressing is treated as documentation, not guesswork.

---

## IPv4 Addressing Model

Private IPv4 addressing is used throughout the environment.

Each VLAN maps cleanly to a single subnet, allowing policies and
troubleshooting to remain intuitive.

Example structure:

| Segment        | VLAN | Subnet             | Purpose                          |
|----------------|------|--------------------|----------------------------------|
| Management     | 10   | 172.16.10.0/28     | Network & host management        |
| Servers        | 20   | 172.16.20.0/27     | VMs, containers, infrastructure  |
| IoT            | 30   | 172.16.30.0/27     | Untrusted devices                |
| Wi-Fi Clients  | 40   | 172.16.40.0/24     | Trusted wireless clients         |
| Office         | 50   | 172.16.50.0/29     | Separate interface for AERO      |
| Wireguard      | 60   | 172.16.60.0/29     | Wireguard VPN                    |

> Subnets shown are representative and may evolve over time.

---

## Gateway Conventions

- The default gateway for each subnet is `.1`
- Gateways are hosted on the edge router
- Routing between subnets is explicitly controlled by firewall rules

Example:

172.16.20.1 = Servers VLAN Gateway

---

## Address Allocation Strategy

Within each subnet:

- `.1` is reserved for the gateway
- Low addresses are reserved for infrastructure
- DHCP pools are defined per VLAN
- Static assignments are used sparingly and documented

Example pattern:

.1 = Gateway
.2 - .20 = Network/Infrastructure devices
.50 - .200 = DHCP pool

---

## Static vs Dynamic Addressing

### Static Addresses
Used for:
- Routers and switches
- Hypervisors
- NAS devices
- Services that must be reachable predictably

Static assignments are documented and intentional.

### DHCP
Used for:
- User devices
- Test systems
- Short-lived clients

DHCP is preferred where permanence is not required.

---

## IPv6 Considerations

IPv6 may be enabled on some segments depending on upstream ISP behavior
and device support.

At present:
- IPv6 is not required for internal service operation
- No internal services depend on IPv6 reachability
- Firewall policies assume IPv4 as the primary control plane

IPv6 usage may be expanded in the future once fully understood and
intentionally designed.

---

## DNS and Naming

- Internal DNS resolves hostnames within the lab
- Hostnames reflect role rather than location
- DNS is preferred over hardcoded IPs wherever possible

Addressing and naming are treated as complementary systems.

---

## Documentation Discipline

Any of the following require updating this document:

- Adding a new VLAN
- Renumbering a subnet
- Changing gateway conventions
- Introducing IPv6 as a first-class dependency

If it isn’t documented here, it isn’t “done.”
