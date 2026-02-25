# Table of Contents - Self-Hosted Beginner Guide

## Chapter Overview

This guide follows a proven learning journey: **why → what → first project → basics → security → growth**. Each chapter builds on the previous, with hands-on exercises and clear next steps.

---

## Chapter 1: Why Bother? (The "Why" Before the "How")

**Pages:** 4-5  
**Description:** Set realistic expectations about what self-hosting actually solves. Covers the benefits (privacy, control, learning) and the costs (time, maintenance, electricity). Debunks the "set and forget" myth.

**Learning Objectives:**
- Understand what self-hosting can and can't do for you
- Know what to expect in terms of time commitment
- Identify which problems you want to solve (privacy? media? automation?)
- Feel excited but grounded about starting

**"Do This Now" Step:** Write down 3 things you want to achieve by self-hosting

---

## Chapter 2: What Do You Actually Need?

**Pages:** 5-6  
**Description:** Cut through the hardware confusion. Explains why a used desktop PC or NUC beats a Raspberry Pi for most beginners. Covers the minimum specs, where to find cheap hardware, and what the community recommends.

**Learning Objectives:**
- Know the difference between x86 and ARM (and why it matters)
- Understand minimum hardware requirements
- Know where to source affordable hardware (Facebook Marketplace, eBay)
- Make an informed decision about what to buy or repurpose

**"Do This Now" Step:** Check what old computers you have lying around

---

## Chapter 3: Setting Up Your First Machine

**Pages:** 5-6  
**Description:** Walk through installing Ubuntu Server (or Debian). No prior Linux experience needed. Covers making a bootable USB, the installation process, and logging in for the first time.

**Learning Objectives:**
- Create a bootable USB installer
- Install Ubuntu Server from scratch
- Log in via terminal/SSH
- Understand the basic Linux directory structure

**"Do This Now" Step:** Install Ubuntu Server on your hardware (estimated 20 minutes)

---

## Chapter 4: Docker - Your First Container

**Pages:** 5-6  
**Description:** Explain containers in plain English (like shipping containers - standardized packages). Install Docker, run your first container, and understand why this makes everything easier.

**Learning Objectives:**
- Understand what Docker is and why it matters
- Install Docker on your server
- Run a simple container (like a "hello world" or simple web app)
- Know basic Docker commands (ps, logs, stop, rm)

**"Do This Now" Step:** Run `docker run hello-world` and see it work

---

## Chapter 5: Your First Service - AdGuard Home

**Pages:** 5-6  
**Description:** Install AdGuard Home as the first service - it's the easiest, most rewarding start. Network-wide ad blocking that works for all your devices immediately. No configuration needed.

**Learning Objectives:**
- Install a service using Docker Compose
- Access the service via web interface
- Configure devices to use your DNS server
- See immediate results (ads blocked!)

**"Do This Now" Step:** Set up AdGuard Home and configure one device to use it

---

## Chapter 6: Understanding Your Network

**Pages:** 5-6  
**Description:** Demystify networking basics: local IP vs public IP, what ports do, and how devices talk to each other. Uses visual explanations (like postal addresses for computers).

**Learning Objectives:**
- Find your local IP address
- Understand what ports are and why services use different ones
- Know the difference between local and public access
- Access your server from other devices on your network

**"Do This Now" Step:** Find your server's IP and access AdGuard from another device

---

## Chapter 7: Adding More Services - Media & Passwords

**Pages:** 5-6  
**Description:** Build on success by adding Jellyfin (media server) and Vaultwarden (password manager). These solve real problems and demonstrate the power of self-hosting.

**Learning Objectives:**
- Install multiple services using Docker Compose
- Set up persistent storage (volumes) so data survives restarts
- Access services by name on your local network
- Understand docker-compose.yml basics

**"Do This Now" Step:** Install Jellyfin and add one video file to stream

---

## Chapter 8: Accessing Your Services From Outside

**Pages:** 5-6  
**Description:** The big question: "How do I access this when I'm not home?" Covers the options: VPN (WireGuard/Tailscale) vs reverse proxy vs Cloudflare Tunnel. Recommends starting with Tailscale for simplicity.

**Learning Objectives:**
- Understand the security tradeoffs of remote access methods
- Set up Tailscale (easiest VPN for beginners)
- Access your services from anywhere securely
- Know when you'd need a domain name

**"Do This Now" Step:** Install Tailscale on your phone and server, test remote access

---

## Chapter 9: Securing Your Setup

**Pages:** 5-6  
**Description:** Now that you can access services remotely, lock it down. Covers: reverse proxy with SSL (Nginx Proxy Manager), basic authentication, and simple firewall rules.

**Learning Objectives:**
- Install and configure Nginx Proxy Manager
- Set up automatic SSL certificates (HTTPS)
- Add basic password protection to services
- Understand the layered security approach

**"Do This Now" Step:** Set up Nginx Proxy Manager and access a service via HTTPS

---

## Chapter 10: Keeping It Running

**Pages:** 5-6  
**Description:** The maintenance chapter nobody else writes about. How to update services without breaking things, set up backups, and monitor for problems. "Set and forget" is a myth.

**Learning Objectives:**
- Update Docker containers safely
- Set up a simple backup strategy
- Monitor services (Uptime Kuma)
- Know when to check for updates

**"Do This Now" Step:** Set up a backup for one service's data folder

---

## Chapter 11: Where Do You Go From Here?

**Pages:** 4-5  
**Description:** The roadmap for continued learning. Based on your goals, which path do you take? Smart home → Home Assistant. File sync → Nextcloud. Home automation → n8n. Plus resources for deeper learning.

**Learning Objectives:**
- Identify your next goal based on what you learned
- Know the recommended next services to try
- Find resources for continued learning (YouTube, forums, docs)
- Understand the path to more advanced topics (virtualization, monitoring)

**"Do This Now" Step:** Pick one service from the "next steps" list and research it

---

## Summary

| Chapter | Title | Pages |
|---------|-------|-------|
| 1 | Why Bother? | 4-5 |
| 2 | What Do You Actually Need? | 5-6 |
| 3 | Setting Up Your First Machine | 5-6 |
| 4 | Docker - Your First Container | 5-6 |
| 5 | Your First Service - AdGuard Home | 5-6 |
| 6 | Understanding Your Network | 5-6 |
| 7 | Adding More Services | 5-6 |
| 8 | Accessing From Outside | 5-6 |
| 9 | Securing Your Setup | 5-6 |
| 10 | Keeping It Running | 5-6 |
| 11 | Where Do You Go From Here? | 4-5 |

**Total:** 52-60 pages

---

## Design Notes

- **Zero jargon:** Every technical term gets explained on first use
- **Hands-on focus:** Every chapter has a concrete "do this now" action
- **Building blocks:** Each chapter builds on previous knowledge
- **Realistic expectations:** Maintenance, troubleshooting woven throughout
- **Multiple paths:** Chapter 11 helps readers find their unique next step
