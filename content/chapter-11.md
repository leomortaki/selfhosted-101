# Chapter 11: Where Do You Go From Here?

You've done something. You set impressive up a server from scratch, installed Docker, ran containers, got ads blocking across your network, streamed media from your own server, and even accessed it from outside your home. You learned about networking, security, and maintenance along the way.

That's not small stuff. Most people never get past "I should really learn to code someday." You're actually doing it.

But here's the thing: where you go next depends entirely on what *you* care about. Self-hosting isn't one path—it's dozens of paths that all start from the same place. This chapter helps you figure out which direction fits your life.

---

## Finding Your Direction

Think back to Chapter 1, where you wrote down three things you wanted to achieve. That list still matters. The best next step is the one that solves a problem you actually have, not one that sounds cool on a YouTube video.

Ask yourself: What's the one frustration I have right now that technology could fix?

- Is it that my photos are scattered across devices?
- Do I want my home lights and thermostat to work together?
- Am I tired of typing the same repetitive tasks over and over?
- Do I want to run my own calendar and contacts without Big Tech?

Whatever your answer, there's a self-hosted tool for it. Let's look at the main paths.

---

## Path 1: The Smart Home Path → Home Assistant

If you want your lights, sensors, thermostats, and gadgets to talk to each other, Home Assistant is the answer. It's the most popular open-source smart home system in the world, and for good reason.

Home Assistant connects to thousands of devices—even ones that don't normally work together. That old thermostat? The smart bulbs you bought on sale? The motion sensor in the garage? Home Assistant brings them all into one place.

**What it does:** Gives you a dashboard to control everything in your home, automations that run on their own (like "turn off all lights when everyone leaves"), and works with almost every smart device brand.

**Why it's great for you:** You already have a server running. Installing Home Assistant takes about 10 minutes with Docker. You'll recognize the compose file structure from Chapter 7.

**Where to start:** Check out the official Home Assistant website (home-assistant.io) and look for the Docker installation guide. The community is massive, so YouTube has excellent tutorials for beginners.

---

## Path 2: The "My Own Cloud" Path → Nextcloud

If you want to replace Google Drive, iCloud, or Dropbox with something you own, Nextcloud is the gold standard. It's like having your own private Google Workspace.

**What it does:** File storage and sync (like Dropbox), but also calendar, contacts, notes, video calls, and even document collaboration. You can install apps for almost anything—it's like a marketplace of useful tools.

**Why it's great for you:** Your server already has Docker. Nextcloud runs in a container just like everything else you've installed. You'll use volumes (remember those from Chapter 7?) to keep your files safe.

**Where to start:** The official Nextcloud Docker guide walks you through it. Be aware that Nextcloud needs a bit more setup than AdGuard—give yourself 30 minutes the first time. The documentation is good, and the subreddit r/Nextcloud is helpful if you get stuck.

---

## Path 3: The Automation Path → n8n

If you find yourself doing the same thing over and over—copying data between apps, sending the same notification, checking a website for updates—n8n (pronounced "n-eight-n") automates it.

**What it does:** Connects different services together. For example: "When I get an email with an attachment, save it to my Nextcloud and send me a text." Or: "Every morning, pull weather data and add it to my calendar." You build workflows by connecting blocks together, like digital LEGO.

**Why it's great for you:** n8n has a visual interface—you don't write code, you draw flows. But it's powerful enough that businesses use it too. You'll feel smart the moment your first automation runs on its own.

**Where to start:** The n8n website (n8n.io) has a cloud version, but you want the self-hosted version. Install it via Docker and start with one simple workflow, like forwarding a specific type of email to a folder.

---

## Path 4: The Media Fortress Path → More Media Tools

If Jellyfin got you excited, there's a whole world beyond it.

**Plex:** Similar to Jellyfin but with a more polished interface and optional paid features. Some people prefer it; some prefer Jellyfin. Try both.

**Sonarr, Radarr, and Lidarr:** These automate your media collection. Tell Sonarr which TV shows you want, and it finds and organizes them automatically. Radarr does the same for movies. Lidarr for music. They're like having a personal media manager that works while you sleep.

**Jellyseerr:** A request system for your media. Install this and your family or friends can request movies and shows. Radarr automatically grabs them. It's incredibly satisfying.

**Where to start:** Each of these runs beautifully in Docker. Search for "Trash Guides" online—they're the gold standard for how to set up these tools the right way.

---

## Path 5: The Privacy Fortress Path → More Security Tools

If locking down your digital life excites you more than automating it, here are some next-level tools.

**Vaultwarden:** You installed this in Chapter 7 as a password manager. But there's more: you can enable the Bitwarden browser extension, set up emergency access for family, and even share passwords securely with others.

**Authy or Bitwarden Authenticator:** Add two-factor authentication to your accounts. Self-hosting your 2FA codes is the ultimate privacy move.

**Pi-hole:** Think of it as AdGuard Home's bigger sibling. It does network-wide ad and tracker blocking at the DNS level, and has more customization for advanced users. You can even run Pi-hole and AdGuard together for maximum blocking.

---

## Path 6: The "I Want to Learn More" Path

Maybe you're not sure what to build yet. You just know you want to get better at this. Here's how to level up.

**Learn Linux properly:** You've been using Ubuntu Server, but you now have a perfect lab to experiment. Mess around with the command line, learn about permissions, understand how processes work. The "Linux Basics" course on Linux Journey (linuxjourney.com) is free and excellent.

**Try virtualization:** Instead of running everything directly on your server, you can run virtual machines—computers within your computer. Proxmox is the most popular choice for home users. It lets you run multiple independent systems on one piece of hardware.

**Set up monitoring:** Remember Uptime Kuma from Chapter 10? Pushover or Gotify can send you real alerts when things break. Build a dashboard that shows you everything about your server in one glance.

**Join the community:** The self-hosting subreddit (r/selfhosted) has over 400,000 members. The Home Assistant community is massive. Discord servers exist for nearly every major tool. Don't learn alone—ask questions, share what you've built, and learn from others.

---

## Resources for Continued Learning

Here's where to go when you get stuck or want to learn more:

**YouTube Channels:**
- *Techno Tim* – Excellent tutorials on Docker, Home Assistant, and infrastructure
- *DB Tech* – Great for beginners, clear explanations
- *Iron Geek* – Good for security-focused content
- *Everything Smart Home* – Focused on Home Assistant

**Websites:**
- *Awesome Selfhosted* (github.com/awesome-selfhosted/awesome-selfhosted) – A massive list of every self-hosted tool
- *Linuxize* – Tutorials for common server tasks
- *StackLinux* – Beginner-friendly guides

**Communities:**
- r/selfhosted on Reddit
- r/HomeAssistant
- r/Docker
- Discord servers for specific tools (Home Assistant, n8n, and others have official ones)

---

## A Note on Going Deeper

As you add more services, your server will get more complex. That's fine—that's how you learn. But a few reminders from earlier chapters:

- Update regularly (Chapter 10)
- Check your backups
- Don't expose things to the internet unless you really need to
- When something breaks, Google the error message. Someone else has had the same problem.

The self-hosting community is incredibly generous with knowledge. Almost every problem you face has been solved and documented somewhere.

---

## Your Turn: Do This Now

Here's your final exercise—the one that turns this book from something you read into something that changes your daily life:

**Step 1:** Read back through this chapter and the paths listed.

**Step 2:** Pick ONE path that excites you. Not five. One.

**Step 3:** Spend 15 minutes researching that specific tool. Search for "[tool name] Docker tutorial" or "[tool name] getting started."

**Step 4:** Install it this week. It doesn't have to be perfect. It just has to run.

That's it. You've already done the hardest part—you started. Everything from here is building on what you already know.

---

## What's Next Is Up to You

Self-hosting isn't a destination. It's a continuous process of learning, building, breaking, and fixing. Some weeks you'll learn something new and feel like a wizard. Other weeks something will break at 2 AM and you'll question everything.

Both are part of the deal. And both are worth it.

You now have skills that most people never develop. You understand how the internet actually works under the hood. You can build tools that solve real problems in your life. You own your data and your infrastructure.

That's powerful. Use it well.

Go build something.
