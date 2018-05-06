---
layout: post
title: Getting the Most Out of Get-Help
date: 2018-05-02 15:47:21.000000000 -05:00
type: post
published: true
status: publish
categories:
- Help
tags:
- Help
- Getting started
- PowerShell
author: jpbruckl
---

This is the second in a series of articles about learning PowerShell. In this article, I'm going to concentrate on the many ways
to use the `Get-Help` cmdlet for function/cmdlet discovery, and usage.

The first article can be found at

## Get-Started

The first thing you need to know about `Get-Help` is that the help files aren't installed locally on your computer. I know, I know,
crazy right? Microsoft made that decision to help with the issue of outdated or incorrect help files. The documentation for PowerShell
is located online where it's easier to keep updated. You can get to the latest version of the PowerShell documentation by going to
[https://microsoft.com/powershell]("https://microsoft.com/powershell") - make sure you select the version that matches the PowerShell
version you're using[^1]. You can install the help files manually, but I prefer using the `-Online` switch, which opens your default
browser to the online version of PowerShell's help documentation.

The simplest way that `Get-Help` is used, is simply to give it the name of a function, cmdlet, or alias that you want to know about.

```powershell
PS C:> Get-Help Get-EventLog

NAME
    Get-EventLog

SYNTAX
    Get-EventLog [-LogName] <string> [[-InstanceId] <long[]>] [-ComputerName <string[]>] [-Newest <int>] [-After <datetime>] [-Before <datetime>] [-UserName <string[]>] [-Index <int[]>] [-EntryType {Error | Information | FailureAudit |
    SuccessAudit | Warning}] [-Source <string[]>] [-Message <string>] [-AsBaseObject]  [<CommonParameters>]

    Get-EventLog [-ComputerName <string[]>] [-List] [-AsString]  [<CommonParameters>]


ALIASES
    None


REMARKS
    Get-Help cannot find the Help files for this cmdlet on this computer. It is displaying only partial help.
        -- To download and install Help files for the module that includes this cmdlet, use Update-Help.
        -- To view the Help topic for this cmdlet online, type: "Get-Help Get-EventLog -Online" or
           go to https://go.microsoft.com/fwlink/?LinkID=113314.
```

`Get-Help` accepts wildcards, too.