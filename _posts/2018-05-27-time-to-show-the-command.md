---
layout: post
title: Time to Show the Command
date: 2018-05-27 12:00:00.000000000 -05:00
published: true
type: post
status: publish
categories:
- Help
tags:
- Help
- Getting started
- PowerShell
- rtpm
author: mwjcomputing
---

`Show-Command` is a neat feature and we decided to include it as part of the three commands that everyone needs to know to use PowerShell. I guess that would make four commands now that everyone using PowerShell needs to know.

Show Me the Command!

`Show-Command` allows you to make a PowerShell command in a window. This window allows you to work through the available parameters that the command uses and then when done, run the command or copy the command to the clipboard. This is done complete with all the parameters you edited in the window.

`Show-Command` is simply invoked by typing `Show-Command` and then the name of the command you want to use. For example, if we wanted to use `Show-Command` to help us with `Get-Help`, we would type `Show-Command -Name Get-Help`. The resulting window looks like this:

![Show-Command][img-show-command-1]

If done, in the ISE the resulting Window looks like this:

![Show-Command in ISE][img-show-command-2]

Pretty simple huh?

**Features of Show-Command**

There are a few features of `Show-Command` and the resulting box you would want to be aware of.

First, the tabs that are displayed are displaying the parameter sets that the command can use. A parameter set is basically a set of parameters that work together. In the show command window, things that are mandatory are denoted with an asterisk, as seen below.

![Show-Command mandatory parameter][img-show-command-3]

Secondly, you can do three things with `Show-Command`. You can inspect the commands parameters, copy your filled-out form to the clipboard and finally, you can run the command straight from the window. The first one is just a function of `Show-Command`. The second two are actual buttons at the bottom of the window as seen below.

![Show-Command Copy and Run][img-show-command-4]

Thirdly, you can fill out what PowerShell calls Common Parameters. Common parameters are parameters that should be on every command that PowerShell has or commands you add via modules. Common parameters include `-ErrorActionPreference`, `-Debug`, `-Force`, etc. We will go over Common Parameters in a future post as they are super important to understand. You need to hit the arrow to expand the list of common parameters.

![Show-Command Show Common Parameters][img-show-command-5]

Once you hit the arrow, the following area shows up.

![Show-Command Show Common Parameters Area][img-show-command-6]

**Experience the Magic**

Well, that is it with `Show-Command`. Time for you to go out and experience the magic of `Show-Command`. Remember to look at each tab if there are multiple tabs as you can find things you didn’t know existed with commands. Also, don’t be afraid to do `Show-Command` when just exploring PowerShell on your own. I know that John and I use this command frequently, especially when we are working with a new set of commands or a new module.

[img-show-command-1]:{{"/img/posts/2018-05-29/show-command-1.png" | absolute_url }}
[img-show-command-2]:{{"/img/posts/2018-05-29/show-command-2.png" | absolute_url }}
[img-show-command-3]:{{"/img/posts/2018-05-29/show-command-3.png" | absolute_url }}
[img-show-command-4]:{{"/img/posts/2018-05-29/show-command-4.png" | absolute_url }}
[img-show-command-5]:{{"/img/posts/2018-05-29/show-command-5.png" | absolute_url }}
[img-show-command-6]:{{"/img/posts/2018-05-29/show-command-6.png" | absolute_url }}