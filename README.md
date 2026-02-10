# Project Kilo - Universe

### Welcome to my personal homelab journal.

**Project Kilo** is a long-term personal infrastructure project focused on replacing paid SaaS subscriptions with self-hosted, free and open-source software (FOSS), while building practical skills in networking, virtualization, and systems administration.

This repo and documents there-in are meant to grow with me as long as I decide to continue on this hobby. My goal is to document the architecture, config templates, and design decisions behind my homelab.

If you're a rookie like me, let's learn together. If you're more experienced, I'd love some feedback. 

Main goals:
	Replace paid subscription services with self-hosted free and open-source alternatives where practical.

Secondary goals: 
	Learn network engineering and system admin concepts and technologies: 
		IPTV 
		RouterOS (MikroTik) 
		OpenWRT 
		VLAN design and segmentation 
		VoIP 
	Learn server and infrastructure management: 
		Cloud / Network Attached Storage 
		Containerization (Docker) 
		Virtualization (Proxmox) 

---
##### Structure 

ISP: Telus Home Internet (FTTH)

Main router: Mikrotik hEX RB750Gr3
	RouterOS 
	DHCP server, DNS, NTP server, VLAN support, VPN 
	WiFi via ISP AP

Secondary router: Cisco Linksys EA4500
	OpenWRT-based
	IoT 
	VoIP 
	WiFi VLAN (planned)

Servers: 
	Synology DS220+
		NAS 
	Proxmox VE (planned)
		LXC containers 
		VM  

Services:
	Jellyfin
	Pi-hole (planned) 
	Home Assistant (planned) 

Software (FOSS): 
	2FAS 
	Bitwarden 
	Chrono (Android) 
	Libby 
	Money Manager 
	Notesnook 
	Obsidian 
	Openlib (Android, experimental) 
	OsmAnd 
	Signal 
	Termux 

Subscriptions (free):
	Audible 
	DuckDNS
	Garmin 
	GitHub 
	Google 
	Ground News 
	Outlook
	stats.fm for Spotify 

Subscriptions (paid):
	Alpha Progression 
	Amazon Prime 
	Disney+ 
	IPTV 
	Netflix 
	Ooma 
	Proton Unlimited 
	Spotify 
	Strava
	Wyze

