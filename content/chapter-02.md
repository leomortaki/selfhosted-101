# Chapter 2: What Do You Actually Need?

## The Hardware Question

Here's the good news: you probably already have everything you need to get started.

Before we dive in, let's clear up something important. You might have heard people raving about Raspberry Pi computers. They're small, cheap, and look cool on a desk. But here's the truth: for most beginners, a Raspberry Pi is actually the *wrong* choice.

Why? Two reasons. First, many self-hosted software tools don't work well on Raspberry Pi. Developers often skip optimizing for it, which means you might find a cool service you want to run, only to discover it won't run on your Pi. Second, a Raspberry Pi is slower than you'd expect. That $50 computer can struggle when you're running more than a couple of services.

So what should you use instead?

## The Sweet Spot: Used Desktop or NUC

The best choice for most beginners is a used desktop computer or a small computer called a NUC (which just means "Next Unit of Computing"). These are everywhere, affordable, and powerful enough to run everything you'll want.

Think about it: every year, companies upgrade their office computers. Those old machines still work perfectly fine—they're just not the newest anymore. You can often pick one up for $50-150, and it'll run circles around a Raspberry Pi.

## Understanding the Specs (Plain English)

When you're looking at computers, you'll see numbers and terms that feel confusing. Let's make sense of them:

**Processor (CPU):** This is the brain of the computer. You want something from the last 5-7 years. If you see "Intel Core i3," "Intel Core i5," or "AMD Ryzen 3/5," you're in good shape. Don't worry about the exact model—anything from this decade will work fine.

**Memory (RAM):** This is short-term memory—how many things the computer can think about at once. Think of it like a desk: bigger desk, more room to work. You want at least 4 gigabytes (4GB). 8GB is better and gives you room to grow. If you see "8GB RAM," that's perfect.

**Storage (Hard Drive/SSD):** This is long-term memory—where your files and programs live. You don't need much to start. 128 gigabytes (128GB) is enough for learning. 256GB or 500GB is better if you plan to store photos or videos. A SSD (solid state drive) is faster than a regular hard drive—get one if you can, but it's not required.

## The x86 vs ARM Thing (Simplified)

You might hear people talk about "x86" and "ARM." Here's what that means in plain English:

x86 is the type of processor in most regular computers. It's powerful and runs almost all software without problems. Every Intel or AMD processor you've ever owned is x86.

ARM is the type of processor in phones, tablets, and Raspberry Pis. It's designed to be energy-efficient and run cooler. But many software tools are written for x86 and don't work well on ARM.

The takeaway: get a computer with an Intel or AMD processor (x86). It'll run everything you want to try.

## What to Look For

Here's your shopping checklist:

✅ **Processor:** Intel Core i3/i5/i7 or AMD Ryzen 3/5/7 (from the last few years)
✅ **Memory:** At least 4GB, ideally 8GB
✅ **Storage:** At least 128GB (SSD preferred, but HDD works)
✅ **Size:** Small desktop or NUC preferred (quiet and takes less space)
✅ **Condition:** Works fine—doesn't need to look pretty

What to avoid:
❌ Raspberry Pi (for now—we'll explain when it makes sense later)
❌ Computers older than 10 years
❌ Anything with less than 2GB RAM

## Where to Find Hardware

**Facebook Marketplace:** Search your local area for "desktop computer" or "used PC." People are constantly selling office upgrades. You can often find good deals and inspect the machine before buying.

**eBay:** Great for comparison shopping. Look for "refurbished" or "used - good condition" desktops. Check the specs carefully and read the description.

**Craigslist:** Similar to Facebook Marketplace. Meet locally and test the machine if possible.

**Local computer shops:** Some cities have small shops that repair and resell computers. You might pay a bit more, but you get to ask questions and sometimes get a short warranty.

**Friends and family:** Ask around! Someone you know probably has an old computer gathering dust. They might even give it to you.

## Community Recommendations

The self-hosting community has pretty solid consensus on this topic. Here's what experienced self-hosters recommend:

**Budget option ($0-50):** Use what you have. If you have an old laptop or desktop from the last 8 years, it probably works fine. Try it first before buying anything.

**Sweet spot ($50-150):** A used small desktop with 8GB RAM. Look for Dell OptiPlex, HP ProDesk, or Lenovo ThinkCentre. These business machines were built to run all day, every day—and they last.

**If you want new ($200-300):** A Intel NUC or similar small computer. These are designed to be quiet and efficient. Great if you want something that looks nice in your home.

## The Real Cost

Let's be honest about money:

- **Used desktop:** $50-150
- **Electricity:** Maybe $5-15 per month (depends on your electricity rates and how much you run it)
- **Internet:** You already have this

That's it. Unlike cloud services that charge you monthly forever, your self-hosted server is a one-time purchase that keeps on giving.

---

## Do This Now

Go look around your home. Check that closet, that corner, the old desk in the garage.

Do you have an old computer sitting somewhere? Laptop or desktop, it doesn't matter. Turn it on and see if it still works.

If you find one that boots up—you're done. You have your server.

If you don't find anything, make a note: "Need to find a used desktop." Then check Facebook Marketplace or eBay this week. Set a budget of $100 and see what's available in your area.

You don't need to buy anything today. Just know what's out there.

---

## What's Next

Once you have your hardware sorted, we'll get you set up with the software. Chapter 3 walks you through installing Ubuntu Server—the operating system that runs your self-hosted world. No prior experience needed. We'll make it easy.
