---
layout: post
title: Learning to Read the (PowerShell) Fabulous Manual
image: /img/posts/2018-05-01/Mao_RTFM_vectorize_by_cmenghi.png
author: jpbruckler
categories: 
- Help
tags:
- Help
- Getting started
- PowerShell
- rtpm
---

_This is the first in series of posts about learning to explore and help yourself with PowerShell. As more installments are added
they will be linked here._

1. [Getting the most out of Get-Help]

Matt and I have nearly 20 years of using PowerShell under our belts at this point, and have had the pleasure of helping drive the adoption
of the language where we work, and helping out people new to PowerShell in getting started. My mantra with new people is
generally summed up with:

> To become proficient in PowerShell, you only need to know 4* commands.
> * Get-Help
> * Get-Command
> * Get-Member
> * Show-Command

__*__ _This used to only be 3 commands, but `Show-Command` has proven to be incredibly useful as a teaching and exploration tool._

![Show-Command][img-show-command]

In subsequent posts, I'll dive into each of those commands in greater detail. This post is largely about learning to get help - a
skill that transcends programming or scripting. No one ever starts learning a new skill and is immediately an expert. Sometimes
you won't know how to ask the question, because you don't have the experience to know what it is that you don't know. Have faith!
It takes a lot of failure and _deliberate practice_ to learn to do anything.

## Where do I Even Start?

![I don't even know][img-dunno]{:height="50%" width="50%" class="center-block"}

Perhaps counterintuitively, if you're just starting out, you might benefit from some reading on how to learn a new skill, and how to
ask questions effectively, so I present to you:

1. [How to ask questions]("http://catb.org/esr/faqs/smart-questions.html")
2. [The Importance of Deep Work & the 30-hour Method for Learning a New Skill]("https://azeria-labs.com/the-importance-of-deep-work-the-30-hour-method-for-learning-a-new-skill/")

## Ok, But Where do I Start with PowerShell?

Basic information you're going to need to get started with PowerShell:

1. All commands follow a `Verb-Noun` naming structure:
![Verb-Noun][img-verb-noun]
2. There's a list of approved verbs. You can find them [online]("https://msdn.microsoft.com/en-us/library/ms714428(v=vs.85).aspx") or with `Get-Verb`
3. There isn't a list of approved nouns ;)
4. The 4 commands mentioned above (`Get-Help`, `Get-Command`, `Get-Member`, `Show-Command`)
5. PowerShell help files aren't installed locally by default, use the `-Online` switch for `Get-Help` when starting out

Armed with that knowledge, the PowerShell ISE (the ISE is a script editor installed by default with PowerShell), and a can-do attitude,
you'll get pretty far.

Some other very useful resources include:

1. [https://powershell.org](https://powershell.org)
1. [https://blogs.msdn.microsoft.com/powershell/](https://blogs.msdn.microsoft.com/powershell/)
1. [http://www.powershellmagazine.com/](http://www.powershellmagazine.com/)
1. [https://powershell.org/forums/](https://powershell.org/forums/)
1. [https://reddit.com/r/powershell](https://reddit.com/r/powershell)
1. [http://ramblingcookiemonster.github.io/](http://ramblingcookiemonster.github.io/)
1. [http://mikefrobbins.com/](http://mikefrobbins.com/)

People to follow on Twitter (if you're not already using twitter, I can't recommend it enough for keeping up with PowerShell developments, and getting help) - a non-exhaustive list:

1. [Jeffrey Snover](https://twitter.com/jsnover)
1. [Lee Holmes](https://twitter.com/Lee_Holmes)
1. [The PowerShell Team](https://twitter.com/PowerShell_Team)
1. [PowerShell Magazine](https://twitter.com/PowerShellMag)
1. [Warren F.](https://twitter.com/psCookieMonster)
1. [Mike F. Robbins](https://twitter.com/mikefrobbins)
1. [PowerShell Tips](https://twitter.com/PowerTip)
1. [Don Jones](https://twitter.com/concentrateddon)

## Finally

Don't be afraid to experiment. Don't be afraid to fail. Don't be afraid to ask questions. There are people out there that
seem to think that we're all born with the innate knowledge to solve our every problem on our own, but that's just not the
case. Try not to get discouraged while you're learning.

[Getting the most out of Get-Help]:{% post_url 2018-05-12-getting-the-most-out-of-get-help %}
[img-show-command]:{{"/img/posts/2018-05-01/show_command.png" | absolute_url }} "'Show-Command -Name Get-Help' output"
[img-dunno]:{{"/img/posts/2018-05-01/dunno.jpg" | absolute_url}}
[img-verb-noun]:{{"/img/posts/2018-05-01/cmdlet-anatomy.png" | absolute_url}}