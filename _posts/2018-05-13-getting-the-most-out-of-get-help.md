---
layout: post
title: Getting the Most Out of Get-Help
date: 2018-05-13 15:47:21.000000000 -05:00
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

This is the third in a series of articles about learning PowerShell. In this article, I'm going to concentrate on the many ways
to use the `Get-Help` cmdlet for function/cmdlet discovery, and usage.

The first article can be found [here]({% post_url 2018-05-01-learn-to-rtpm %}).

`Get-Help` is extremely flexible, and extremely valuable to the novice and advanced PowerShell developer alike. It can be used to
discover commands, find examples, and find related commands/information.

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
PS C:> Get-Help -Name Get-EventLog

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

While the king of command discovery is [Get-Command], with the ability to use wildcards and list commands that take the same parameter,
`Get-Help` is a close second.

When `Get-Help` finds more than one help file that matches the `-Name` parameter provided, it prints to the console a list of the matching
files, which is what makes this such a useful tool for discovery.

### Wildcard Searching

`Get-Help` supports the use of wildcards, so you can search for help topics installed locally. A lot of Microsoft and 3rd party modules
include `about_TOPIC` files, that have additional information about key language or module concepts. So how do you find all this wonderful
information, when all you know for sure is that these help files start with `about_`? Enter the wildcard.

`Get-Help` accepts the asterisk as a wildcard character meaning _any character at all, from 0 to infinity matches_. A question mark can
also be used, and is interpreted as _any character at all, exactly 1 time_.

For example:

1. `Get-Help -Name about_function*` returns several results, as the asterisk matches any character that comes after the word
  function.
1. `Get-Help -Name about_function?` will instead output the contents of the `about_Functions` file, since the ? matched the s
  character.

You can list all the about topics by using the command `Get-Help about*`:

```powershell
PS C:> Get-Help about*

Name                              Category  Module                    Synopsis
----                              --------  ------                    --------
about_ActivityCommonParameters    HelpFile                            Describes the parameters that Windows PowerShell
about_Aliases                     HelpFile                            Describes how to use alternate names for cmdlets...
about_Arithmetic_Operators        HelpFile                            Describes the operators that perform arithmetic ...
about_Arrays                      HelpFile                            Describes arrays, which are data structures desi...
about_Assignment_Operators        HelpFile                            Describes how to use operators to assign values ...
about_Automatic_Variables         HelpFile                            Describes variables that store state information...
about_Break                       HelpFile                            Describes a statement you can use to immediately...
about_Checkpoint-Workflow         HelpFile                            Describes the Checkpoint-Workflow activity, which
about_CimSession                  HelpFile                            Describes a CimSession object and the difference...
about_Classes                     HelpFile                            Describes how you can use classes to develop in ...

<snip>

about_ActivityCommonParameters    HelpFile                            Describes the parameters that Windows PowerShell
about_Checkpoint-Workflow         HelpFile                            Describes the Checkpoint-Workflow activity, which
about_ForEach-Parallel            HelpFile                            Describes the ForEach -Parallel language constru...
about_InlineScript                HelpFile                            Describes the InlineScript activity, which runs ...
about_Parallel                    HelpFile                            Describes the Parallel keyword, which runs the
about_Sequence                    HelpFile                            Describes the Sequence keyword, which runs selected
about_Suspend-Workflow            HelpFile                            Describes the Suspend-Workflow activity, which s...
about_WorkflowCommonParameters    HelpFile                            This topic describes the parameters that are val...
about_Workflows                   HelpFile                            Provides a brief introduction to the Windows
```

`Get-Help` returned 146 different about topics. That's a lot of information to wade through. Let's say you wanted to write
a function, but didn't know where to start. You could use `Get-Help` to _discover_ what help there is, with the command
`Get-Help about_function*`:

```powershell
PS C:>  Get-Help about_function*

Name                              Category  Module                    Synopsis
----                              --------  ------                    --------
about_Functions                   HelpFile                            Describes how to create and use functions in Win...
about_Functions_Advanced          HelpFile                            Introduces advanced functions that act similar t...
about_Functions_Advanced_Methods  HelpFile                            Describes how functions that specify the CmdletB...
about_Functions_Advanced_Param... HelpFile                            Explains how to add parameters to advanced funct...
about_Functions_CmdletBindingA... HelpFile                            Describes the attribute that makes a function wo...
about_Functions_OutputTypeAttr... HelpFile                            Describes an attribute that reports the type of ...
```

6 results is much more managable than 146, and more than likely, `about_Functions` is going to get you the information you
need to start writing functions.

### Discover Parameters

Another useful feature of `Get-Help` comes from being able to find commands that take a certain parameter. For instance,
a lot of commands take a `-ComputerName` parameter, since PowerShell is built to be a remote administration tool. To find
commands based on a parameter, you would use `Get-Help * -Parameter ComputerName`. This combines the wildard functionality
with the ability to search on Parameter names.

```powershell
PS C:> Get-Help * -Parameter ComputerName

Name                              Category  Module                    Synopsis
----                              --------  ------                    --------
Connect-PSSession                 Cmdlet    Microsoft.PowerShell.Core Reconnects to disconnected sessions.
Enter-PSSession                   Cmdlet    Microsoft.PowerShell.Core Starts an interactive session with a remote comp...
Get-PSSession                     Cmdlet    Microsoft.PowerShell.Core Gets the Windows PowerShell sessions on local an...
Invoke-Command                    Cmdlet    Microsoft.PowerShell.Core Runs commands on local and remote computers.
New-PSSession                     Cmdlet    Microsoft.PowerShell.Core Creates a persistent connection to a local or re...
Receive-Job                       Cmdlet    Microsoft.PowerShell.Core Gets the results of the Windows PowerShell backg...
Receive-PSSession                 Cmdlet    Microsoft.PowerShell.Core Gets results of commands in disconnected sessions.
Remove-PSSession                  Cmdlet    Microsoft.PowerShell.Core Closes one or more Windows PowerShell sessions (...
Add-Computer                      Cmdlet    Microsoft.PowerShell.M... Add the local computer to a domain or workgroup.
Clear-EventLog                    Cmdlet    Microsoft.PowerShell.M... Clears all entries from specified event logs on ...
```

### Searching by Category

Most help topics have some metadata associated with them, and one of the most useful pices of metadata is __Category__,
which can be searched by using the `-Category` parameter of the `Get-Help` command. 

There are certain values that the `-Category` parameter will take, and those are listed in the help contents for the `Get-Help`
command itself. In my experience, most of the Categories that are acceptable to search for aren't even used. One way to see
which categories are in use on your system, you can run the command below. 

This command makes use of the wildcard character * to search for all help topics, then pipes those results to `Where-Object`,
which checks to see if the Category property is not null, and if so, passes the result from `Get-Help` off to `Group-Object`,
which then displays the results; showing all the categories found (__Name__ column), and the number of help topics associated
with that category.

```powershell
PS C:\> Get-Help * | Where-Object Category -ne $null | Group-Object -Property Category

Count Name                      Group
----- ----                      -----
  162 Alias                     {@{Name=foreach; Category=Alias; Synopsis=ForEach-Object; Component=; Role=; Functiona...
  924 Function                  {@{CommonParameters=False; WorkflowCommonParameters=False; details=; Syntax=; paramete...
    1 ExternalScript            {ridk.ps1 ...
  620 Cmdlet                    {@{examples=@{example=System.Management.Automation.PSObject[]}; inputTypes=@{inputType...
    7 Provider                  {@{DetailedDescription=System.Management.Automation.PSObject[]; Notes=; Capabilities=S...
  148 HelpFile                  {TOPIC...
```

## Getting Help for Providers

Completely explaining providers is beyond the scope of this post (but you could read about them with `Get-Help *provider* -Category HelpFile`),
what I will say is that PowerShell has certain providers that it possible to navigate things like a filesystem. For example,
you can change directory into the __HEKY_LOCAL_MACHINE__ registry hive just by doing this:

```powershell
PS C:\> cd HKLM:
HKLM:\>
```

Which is pretty neat. It's also neat that you can get help about specific providers. If you happen to know the name of the
provider, you can just use that name in the `-Name` parameter, like:

```powershell
PS C:\> Get-Help -Name registry

PROVIDER NAME
    Registry

DRIVES
    HKLM:, HKCU:

SYNOPSIS
    Provides access to the system registry keys and values from Windows PowerShell.

DESCRIPTION
    The Windows PowerShell Registry provider lets you get, add, change, clear, and delete registry keys and values in
    Windows PowerShell.
...
```

But if you don't happen to know the name of the provider, you can also provide a __path__ to `Get-Help`, like so:

```powershell
PS C:\> Get-Help New-Item -Path Cert:\CurrentUser\

NAME
    New-Item

SYNOPSIS
    Creates new certificate stores in the LocalMachine store location.


SYNTAX
    New-Item [[-Path] <String[]>] [-Confirm] [-Credential <PSCredential>] [-Force] [-ItemType <String>] -Name <String>
    [-UseTransaction] [-Value <Object>] [-WhatIf] [<CommonParameters>]

    New-Item [-Path] <String[]> [-Confirm] [-Credential <PSCredential>] [-Force] [-ItemType <String>] [-UseTransaction]
    [-Value <Object>] [-WhatIf] [<CommonParameters>]

    New-Item [-Path] <string[]> [-Name <string>] [-Confirm] [-WhatIf] [<CommonParameters>]

    New-Item [-Path] <string[]> [-Confirm] [-WhatIf] [<CommonParameters>]

...
```

The above command shows provider specific help for the `New-Item` command for the Cert PowerShell provider.

## -ShowWindow

The last thing I want to share about `Get-Help` is the `-ShowWindow` parameter, which opens up a searchable interface with
the help text in it. This is an incredibly useful feature, especially when viewing some of the longer help items, like
`about_comment_based_help`.

```powershell
PS C:\> Get-Help about_comment_based_help -ShowWindow
```

![Show-Window][img-show-window]

This beats the heck out of trying to read the entire thing in a console window.

# Finally

Effectiveness with a new language often comes down to familiarity with that language. PowerShell has many tools available
to get to know your way around the ins and outs of the language, and `Get-Help` is a very powerful one. 

I hope this post was able to help you learn some more about finding PowerShell answers, or at least showed you a thing or
2 about `Get-Help` that you didn't already know.

[MSDN]:https://docs.microsoft.com/en-us/powershell/module/Microsoft.PowerShell.Core/Update-Help?view=powershell-5.1
[parameters]:https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_functions?view=powershell-6#named-parameters
[switches]:https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_functions?view=powershell-6#switch-parameters
[Get-Command]:{% post_url 2018-05-13-exploring-with-get-command %}
[img-update-help]:{{"/img/posts/2018-05-13/update-help-start.png" | absolute_url }}
[img-get-help-wildcard]:{{"/img/posts/2018-05-13/get-help-function-wildcard.PNG" | absolute_url}}
[img-show-window]:{{"/img/posts/2018-05-13/show-window.png" | absolute_url }}

### Footnotes

[^1]: [https://docs.microsoft.com/en-us/powershell/scripting/powershell-scripting](https://docs.microsoft.com/en-us/powershell/scripting/powershell-scripting)