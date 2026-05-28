---
layout: post
title: "Cleaning Up Xcode Simulator Runtimes"
excerpt_separator:  <!--more-->
categories:
  - Random Code
tags:
  - macOS
  - Xcode
  - iOS
---

I have a MacBook Air M3 with 256GB of storage. It is not a lot.
I use it for my Python projects and iOS projects, so Xcode and all its baggage are a permanent fixture.

Recently I noticed my disk was almost full, and my System Data was over 100GB.
I had no idea what was in there or how to clean it.
I tried the usual — clearing caches, emptying the bin — and nothing moved the needle.

<!--more-->

I ended up trying [DaisyDisk](https://daisydiskapp.com/), which visualises your disk as a sunburst chart so you can see exactly what is taking up space.
It made it very easy to find the offenders.
I cleaned over 50GB in one session and bought the app straight after.

DaisyDisk also surfaced data left behind by apps I had long deleted — 1GB from Zed Editor, 3GB from the Prime Video app.
Apps don't always clean up after themselves when you remove them.

One of the biggest culprits was Xcode simulator runtimes — large disk images that pile up silently as you install new iOS versions and never remove the old ones.
I googled the specific folders DaisyDisk pointed me to and found the `xcrun simctl` commands to deal with them:

- **List installed runtimes** — shows name, version, and UUID:
  ```
  xcrun simctl runtime list
  ```

- **List runtimes as JSON** — useful if you want to script the cleanup:
  ```
  xcrun simctl runtime list -j
  ```

- **Delete a specific runtime by UUID** — use the UUID from the list above:
  ```
  xcrun simctl runtime delete "A1B2C3D4-E5F6-7890-ABCD-EF1234567890"
  ```

- **Recover lost runtime images** — scans for runtime images that exist on disk but are no longer mounted, and remounts them:
  ```
  xcrun simctl runtime scan-and-mount
  ```

Each runtime can be several gigabytes. I kept only the ones I actively test against and freed up a good chunk of space.

If your System Data is bloated and you have no idea why, I'd start with DaisyDisk.
