# Chapter 7: Adding More Services - Media & Passwords

*Your server can do more than block ads.*

In the last chapter, you installed AdGuard Home — a service that runs in the background, protecting your whole network. Now let's install two services that you'll actually interact with every day.

We're going to install:

1. **Jellyfin** — a media server that lets you stream your own videos, music, and photos to any device
2. **Vaultwarden** — a password manager that keeps your passwords secure and accessible only to you

Both are incredibly useful, and both demonstrate something important: how Docker stores your data so it doesn't disappear when you restart things.

Let's start with Jellyfin.

---

## Part 1: Jellyfin — Your Personal Netflix

### What Does a Media Server Do?

Imagine you have a box of DVDs and Blu-rays in your closet. Every time you want to watch something, you have to:
1. Find the right disc
2. Put it in your player
3. Hope it doesn't scratch

Now imagine all those movies are in one place, and you can watch any of them on any device — your phone, laptop, smart TV, tablet — without getting up. That's what a media server does.

Jellyfin scans a folder on your server, finds all your videos and music, and presents them in a beautiful interface. Think of it as your own private Netflix.

**Why self-host this?**
- Stream your movie collection anywhere
- No subscription fees (unlike Netflix, Hulu, etc.)
- Keep full control of your content
- Watch on multiple devices simultaneously

### Step 1: Create the Folder and Compose File

Just like with AdGuard, we need a folder for Jellyfin:

```bash
mkdir -p ~/docker/jellyfin
cd ~/docker/jellyfin
```

Now let's create the Docker Compose file. This time, it will be a bit longer because we need to set up storage for your media files:

```bash
nano docker-compose.yml
```

Paste in these lines:

```yaml
version: "3"

services:
  jellyfin:
    image: jellyfin/jellyfin
    container_name: jellyfin
    restart: unless-stopped
    ports:
      - "8096:8096"
      - "8920:8920"
    volumes:
      - ./config:/config
      - ./cache:/cache
      - /home/yourusername/media:/media
    environment:
      - TZ=America/New_York
```

Wait — this looks different from AdGuard. Let's break it down:

**image**: `jellyfin/jellyfin` — this is the software we're downloading

**ports**: 
- Port 8096 is for the web interface (where you'll watch videos)
- Port 8920 is for secure access (HTTPS), which we'll set up later

**volumes** (this is the important part):
- `./config:/config` — stores your Jellyfin settings, user accounts, and library information
- `./cache:/cache` — temporary files that help Jellyfin run faster
- `/home/yourusername/media:/media` — THIS is where your videos go. The part before the colon (`/home/yourusername/media`) is a folder ON YOUR SERVER. The part after the colon (`/media`) is where Jellyfin looks inside its container.

*Important:* Change `/home/yourusername/media` to your actual home folder path. If your username is "bob", it would be `/home/bob/media`.

**environment**: We're setting the timezone so Jellyfin shows the right time

### Step 2: Create Your Media Folder

Now create the folder where you'll put your videos:

```bash
mkdir -p /home/yourusername/media
```

(Replace "yourusername" with your actual username on the server.)

### Step 3: Start Jellyfin

Let's launch it:

```bash
docker compose up -d
```

You should see:

```
[+] Running 1/1
 ✔ jellyfin  Started
```

### Step 4: Set Up Jellyfin Through the Web

Now for the fun part. Open your browser and go to:

```
http://192.168.1.100:8096
```

(Replace `192.168.1.100` with your server's IP address.)

You'll see a welcome screen. Let's set it up:

**Step 1: Choose Your Language**
Select your language and click "Next"

**Step 2: Create Admin Account**
Pick a username and password. This is for managing Jellyfin (adding users, changing settings). Click "Next"

**Step 3: Add Media Library**
Click "Add Media Library"

- **Content Type:** Movies
- **Display Name:** Movies (or whatever you want)
- **Folder:** Click "Browse" and select the `/media` folder we created earlier

Click "OK" and then "Next"

**Step 4: Preferred Metadata Language**
Pick your language and click "Next"

**Step 5: Enable Remote Access**
You can leave this as-is for now. We'll cover remote access in Chapter 8. Click "Next"

**Step 6: Complete!**
Click "Finish"

You're in! You'll see the Jellyfin dashboard.

### Step 5: Add a Video File

Now let's add an actual video to watch.

First, copy a video file (MP4, MKV, or AVI) to your media folder on the server:

```bash
cp /path/to/your/video.mp4 /home/yourusername/media/
```

(Replace `/path/to/your/video.mp4` with the actual location of a video file on your server.)

Now go back to your Jellyfin browser tab. Click on "Movies" in the sidebar. You should see your video appear!

Click on it and press Play. You're streaming your own video through your own server.

---

## Part 2: Vaultwarden — Your Personal Password Manager

### What Is Vaultwarden?

Every website you use — banking, email, social media — should have a different password. That's common knowledge. But remembering 50+ unique passwords? That's impossible without help.

Most people use password managers like 1Password or LastPass. These are services that:
1. Store all your passwords in an encrypted "vault"
2. Generate strong, random passwords for you
3. Automatically fill in passwords when you visit websites

The problem? Those services store your passwords on THEIR servers. You have to trust them completely.

Vaultwarden is the self-hosted alternative. It does everything the big name managers do, but the data lives on YOUR server. No subscription fees. Complete privacy.

**Why self-host this?**
- No monthly fee (free forever)
- Your passwords never leave your network
- Syncs across all your devices
- Open source (anyone can verify it's secure)

### Step 1: Create the Folder

```bash
mkdir -p ~/docker/vaultwarden
cd ~/docker/vaultwarden
```

### Step 2: Create the Docker Compose File

```bash
nano docker-compose.yml
```

Paste in:

```yaml
version: "3"

services:
  vaultwarden:
    image: vaultwarden/server
    container_name: vaultwarden
    restart: unless-stopped
    ports:
      - "8080:80"
    volumes:
      - ./data:/data
    environment:
      - SIGNUP_ALLOWED=true
```

Let's explain what's new:

**image**: `vaultwarden/server` — this is an open-source implementation compatible with Bitwarden (a popular password manager)

**ports**: Port 8080 for the web interface

**volumes**: `./data:/data` — this stores your password vault. This is the most critical folder because it contains all your passwords, encrypted.

**environment**: `SIGNUP_ALLOWED=true` — this lets you create an account. Once you've set up your account, you might want to change this to `false` to prevent other people from signing up.

### Step 3: Start Vaultwarden

```bash
docker compose up -d
```

### Step 4: Create Your Account

Open your browser and go to:

```
http://192.168.1.100:8080
```

(Again, replace with your server's IP.)

You should see the Vaultwarden login page. Click "Create Account"

Fill in:
- **Email:** Your email address
- **Master Password:** This is THE most important password. It encrypts your entire vault. If you forget this, you CANNOT recover your passwords. Write it down somewhere safe!
- **Master Password Hint:** A hint to help you remember

Click "Submit"

You're in! This is your password vault.

### Step 5: Install Browser Extension (Optional but Recommended)

To get the full benefit, install the browser extension:

1. Go to the Vaultwarden website in your browser
2. Look for "Browser Extensions" 
3. Install the extension for Chrome/Firefox/Edge
4. When it asks for the server URL, enter: `http://192.168.1.100:8080`

Now you can:
- Save passwords when you create accounts
- Auto-fill passwords when you log in to websites
- Check if your passwords have been exposed in data breaches

---

## Understanding Volumes — Why Your Data Doesn't Disappear

You might have noticed something: both Jellyfin and Vaultwarden have folders that start with `./` in their volumes section.

Let's talk about why this matters.

### The Problem

When you run a container, it exists only as long as it's running. If you delete the container, everything inside it disappears. All your settings, all your data — gone.

That's obviously a problem. You don't want to lose your password vault every time you update the software.

### The Solution: Volumes

A **volume** is like a bridge between your server's hard drive and the inside of the container.

Think of it like this:

- The container is a house
- Your server's hard drive is a storage unit down the street
- A volume is a teleport hallway connecting them

Data that goes through this hallway gets saved on your hard drive. Even if the house (container) gets destroyed and rebuilt, the stuff in the storage unit (your hard drive) is still there.

That's why we wrote:

```yaml
volumes:
  - ./data:/data
```

The `./data` part means "a folder called 'data' in the same folder as this docker-compose.yml file". The `/data` part is where the container expects to find its data.

So when Vaultwarden saves a password, it goes into `/data` inside the container, which actually saves it to the `data` folder on your server. Pretty cool, right?

### This Is a Big Deal

Understanding volumes is one of the most important things about self-hosting. It means:

- **You can update** your services without losing data
- **You can move** your services to a different server and take your data with you
- **You can back up** your data by copying these folders

We'll talk more about backups in Chapter 10.

---

## What If It Doesn't Work?

**Jellyfin problems:**

- *Video won't play:* Make sure the video file is in your `/media` folder and is a supported format (MP4, MKV, AVI work best)
- *Can't see videos:* Click the refresh icon in Jellyfin to rescan your media library
- *Permission denied:* Make sure the media folder is readable. Run `chmod -R 755 /home/yourusername/media`

**Vaultwarden problems:**

- *Can't create account:* Check that you set `SIGNUP_ALLOWED=true`
- *Extension can't connect:* Make sure you entered the correct server URL (including the port number)
- *Forgot master password:* Unfortunately, there's no recovery. You'll need to delete the data folder and start fresh

---

## What's Next?

You've now installed three services:

1. **AdGuard** — blocks ads network-wide
2. **Jellyfin** — streams your media
3. **Vaultwarden** — manages your passwords

That's a solid foundation! But there's one thing we haven't figured out yet: how do you access these services when you're NOT at home?

In the next chapter, we're going to understand your network better. You'll learn about IP addresses, ports, and how devices talk to each other. This knowledge is essential for accessing your services remotely.

But first — go watch that video you added to Jellyfin. You earned it!

---

# Do This Now

Your action steps for this chapter:

1. **Install Jellyfin** using the Docker Compose commands above
2. **Create your media folder** (`mkdir -p /home/yourusername/media`)
3. **Copy one video file** to that folder
4. **Set up Jellyfin** through the web interface at `http://[your-server-ip]:8096`
5. **Watch the video** in your browser to confirm it works
6. **Install Vaultwarden** using the Docker Compose commands
7. **Create your Vaultwarden account** at `http://[your-server-ip]:8080`
8. **Add one password** to test it works

Estimated time: 30-40 minutes

Take your time with this one. Getting media streaming working for the first time is incredibly satisfying!