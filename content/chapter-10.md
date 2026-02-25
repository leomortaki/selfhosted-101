# Chapter 10: Keeping It Running

*Welcome to the chapter nobody talks about.* 

By now, you've built something great. You have AdGuard blocking ads, Jellyfin streaming your videos, Vaultwarden keeping your passwords safe. Everything works. Life is good.

But here's the truth nobody tells you when you start self-hosting: **your server needs love.** Things break. Updates come out. Sometimes your server just needs a restart. And if you're not paying attention, you might not even know something is wrong until it's been broken for days.

The good news? Setting up proper maintenance doesn't take long. Once it's in place, your server essentially runs itself. You'll sleep better at night knowing that if something goes wrong, you'll find out quickly.

Let's cover the three pillars of keeping your server healthy: updating, backups, and monitoring.

---

## Updating Your Services (Without Breaking Everything)

Think about the apps on your phone. Every few weeks, they ask you to update—sometimes for new features, often for security fixes. Your self-hosted services work the same way.

Developers constantly release new versions to:

- Fix security holes (important!)
- Add new features
- Repair bugs you might not even know existed

The challenge is that updates can sometimes change how things work. That's why we update carefully.

### The Simple Way: Watchtower

Remember how Docker lets you run services in standardized packages? There's a tool called **Watchtower** that automatically checks for updates to your containers and notifies you—or even updates them automatically.

Here's how simple it is to add Watchtower to your setup:

```yaml
services:
  watchtower:
    image: containrrr/watchtower
    container_name: watchtower
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
    environment:
      - WATCHTOWER_SCHEDULE=0 0 4 * * *
      - WATCHTOWER_NOTIFICATIONS=shoutrrr
      - WATCHTOWER_NOTIFICATION_URL=shoutrrr://...
```

That schedule `0 0 4 * * *` means "check for updates every day at 4 AM." You don't need to remember to check—Watchtower does it for you.

### The Even Simpler Way: Just Check Manually

If that sounds like too much automation (some people love being hands-on), you can manually check for updates. Here's the command:

```bash
docker-compose pull
docker-compose up -d
```

The `pull` command downloads the newest version of each image. The `up -d` command restarts your services with the new version. The `-d` means "run in detached mode," which is just a fancy way of saying "in the background."

### A Few Tips for Updating

- **One service at a time:** If you have multiple services, update one, test it, then move to the next
- **Check the logs:** After updating, run `docker-compose logs -f [service-name]` to see if anything broke
- **Don't panic:** If an update breaks something, you can always go back. Docker keeps old versions around until you explicitly delete them

### What About Breaking Changes?

Sometimes a developer releases an update that changes how their service works. Maybe the interface looks different, or a setting moved. This is rare, but it happens.

The solution? Before updating, check the service's documentation or the comments on Docker Hub. Usually, someone will warn the community if an update requires extra steps.

---

## Backups: Your Safety Net

Here's a scenario that happens to everyone: you're making changes to your server, something goes wrong, and—oops—your data is gone. Maybe you deleted the wrong folder. Maybe a drive failed. Maybe a software update didn't go well.

Without a backup, you've lost everything.

With a backup, you restore in minutes and move on with your life.

### What Do You Actually Need to Back Up?

If you've been following this guide, you have a `docker-compose.yml` file that defines your services. This file is important—but it's also easy to recreate. The *real* precious stuff is your data:

- **Your media files:** Videos, music, photos
- **Your AdGuard statistics:** All those ad-blocking logs
- **Your Vaultwarden passwords:** Obviously important
- **Jellyfin library data:** Your watch history, user settings

In Docker terms, this is everything in your `volumes` section—the folders that live on your actual computer instead of inside the container.

### The Simple Backup Method: Copy Your Folders

The most straightforward backup approach is to just copy your data folders to another location. You could:

- Copy them to an external hard drive
- Copy them to a different computer on your network
- Copy them to cloud storage (Dropbox, Google Drive, etc.)

Here's a simple bash script that backs up your Docker data folder:

```bash
#!/bin/bash
DATE=$(date +%Y-%m-%d)
tar -czf backup-$DATE.tar.gz /home/yourusername/docker-data
```

This creates a compressed file called `backup-2024-01-15.tar.gz` (or whatever today's date is) containing everything in your data folder.

### The Slightly Fancier Method: Restic

If you want something more robust, there's a tool called **Restic** that does smart backups. Instead of copying everything every time, it remembers what changed and only backs up the differences. It's like how Google Photos knows you added three new pictures, so it only uploads those three instead of your entire photo library.

Installing Restic is just another Docker container:

```yaml
services:
  restic:
    image: restic/restic
    volumes:
      - ./backups:/backups
      - /path/to/your/docker-data:/data
    environment:
      - BACKUP_REPO=/backups
    command: backup /data
```

Set it up once, then schedule it to run automatically.

### How Often Should You Back Up?

This depends on how often your data changes:

- **Vaultwarden (passwords):** Back up every time you add important new passwords, or at least weekly
- **Jellyfin (media):** You probably already have your original files somewhere, but back up metadata and watch history weekly
- **AdGuard:** Back up monthly or after making big configuration changes

---

## Monitoring: Know What's Happening

You can't fix what you don't know is broken.

Here's the uncomfortable truth: if your server goes down right now, how would you know? Would you check it tomorrow? Next week? Would a friend trying to watch a movie on Jellyfin be the first to tell you?

That's where monitoring comes in.

### What Is Monitoring?

Monitoring is simply keeping an eye on your services to make sure they're working. It's like having a smoke detector—hopefully it never goes off, but you'll be glad it's there if something catches fire.

### Meet Uptime Kuma

**Uptime Kuma** is a self-hosted monitoring tool that's surprisingly fun to use. It basically asks your services "Are you alive?" every few seconds, and logs whether they respond.

When a service stops responding, Uptime Kuma can:

- Send you an email
- Send you a Telegram message
- Show you a notification
- Play a sound

Setting up Uptime Kuma takes about five minutes:

```yaml
services:
  uptime-kuma:
    image: louislam/uptime-kuma
    container_name: uptime-kuma
    volumes:
      - ./uptime-kuma-data:/app/data
    ports:
      - "3001:3001"
    restart: unless-stopped
```

After this runs, open your browser and go to `http://[your-server-ip]:3001`. You'll set up your first account, and then you can add monitors.

### Adding Your First Monitor

In the Uptime Kuma interface, click "Add New Monitor." Here's what you'll fill in:

- **Monitor Type:** HTTP(s)
- **URL:** `http://[your-server-ip]:[service-port]` (for example, `http://192.168.1.100:3000` for AdGuard)
- **Heartbeat Interval:** How often to check (every 60 seconds is fine for most services)
- **Timeout:** How long to wait before deciding it's down (30 seconds is good)

Now Uptime Kuma will check your service every minute. If it stops responding, you'll get notified.

### What Should You Monitor?

At minimum, monitor:

- **AdGuard:** Because ad-blocking is your first service
- **Jellyfin:** Because you want to know when movies won't play
- **Vaultwarden:** Because password access matters
- **Your server itself:** Some people monitor whether the server is reachable at all

You can add as many as you want. There's no limit.

---

## Bringing It All Together

Now you have three layers of protection:

1. **Updates:** Your services stay current with security fixes and new features
2. **Backups:** Your data survives hardware failures and mistakes
3. **Monitoring:** You know when something breaks

This is what "set and forget" actually means—not that you never touch your server, but that you've set up systems that run automatically and tell you when attention is needed.

You don't need to check your server every day. You just need to know that if something breaks, you'll find out quickly.

---

## A Note on Maintenance Mindset

Here's the secret that experienced self-hosters know: **maintenance is not a chore—it's a habit.**

Once a month, you might:

- Check your backups ran successfully
- Look at Uptime Kuma to see if anything had issues
- Run `docker-compose pull` to get the latest updates
- Spend 15 minutes reading about new features in your favorite services

That's it. Fifteen minutes a month to keep everything running smoothly.

---

# Do This Now

Let's put this chapter into practice right now.

**Your exercise: Set up Uptime Kuma and add one monitor.**

1. Add the Uptime Kuma container to your `docker-compose.yml` (or create a new file just for it)

2. Start it with `docker-compose up -d`

3. Open your browser to `http://[your-server-ip]:3001` and set up your account

4. Add one monitor for AdGuard Home (or whichever service you set up first)

5. Wait a minute and refresh the page—you should see it's "UP" with a green dot

That's it. You've just added monitoring to your server. Now if something breaks, you'll know.

When you're done, take a screenshot. You're officially a server administrator now—and server admins sleep better at night because they monitor their systems.

---

## What's Next?

You made it. You now have:

- A running server with useful services
- Remote access so you can use your services anywhere
- Security (HTTPS, passwords)
- Backups to protect your data
- Monitoring to alert you to problems

That's a fully functional self-hosted setup. Congratulations!

In the final chapter, we'll talk about where you can go from here. Maybe you want to explore home automation with Home Assistant, or set up your own cloud storage with Nextcloud, or dive deeper into the Docker rabbit hole. Whatever calls to you, you now have the foundation to explore.

But for now, celebrate what you've built. You've joined a community of people who understand that having control over your technology is worth the effort.

Welcome to self-hosting.
