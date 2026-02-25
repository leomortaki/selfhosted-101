# Chapter 9: Securing Your Setup

*Estimated reading time: 15 minutes*

---

In the last chapter, you learned how to access your services from anywhere using Tailscale. That's incredibly useful—but here's an important truth: anytime you open a door to the outside world, you need a lock on it.

Think of it like your home. You want guests to visit, so you have a front door. But you don't leave it wide open, do you? You have a lock, maybe a doorbell camera, and you probably ask who someone is before letting them in.

The same thinking applies to your self-hosted services. In this chapter, you'll learn how to:

- Set up a secure gateway that handles all incoming traffic (Nginx Proxy Manager)
- Encrypt the connection so nobody can spy on your data (SSL/HTTPS)
- Add password protection as a first line of defense
- Set up a firewall to block unwanted visitors

Let's get your setup locked down.

---

## What Does "Securing" Actually Mean?

Before we dive in, let's clarify what we're actually protecting against.

When you expose a service to the internet—even with a VPN like Tailscale—you're creating a potential entry point. Here's what can go wrong if you don't secure things:

**1. Unencrypted connections = Anyone can read your data**

When you access a service over plain HTTP (without the "S"), your password, messages, and data travel as plain text. Imagine sending a postcard instead of a sealed letter—anyone who handles it can read it.

**2. No password protection = Anyone can walk right in**

Some services come with no default password at all. If someone guesses the web address, they can access everything.

**3. Open ports = An unlocked window**

Every service that listens on the internet has a "port." Leaving ports open without protection is like leaving windows open with no screens.

The good news? You don't need to be a security expert. We'll use tools that handle most of this automatically.

---

## Meet Your Security Guard: Nginx Proxy Manager

In Chapter 8, you learned about reverse proxies—a piece of software that sits in front of your services and directs traffic. Nginx Proxy Manager (often abbreviated as NPM) is that same idea, but with superpowers.

NPM does three important things:

1. **Routes traffic** - It receives incoming requests and sends them to the right service (like a receptionist directing visitors)

2. **Adds encryption automatically** - It fetches and manages SSL certificates (we'll explain what those are in a moment) without you needing to do anything technical

3. **Adds password protection with one click** - You can require a username and password before anyone even reaches your service

Think of Nginx Proxy Manager as a combination of a receptionist, an encrypted tunnel builder, and a bouncer. Pretty powerful, right?

### Installing Nginx Proxy Manager

NPM runs as a Docker container, just like the services you've already installed. Here's the docker-compose.yml:

```yaml
version: '3.8'

services:
  npm:
    image: 'jc21/nginx-proxy-manager:latest'
    container_name: nginx-proxy-manager
    restart: unless-stopped
    ports:
      - '80:80'      # HTTP traffic
      - '443:443'   # Encrypted HTTPS traffic
      - '81:81'     # NPM's own admin interface
    volumes:
      - ./data:/data
      - ./letsencrypt:/etc/letsencrypt
```

Save this as `docker-compose.yml` in a new folder called `nginx-proxy-manager`, then run:

```bash
docker-compose up -d
```

Give it a minute to start up, then open your browser and go to:

```
http://YOUR_SERVER_IP:81
```

You'll see the NPM login screen. The default credentials are:

- **Email:** admin@example.com
- **Password:** changeme

*Change these immediately after logging in!*

---

## What Is SSL/HTTPS? (The Simple Version)

You know how some website addresses start with "http://" and others with "https://"? That extra "s" stands for "secure." But what does it actually mean?

**Without HTTPS (http://):** When your phone sends your password to your server, it's like whispering it across a crowded room. Anyone close enough can hear it.

**With HTTPS (https://):** It's like speaking in a secret language that only you and your server understand. Even if someone overhears, they can't understand anything.

The "secret language" is enabled by something called an SSL certificate. It's not as complicated as it sounds—it's just a small file that proves your server is who it claims to be, and it encrypts everything in transit.

Here's the beautiful part: Nginx Proxy Manager can get these certificates for free, automatically, from a nonprofit called Let's Encrypt. You don't need to pay anything or understand the technical details.

### Enabling HTTPS for a Service

Once NPM is running, here's how to add HTTPS to any service:

**Step 1:** In NPM, click "Proxy Hosts" → "Create Proxy Host"

**Step 2:** Fill in the details:

- **Domain Name:** The web address people will use (e.g., jellyfin.yourhome.com)
- **Forward IP:** Your server's local IP address (e.g., 192.168.1.100)
- **Forward Port:** The port your service runs on (e.g., 8096 for Jellyfin)

**Step 3:** Scroll down and check these options:

- **Force SSL:** This automatically redirects anyone trying to use plain HTTP to the secure version
- **Enable SSL/HTTPS:** Click this and select "Request a new SSL Certificate"

**Step 4:** Enter your email address (Let's Encrypt uses this to remind you when certificates are due for renewal)

**Step 5:** Click Save

That's it. NPM will contact Let's Encrypt, get the certificate, and configure everything. Within seconds, your service is accessible via HTTPS.

You'll see a little lock icon in your browser's address bar. That lock means the connection is secure.

---

## Adding Basic Password Protection

Even with HTTPS, you might want an extra layer of security. Maybe you haven't set up strong passwords on all your services yet, or you want to make absolutely sure only you can access them.

NPM lets you add "Basic Authentication" with just a few clicks. This means anyone trying to access a service must enter a username and password that you define—not the service's own login.

### Setting It Up

**Step 1:** In NPM, go to the proxy host you created earlier and click "Edit"

**Step 2:** Scroll to the "Basic Authentication" section

**Step 3:** Check "Enable Basic Authentication"

**Step 4:** Click "Add" to create a user. Enter:
- **Username:** (pick something like "admin" or "family")
- **Password:** (pick a strong password)

**Step 5:** Click Save

Now when anyone tries to access that service—even from inside your home network—they'll see a popup asking for the username and password you just created.

*Important:* This is an extra layer, not a replacement for good passwords on your actual services. Think of it like a security gate outside your house—you still want locks on your doors inside.

---

## Your Digital Bouncer: The Firewall

Now let's talk about the firewall. If NPM is the receptionist and the bouncer, the firewall is the walls around your property. It decides which doors exist and who's allowed to knock on them.

A firewall monitors all incoming and outgoing network traffic and blocks anything that doesn't meet your rules. For a home server, you typically want to:

- **Allow** traffic you've specifically requested (like your own web browsing)
- **Block** incoming traffic unless it's for a service you want publicly accessible

### The Simple Firewall Setup

For most home self-hosters, you don't need complex firewall rules. Here's the practical approach:

**1. Only open ports you need**

Remember when we talked about ports in Chapter 6? Each service uses a specific port. Instead of opening everything, only open:

- Port 80 (HTTP)
- Port 443 (HTTPS)

These are the standard web ports. NPM will handle routing traffic to your services from these ports—you don't need to open individual ports for each service.

**2. Use UFW (Uncomplicated Firewall)**

Ubuntu comes with a firewall tool called UFW (Uncomplicated Firewall—computer people love acronyms). It's already installed; you just need to turn it on.

Run these commands:

```bash
# Check status
sudo ufw status

# Allow SSH (so you don't lock yourself out!)
sudo ufw allow ssh

# Allow HTTP and HTTPS
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp

# Turn on the firewall
sudo ufw enable
```

*Warning:* Never lock yourself out of SSH! Always allow SSH (port 22) before enabling the firewall.

**3. Check who tried to visit**

You can see blocked attempts with:

```bash
sudo ufw status numbered
```

You might be surprised how many automated bots are constantly scanning the internet, looking for weak spots. The firewall stops them at the door.

---

## Security Layers: How It All Fits Together

Let's visualize your security setup now:

```
Internet
    ↓
[Firewall - Blocks unwanted ports]
    ↓
[Nginx Proxy Manager - Routes to correct service]
    ↓
[SSL Certificate - Encrypts the connection]
    ↓
[Basic Auth - Password gate]
    ↓
[Your Service - The actual app]
```

Each layer does a specific job. Even if one layer fails, others are there as backup. This is called "defense in depth"—a fancy term for "lots of locks are better than one."

Here's the order of what a random stranger on the internet would encounter:

1. **Firewall:** "Sorry, the door is closed."
2. **Without proxy:** They might find an open port but won't know which service it leads to
3. **With NPM:** They reach the right service, but no SSL means the connection is visible
4. **With SSL:** The data is encrypted, but they'd still need to guess your password
5. **With Basic Auth:** They need your username and password just to get through the door

That's five layers of defense. Not bad for a beginner setup!

---

## Common Mistakes to Avoid

Before we move to the exercise, let's cover some pitfalls:

**Mistake #1: Opening too many ports**

More open ports = more potential entry points. Only open what you need, and route everything through NPM.

**Mistake #2: Using weak passwords**

If your basic auth password is "password123," it's not really protection. Use a password manager (you installed Vaultwarden in Chapter 7, right?) to generate strong, unique passwords.

**Mistake #3: Ignoring certificate renewals**

Let's Encrypt certificates expire after 90 days. The good news: NPM automatically renews them. Just don't stop the container for too long!

**Mistake #4: Turning off the firewall "because it's annoying"**

Yes, sometimes the firewall blocks things you want. But it's protecting you. Learn which rules to add instead of turning it off.

---

## Do This Now

Time to put this chapter into action. Here's your exercise:

### Set Up Nginx Proxy Manager with SSL

**What you'll accomplish:** Install NPM, add one of your existing services (like Jellyfin or Vaultwarden), and access it via HTTPS with basic authentication.

**Steps:**

1. **Create the NPM folder and docker-compose.yml** (use the code from earlier in this chapter)

2. **Start the container:**
   ```bash
   cd nginx-proxy-manager
   docker-compose up -d
   ```

3. **Access NPM admin interface** at `http://YOUR_SERVER_IP:81` and change the default password

4. **Create a proxy host** for one of your existing services:
   - Use a simple subdomain like `jellyfin.yourhome.local` (you don't need a real domain for local use)
   - Forward to your server's IP and the service's port
   - Enable SSL and select "Request a new SSL Certificate"
   - Add basic authentication with a username and strong password

5. **Test it:** Access the service through the new URL. You should see:
   - A lock icon in your browser (SSL working)
   - A popup asking for username/password (basic auth working)

**Congratulations!** You've just secured your first service. This same process works for any other services you want to expose.

---

## What's Next?

In Chapter 10, we'll cover the unsexy but essential topic of maintenance. How do you update services without breaking things? How do you back up your data? What happens if your server crashes?

"Set and forget" is a myth—but with the right maintenance habits, you can keep your setup effort.

See you there!
 running smoothly with minimal