---
layout: post
title: Dell XPS 13 7390 Wifi Problems
excerpt_separator:  <!--more-->
categories:
  - Life
tags:
  - Learning
---
Hello everyone,

If you are a develepor in today's day and age, you might have requested to get a Dell XPS laptop. Of course you asked for the Ubuntu developer version. Hopefully you got it.

If you didn't get it, and got the Windows version instead, you installed Ubuntu, and probably no longer have Wifi. That is what happened to me. Lets solve it.

To start, when the laptop is boothing, go into the BIOS and make sure you get the model right. After that, with the model number, go into Dell's website and
get the specs - precisely the Wireless card model.

In my case, it said the Wireless card was a `Killer AX1650W` but it said on every Ubuntu menu `Intel Corporation`. This is because the Killer card was a partnership with Intel I assume.
So don't lose your mind thinking that you got a different card. Just follow all the stackoverflow tutorials.

The best is to check the Killer website though: [here](https://support.killernetworking.com/knowledge-base/killer-ax1650-in-debian-ubuntu-16-04/).

Follow the steps, reboot, and you are done. Wifi is back!

Thanks for reading,

Jose
