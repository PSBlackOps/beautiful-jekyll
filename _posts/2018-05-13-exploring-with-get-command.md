---
layout: post
title: Exploring With Get-Command
author: mwjcomputing
categories: 
- Help
tags:
- Help
- Getting started
- PowerShell
---

_This is the second in series of posts about learning to explore and help yourself with PowerShell._
_Other installments:_

* _[Learning to Read the (PowerShell) Fabulous Manual](2018-05-01-learn-to-rtpm.md)_

## Why Get-Command

`Get-Command` is super helpful at a fundamentally basic level. It does exactly what it says it does. (You will find out that most PowerShell resources do that.) It gets retrieves commands that are installed on the system.

Let's get started, with a simple example, by getting the command information for `Get-Help`.

```PowerShell
    Get-Command -Name Get-Help
```

The results should look as they do below.

![]({{"/img/posts/get-command-1.PNG" | absolute_url }} "'Get-Command -Name Get-Help' output")

As you can see, you can get information about the command you passed as the parameter argument to the parameter Name.

## Arguments / Parameters

Let's take a side step for a minute and talk about arguments and parameters. Arguments are the names we use to identify how information is sent to the command. Parameters are the data that arguments take to help the command process the request. Take a look at the picture below. You can see that `-Name` is the argument and `Get-Help` is the parameter.

![]({{"/img/posts/get-command-2.PNG" | absolute_url }} "Argument and Parameter image")

We will go further into this and how to read help in a different  post, but this should get you what we need to press forward.

## Other fun Get-Command Arguments

There are a few other arguments that are nice to have with Get-Command.

My personal favorite is `-Verb`. With the verb argument you can specify, as a parameter, one of the following approved verbs and retrieve all the commands that start with that verb. (You can get a list of approved verbs by running the `Get-Verb` command.)

```PowerShell
    Get-Command -Noun 'Show'
```

A view of the output from the above command is below.

![]({{"/img/posts/get-command-3.PNG" | absolute_url }} "'Get-Command -Noun 'Show'' Output")

If you run `Get-Command` all by itself, it gets you all of the following types of commands installed on your computer.

* Alias
* Function
* Cmdlet
* Workflow

Running `Get-Command` by itself can be lengthy, and potentially overwhelming, but it is really helpful when trying to discover what commands you can use on a system.

Another thing you can do is get many more commands that can be run on the system by typing the following.

```PowerShell
    Get-Command *
```

This command run on my system produces 2,592 possible commands, functions, aliases, etc. on my system.

## Other Items of Note

* If you run Get-Command and specify a command, PowerShell automatically loads the module that the command resides in. (We will cover modules in another post.)
* Also, remember that you can grab more information about `Get-Command` by typing `Get-Help -Name Get-Command` at a PowerShell prompt.

## Finally

I hope this post gets you down the path to exploring PowerShell on your own. As John said, don't be afraid to explore PowerShell. Happy PowerShelling!