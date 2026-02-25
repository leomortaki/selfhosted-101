# Chapter 8: Accessing Your Services From Outside

*Estimated reading time: 15 minutes*

---

## The Problem You're Facing

By now, you've got services running on your server at home. AdGuard is blocking ads. Jellyfin is streaming your videos. Vaultwarden is keeping your passwords safe. Life is good.

But here's the catch: all of this only works when you're on your home WiFi.

What happens when you're at work and need a password from Vaultwarden? Or you're traveling and want to watch a movie from your Jellyfin library? Or you're at a coffee shop and want to check on your home network?

This chapter answers the most common question beginners ask: **"How do I access my stuff when I'm not at home?"**

---

## Why Can't You Just Open a Port?

You might think: "Why not just open my server to the internet and type in my home IP address?"

Technically, you could do that. But there are three big problems:

1. **Your home IP address changes.** Internet providers periodically change your public IP address. Tomorrow, your "front door" might be at a completely different number. You can't memorize a changing address.

2. **It's not secure.** Opening a port directly to the internet is like leaving your front door unlocked. Anyone can try to get in. Hackers constantly scan the internet for open ports and try to guess passwords.

3. **No encryption.** When you access your server from outside, your data travels through the public internet. Without protection, anyone on the same WiFi as you (or monitoring network traffic) can see your passwords and sensitive information.

So we need a better solution. Let's look at your options.

---

## Your Three Options (In Plain English)

### Option 1: VPN - The Secure Tunnel

Think of a VPN (Virtual Private Network) like a secret tunnel that connects your phone directly to your home network. When you use a VPN, your phone "pretends" to be on your home WiFi, even when you're thousands of miles away.

**How it works:** You install VPN software on both your server and your phone. When you connect, your phone creates an encrypted tunnel to your home. All your traffic goes through this tunnel, like a private highway that nobody else can use.

**Pros:**
- Very secure (encryption is built-in)
- Works with all services (no special configuration per service)
- You don't need to buy a domain name

**Cons:**
- Slight learning curve to set up
- Need to remember to turn on the VPN before accessing your services

### Option 2: Reverse Proxy - The Reception Desk

A reverse proxy is like having a receptionist at your home. When someone from the outside world wants to visit, they don't go directly to your server. Instead, they go to your "receptionist" (the proxy), who then directs them to the right service.

This is how websites work. But for home services, you'd typically buy a domain name (like myhome.dynv6.net) and point it to your home.

**How it works:** When you type yourdomain.com/vaultwarden, the proxy sees the "/vaultwarden" part and sends you to your password manager. When you type yourdomain.com/jellyfin, it sends you to your media server.

**Pros:**
- Easy to remember URLs (yourdomain.com instead of an IP address)
- Professional feel
- Works great when you need to share access with others

**Cons:**
- Requires buying a domain name (costs money)
- More complex to set up
- Need to handle SSL certificates for security

### Option 3: Cloudflare Tunnel - The Smart Shortcut

Cloudflare Tunnel is a newer approach that doesn't require opening any ports on your home network. Instead, your server connects OUT to Cloudflare's servers, creating a secure path. When you want to access your services, you go through Cloudflare.

**How it works:** You install a small program on your server that creates a permanent connection to Cloudflare. Cloudflare then handles the outside world, routing traffic to your home through that connection. You never open any ports.

**Pros:**
- No port forwarding needed (more secure by default)
- Built-in security features from Cloudflare
- Works without a static IP

**Cons:**
- Need to use Cloudflare's ecosystem
- Slight dependency on an external service
- Can be confusing to set up for beginners

---

## Which One Should You Start With?

For most beginners, we recommend **Tailscale** (a VPN built on WireGuard). Here's why:

1. **Easiest to set up.** Tailscale was designed to be simple. Install an app on your phone, run a command on your server, and you're done. No router configuration, no domain names, no port forwarding.

2. **Works automatically.** Once set up, you don't need to think about it. Your phone is always "on" your home network when you turn on the VPN.

3. **Free for personal use.** Tailscale offers a free tier that's more than enough for personal self-hosting.

4. **Encryption built-in.** All your traffic is encrypted automatically. Safe on public WiFi.

Think of it this way:
- **VPN (Tailscale)** = Direct secure tunnel to your home
- **Reverse Proxy** = Professional setup with custom domain (good for sharing with others)
- **Cloudflare Tunnel** = No-ports-needed approach (good for complex setups)

Start with Tailscale. Once you're comfortable, you can explore the others.

---

## What You'll Need

Before we start, make sure you have:
- Your server running (from Chapter 3)
- A phone, tablet, or laptop you want to use to access your services remotely
- An email address (for Tailscale account)
- About 15 minutes

---

## Installing Tailscale on Your Server

Let's start by installing Tailscale on your server. This is the "home base" end of your secure tunnel.

### Step 1: Install Tailscale

Copy and paste this command into your server's terminal:

```bash
curl -fsSL https://tailscale.com/install.sh | sh
```

This downloads and installs the Tailscale software. You'll see some text scroll by as it installs.

### Step 2: Connect to Your Network

Once installed, tell Tailscale to connect to your account:

```bash
sudo tailscale up
```

This will open a web browser link (or give you a URL to visit). Click it, sign in with your email, and approve your device.

That's it! Your server is now part of your private Tailscale network.

### Step 3: Note Your Tailscale IP

Tailscale will show you an IP address that starts with `100.`. This is your server's address on your private network. Write it down—you'll need it.

For example: `100.64.123.456`

---

## Installing Tailscale on Your Phone

Now let's get your phone connected.

### On iPhone (App Store) or Android (Play Store):
1. Search for "Tailscale" and install the app
2. Open the app and sign in with the same account you used on your server
3. Tap "Start"

Your phone is now connected!

### On Computer (Mac/Windows/Linux):
1. Go to https://tailscale.com/download
2. Download and install the app for your operating system
3. Sign in with the same account
4. Turn on the connection

---

## Testing Your Connection

Now let's verify that everything works.

### From your phone:
1. Make sure you're NOT on your home WiFi (turn off WiFi and use mobile data, or go to a friend's house)
2. Open your browser and type the Tailscale IP you wrote down earlier (the `100.` address)
3. Add the port number for a service you know is running

For example: `http://100.64.123.456:8080`

- Port 8080 = AdGuard (if you set it up in Chapter 5)
- Port 8096 = Jellyfin (if you set it up in Chapter 7)

You should see your service! 🎉

### Try this:
- Open Vaultwarden (port 8081) and log in
- Open Jellyfin (port 8096) and play a video
- Open AdGuard (port 8080) and check your statistics

You're now accessing your home services from anywhere in the world, through an encrypted tunnel. The data between your phone and your server is completely private.

---

## How to Find Your Service Ports

In the previous chapters, we mentioned ports but didn't explain them in detail. Here's a quick reference:

When you set up a service with Docker (like in Chapter 5 and 7), the docker-compose.yml file specifies which port to use. You can always check:

- In your docker-compose.yml file, look for `ports:` - the number after the colon is the port
- Or run `docker ps` on your server to see all running containers and their ports

Common ports you'll use:
- 8080 = AdGuard Home
- 8081 = Vaultwarden
- 8096 = Jellyfin

---

## Understanding What Just Happened

Let me explain what you just built:

```
[Your Phone] ---> [Internet] ---> [Tailscale Tunnel] ---> [Your Server]
                 (encrypted)                         (decrypts here)
```

When you access your server through Tailscale:
1. Your phone encrypts your request
2. It goes through the public internet to Tailscale's servers
3. Tailscale routes it to your home server through the tunnel you created
4. Your server decrypts it, processes your request, and sends back the answer
5. The answer comes back through the same encrypted tunnel

Anyone watching the internet traffic sees only gibberish. They can't see your passwords, your videos, or which services you're accessing.

---

## What Tailscale Doesn't Work?

Sometimes If, home internet routers have settings that interfere. If your connection doesn't work:

1. **Check that Tailscale is running on both devices** - Look for the green indicator in the app

2. **Check your firewall** - Some routers have built-in firewalls that might block Tailscale. Try accessing from a different network (like your phone's mobile data)

3. **Check the IP address** - Make sure you're using the Tailscale IP (the 100.x.x.x address), not your home's public IP

4. **Restart Tailscale** - Run `sudo tailscale down` then `sudo tailscale up` on your server

Most connection issues resolve themselves within a few minutes of setup.

---

## When Would You Need a Domain Name?

You might be wondering: "Do I ever need to buy a domain name?"

Not for Tailscale. The 100.x.x.x address works forever.

But you might want a domain name if:
- You want to share access with friends and family (easier to remember than an IP)
- You want professional-looking URLs
- You want to set up multiple services with nice addresses (like vault.myhouse.com instead of 100.x.x.x:8081)

We'll cover domain names and reverse proxies in Chapter 9, once you've got the basics down.

---

## What's Next?

You now have secure, encrypted access to all your home services from anywhere in the world. This is a huge milestone!

In the next chapter, we'll talk about security. Now that you can access your services remotely, we need to make sure nobody else can. We'll cover:
- Setting up a reverse proxy (Nginx Proxy Manager)
- Adding automatic HTTPS (SSL certificates)
- Adding password protection to your services

But first, let's make sure you can actually access your services. That's what we'll practice right now.

---

## Do This Now

**Your mission, should you choose to accept it:**

1. **Install Tailscale on your server** (run the install command from this chapter)

2. **Connect it to your account** (run `sudo tailscale up` and follow the link)

3. **Install Tailscale on your phone** (or another device)

4. **Test remote access** - Turn off your home WiFi, use mobile data, and access one of your services

Take a screenshot of yourself accessing Jellyfin or Vaultwarden from outside your home. This is a real achievement!

**Expected time:** 15-20 minutes  
**Difficulty:** Easy  
**You'll feel like a hacker.** 🕵️

---

## Quick Reference

### Useful Tailscale Commands (for your server)

```bash
# Check status
tailscale status

# Turn off Tailscale
sudo tailscale down

# Turn on Tailscale
sudo tailscale up

# See your Tailscale IP
tailscale ip -4
```

### Troubleshooting Checklist

| Problem | Solution |
|---------|----------|
| Can't connect | Make sure Tailscale is running on both devices |
| Wrong page loads | Check you're using the right port number |
| Connection slow | Try a different network (mobile vs WiFi) |
| Services not running | Check with `docker ps` that your services are actually running |

---

## Recap

In this chapter, you learned:

- Why opening ports directly to the internet is a bad idea
- The three main ways to access your services remotely: VPN (Tailscale), reverse proxy, and Cloudflare Tunnel
- Why Tailscale is the easiest starting point for beginners
- How to install and configure Tailscale on both your server and phone
- How to test your remote access connection

You now have the power to access your entire home server from anywhere. This opens up a world of possibilities—checking your security cameras, grabbing a password, streaming your media, all from your phone.

In the next chapter, we'll make sure nobody else can access your services without permission. Security time! 🔐
