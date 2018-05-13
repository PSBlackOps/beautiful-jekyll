---
layout: post
title: Getting the Most Out of Get-Help
date: 2018-05-12 15:47:21.000000000 -05:00
type: post
published: true
status: publish
categories:
- Help
tags:
- Help
- Getting started
- PowerShell
- rtpm
author: jpbruckler
---

This is the second in a series of articles about learning PowerShell. In this article, I'm going to concentrate on the many ways
to use the `Get-Help` cmdlet for function/cmdlet discovery, and usage.

The first article can be found [here]({% post_url 2018-05-01-learn-to-rtpm %}).

`Get-Help` is extremely flexible, and extremely valuable to the novice and advanced PowerShell developer alike. It can be used to
find commands, discover 

## Get-Started

The first thing you need to know about `Get-Help` is that the help files aren't installed locally on your computer. I know, I know,
crazy right? Microsoft made that decision to help with the issue of outdated or incorrect help files. The documentation for PowerShell
is located online where it's easier to keep updated [^1]. 

Online help isn't discoverable by `Get-Help` though, so the first thing to do is install the PowerShell help files locally on your
system. You'll need an internet connection, and administrative rights on the machine you're installing help on. You can read all about
`Update-Help` on [MSDN], but installing help locally is pretty easy.

1. Open an administrative/elevated PowerShell prompt
    1. From within a normal PowerShell prompt, you can type `Start-Process powershell.exe -Verb RunAs` to create an elevated PowerShell
    prompt.
2. Type: `Update-Help`
3. It's going to take a few minutes to run, but a progress bar will be shown as help files are downloaded and installed. ![update-help][img-update-help]
4. When I installed help as part of writing this post, I received an error that the help files for 'WindowsUpdateProvider' couldn't be
  found and weren't downloaded. If you see something similar, that's OK.

## Get-Help Basics

The simplest way that `Get-Help` is used, is simply to give it the name of a function, cmdlet, or alias that you want to know about.

__Note__: The output below is what you will see when issuing a `Get-Help` command after having installed the help files locally. If
help files are not installed locally, you will still get basic syntax, but will not have access to the full help text for a command.

```powershell
PS C:> Get-Help Get-EventLog

NAME
    Get-EventLog

SYNOPSIS
    Gets the events in an event log, or a list of the event logs, on the local or remote computers.


SYNTAX
    Get-EventLog [-LogName] <String> [[-InstanceId] <Int64[]>] [-After <DateTime>] [-AsBaseObject] [-Before
    <DateTime>] [-ComputerName <String[]>] [-EntryType {Error | Information | FailureAudit | SuccessAudit | Warning}]
    [-Index <Int32[]>] [-Message <String>] [-Newest <Int32>] [-Source <String[]>] [-UserName <String[]>]
    [<CommonParameters>]

    Get-EventLog [-AsString] [-ComputerName <String[]>] [-List] [<CommonParameters>]


DESCRIPTION
    The Get-EventLog cmdlet gets events and event logs on the local and remote computers.

    You can use the parameters of this cmdlet to search for events by using their property values. This cmdlet gets
    only the events that match all of the specified property values.

    The cmdlets that contain the EventLog noun work only on classic event logs. To get events from logs that use the
    Windows Event Log technology in Windows Vista and later versions of Windows, use Get-WinEvent.


RELATED LINKS
    Online Version: http://go.microsoft.com/fwlink/?LinkId=821585
    Clear-EventLog
    Limit-EventLog
    New-EventLog
    Remove-EventLog
    Show-EventLog
    Write-EventLog

REMARKS
    To see the examples, type: "get-help Get-EventLog -examples".
    For more information, type: "get-help Get-EventLog -detailed".
    For technical information, type: "get-help Get-EventLog -full".
    For online help, type: "get-help Get-EventLog -online"
```

With no other [parameters] or [switches], `Get-Help` will display basic syntax about a command, and a description. The __REMARKS__
section indicates that additional switches can be used to display additional information. The most useful switch is `-Full`, which
outputs all the help information for a command, including examples of how the command can be used.

## Get-Help Discovery

`Get-Help` supports the use of wildcards, so you can search for help topics installed locally. A lot of Microsoft and 3rd party modules
include `about_TOPIC` files, that have additional information about key language or module concepts.

Let's say you wanted to write a function, but didn't know where to start. You could use `Get-Help` to _discover_ what help there is,
with the command `Get-Help *function*`:

![Get-Help Wildcard][img-get-help-wildcard]



You can get to the latest version of the PowerShell documentation by going to
[https://microsoft.com/powershell] - make sure you select the version that matches the PowerShell
version you're using. You can install the help files manually, but I prefer using the `-Online` switch, which opens your default
browser to the online version of PowerShell's help documentation.


`Get-Help` accepts wildcards, too. This is useful when you need to get the help of a command or an `about` topic
but you aren't sure what it's called. The downside is, without th


[MSDN]:https://docs.microsoft.com/en-us/powershell/module/Microsoft.PowerShell.Core/Update-Help?view=powershell-5.1
[parameters]:https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_functions?view=powershell-6#named-parameters
[switches]:https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_functions?view=powershell-6#switch-parameters
[img-update-help]:{{"/img/posts/2018-05-12/update-help-start.png" | absolute_url }}
[img-get-help-wildcard]:{{"/img/posts/2018-05-12/get-help-function-wildcard.PNG" | absolute_url}}


[^1]: [https://docs.microsoft.com/en-us/powershell/scripting/powershell-scripting]
(https://docs.microsoft.com/en-us/powershell/scripting/powershell-scripting)