# Chapter 5: Your First Service - AdGuard Home

*Finally! Let's install something useful.*

In the last chapter, you installed Docker and ran a test container. That was practice. Now let's install something you'll actually use every day.

We're going to install **AdGuard Home**. Here's what it does:

**It blocks ads and trackers across your entire home network.**

That means every phone, tablet, computer, and smart TV in your house will get fewer ads. No browser extensions needed. No per-device setup. You set it up once, and it works for everything.

---

## What Is AdGuard Home, Really?

Imagine you have a bouncer at the entrance of your home network. Every time a device asks, "Hey, can I load this website?" AdGuard checks a list. If the website is known for showing ads or tracking you, AdGuard says "Nope" and blocks it.

The cool part? You don't need to install anything on your devices. You just change one setting on your router (we'll get to that), and every device on your network automatically uses AdGuard.

Benefits you'll notice:

- **Fewer ads** on YouTube, websites, and apps
- **Faster loading** pages (blocked stuff doesn't load)
- **More privacy** (trackers get blocked)
- **Less data usage** on your mobile plan

Let's install it.

---

## Step 1: Create the Folder Structure

Remember how Docker works? You need a folder to store your service's configuration. Let's create one for AdGuard.

On your server, run:

```bash
mkdir -p ~/docker/adguard
cd ~/docker/adguard
```

That's it. We created a folder called `adguard` inside your `docker` folder.

---

## Step 2: Write the Setup Instructions (Docker Compose)

In the last chapter, you ran containers one at a time using `docker run`. For more complex services, we use a file called `docker-compose.yml`. This file tells Docker everything it needs to know about your service.

Create this file inside your `adguard` folder:

```bash
nano docker-compose.yml
```

Now paste in these lines:

```yaml
version: "3"

services:
  adguard:
    image: adguard/adguardhome
    container_name: adguard
    restart: unless-stopped
    ports:
      - "53:53/tcp"
      - "53:53/udp"
      - "3000:3000/tcp"
    volumes:
      - ./work:/opt/adguardhome/work
      - ./conf:/opt/adguardhome/conf
```

What does all this mean? Let's break it down:

- **image**: This tells Docker what software to download (AdGuard Home)
- **container_name**: A friendly name for this container
- **restart: unless-stopped**: If your server restarts, AdGuard automatically starts again
- **ports**: These are like doorways. Port 53 is for DNS (what we're blocking ads with). Port 3000 is for the web interface where you'll manage it.
- **volumes**: These are folders that live on your server but are accessible inside the container. We need two: one for its work files and one for your settings. That way, if you delete and recreate the container, your settings stay.

When you've pasted it in, save and exit:

- Press **Ctrl + O** (the letter O, not zero)
- Press **Enter**
- Press **Ctrl + X**

---

## Step 3: Start AdGuard

Now let's actually run it:

```bash
docker compose up -d
```

You should see something like:

```
[+] Running 1/1
 ✔ adguard  Started
```

Congratulations! AdGuard Home is running.

---

## Step 4: Set It Up Through the Web Interface

Now comes the easy part. AdGuard has a visual interface you can use from your browser.

From a computer on the same network as your server, open your browser and type:

```
http://192.168.1.X:3000
```

*Wait—what's the IP address?*

Right. In Chapter 3, you set up your server, but let's quickly find its IP address again. On your server, run:

```bash
hostname -I
```

The first number shown is your server's IP address. It probably looks something like `192.168.1.100`.

So in your browser, you'd type:

```
http://192.168.1.100:3000
```

(Replace the numbers with whatever your server shows you.)

You should see a welcome screen. Let's finish the setup:

**Step 1: Getting Started**
Click "Get Started."

**Step 2: Web Interface**
Leave the settings as they are. Just note the port (3000) — that's how you'll access AdGuard later. Click "Next."

**Step 3: DNS Settings**
Again, leave defaults. Click "Next."

**Step 4: Create Admin Account**
This is important. Create a username and password you'll remember. This is what you'll type when you want to change your AdGuard settings. Write it down!

Click "Next" and then "Finish."

You're in! You'll see the AdGuard dashboard.

---

## Step 5: Make Your Devices Use AdGuard

Here's the magic moment. Right now, AdGuard is installed and running. But your devices don't know to use it yet.

There are two ways to do this:

### Option A: Change Your Router (Recommended)

This is the best method because it covers EVERY device automatically.

1. Open your router's settings page (usually `192.168.1.1` or `192.168.0.1`)
2. Look for "DNS" or "DHCP" settings
3. Find the place where it says "DNS Server" or "Preferred DNS"
4. Change it from whatever it is now to your server's IP address

For example, if your server is at `192.168.1.100`, you'd enter:

```
192.168.1.100
```

Save your settings.

Now every device connected to your router will use AdGuard. Phones, laptops, smart TVs, everything.

### Option B: Change One Device Manually

If you can't change your router settings (some ISPs don't let you), you can change individual devices:

**On Windows:**
1. Go to Settings → Network & Internet → Wi-Fi (or Ethernet)
2. Click on your network
3. Scroll down to "DNS server" and change it to manual
4. Enter your server's IP

**On Mac:**
1. Go to System Settings → Network
2. Click your Wi-Fi or Ethernet
3. Click "Details" → "DNS"
4. Add your server's IP

**On Android:**
1. Go to Settings → Network → Wi-Fi
2. Long-press your network → "Modify network"
3. Expand "Advanced" → Change IP settings to "Static"
4. Enter your server's IP as DNS 1

**On iPhone:**
1. Go to Settings → Wi-Fi
2. Tap the "i" next to your network
3. Tap "Configure DNS" → "Manual"
4. Add your server's IP

---

## Step 6: Test It Out

Now let's verify it's working.

Go back to your AdGuard dashboard in your browser (the `http://192.168.1.100:3000` page). Click on the "Dashboard" icon in the top left.

Look at the top of the page. You should see numbers going up:

- **Queries** — This counts how many times devices on your network asked for web pages
- **Blocked** — This shows how many ads or trackers got blocked

Wait a minute and refresh. The numbers should increase as your devices browse the web.

You can also test manually. Try visiting a website known for lots of ads — you should notice fewer ads than usual.

---

## What If It Doesn't Work?

Don't panic. Here are the two most common problems:

**Problem: I can't access the web interface**

- Check that you typed the IP address correctly: `http://192.168.1.100:3000` (replace with YOUR server's IP)
- Make sure you added `:3000` at the end
- Is the container running? Run `docker ps` and check that "adguard" is in the list

**Problem: Devices still show ads**

- Make sure you changed the DNS setting on your router OR your specific device
- After changing router DNS, you may need to restart your device or toggle Wi-Fi off and on
- Check the AdGuard dashboard — are queries showing up? If not, traffic isn't going through AdGuard yet

---

## What's Next?

You've now installed your first real service. This is a big deal. You:

1. ✅ Created a Docker Compose file
2. ✅ Ran a service using Docker
3. ✅ Configured it through a web interface
4. ✅ Connected devices to use it

In the next chapter, we're going to take a step back and understand how your home network actually works. This will help you troubleshoot problems and set up more services confidently.

But first — enjoy your ad-free browsing!

---

# Do This Now

Your action step for this chapter:

1. **Install AdGuard Home** using the Docker Compose commands above
2. **Access the web interface** at `http://[your-server-ip]:3000`
3. **Create your admin account** with a password you'll remember
4. **Change one device** (your phone or laptop) to use your server's IP as its DNS server
5. **Verify it's working** — check the dashboard to see queries and blocked items

Estimated time: 15-20 minutes

This is where it starts getting fun. You've got a real service running!
