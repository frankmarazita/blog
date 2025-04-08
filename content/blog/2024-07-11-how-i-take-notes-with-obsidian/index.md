---
title: "How I Take Notes with Obsidian"
date: 2024-07-11
summary: "A deep dive into my note taking system with Obsidian, including my syncing setup, plugins, and note taking philosophy."
toc: true
readTime: true
autonumber: true
showTags: false
---

**_Note: The way that I use Obsidian is always changing so this post will be considered an ongoing WIP. I'll do my best to maintain this post with whatever current tools and techniques I'm using!_**

### Introduction

I had a goal at the beginning of 2023 to migrate all my notes and frequently accessed information to single location. I wanted to be able to access this information from any device and have it be easily searchable.

I had notes in various places such as Google Keep, Google Drive, Phone Notes, Joplin (which I used for a while), various emails, random git repos. It was a mess and it was playing on my mind that I was going to lose some of this information. I began to look for a solution that would allow me to consolidate all my notes into a single location.

I came across [Obsidian](https://obsidian.md/) and at first saw it featured in a few YouTube thumbnails but it never really caught my attention. After hearing a few people talk about it, I decided to give it a go. I was immediately impressed with its very basic and simple interface. It was exactly what I was looking for.

Luck for me, most of my existing notes were all text based with rarely any images or attachments. This made it easy to migrate to a new system. The most annoying thing was probably the formatting of some of my existing notes, but I was willing to put up with that.

Like Joplin which I used previously, Obsidian is a markdown based note taking app, however unlike Joplin, Obsidian doesn't store your notes in a database. Instead, it stores your notes in a folder on your computer. This to me is a huge advantage.

The standout features of Obsidian for me personally are:

- Notes are stored in markdown format in a folder on your device

  - I can easily access my notes from any text editor and I'm not locked into a proprietary format
  - If a day ever comes where Obsidian is no longer maintained, you can easily move to another markdown based note taking app
  - Privacy is also a big concern for me and I like that I own my data
  - I can store my notes in a git repository which means that I have a history of all my notes

- Plugin system
  - This allows you to extend the functionality of the software to suit your own note taking style
  - If there is a feature that you want that isn't native to Obsidian, there is probably a plugin available for it
  - There is a massive community around Obsidian which means that there are a lot of plugins available

### Note Syncing Setup

Another great feature of Obsidian is that it has an extensive plugin system. This allows you to extend the functionality of the software to suit your own note taking style. While Obsidian has a native but paid sync service, there are also plugins that allow you to choose your own syncing solution.

To me, having quick access to my notes on all devices is a must. I have a desktop, laptop and phone which I use regularly and want to be able to access my notes from any of these devices. The notes should be in sync and up to date. another must is a backup solution. I want to ensure that my notes always have a backup of some sort.

My solution for syncing and backups is a combination of the following plugins and tools:

- [Self-hosted LiveSync](https://github.com/vrtmrz/obsidian-livesync)
- [Obsidian Git](https://github.com/Vinzent03/obsidian-git)
- [Tailscale](https://tailscale.com/)
- [CouchDB](https://couchdb.apache.org/)
- [docker-obsidian](https://github.com/linuxserver/docker-obsidian)

I mostly use the Self-hosted LiveSync plugin to sync my notes between all my obsidian devices. I have a CouchDB instance running on a VPS which the plugin uses to sync the notes. All my devices and the VPS are connected via Tailscale which allows me to access the CouchDB instance from anywhere privately. As a backup solution, I use Obsidian Git to commit changes to the CouchDB instance.

Having a Git repository tracking my notes is a great backup solution. I can easily revert to a previous version of a note if I make a mistake or delete something by accident. I can also easily see the changes I've made to a note over time. I have Obsidian Git configured to commit changes to a private Git repository every 5 minutes.

The other notable part of my setup is that I have a docker container running Obsidian in a VNC container. This allows me to access my notes from any device that has an internet connection via the web browser. This is useful for when I want to access my notes from a device that I don't want to copy my notes to. I can connect via Tailscale or ssh tunnel. Enabling the `Web viewer` core plugin is quite useful for viewing webpages inside of the VNC container.

### Plugins and Customisation

Alongside the plugins that I use for syncing and backing up my notes, there are also a variety of plugins I find useful for their quality of life improvements and workflow improvements.

**AI and Language Models**

- [Github Copilot](https://github.com/Pierrad/obsidian-github-copilot)

  - This extension leverages the Github Copilot AI and adds autocomplete functionality to Obsidian. I find it useful for all sorts of things in my notes, not just code. I generally find it useful for writing out complex ideas and concepts.

- [MCP Obsidian](https://github.com/MarkusPfundstein/mcp-obsidian)

  - This is an MCP server for your obsidian notes, which allows for AI chat services such as Clauded and Github Copilot Chat to read and make changes to your notes. It leverages the `Obsidian Local Rest API` plugin for it's communication. This can be extremely powerful for automating tasks and making changes to your notes.

**File Type Specific**

- [Excel](https://github.com/ljcoder2015/obsidian-excel)

  - Sometimes when taking a note, inline text tables just don't cut it. I use this plugin to edit and view Excel files in Obsidian. I find it useful for when I need to create a more complex table.

- [Excalidraw](https://github.com/zsviczian/obsidian-excalidraw-plugin)

  - I use this plugin to create and edit Excalidraw diagrams that live in my notes. I find it useful for creating quick diagrams and flowcharts.

- [Obsidian Asciinema](https://github.com/frankmarazita/obsidian-asciinema)

  - This is a plugin that I have started to build myself. It allows you to embed asciinema recordings in your notes. A frequent scenario is when I want to record the steps that I take to install a piece of software on my machine, usually when following an online tutorial. It is currently a very early work in progress.

**Tools**

- [Obsidan Local Rest API](https://github.com/coddingtonbear/obsidian-local-rest-api)

  - This is one of my most used plugins. It allows you to run a local REST API server that can be used to interact with your notes. I use this plugin to automate tasks and make changes to my notes. It is also used by the MCP Obsidian plugin.

- [Linter](https://github.com/platers/obsidian-linter)

- [Advanced Cursors](https://github.com/SkepticMystic/advanced-cursors)

- [Second Window ](https://github.com/javalent/second-window)

- [Kindle Highlights](https://github.com/hadynz/obsidian-kindle-plugin)

When it comes to visual customisation of the editor, I usually try keep things to as much of a default as possible. I tend to find that with heavy customisations comes unexpected issues, these could be due to plugins not being maintained while the core platform updates. There is also the retention of familiarity if I need to use another device without my customisations. If I wasn't using obsidian across multiple synced devices, I may be more inclined to spend time on customisations and worry less about these problems occurring.

### My Note Taking Philosophy

When it comes to note-taking, my philosophy revolves around a few core principles that ensure my system remains efficient, accessible, and useful across various aspects of my life. Here's a deeper dive into how I approach this:

**Accessibility from Any Device**

The cornerstone of my note-taking philosophy is accessibility. I believe that my notes should be available to me at all times, from any device. This means everything must be centralized in one location, ensuring that no matter where I am or what device I'm using, be it my desktop, laptop, or phone, I can quickly access the information I need. This eliminates the frustration of searching through multiple platforms and ensures that my workflow remains seamless.

**The Dump Note**

A key element of my note-taking system is what I call the "Dump Note." This is essentially a catch-all note located at the root of my Obsidian vault. Its primary purpose is to serve as a dumping ground for tasks and thoughts that are yet to be organized as well as any idea capture. Whenever I come across something I need to remember or jot down quickly, especially on my mobile app, it goes straight into the Dump Note. This method ensures that no idea or task is lost, and I can sort through them later when I have the time to organize everything properly. Everything has a place, but you don't always have time to put it in its place. This note is always pinned as a tab on all my devices.

What is also really awesome about Obsidian on mobile is that I can share to the Dump Note. This means that if I come across something that I want to remember, I can share it to the Dump Note directly and it will be there for me to sort through later.

It is my most frequently accessed and modified note and I find it to be a very useful tool in my note taking system. Nothing there is considered permanent and it is always in a state of flux.

**Organised Content Categories**

To keep my notes structured and easy to navigate, I tend to categorise them into specific content types. Here are some of the key categories I use and notes I keep:

- Personal Notes: Here, I store thoughts, reflections, and important information that I might need to refer back to. Some of these subcategories include self care, philosophy, personal goals, new year resolutions, and more. This section is essentially a digital diary that helps me track my personal growth and development.

- TODO Lists: These are broken down into subcategories such as General Life Admin, Projects to Start, Project-Specific TODOs, Movies to Watch, Books to Read, and Things to Buy. This detailed categorisation helps me stay on top of various aspects of my personal and professional life. Even if these lists grow and become extensive beyond completion, I would rather capture everything and have it available for reference than risk forgetting something.

- Work Log: A record of my professional timelines, projects completed etc, which helps in tracking progress and productivity. This can especially come in handy during performance reviews, reflecting on past achievements, or when you need to update your resume.

- Personal "Awesome Lists": These lists include my favourite tools, resources, and anything else that I find particularly useful or inspiring. I have a variety of lists with links to articles, blogs, tools, videos, and more, making it easy to revisit and share these valuable resources. Sometimes something is strange enough that I want to remember it, but not important enough to remember it and have it front of mind.

- Kindle Snippets: Excerpts and highlights from books I read on my Kindle, ensuring that I can easily revisit and reference them. I use the Kindle Snippets plugin to import these highlights directly into my Obsidian vault, making it a seamless process.

**_This is not an exhaustive list of my categories, but it gives you an idea about some of the key areas I focus on. I'll continue to update and refine these categories as my note-taking system evolves._**

The way that you choose to categorise your notes will slowly evolve over time. I don't believe that there is a best way. What's important is that you are able to efficiently find the information you need when you need it. Allow yourself to make change and move things around as you see fit.

**Note Taking Practice Experiences**

Over time, I've used a variety of practices. Here are some of the key practices that have stood out:

- Daily Notes: Maintaining daily notes keeping a consistent log of my activities and thoughts, as well as daily TODO lists. I did this for over a year and found it to be very useful initially but eventually found that I was spending too much time on it. It made maintaining habits easier but I found it to be stressful if I missed a day or didn't complete everything on my TODO list.

- Graph View, Backlinks, and Tags: I know that some people swear by the graph view and backlinks, but I haven't found them to be particularly useful for me in any way. There are generally few associations between any of my notes and I don't use tags. I find that the search functionality in Obsidian is good enough for me to find what I need.

### Future Exploration

Looking ahead, there are a few areas I’m keen to explore further:

- Public Note Sharing: I'm intrigued by the idea of making a subset of my notes public. Sharing my notes could not only help others but also invite feedback and collaboration. The concept of "working with the garage door open", being transparent and open about my work, resonates with me, and I’d like to see how this approach could benefit both myself and others.

- A TO-DONT's List: I've been thinking about creating a "TO-DONT's" list, which would essentially be a list of things I want to avoid or stop doing. This could include bad habits, unproductive activities, or anything that doesn't serve my personal or professional growth. I believe that being mindful of what not to do can be just as important as knowing what to do.

### Conclusion

I'm really happy with Obsidian and how it has helped me organise my notes so far. It currently ticks all the boxes for me and I can't see myself moving to another note taking app anytime soon. I'm looking forward to seeing how Obsidian evolves in the future and what new features are added.

I hope this post has been helpful to you in some way. If you have any questions or suggestions, feel free to reach out. I'm always looking for ways to improve my note taking system.
