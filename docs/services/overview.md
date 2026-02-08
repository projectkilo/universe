
The following is written by ChatGPT. While I do intend to change it in the future and build upon it, until I learn more and get better at documenting, I'm using this as my starting reference.

# Homelab Overview

This document provides a high-level overview of the Project Kilo homelab:
its purpose, guiding principles, and architectural philosophy.

This repository documents the *design and intent* of the lab, not a
verbatim snapshot of live systems.

---

## Purpose

The Project Kilo homelab exists to:

- Learn and validate real-world infrastructure concepts
- Host self-managed services for personal use
- Experiment safely with networking, virtualization, and PKI
- Serve as a long-term reference and documentation archive

The lab is designed to evolve over time without requiring frequent
re-architecture.

---

## Core Principles

### 1. Separation of Concerns
Infrastructure, services, documentation, and secrets are treated as
distinct concerns.

- GitHub contains **sanitized documentation and templates**
- Sensitive data is stored separately and never committed

### 2. Reproducibility
The lab should be rebuildable from documentation alone.

If a system cannot be explained clearly, it is considered incomplete.

### 3. Least Privilege
Network segmentation, firewall rules, and service permissions are
designed to limit blast radius rather than assume trust.

### 4. Incremental Complexity
Complexity is introduced only when it provides clear value.
“Just because it’s possible” is not sufficient justification.

---

## High-Level Architecture

At a high level, the homelab consists of:

- A dedicated edge router handling routing, firewalling, and VLANs
- A managed switching layer providing network segmentation
- One or more virtualization hosts for services and experimentation
- A NAS for storage and application hosting
- A controlled Wi-Fi environment with logical separation

Internal services are accessed primarily over the LAN, with selective
exposure where explicitly required.

---

## Documentation Model

Documentation in this repository is structured into:

- **Network**: addressing, VLANs, firewall model
- **Services**: purpose, dependencies, and configuration notes
- **Decisions**: architectural choices and tradeoffs
- **Runbooks**: operational procedures and recovery steps

This structure is intentional and enforced to avoid ad-hoc sprawl.

---

## Out of Scope

This repository intentionally does **not** contain:

- Passwords or credentials
- Private keys or certificates
- Full device configuration exports
- Backups or live system state

These are managed separately.

