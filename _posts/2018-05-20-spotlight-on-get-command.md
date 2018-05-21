---
layout: post
title: Spotlight on Get-Member
date: 2018-05-20 10:47:21.000000000 -05:00
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

_If you're coming to this with a background in OOP, or understand Objects in code, be aware that
this post simplifies those concepts in order to appeal to the widest group of people, sometimes
nuance is going to be lost._

`Get-Member` is an incredibly useful command, but can be confusing to people that are coming to
PowerShell from a different scripting language. In most other scripting languages, you generally
are dealing with data as strings or numbers (depending on the language you're coming from, there
may also be other data types, like arrays, or tuples, but generally speaking, the members in those
data collections are all strings or numbers).

In PowerShell, strings are really .NET Framework objects, `[System.String]`. Objects have properties,
and methods. For the uninitiated, it's easiest to think of properties like an adjective or noun, and
methods as a verb. Since this post is about `Get-Member`, and not about introducing Object Oriented
Programming, that's about as deep as I'll go into what an object is.

If you want to learn more about Object Oriented Programming, you can start with this short video on
YouTube.

* [Object Oriented Programming in 7 minutes](https://www.youtube.com/watch?v=pTB0EiLXUC8)

## Objects in PowerShell

PowerShell is object oriented. Everything is an object. The output you get from `Get-Service` looks
like a bunch of strings in your console window, but if you were to save the output into a variable,
you'd see that `Get-Service` actually outputs `System.ServiceProcess.ServiceController` objects.

{% highlight powershell linenos %}
PS C:\> $Services = Get-Service
PS C:\> $Services | Select-Object -First 1 | Get-Member
   TypeName: System.ServiceProcess.ServiceController

Name                      MemberType    Definition
----                      ----------    ----------
Name                      AliasProperty Name = ServiceName
RequiredServices          AliasProperty RequiredServices = ServicesDependedOn
Disposed                  Event         System.EventHandler Disposed(System.Object, System.EventArgs)
Close                     Method        void Close()
Continue                  Method        void Continue()
CreateObjRef              Method        System.Runtime.Remoting.ObjRef CreateObjRef(type requestedType)
Dispose                   Method        void Dispose(), void IDisposable.Dispose()
Equals                    Method        bool Equals(System.Object obj)
ExecuteCommand            Method        void ExecuteCommand(int command)
GetHashCode               Method        int GetHashCode()
GetLifetimeService        Method        System.Object GetLifetimeService()
GetType                   Method        type GetType()
InitializeLifetimeService Method        System.Object InitializeLifetimeService()
Pause                     Method        void Pause()
Refresh                   Method        void Refresh()
Start                     Method        void Start(), void Start(string[] args)
Stop                      Method        void Stop()
WaitForStatus             Method        void WaitForStatus(System.ServiceProcess.ServiceControllerStatus desiredStatus), void WaitForStatus(System.ServiceProcess.ServiceControllerStatus desiredStatus, timespan timeout)
CanPauseAndContinue       Property      bool CanPauseAndContinue {get;}
CanShutdown               Property      bool CanShutdown {get;}
CanStop                   Property      bool CanStop {get;}
Container                 Property      System.ComponentModel.IContainer Container {get;}
DependentServices         Property      System.ServiceProcess.ServiceController[] DependentServices {get;}
DisplayName               Property      string DisplayName {get;set;}
MachineName               Property      string MachineName {get;set;}
ServiceHandle             Property      System.Runtime.InteropServices.SafeHandle ServiceHandle {get;}
ServiceName               Property      string ServiceName {get;set;}
ServicesDependedOn        Property      System.ServiceProcess.ServiceController[] ServicesDependedOn {get;}
ServiceType               Property      System.ServiceProcess.ServiceType ServiceType {get;}
Site                      Property      System.ComponentModel.ISite Site {get;set;}
StartType                 Property      System.ServiceProcess.ServiceStartMode StartType {get;}
Status                    Property      System.ServiceProcess.ServiceControllerStatus Status {get;}
ToString                  ScriptMethod  System.Object ToString();
{% endhighlight %}

Walking through the example code above, in line 1, I save the output of `Get-Service` into the
`$Services` variable.

On line 2, I use `Select-Object` to only select the first service in the `$Services` variable,
then I use `Get-Member` to show what type of object we're working with (`System.ServiceProcess.ServiceController`)
as well as the properties and methods available with that object.

Ok, so now what? We used `Get-Member`. I'm whelmed.

`Get-Member` gives you a peak under the covers into objects, letting you interact with them in ways
that are different or impossible with the built-in cmdlets. As an example, you can start and stop a
service using the methods of the `System.ServiceProcess.ServiceController`.

{% highlight powershell linenos %}
PS C:\> Get-Process wuauserv

Status   Name               DisplayName
------   ----               -----------
Stopped  wuauserv           Windows Update

# Get the service and store a System.ServiceProcess.ServiceController
# object in the $Service variable
PS C:\> $Service = Get-Service wuauserv

# Use the Status property of the object to see if the service is running
# or stopped
PS C:\> $Service.Status
Stopped

# Start the service using the Start method
PS C:\> $Service.Start()

# Print the status of the service again. When using the Start() method,
# the object isn't automatically refreshed to reflect the running
# status.
PS C:\> $Service.Status
Stopped

# Use the Refresh method to refresh the object
PS C:\> $Service.Refresh()

# Print the status of the service again. This time the status shows that
# the service is running.
PS C:\> $Service.Status
Running
{% endhighlight %}