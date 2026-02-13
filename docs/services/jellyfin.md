
# Jellyfin Service

This document describes the Jellyfin service deployment in the Project Kilo homelab.

---

## Purpose

Jellyfin provides media streaming services for personal use. It is hosted
on the NAS within a containerized environment.

---

## Deployment Overview

- **Platform:** Container Manager on DS220+  
- **Network:** 172.16.20.30/28  
- **Firewall:** Access allowed to management (172.16.10.0/28), WiFi (172.16.40.0/24), and Wireguard (172.16.60.0/29 - planned)  
- **Persistence:** Media library stored on NAS volumes, container data on persistent volumes

---

## Service Details

- **Port Mapping:** Exposed to VLANs as needed; internal container ports only accessible via Docker networking  
- **Reverse Proxy:** https://jellyfin.example.com
- **Authentication:** Handled by Jellyfin user accounts; no external passwords are stored in Git  
- **Backups:** Database and config snapshots are stored offline or in private storage

---

## Configuration Notes

- All configuration is containerized and uses environment variables  
- Sensitive information is **not committed** to Git  
- Sample `.env` variables are provided in `configs/docker/jellyfin/.env.example`

---

## Runbooks / Maintenance

- To update Jellyfin:
  1. Pull the new Docker image
  2. Stop the existing container
  3. Start container with the updated image
- To migrate media storage:
  - Update the volume mappings in `docker-compose.yml`  
  - Ensure file permissions are preserved
- Logs are stored in `/var/lib/jellyfin/logs` and rotated regularly

---

## References

- [Docker official Jellyfin image](https://hub.docker.com/r/jellyfin/jellyfin)
- Reverse proxy patterns documented in `docs/services/reverse-proxy.md` (planned)
