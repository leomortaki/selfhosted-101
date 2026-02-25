# Chapter 3: Setting Up Your First Machine

*Estimated reading time: 15 minutes*
*Estimated "do this now" time: 20 minutes*

---

In the last chapter, you figured out what hardware to use. Now it's time to turn that old computer into something useful. We're going to install **Ubuntu Server** — a free operating system that turns your machine into a proper server.

Don't worry if that sentence made no sense. We're about to break it all down.

## What Even Is Ubuntu Server?

Let's start with some definitions, because this chapter is going to throw some new words at you.

**Operating System** (or OS) is the main software that runs your computer. It's the thing that lets you move your mouse, open apps, and save files. Windows and macOS are operating systems. Ubuntu Server is another one — but instead of giving you a desktop with icons and windows, it gives you a *text-only* interface. No pictures, no clicking. Just words on a screen.

Think of it like the difference between a car's dashboard (with screens and buttons) and a race car cockpit (with just essential controls). Ubuntu Server is stripped down and designed to run reliably without any extra bells and whistles.

**Ubuntu** (pronounced "oo-BOON-too") is a flavor of Linux. Linux is an operating system — the same kind that runs most of the internet, your Android phone, and supercomputers. Ubuntu is the most beginner-friendly version of Linux. It's free, it's secure, and it has a huge community to help you.

**Server** doesn't mean a fancy piece of hardware. It just means "a computer that provides services to other computers." Your server will provide services like ad-blocking, media streaming, and password storage to the other devices in your home.

So when we say "Ubuntu Server," we mean: a free, reliable operating system that runs without a graphical interface, designed to serve other devices on your network.

Simple enough? Let's move on.

## Why Ubuntu Server?

You might be wondering: why not just use Windows?

Three reasons:

1. **It's free.** No license fees, ever.
2. **It's stable.** Servers run for months or years without needing to be restarted.
3. **It's secure.** Linux has far fewer viruses and malware than Windows.

Ubuntu Server also makes installing software incredibly easy — which is exactly what we'll do in the next chapters.

## What You'll Need Before We Start

Before we begin the installation, gather these things:

- **Your target computer** (the one you want to turn into a server)
- **Another computer** (laptop or desktop) to create the installer
- **A USB stick** (at least 8GB — this will be erased, so use one you don't need)
- **Internet connection** (for downloading Ubuntu and updates)
- **About 30 minutes** of uninterrupted time

## Step 1: Download Ubuntu Server

On your *other* computer (not the server), open your web browser and go to:

> https://ubuntu.com/download/server

You should see a big button that says "Download Ubuntu Server." Click it.

**Important:** Make sure you download the **Server** version, not the Desktop version. Desktop has pictures and windows; Server is text-only. We want Server.

The file you download will be called something like `ubuntu-24.04-live-server-amd64.iso`. The `.iso` part just means "image file" — it's a complete copy of Ubuntu packaged into one file.

This download might take a few minutes depending on your internet speed. While it's downloading, let's prepare the USB stick.

## Step 2: Make a Bootable USB

An ISO file isn't something you can just "open." To use it, we need to turn it into a **bootable USB** — a USB stick that can start your computer and run Ubuntu.

### What Does "Bootable" Mean?

When you turn on your computer, it follows a set of instructions to get started. This process is called **booting**. Normally, your computer boots from its hard drive into Windows or macOS.

A bootable USB tells your computer: "Instead of starting from your hard drive, start from this USB stick instead." It's like inserting a different instruction manual for how to start up.

### How to Create One

The easiest way is using a free tool called **Rufus** (Windows) or **Etcher** (Mac/Windows). Here's how:

**Using Etcher (works on Mac and Windows):**

1. Go to https://etcher.balena.io/ and download Etcher
2. Install and open it
3. Click "Flash from file" and select your Ubuntu `.iso` file
4. Click "Select target" and choose your USB stick
5. Click "Flash!" and wait for it to finish

**Using Rufus (Windows):**

1. Go to https://rufus.ie/ and download Rufus
2. Open it (no installation needed)
3. Under "Device," select your USB stick
4. Click "Select" and choose your Ubuntu `.iso` file
5. Leave everything else as default
6. Click "Start" and wait for it to finish

> ⚠️ **Warning:** This will completely erase everything on the USB stick. Make sure you've saved anything important from it first.

When it's done, you have a Ubuntu installer on a USB stick. Pretty cool, right?

## Step 3: Prepare Your Server Computer

Now let's get your target computer ready. Here's what to do:

1. **Turn off the computer** completely
2. **Plug in the USB stick** into a USB port
3. **Turn on the computer** and watch the screen carefully

You'll see a brief message that says something like "Press F2 to enter setup" or "Press DEL for BIOS." This is your cue to tap a key (usually F2, F12, DELETE, or ESC) to open the **BIOS** — the basic software that controls your computer's hardware.

> **What is the BIOS?** Think of it as the control center for your computer's fundamental settings. It's where you decide which devices to boot from. We need to tell it to boot from our USB stick first.

Once you're in the BIOS:

1. Look for a "Boot" or "Boot Order" section
2. Move your USB stick to the top of the list
3. Save and exit (usually by pressing F10 and confirming)

Your computer should now restart and boot from the USB stick.

## Step 4: The Installation Process

When your computer boots from the USB, you'll see a purple screen with the Ubuntu logo. After a moment, you'll see a text-based menu. Here's what to do:

### Screen 1: Welcome

You'll see options to try Ubuntu or install it. Press **Enter** on "Install Ubuntu Server."

### Screen 2: Keyboard Layout

Use the arrow keys to select your keyboard layout. Most people can just press **Enter** to accept the default (English (US)). If you use a different layout, find it in the list.

### Screen 3: Type of Installation

You'll see options like "Ubuntu Server" and "Ubuntu Server (minimized)." Select "Ubuntu Server" and press **Enter**.

### Screen 4: Network Configuration

Ubuntu will try to automatically detect your network. If you're using Ethernet (plugging into your router with a cable), it should just work. You'll see it list your network connection.

If you're using Wi-Fi, you'll need to select your network and enter your password. Use the arrow keys to navigate, Tab to move between fields, and Enter to select.

> **What is Ethernet?** It's the standard way to connect computers to the internet using a cable. It looks like a wider phone cable with clips on the side. Most servers use Ethernet because it's faster and more reliable than Wi-Fi.

### Screen 5: Storage Configuration

This is the part where we decide how Ubuntu uses your hard drive. For a beginner, the easiest option is to use the entire disk.

1. Select "Use an entire disk"
2. Select the disk you want to use (usually there's only one option)
3. Review the changes — Ubuntu will show you what it's going to do
4. Select "Done" and confirm

> ⚠️ **Warning:** This will erase everything on the selected hard drive. Make sure you've backed up any data you wanted to keep.

### Screen 6: Your Profile

Now Ubuntu needs to know who you are. You'll set up:

- **Your name** — your full name
- **Server's name** — a name for this computer (like "myserver" or "homeserver")
- **Username** — the name you'll use to log in (pick something short, like "admin" or your name)
- **Password** — pick a password you'll remember

> **What is a username?** It's the name you type to identify yourself to the computer. On personal computers, you might log in as "John" or "Mom." Here, you'll create a username for yourself.

> **What is a password?** The secret phrase that proves you are who you say you are. Choose something you'll remember!

### Screen 7: SSH Setup

SSH (pronounced "S-S-H") stands for **Secure Shell**. It's a way to connect to your server from another computer using text commands. We'll use this in just a few minutes.

When asked if you want to "Install OpenSSH server," select **Yes**. This makes it easier to control your server remotely.

### Screen 8: Server Snaps

Ubuntu will ask what software you'd like to install. For now, just press **Enter** to continue without selecting anything extra. We'll install software ourselves in later chapters.

### The Final Wait

Now Ubuntu installs. This takes 5-10 minutes. You'll see a progress bar. Go refill your water bottle — you've earned it.

When it's done, you'll see a message saying "Installation complete!" Remove the USB stick and press **Enter** to restart.

## Step 5: Log In For the First Time

Your computer restarts. This time, instead of Windows or the USB menu, you'll see a black screen with text. It looks like this:

```
Ubuntu 24.04 LTS myserver tty1
myserver login: _
```

This is called the **terminal** or **command line**. Instead of clicking icons, you type commands. It's how people used to use all computers — and it's still the most powerful way to use a server.

> **What is the terminal?** It's a text-only interface to your computer. Instead of pointing and clicking, you type instructions. The cursor (the blinking line) is where you type.

> **What is a command?** An instruction you type for the computer to follow. For example, typing `ls` and pressing Enter tells the computer to "list files."

To log in, type the username you created (press Enter) and then type your password (press Enter). 

> **Note:** When typing your password, nothing appears on screen. This is normal — it's a security feature so nobody can see how many characters your password has. Just type it and press Enter.

If you typed everything correctly, you'll see a welcome message and a prompt that looks like:

```
username@myserver:~$ _
```

Congratulations! You're now logged into your server.

## Understanding What You're Seeing

Let me break down that prompt:

```
username@myserver:~$
```

- **username** — that's you (your login name)
- **@** — "at" (you are at)
- **myserver** — the name of this computer
- **~** — your home folder (where your personal files go)
- **$** — means you're a regular user (not the administrator)

> **What is a folder?** A place where you store files. It's the same thing as a "directory." Your documents, photos, and downloads are all in folders.

> **What is the home folder?** The personal space for your user account. When you log in, this is where you "start."

> **What does $ mean?** In the terminal, `$` means you're a normal user with limited permissions. If you see `#`, you're the administrator (root user). We'll get to why that matters later.

## Looking Around: Your First Commands

Let's try a few simple commands. Don't worry — you can't break anything by typing these.

### Command 1: See Where You Are

Type this and press Enter:

```bash
pwd
```

This stands for "print working directory." It shows you what folder you're currently in. You should see `/home/yourusername` — that's your home folder.

### Command 2: List Files

Type this and press Enter:

```bash
ls
```

This lists the files in your current folder. Right now, it's probably empty — that's fine.

### Command 3: See Who You Are

Type this and press Enter:

```bash
whoami
```

This tells you what username you're logged in as.

### Command 4: Check the Date

Type this and press Enter:

```bash
date
```

Just so you know, your server doesn't have a fancy calendar app — you have to ask it politely with this command.

### Command 5: Get Help

Type this and press Enter:

```bash
help
```

This shows a list of available commands. Don't worry about memorizing them — we'll learn the ones we need as we go.

## The Linux Directory Structure

Now that you're logged in, let's talk about how Linux organizes files. Understanding this now will save you confusion later.

### The Root Folder

In Linux, everything starts from a single folder called the **root** folder. Think of it as the trunk of a tree — all other folders branch out from it.

The root folder is written as `/` (just a forward slash).

### Important Folders

Here are the folders you'll encounter most:

- **`/`** — The root (the main starting point)
- **`/home`** — Where user files live (like `/home/yourusername`)
- **`/etc`** — Configuration files (settings for programs)
- **`/var`** — Variable data (logs, databases)
- **`/opt`** — Optional/extra software
- **`/root`** — The administrator's home folder (yes, it's different!)
- **`/tmp`** — Temporary files (these get deleted when you restart)

> **What is a configuration file?** A special file that tells a program how to behave. It's like settings — you change them to customize how the software works.

Don't worry if this doesn't fully make sense yet. You'll see these folders in action as we install services.

## Shutting Down (Safely!)

When you want to turn off your server, don't just hold the power button. That could corrupt files.

Instead, use this command:

```bash
sudo shutdown now
```

> **What is sudo?** It's a command that means "do this as the administrator." You'll need it for any command that affects the system. It will ask for your password.

Your server will shut down gracefully. When the screen goes black, you can safely unplug it.

## 🎯 Do This Now

This is your hands-on exercise for this chapter:

**Install Ubuntu Server on your hardware**

Here's what to do:

1. Download Ubuntu Server from https://ubuntu.com/download/server
2. Create a bootable USB using Etcher or Rufus
3. Boot your server from the USB (remember: press F2/DEL/F12 to enter BIOS)
4. Follow the installation steps in this chapter
5. Log in and run these commands:
   - `pwd` — to see where you are
   - `ls` — to list files
   - `whoami` — to confirm your username
   - `date` — to check the time

Take a screenshot of your terminal after logging in. You did it!

---

## What Comes Next?

You now have a running Ubuntu Server. It's doing nothing useful yet — but that's about to change.

In the next chapter, we're going to install **Docker** — a tool that makes installing and running software incredibly easy. Docker is like having standardized shipping containers for apps: they arrive ready to go, they don't interfere with each other, and you can move them anywhere.

See you there.

---

**Chapter Summary:**

- Ubuntu Server is a free, stable, secure operating system for servers
- A bootable USB lets you install Ubuntu from a USB stick
- The BIOS controls how your computer starts up
- The terminal is a text-based interface where you type commands
- Linux organizes files in a tree structure starting from `/` (root)
- Always use `sudo shutdown now` to turn off your server safely
