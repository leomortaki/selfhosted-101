# Chapter 4: Docker - Your First Container

## Welcome to the World of Containers

Remember when we talked about shipping containers in Chapter 1? Those standardized metal boxes that revolutionized global trade? Well, get ready because Docker does exactly the same thing for software.

Think about how shipping works. Before containers came along, loading a ship was a nightmare. Workers had to load each item individually—crates of different sizes, fragile goods, heavy machinery. It took forever, things got damaged, and nobody could agree on how to pack it all.

Then someone invented the shipping container. Standard size. Standard way of loading. You put your stuff in, seal it up, and it works everywhere. The truck, the train, the ship—they all handle the same container the same way. Game changer.

Docker is like that for software. Instead of worrying about whether your program will run on someone else's computer, you package it up in a standardized "container" that works the same way everywhere.

## Why Does This Matter?

Here's the problem Docker solves: remember when you installed that program on your friend's computer and it didn't work? Maybe they had a different version of Python. Or their operating system was different. Or some library was missing. Classic "works on my machine" problem.

With Docker, your software travels in its own little box that includes:
- The program itself
- Everything the program needs to run
- Its own mini-operating system

Nothing from the outside can mess with it. And nothing from inside can mess with your actual computer. It's completely isolated. Pretty cool, right?

## The Language of Containers

Before we dive in, let's learn a few terms. I promise they're simple:

**Image** - Think of this as the blueprint or the recipe. It's the template that tells Docker how to build your container. You don't run an image directly; you use it to create containers.

**Container** - This is the actual running version of the image. It's like using your recipe to bake a cake—the recipe is the image, the cake is the container.

**Volume** - Remember when we talked about saving your files in Chapter 3? A volume is Docker's way of saying "keep this data safe even if the container gets deleted." It's like a separate compartment that survives when you throw away the container.

**Dockerfile** - A text file that tells Docker how to build your image. Like writing out a recipe step by step.

That's it. Four words. Image, container, volume, Dockerfile. You've got this.

## Installing Docker

Now let's get Docker installed on your server. We're going to use the official install script because it handles all the tricky parts for us.

### Step 1: Download and Run the Install Script

Open your terminal (or SSH into your server like we learned in Chapter 3) and type this:

```bash
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
```

What does this do?
- `curl` downloads a script from the internet
- `sudo` runs it with special permissions (admin rights)
- The script sets up Docker on your system

You'll see a lot of text scroll by. That's normal—it's just the script doing its job.

### Step 2: Add Your User to the Docker Group

By default, only special administrators can use Docker. Let's add your user so you don't have to type passwords every time:

```bash
sudo usermod -aG docker $USER
```

After this command, you'll need to log out and log back in for the change to take effect. If you're SSH'd in, just reconnect.

### Step 3: Verify It Works

Let's make sure Docker installed correctly:

```bash
docker --version
```

You should see something like `Docker version 24.0.0` or similar. If you do, congratulations! Docker is installed.

## Running Your First Container

This is the moment you've been waiting for. Let's run the classic "hello world" of containers:

```bash
docker run hello-world
```

Watch what happens. Docker will:
1. Look for a "hello-world" image on your computer
2. Not find it (because you just installed Docker)
3. Automatically download it from the internet (Docker Hub, which is like an app store for container images)
4. Run it in a container
5. Show you a friendly message

The output should look something like this:

```
Hello from Docker!
This message shows that your installation appears to be working correctly.
...
```

If you see this message, give yourself a pat on the back. You've just run your first container!

## What's Actually Happening Here?

Let me break down what `docker run hello-world` does, piece by piece:

- `docker` - You're talking to the Docker program
- `run` - "I want to start a container"
- `hello-world` - "Use this image to create the container"

The magic is that Docker figured out you didn't have the image locally, so it automatically downloaded it. Next time you run it, it'll be much faster because the image is already on your computer.

## Looking at Your Containers

Let's see what containers you have running:

```bash
docker ps
```

This shows "running" containers. Right now, you probably don't have any running because hello-world just says hi and exits.

Let's see ALL containers (including ones that finished):

```bash
docker ps -a
```

Now you'll see the hello-world container in the list. It probably shows "Exited" because it finished its job.

## Cleaning Up

Those exited containers take up a little space. Let's remove it:

```bash
docker rm $(docker ps -aq)
```

This removes all stopped containers. Don't worry—you can always run hello-world again anytime.

## A More Interesting Example

Hello-world is fun, but let's run something actually useful. Let's run a simple web server that just displays a webpage:

```bash
docker run -d -p 8080:80 nginx
```

Whoa, there's a lot of new stuff here! Let me explain:

- `-d` - "Detached" mode. Run it in the background so it keeps going
- `-p 8080:80` - "Port mapping." The container uses port 80 internally, but we want to access it via port 8080 on our computer
- `nginx` - The name of the image we're using (nginx is a popular web server)

Now let's check if it's running:

```bash
docker ps
```

You should see nginx in the list, running on port 8080.

## Accessing Your Container

Here's the cool part. Open a web browser on your computer and type:

```
http://your-server-ip:8080
```

(Replace "your-server-ip" with your server's IP address from Chapter 3)

You should see a "Welcome to nginx" page! That's the web server running inside the container, accessible from your browser.

## Stopping and Removing Containers

Let's clean up. First, stop the nginx container:

```bash
docker stop $(docker ps -q)
```

This stops all running containers. Now let's remove them too:

```bash
docker rm $(docker ps -aq)
```

Run `docker ps -a` again to confirm everything is gone.

## Why This Is a Big Deal

Think about what just happened. You:
1. Installed software (nginx web server)
2. Ran it in an isolated container
3. Accessed it from your browser
4. Cleaned it up completely

And you never had to:
- Install nginx manually
- Configure any settings
- Worry about it conflicting with other software
- Figure out how to uninstall it

This is the power of Docker. Software that works, every time, zero hassle.

## The Big Picture

Here's why Docker matters for self-hosting:

**No more "it works on my machine" problems** - If it works in the container, it'll work on your server.

**Easy to try new things** - Want to test a new program? Run it in a container. Don't like it? Delete it. Simple.

**One command installation** - Most self-hosted software provides a Docker image. One command and it's running.

**Isolation** - One program's problems don't affect others. If something breaks, you can delete just that container.

**Easy updates** - Pull a new image, delete the old container, create a new one. Done.

---

## Do This Now

Your turn. Here's what to do right now:

1. **Make sure Docker is installed** - Run `docker --version` and celebrate if you see a version number

2. **Run the hello-world container** - Type `docker run hello-world` and watch it work

3. **Run nginx and see it in your browser** - Use `docker run -d -p 8080:80 nginx`, then open `http://your-server-ip:8080` in your browser

4. **Clean up** - Stop and remove all containers with:
   ```bash
   docker stop $(docker ps -q)
   docker rm $(docker ps -aq)
   ```

Take a screenshot of the nginx welcome page—you've just run your first web server!

---

## What Comes Next

In Chapter 5, we're going to put Docker to work. You'll install AdGuard Home, which blocks ads network-wide for every device in your home. It's the perfect first service: useful immediately, impressive results, and a great way to practice your Docker skills.

But first, make sure you've played around with the commands in this chapter. Try running nginx a few more times, experiment with the `docker ps` commands, and get comfortable. Once Docker feels natural, you're ready for the fun stuff.

See you in Chapter 5!
