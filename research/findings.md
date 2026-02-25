# Self-Hosted Beginner PDF - Research Findings

**Date:** February 2026  
**Source:** Reddit r/selfhosted, r/homelab, web searches, community posts

---

## Top 20 Beginner Questions from Reddit

### Hardware & Getting Started
1. **"What hardware do I need?"** - Confusion about Raspberry Pi vs old PC vs NUC vs dedicated server
2. **"Is a Raspberry Pi good enough to start?"** - Common misconception that Pi is ideal for beginners
3. **"Where do I start as a true beginner?"** - Overwhelmed by countless options
4. **"What OS should I run?"** - Ubuntu Server vs Debian vs Proxmox vs CasaOS
5. **"Do I need a static IP?"** - Confusion about dynamic IP vs DDNS

### Networking & Security
6. **"How do I access my services from outside home?"** - VPN vs reverse proxy vs Cloudflare Tunnel
7. **"What is a reverse proxy and why do I need one?"** - Nginx Proxy Manager, Traefik, Caddy confusion
8. **"How do I secure my self-hosted services?"** - Authentik, authentication, SSL certificates
9. **"Do I need a domain name?"** - Can you do this without buying a domain?
10. **"What is Docker and do I need it?"** - Containers vs bare metal confusion

### Service Selection
11. **"What should I host first?"** - Analysis paralysis on first service
12. **"What's the best media server?"** - Plex vs Jellyfin vs Emby debate
13. **"Is Nextcloud worth it?"** - Questions about complexity vs benefit
14. **"What about Home Assistant?"** - Smart home integration questions

### Troubleshooting & Maintenance
15. **"How do I update my services?"** - "Set and forget" misconception
16. **"My service isn't working, how do I debug?"** - Logging, common errors
17. **"How do I backup my data?"** - Backup strategies for beginners
18. **"Port forwarding vs VPN - which is safer?"** - Security tradeoffs

### Learning Curve
19. **"I have zero technical background, where do I start?"** - Non-technical beginners
20. **"How do I learn what I'm doing instead of just following tutorials?"** - Wanting to understand fundamentals

---

## Recommended First Services (Ranked by Beginner-Friendliness)

### Tier 1: Easiest - Start Here
| Rank | Service | Why Easy | Use Case |
|------|---------|----------|----------|
| 1 | **AdGuard Home** | One-container, network-wide ad blocking, simple UI | DNS-level ad blocking |
| 2 | **Jellyfin** | Free, open-source media server, great client apps | Movies, TV, personal media |
| 3 | **Vaultwarden** | Bitwarden alternative, simple Docker setup | Password management |
| 4 | **Home Assistant** | Massive community, lots of tutorials, YAML/simple modes | Smart home |

### Tier 2: Moderate - After Getting Comfortable
| Rank | Service | Why Moderate | Use Case |
|------|---------|--------------|----------|
| 5 | **Nextcloud** | More complex setup, but all-in-one solution | File sync, photos, calendar, contacts |
| 6 | **Immich** | Photo backup, excellent mobile apps | Google Photos alternative |
| 7 | **Nginx Proxy Manager** | GUI for reverse proxy, handles SSL | Access services remotely |
| 8 | **Pocket Casts/ArchiveBox** | Simple bookmark/archive service | Save articles, podcasts |

### Tier 3: Advanced - Later Goals
| Rank | Service | Complexity | Use Case |
|------|---------|------------|----------|
| 9 | **Traefik** | Advanced reverse proxy, config-heavy | Production deployments |
| 10 | **Authentik** | Identity provider, steep learning curve | Single sign-on, SSO |
| 11 | **WireGuard/Tailscale** | VPN for remote access | Secure external access |
| 12 | **n8n** | Automation platform | Workflow automation |

---

## The Learning Path (What to Learn in Order)

### Phase 1: Foundation (Week 1-2)
1. **Linux basics**
   - Command line navigation (ls, cd, mkdir, rm)
   - Text editing (nano, vim)
   - Package management (apt)
   - SSH access

2. **Networking fundamentals**
   - IP addresses (local vs public)
   - Ports and port forwarding
   - DNS basics (what happens when you type a URL)
   - DHCP basics

3. **Your first service**
   - Install via Docker Compose
   - Access via localhost
   - Basic troubleshooting

### Phase 2: Containerization (Week 2-3)
4. **Docker basics**
   - Containers vs images
   - Docker Compose file structure
   - Volumes for persistence
   - Networks

5. **Container management**
   - Portainer (beginner-friendly GUI)
   - Viewing logs
   - Restart policies

### Phase 3: Networking & Remote Access (Week 3-4)
6. **Reverse proxy concepts**
   - What it does and why
   - Nginx Proxy Manager (easiest to start)
   - SSL/HTTPS basics (Let's Encrypt)

7. **Remote access options**
   - VPN (WireGuard)
   - Cloudflare Tunnel (no port forwarding)
   - DDNS concepts

### Phase 4: Security (Week 4+)
8. **Authentication**
   - Basic auth, reverse proxy auth
   - Authentik introduction
   - OAuth/OIDC basics

9. **Hardening**
   - Firewall basics (ufw)
   - Fail2ban
   - Regular updates

### Phase 5: Advanced (Ongoing)
10. **Virtualization**
    - Proxmox basics
    - LXC vs VMs

11. **Backup strategies**
    - Rsync, Restic
    - Cloud backup
    - 3-2-1 rule

12. **Monitoring**
    - Uptime Kuma
    - Logs aggregation

---

## Gaps in Existing Guides

### 1. **No "Why Before How"**
- Most guides jump straight to installation
- Missing: *Why* self-host? What problems does it solve?
- Missing: Realistic expectations (maintenance required)

### 2. **Hardware Recommendations Are Outdated**
- Pi recommendations persist but community agrees: x86 (old PC/NUC) is better
- No clear guide on what specs actually matter
- Missing: Cost-benefit analysis of different approaches

### 3. **Security Is Either Over-Simplified or Overwhelming**
- "Just use a VPN" without explaining tradeoffs
- Or: Full security suite that's overkill for beginners
- Gap: Layered security approach - start simple, add layers

### 4. **The "First Service" Problem**
- Everyone says "start with X" but X varies wildly
- Missing: Decision tree for what to host first based on use case

### 5. **Maintenance Is Ignored**
- "Set up and forget" mentality leads to vulnerabilities
- Missing: Update strategies, monitoring for updates, backup testing

### 6. **No Clear Progression**
- Many guides are just lists of cool apps
- Missing: Logical ordering of complexity
- Gap: How do you know when you're ready for the next level?

### 7. **Troubleshooting Is Underrepresented**
- What to do when things break
- Common beginner mistakes
- How to read logs

### 8. **Mac/Windows Context Missing**
- Most guides assume Linux
- Missing: Working from macOS/Windows, using WSL, remote Linux server

---

## What Makes This Guide Different

Based on the gaps above, this PDF should:

1. **Start with "why"** - Set realistic expectations
2. **Recommend x86 hardware** - Explain why Pi has limitations
3. **Provide a decision tree** - "If you want X, start with Y"
4. **Include maintenance from day 1** - Updates, backups
5. **Build in troubleshooting** - Each section includes "what if it breaks"
6. **Show the progression** - Roadmap to advance skills
7. **Acknowledge different starting points** - Mac, Windows, Linux users

---

## Key Resources Mentioned by Community

### YouTube Channels
- Techno Tim
- Christian Lempa
- DB Tech

### Websites
- awesome-selfhosted (GitHub)
- selfh.st
- ITS FOSS articles

### Forums
- r/selfhosted
- r/homelab
- Proxmox forums

### Tools Frequently Recommended
- CasaOS (easy start UI)
- Portainer (Docker management)
- Nginx Proxy Manager (reverse proxy)
- Docker Compose (service management)
