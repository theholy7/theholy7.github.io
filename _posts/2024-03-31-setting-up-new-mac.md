---
layout: post
title: Setting up a new Mac
excerpt_separator:  <!--more-->
categories:
  - Life
tags:
  - Work
---
I wanted to write a blogpost about how I setup my new Mac for work. However, I find myself being annoyed at my own process of setting up my Mac.
I feel this because my process feels inefficient.

Let me walk you through how I setup things. And hopefully I will figure out the questions I should be asking myself to improve it.

The first step when I got my new Mac was to make sure everything was up to date. So I let my computer do it's thing and update properly. After that, I reviewed all my trackpad and mouse settings:
- Enable tapping to click, and right-click in the bottom right
- Using the old school scroll direction
- Review all the gestures, and disable Launchpad

Next, I setup my Desktop and dock, and all the hot-corners:
- Top left - show desktop
- Top right - quick note
- Bottom right - turn off screen (which i setup to lock after a few seconds)

I also change my Finder too: to show extensions, delete bin after 30 days. I create a folder called "Developer" where I keep all the repositories I use to work and for personal projects. And I also set my finder to show files and folders as columns.

With these basic steps done, I sign in on iCloud and I install 1Password. I need to start with 1Password to sign into all the apps and websites. After it, I do Obsidian, Xcode and its command-line tools, Tailscale, Slack, Notion, Linear, VSCode, and iTerm2.

I quickly open most apps, just to make sure I do all the MacOS permissions and syncs. For example:
- Reminders
- Calendars, and I setup my Google Accounts (work and personal)
- Maps
- Mail

Finally, I performed all my terminal setup tasks. This means installing Homebrew, OhMyZsh, PowerLevel10k, Python (with pyenv and pipenv), and setup Git.

By setup Git, I mean ensuring that SSH and GPG are correctly configured, so that I use them for my signed commits, and pushes and pulls.

**What are my questions after this setup?**

- I know Macs have a [Migration Assitant](https://support.apple.com/en-us/102613) - should I be using it and just get data from the old mac? Feels like setting up a clean mac prevents me from bringing clutter.
- How many GPG keys should I have? - The answer seems [unclear](https://security.stackexchange.com/questions/29851/how-many-openpgp-keys-should-i-make) as we can have either one key and multiple subkeys, or just have multiple keys.
- I wish that I could just install all my normal apps with a single app or system - what is the best way to do it? I know I forgot some apps, and I will only install them when I face the issue they solve.
- I had some issues signing up to google with my security key. It was really weird, and I had to set them again as Passkeys instead of 2FA. I have no idea why they were not working, and I am lucky I did not get locked out. What the heck happened?
