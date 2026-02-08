
The following is written by Chat GPT. I do intend to change this in the future and build on it, but for now is a reference starting point

# Firewall Model

This document describes the **logical firewall philosophy** for the Project Kilo homelab.  

It defines the principles and intent behind the rules, rather than listing
every single rule. This ensures that every firewall change has a clear purpose.

---

## Design Goals

The firewall is designed to:

1. **Segment and isolate**
   - Separate management, servers, trusted clients, IoT, and guest networks
   - Minimize lateral movement
2. **Explicitly allow what is needed**
   - Default-deny everything else
   - Prevent accidental exposure of critical services
3. **Support experimentation safely**
   - Test networks or VMs cannot break infrastructure
   - Temporary rules are documented and removed after testing
4. **Keep it auditable**
   - Decisions are recorded, not hidden in rule lists

---

## High-Level Segmentation Rules

| From             | To                   | Access Policy                        | Notes |
|-----------------|--------------------|-------------------------------------|-------|
| Management VLAN  | All segments        | Restricted, explicitly allowed only | Admin access only |
| Servers VLAN     | Trusted Clients     | Allowed for necessary services      | E.g., web services, internal APIs |
| Servers VLAN     | IoT VLAN            | Denied by default                   | Prevent IoT devices from reaching servers |
| IoT VLAN         | Servers VLAN        | Denied                               | Two-way restriction |
| Guest VLAN       | Internal LAN        | Denied                               | Internet only |
| Trusted Clients  | Servers VLAN        | Allowed where needed                 | Admin + user apps |
| Any              | Internet            | Allowed/filtered per device role    | NAT + firewall outbound policies |

> This table represents *intent*, not the literal MikroTik ACLs.

---

## Edge Router Philosophy

- **Default deny all inter-VLAN traffic**
- Exceptions are **documented and intentional**
- Routing and firewalling are centralized on the edge router
- Stateful inspection ensures only valid sessions are allowed
- Logging is enabled for critical segments

---

## Firewall Layering

1. **Per-VLAN Layer** – restrict broadcast and internal traffic  
2. **Edge Router Layer** – centralized filtering and routing policies  
3. **Service Layer** – internal service-level restrictions (Docker networks, container ACLs)  

This multi-layer approach ensures that **compromise of one layer does not expose everything**.

---

## Temporary / Experimental Rules

- Mark experimental rules clearly in the router config
- Document in `docs/runbooks/` for review and removal
- Always revert once testing is complete

---

## Security Notes

- IoT and guest networks are considered **untrusted**  
- Servers and management are **high-value assets**  
- Trusted clients are **semi-trusted**, treated with caution  
- Firewall rules should always be reviewed after any network change

---

## Philosophy Takeaways

- **Allow only what is necessary**  
- **Document why each exception exists**  
- **Segment to reduce blast radius**  
- **Treat experimentation as temporary by default**  

> Following these principles keeps the network predictable, auditable,
> and resilient to mistakes.
