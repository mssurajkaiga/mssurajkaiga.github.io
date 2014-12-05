---
author: mssurajkaiga
comments: true
date: 2012-07-03 20:32:18+00:00
layout: post
slug: my-first-pidgin-plugin
title: My first Pidgin Plugin
wordpress_id: 1
categories:
- Pidgin
- Plugin
tags:
- c
- coding
- libpurple
- open source
- piding
- plugin
- programming
---

**Pidgin** (formerly named **Gaim**) is an open-source multi-platform instant messaging client, based on a library named **libpurple** (as Wikipedia says). I have been using it for some time since I started using Linux (currently Ubuntu 12.04).

I decided to contribute to Pidgin about a month back. So, I read its documentation on libpurple based plugin development (quite old and incomplete, but still covers pretty much all the basics). I checked out its active tickets and found some easy ones that I could handle. I started working on a plugin that disables conversation (both IM and chat) loggin when you are not available (busy, away, invisible, etc). I didn't at first understand the log.h documentation and hence got confused resulting in a wrong approach. It resulted in a .c file that didn't compile. Frustrated, I decided to take a break and continued tweaking a website I was building for some seniors at my college. In between I tried few times with new approaches but to no avail. Finally, I decided to quit it when I got another web scraping project from another senior at my college. I finished it but became bored soon enough. So yesterday I returned back to pidgin.

This time I determined the logger currently in use and freed it when the status was no longer available. When user became available then the status-changed function would set the previous logger. Although the .c file produced a .so file, the plugin crashed as soon as I enabled it and changed my status as not available. Turns out I was again on the wrong path. While browsing the **libpurple**'s API documentation I found conversation API and it struck me another idea. Upon browsing through it, I found that this idea can be implemented. Instead of freeing and setting the system logger, I could just enable or disable logging for a particular conversation by using a function in the conversation API. I then wrote a c file that retrieves the current conversations and checks the user status( once when the plugin loads and then every time the status changes). The conversation handle would be passed to a function which would check the current status of logging and enable/disable it as required. When the plugin unloads it resets all conversations back to logging-enabled status. This resulted in a successful make of a .so file. This time the plugin worked just fine and I was more than relieved!!!

Here is the ticket: [http://developer.pidgin.im/ticket/8153](http://developer.pidgin.im/ticket/8153)
Here is the source code: [https://github.com/mssurajkaiga/Pidgin-Plugins/tree/master/selective%20logging](https://github.com/mssurajkaiga/Pidgin-Plugins/tree/master/selective%20logging)
