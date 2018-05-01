---
layout: post
title: Learning to Read the Fabulous Manual
image: /img/posts/Mao_RTFM_vectorize_by_cmenghi.png
author: jpbruckler
category: help
---

Earlier this week I read an article by [April Wensel](https://twitter.com/aprilwensel) on Medium called [It's time to retire RTFM](https://medium.com/compassionate-coding/its-time-to-retire-rtfm-31acdfef654f). In the article, April talks about the toxicity that 
exists in the technical world as it relates to those that are looking for help, and how to approach these situations from a more 
compassionate place, which ultimately leads to actual understanding. This got me thinking about my own responses to requests for help 
from Those That Know Less, and I probably need to re-evaluate the way I approach some of these situations.

The intent of this post, however, is to share methods for seeking help with PowerShell related issues. As PowerShell has grown in 
popularity, there has been no shortage of websites[^1], blogs[^2] [^3], forums[^4] and subreddits[^5] dedicated to the eddification of the 
PowerShell masses. It can be overwhelming for people just starting out (heck, it can be overwhelming for grizzled veterans, too!), so 
many sources of (often conflicting) information - which one to trust? Sometimes the problem with getting help is not knowing what to 
ask. You know the problem you're having, but you're having a hard time coming up with the secret jargon that will allow Google to 
unlock all the mysteries for you.

## Where do I Even Start?

Maybe you've only dabbled with PowerShell before. Maybe you've used/modified some scripts you found online. Maybe you got elected to 
learn PowerShell for your team, or maybe you just decided it was time to add that skill to your repertoire. However the road started, 
you're now staring at a PowerShell prompt asking yourself "Is there a command to do _____?".

The answer, of course, is probably yes. PowerShell has a ton of built-in commands, and there are thousands of modules that offer additional 
commands and functionality for your PowerShelling pleasure.

{% highlight powershell %}
Get-Help -Noun *Storage* -Online
{% endhighlight %}



***
[^1]: [https://powershell.org](https://powershell.org)
[^2]: [https://blogs.msdn.microsoft.com/powershell/](https://blogs.msdn.microsoft.com/powershell/)
[^3]: [http://www.powershellmagazine.com/](http://www.powershellmagazine.com/)
[^4]: [https://powershell.org/forums/](https://powershell.org/forums/)
[^5]: [https://reddit.com/r/powershell](https://reddit.com/r/powershell)