---
author: mssurajkaiga
comments: true
date: 2012-07-06 09:36:19+00:00
layout: post
slug: yet-another-pidgin-plugin
title: Yet another Pidgin plugin
wordpress_id: 20
categories:
- Pidgin
- Plugin
tags:
- c
- coding
- open source
- pidgin
- plugin
- programming
- slash command
---

I continued browsing through the tickets in the pidgin developers section and found another one that I could do.

The basic purpose of this plugin is to let you change your account's status by using slash-commands (like irc commands). The commands I wanted to implement were :



	
  * /away <message> = to set your status as "away",

	
  * /dnd <message> = to set your status as "Do not disturb",

	
  * /online <message> = to set your status as "Available",

	
  * with <message> being optional.


This required the use of the commands and status APIs. The implementation of this plugin seemed pretty easy enough as there already existed a documentation for  using commands while chatting, so I looked it up and found  commands_example.c file for implementing chat commands. The cmds.h file let you create your own set of commands and hooks it up with a call-back function to be called when the command is typed. I created the required commands and their call-backs function prototypes.  Till this part everything was easy as it was just modification of the example file's code.  Now to implement the status changing part I had to use the status API.  I searched through the documentation but could not find a function that returned the statuses I wanted. I could create a new status from existing function but I didn't the want the plugin to create a duplicate statuses every time the person entered the command. Instead I wanted to lookup if the status already existed and then change the status as required. So, I decided to lookup the savedstatuses.h file documentation. I created the plugin with just the /away command first and it worked but with two problems -

	
  * I always needed to pass the <message> parameter for the command to successfully work.

	
  * Whatever <message> I passed, it did not matter, the status always changed to the default away status .


I overcame the first problem by setting the command usage flag to PURPLE_CMD_FLAG_ALLOW_WRONG_ARGS enabling the command to take no message parameter.  This created a new problem with the command returning an error that this command could not be used for this protocol. This turned out because I replaced the existing flag of PURPLE_CMD_FLAG_IM with the above one. Instead I should have kept both the flags separated by the bitwise( | ) operator (I was unaware I could use multiple flags). This being corrected, I took up the second problem. The /away command merely set the status using an inbuilt savedstatus function which didn't take any parameters and activated the default idle-away status resulting in the second problem. I couldn't rectify it so I decided to implement the /dnd command. Sadly for /dnd, there existed no such function which changed the status to the "busy" type. So I used the find function in the savedstatus api to search for any existing status with given <message> and activate it if it existed, else create a new saved status with the <message> parameter as its title and activate it. Implementing this method in the /away command solved the second problem as well. I duplicated this method for the /online command as well.

The .c file successfully compiled to give a .so plugin file which worked but with some minor problems that was then fixed. The only major problems were that it resulted in duplicate saved-statuses every time the user repeated the command without any parameter and that saved statuses kept on accumulating. The former was fixed by applying the find function to lookup the status even if no parameter was passed. I will fix the latter sometime later by adding a configure option to let the user choose if he wants to keep the saved statuses or not.

All-in-all I was glad I could complete it. I initially thought of writing a post that explains the code of the slash_commands.c file but then figured it will be even more boring than this post!!! Besides the file already has comments explaining the code!

Here is the ticket: [http://developer.pidgin.im/ticket/7984](http://developer.pidgin.im/ticket/7984)
Here is the source code: [https://github.com/mssurajkaiga/Pidgin-Plugins/tree/master/slash%20commands](https://github.com/mssurajkaiga/Pidgin-Plugins/tree/master/slash%20commands)
