# Chapter 6: Understanding Your Network

## Why This Chapter Matters

In the last chapter, you installed AdGuard Home and got it running on your server. You can access it from your server's web browser—but that's not very useful. You want to access it from your laptop, your phone, your smart TV—any device in your home.

To do that, you need to understand how devices find each other on your network. This is the missing piece that confuses most beginners, and it's actually simpler than you think.

Think of your home network like a small town. Your router is the post office. Every house has a unique address. And your server is one of the houses—waiting to receive mail (requests) and send back responses.

Let's demystify this.

---

## Your Network Is Like a Neighborhood

Imagine a small neighborhood with houses on it. Each house has a unique house number:

- House #1: The family laptop
- House #2: Your phone
- House #3: Your server (where AdGuard lives)
- House #4: Your smart TV

When your phone wants to ask your server "Hey, show me the AdGuard dashboard," it needs to know where the server lives. That's where IP addresses come in.

### What Is an IP Address?

An **IP address** is just a unique number that identifies a device on your network. It's like a house address, but for computers.

In most home networks, IP addresses look something like this: `192.168.1.100`

Break it down:
- `192.168.1` — this part is your network (every device in your home shares this)
- `.100` — this last number is the unique identifier for a specific device

So your server might be `192.168.1.100`, your phone might be `192.168.1.105`, and so on.

These are called **local IP addresses** because they only work inside your home network. That's why you can't type your server's IP address into your phone when you're at a coffee shop—it won't work. Your phone isn't on your home network anymore.

---

## Finding Your Server's Address

Now let's find your server's IP address. This is something you'll need often, so learn it now.

### On Your Server (Ubuntu)

Run this command on your server:

```bash
ip a
```

Look for the section called `eth0` or `ens` followed by numbers. You'll see something like:

```
inet 192.168.1.100/24
```

That `192.168.1.100` is your server's local address. Write it down—you'll use it constantly.

### The Easy Way: Check Your Router

If that command feels intimidating, here's an alternative:

1. Log into your router (usually by typing `192.168.1.1` in a browser)
2. Look for a section called "Connected Devices" or "DHCP Clients"
3. You'll see a list of all devices on your network, including your server

Your router's manual or the sticker on the bottom will tell you the login credentials.

---

## Ports: The Doors of Your House

Now you know the address. But there's one more piece: the **port**.

Think of your server as an apartment building with many doors. Each door (port) leads to a different service:

- Port 80: The front door (regular websites)
- Port 443: The secure front door (websites with the lock icon)
- Port 3000: AdGuard's specific door
- Port 53: The DNS door (what AdGuard uses)

When you type `192.168.1.100:3000` into your browser, you're saying: "Go to house number 192.168.1.100, and use door number 3000."

That's it.

### Common Ports You'll Encounter

| Service | Port | What It's For |
|---------|------|---------------|
| HTTP (regular website) | 80 | Viewing websites |
| HTTPS (secure website) | 443 | Viewing secure websites |
| AdGuard Home | 3000 | Its web interface |
| SSH | 22 | Logging into your server remotely |
| Plex/Jellyfin | 32400 / 8096 | Media servers |

You don't need to memorize these. But when you install new services, you'll often need to know which port they use—so always check the installation instructions.

---

## How Devices Talk to Each Other

Here's the flow when your phone accesses AdGuard:

1. Your phone says: "I want to talk to 192.168.1.100, port 3000"
2. Your router (the post office) forwards that request to your server
3. Your server's AdGuard service receives it
4. AdGuard responds with the data your phone needs
5. The data travels back through the router to your phone

This happens in milliseconds. You won't notice any delay.

### Local vs. Public: The Key Distinction

This is where most people get confused.

**Local access** (from inside your home):
- You type `192.168.1.100:3000` on your laptop
- It works perfectly
- Your request never leaves your house

**Public access** (from outside your home):
- You try to type your home IP address from a coffee shop
- It doesn't work
- Your request has no way to find your home network

We'll cover how to access your services from outside your home in Chapter 8. For now, focus on getting comfortable accessing services from devices *inside* your network.

---

## Accessing AdGuard from Another Device

This is the moment you've been building toward. Let's actually do it.

### Do This Now: Access AdGuard from Your Laptop

**Step 1:** Make sure your laptop is connected to the same WiFi network as your server.

**Step 2:** Open a web browser on your laptop (Chrome, Firefox, Safari—whatever you prefer).

**Step 3:** In the address bar, type:

```
http://192.168.1.100:3000
```

(Replace `192.168.1.100` with whatever your server's IP address actually is)

**Step 4:** Press Enter.

You should see the AdGuard Home login screen! If you set up a password in Chapter 5, log in. If not, you're directly in.

**Step 5:** Try accessing it from your phone too.

- Connect your phone to the same WiFi
- Open your phone's browser
- Type the same address: `http://192.168.1.100:3000`

You now have network-wide ad blocking working from every device in your house. That's powerful!

### Troubleshooting

If it doesn't work:

1. **Double-check the IP address** — run `ip a` on your server again to confirm
2. **Check the port** — make sure you typed `:3000` (the colon matters!)
3. **Are you on the same network?** — make sure laptop and server share the same WiFi
4. **Is Docker running?** — run `docker ps` to confirm AdGuard is actually running

Don't panic if it doesn't work immediately. Networking can be finicky. Check each item systematically, and you'll find the issue.

---

## What You've Learned

Let's recap what this chapter covered:

- **IP addresses** are like house numbers for devices on your network
- **Local IP addresses** only work inside your home
- **Ports** are like doors—each service uses a different one
- Your router acts as the post office, directing traffic to the right place
- Accessing services by IP:port lets you reach any device on your network

You now have the foundation to understand how your entire home network works. This knowledge applies to every service you'll install going forward.

---

## What's Next

In the next chapter, we'll build on this knowledge. You'll install two more services: Jellyfin (for your personal Netflix) and Vaultwarden (for a password manager that you control).

But first, take a moment to appreciate what you just accomplished. You installed a network-wide ad blocker that works on every device in your house—from your laptop to your smart TV. That's something most people never figure out.

You just did.

---

## Quick Reference

### Finding Your Server's IP
```bash
ip a
```

### Checking Running Services
```bash
docker ps
```

### Accessing AdGuard
```
http://[YOUR_SERVER_IP]:3000
```

### Checking Your Public IP (for curiosity)
```bash
curl ifconfig.me
```

---

## "Do This Now" Summary

✅ **Done:** Found your server's IP address using `ip a`  
✅ **Done:** Accessed AdGuard from your laptop browser  
✅ **Done:** Accessed AdGuard from your phone  

If you completed all three, congratulations—you understand your network!
