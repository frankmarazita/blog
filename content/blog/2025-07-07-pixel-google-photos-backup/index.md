---
title: "How I Turned a Pixel 1 into a Headless Google Photos Backup Server for My Home Lab"
date: 2025-07-07
summary: "A guide on repurposing an old Pixel 1 as a secure, automated backup server for photos and videos using Google Photos."
toc: true
readTime: true
autonumber: true
showTags: false
---

Few people know this, but the original **Google Pixel (Pixel 1)** still offers a hidden gem: **unlimited original-quality Google Photos backups**. While newer Pixels have lost this benefit, the Pixel 1 can be repurposed as a compact, headless backup server for photos and videos. Here’s how I set mine up and why it works so well.

### Why I Chose the Pixel 1

The Pixel 1 is perfect for this task:

- Unlimited original-quality uploads to Google Photos
- Affordable and easy to source second-hand
- Small, energy-efficient, and reliable for 24/7 operation
- Can run completely headless (no screen interaction required)

Its combination of free cloud storage and minimal hardware needs makes it ideal for home lab automation.

### The Network Setup

I wanted a secure, always-on solution, so I added the Pixel to my **Tailscale network**. This:

- Allows secure remote access to the device
- Eliminates the need for port forwarding or exposing services to the internet
- Keeps all transfers encrypted across devices

The Pixel sits on my network alongside my home server running FTP, which acts as the central hub for photo and video collection.

### Workflow Overview

The automation is split into four main stages:

#### 1. Devices Upload to FTP Server

All my personal devices automatically push new media to a shared folder on the FTP server. This is configured individually per device, but for my daily Android device, I use the [**Autosync**](https://play.google.com/store/apps/details?id=com.ttxapps.autosync&hl=en-US) app.

The **Autosync** app is a paid, but very reliable sync app that allows for multiple configurations of an FTP connection. This means that I can select multiple different locations on the device's file system and set them up as folders which will sync to the main server. I use an FTP connection to my server which is on the same Tailscale network, this means that I am able to sync my files from anywhere in the world. This is especially helpful when travelling overseas.

I use [**vsftpd**](https://hub.docker.com/r/fauria/vsftpd/) running in a Docker container on my server to provide the FTP service. This is a very lightweight and simple FTP server that works well for this purpose. This is not exposed to the internet, only accessible via Tailscale.

#### 2. Pixel Pulls Media

I use the same **Autosync** app on the Pixel device side. This automatically pulls any new files from the FTP server to its local storage. This ensures that nothing is missed.

#### 3. Google Photos Upload

The Google Photos app continuously watches the local folders and uploads everything at 'original quality'. Because the Pixel 1 has unlimited backup, this is fully free and reliable. The files don't need to originate from the Pixel 1 itself, they just need to be uploaded from it.

#### 4. Cleanup and Retention

To ensure that I am not taking too much space on my personal devices, I have rules set up in **Autosync** such that after files have been uploaded, they are removed from the local device after 7 days.

The Pixel device has a similar rule, such that after it has downloaded files from the server, it will remove them from the server after 7 days.

This creates a minimum 7-day buffer where every file exists in three places: the original device, the FTP server, and Google Photos.

### Handling Videos

Videos follow the same pipeline as photos, configured to upload from their respective folder locations on the device. This ensures that even high-resolution videos are backed up automatically.

### Battery Management

There can be issues with keeping the Pixel 1 device plugged in 24/7. The main one being leaving a phone plugged in all day can degrade the battery.

To address this an option is to limit charging to ~80% using an app such as tasker to toggle a smart plug when the device battery reaches certain levels.

The goal is a reliable, low-maintenance system that doesn’t wear out the device unnecessarily.

_I have already needed to replace the battery once in the past since I failed to consider this._

Note: There is info online on how to run the Pixel 1 device without an internal battery, but this requires some electrical work.

### Security and Privacy

The setup prioritizes privacy:

- Only the Google Photos account is signed in
- No personal messages, contacts, or apps are installed
- Tailscale keeps all network traffic secure without exposing ports to the internet

By keeping the Pixel isolated, I minimize risk while keeping the automation fully functional.

### Tools I Use

- **Google Pixel 1** (factory reset + minimal apps)
- **Autosync** for FTP → Pixel sync
- **Tasker** for automated cleanup
- **Tailscale** for secure network access
- **FTP server** on my server
- **Google Photos** app for cloud upload

### Limitations

- The Pixel 1 is old hardware, so performance is modest
- The unlimited original-quality upload is a Google feature, not a guarantee — future policy changes could affect this.

### Future Improvements

I plan to enhance the setup by:

- Replacing FTP with **Syncthing** or something similar.

  - I don't really like relying on a paid Android app to do a lot of the heavy lifting in this flow.
  - I may need to reconsider how I clean up files after they have been uploaded / downloaded from the devices.

- Having a self hosted media server with a copy of my files locally.
  - As I slowly attempt to move away from cloud services, this is something that I would like to implement. Having a mirror at the very least.

### Benefits

This system has several advantages:

- Free, unlimited original-quality backups. I currently have at least 100GB+
- True set-and-forget automation
- Centralized media repository without subscriptions
- Works seamlessly across devices

### Conclusion

With a single retired Pixel 1, I built a fully automated, secure, and private backup server for all my photos and videos.

It’s cheap, reliable, and effortless.

If you have a Pixel 1 gathering dust, it could become the cornerstone of your home media backup strategy. However, they are starting to become a bit more rare on Ebay these days and the prices are slowly creeping upwards.
