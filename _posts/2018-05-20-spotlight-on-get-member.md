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

`Get-Member` is used to get the methods and properties of an object. Which is handy, since everything
in PowerShell is an object. This is probably the cmdlet I use most when developing scripts or trying
to wrangle some information out of a command or system in an interactive session.

If you don't know what a property, method, or object is, they are the building blocks of Object-Oriented
Programming, known as OOP. At a very basic level, you can think of an object as a structure that contains
information (properties), and can do things (methods).

This is probably best explained with an example. Let's use WMI to interact with a process. Start Notepad
on your computer. In your PowerShell session, use `Get-WmiObject` to get an object representing the
Notepad process.

## Peeping at Properties

```powershell
PS C:\> $notepad = Get-WmiObject -Class Win32_Process -Filter "name='notepad.exe'"
```

`Get-Member` can now be used to return information about the notepad process. These pieces of information
are stored in the object's properties.

```powershell
C:\Users\jpbru> $notepad | Get-Member -MemberType Properties


   TypeName: System.Management.ManagementObject#root\cimv2\Win32_Process

Name                       MemberType     Definition
----                       ----------     ----------
Handles                    AliasProperty  Handles = Handlecount
ProcessName                AliasProperty  ProcessName = Name
PSComputerName             AliasProperty  PSComputerName = __SERVER
VM                         AliasProperty  VM = VirtualSize
WS                         AliasProperty  WS = WorkingSetSize
Caption                    Property       string Caption {get;set;}
CommandLine                Property       string CommandLine {get;set;}
CreationClassName          Property       string CreationClassName {get;set;}
CreationDate               Property       string CreationDate {get;set;}
CSCreationClassName        Property       string CSCreationClassName {get;set;}
CSName                     Property       string CSName {get;set;}
Description                Property       string Description {get;set;}
ExecutablePath             Property       string ExecutablePath {get;set;}
ExecutionState             Property       uint16 ExecutionState {get;set;}
Handle                     Property       string Handle {get;set;}
HandleCount                Property       uint32 HandleCount {get;set;}
InstallDate                Property       string InstallDate {get;set;}
KernelModeTime             Property       uint64 KernelModeTime {get;set;}
MaximumWorkingSetSize      Property       uint32 MaximumWorkingSetSize {get;set;}
MinimumWorkingSetSize      Property       uint32 MinimumWorkingSetSize {get;set;}
Name                       Property       string Name {get;set;}
OSCreationClassName        Property       string OSCreationClassName {get;set;}
OSName                     Property       string OSName {get;set;}
OtherOperationCount        Property       uint64 OtherOperationCount {get;set;}
OtherTransferCount         Property       uint64 OtherTransferCount {get;set;}
PageFaults                 Property       uint32 PageFaults {get;set;}
PageFileUsage              Property       uint32 PageFileUsage {get;set;}
ParentProcessId            Property       uint32 ParentProcessId {get;set;}
PeakPageFileUsage          Property       uint32 PeakPageFileUsage {get;set;}
PeakVirtualSize            Property       uint64 PeakVirtualSize {get;set;}
PeakWorkingSetSize         Property       uint32 PeakWorkingSetSize {get;set;}
Priority                   Property       uint32 Priority {get;set;}
PrivatePageCount           Property       uint64 PrivatePageCount {get;set;}
ProcessId                  Property       uint32 ProcessId {get;set;}
QuotaNonPagedPoolUsage     Property       uint32 QuotaNonPagedPoolUsage {get;set;}
QuotaPagedPoolUsage        Property       uint32 QuotaPagedPoolUsage {get;set;}
QuotaPeakNonPagedPoolUsage Property       uint32 QuotaPeakNonPagedPoolUsage {get;set;}
QuotaPeakPagedPoolUsage    Property       uint32 QuotaPeakPagedPoolUsage {get;set;}
ReadOperationCount         Property       uint64 ReadOperationCount {get;set;}
ReadTransferCount          Property       uint64 ReadTransferCount {get;set;}
SessionId                  Property       uint32 SessionId {get;set;}
Status                     Property       string Status {get;set;}
TerminationDate            Property       string TerminationDate {get;set;}
ThreadCount                Property       uint32 ThreadCount {get;set;}
UserModeTime               Property       uint64 UserModeTime {get;set;}
VirtualSize                Property       uint64 VirtualSize {get;set;}
WindowsVersion             Property       string WindowsVersion {get;set;}
WorkingSetSize             Property       uint64 WorkingSetSize {get;set;}
WriteOperationCount        Property       uint64 WriteOperationCount {get;set;}
WriteTransferCount         Property       uint64 WriteTransferCount {get;set;}
__CLASS                    Property       string __CLASS {get;set;}
__DERIVATION               Property       string[] __DERIVATION {get;set;}
__DYNASTY                  Property       string __DYNASTY {get;set;}
__GENUS                    Property       int __GENUS {get;set;}
__NAMESPACE                Property       string __NAMESPACE {get;set;}
__PATH                     Property       string __PATH {get;set;}
__PROPERTY_COUNT           Property       int __PROPERTY_COUNT {get;set;}
__RELPATH                  Property       string __RELPATH {get;set;}
__SERVER                   Property       string __SERVER {get;set;}
__SUPERCLASS               Property       string __SUPERCLASS {get;set;}
Path                       ScriptProperty System.Object Path {get=$this.ExecutablePath;}
```

That's a pretty long list of properties, but it illustrates the kind of power `Get-Member` gives
you. These properties can all be used as a filter when performing other WMI lookups using the
Win32_Process class. For instance, let's get a list of all the processes running on a computer with
a ThreadCount greater than 25, and only display the ProcessID, Name, ThreadCount and ExecutablePath:

```powershell
PS C:\> Get-WmiObject -Class Win32_Process -Filter 'ThreadCount > 25' | Select-Object ProcessID, Name, ThreadCount, ExecutablePath

ProcessID Name                      ThreadCount ExecutablePath
--------- ----                      ----------- --------------
        4 System                            247
      960 svchost.exe                        27
     2028 Memory Compression                146
     3464 nvcontainer.exe                    29
     3592 MsMpEng.exe                        50
     6056 Razer Synapse Service.exe          30
     8680 SearchIndexer.exe                  41
    12356 nvcontainer.exe                    26
    10708 explorer.exe                       48
    11544 NVIDIA Web Helper.exe              90
     9064 Microsoft.Notes.exe                32
    12660 ShellExperienceHost.exe            34
    13036 SearchUI.exe                       39
     9092 SkypeHost.exe                      33
    12492 chrome.exe                         32
     9984 chrome.exe                         27
     9140 SnagitEditor.exe                   74
     8872 Razer Central.exe                  37
     9072 PeopleApp.exe                      29
    15180 Dropbox.exe                       120
    17680 nvcontainer.exe                    27 C:\Program Files (x86)\NVIDIA Corporation\NvContainer\nvcontainer.exe
     8888 explorer.exe                       53 C:\WINDOWS\Explorer.EXE
    18712 NVIDIA Web Helper.exe              91 C:\Program Files (x86)\NVIDIA Corporation\NvNode\NVIDIA Web Helper.exe
    18148 ShellExperienceHost.exe            30 C:\Windows\SystemApps\ShellExperienceHost_cw5n1h2txyewy\ShellExperienceHost.exe
```
## Messing with Methods

`Get-Member` can be used to find out what actions (methods) an object can perform. Use the
`-MemberType` argument to return only the Methods for this object.

```powershell
PS C:\> $notepad | Get-Member -MemberType Method


   TypeName: System.Management.ManagementObject#root\cimv2\Win32_Process

Name                    MemberType Definition
----                    ---------- ----------
AttachDebugger          Method     System.Management.ManagementBaseObject AttachDebugger()
GetAvailableVirtualSize Method     System.Management.ManagementBaseObject GetAvailableVirtualSize()
GetOwner                Method     System.Management.ManagementBaseObject GetOwner()
GetOwnerSid             Method     System.Management.ManagementBaseObject GetOwnerSid()
SetPriority             Method     System.Management.ManagementBaseObject SetPriority(System.Int32 Priority)
Terminate               Method     System.Management.ManagementBaseObject Terminate(System.UInt32 Reason)
```

The most useful method at this point is the `Terminate` method. Using PowerShell, once we get a handle
on a process, it can be terminated using this method. Running the command below will close the Notepad
process.

```powershell
PS C:\> $notepad.Terminate()
```

Note, when calling methods, you use parentheses to cause a method to perform the action it was designed
to do. If you call a method without the parentheses, PowerShell outputs information on the arguments a
method can take. For example, calling `$notepad.terminate` shows that a reason can be provided as an
argument to Terminate, and that the reason must be a 32-bit integer.

```powershell
PS C:\> $notepad.Terminate

OverloadDefinitions
-------------------
System.Management.ManagementBaseObject Terminate(System.UInt32 Reason)
```

WMI objects are a little funny in that, in order to see static methods for an object, you need to use the
`[wmiclass]` type accelerator.

*__Note:__ It's not necessary to understand [type accelerators] for the purpose of using `Get-Member`. I'm
using it here to help illustrate the concepts of discovering and using object information.*

```powershell
PS C:\> [wmiclass] 'Win32_Process' | Get-Member -MemberType Method

 TypeName: System.Management.ManagementClass#ROOT\cimv2\Win32_Process

Name   MemberType Definition
----   ---------- ----------
Create Method     System.Management.ManagementBaseObject Create(System.String CommandLine, System.String CurrentDirectory, System.Management.ManagementObject#Win32_ProcessStartup ProcessStartupInformation)
```

So based on this, it looks like `Win32_Process` can be used to create (launch) a process. So let's use
the `Create()` method to create a Notepad process, since we terminated the first one. The output from
`Get-Member` shows that the `Create()` method can take several arguments:
1. CommandLine
1. CurrentDirectory
1. ProcessStartupInformation

The only arguments we need to worry about are `CommandLine` and `CurrentDirectory`. You can find the
documentation for the `Win32_Process Create()` method [here] on MSDN. The documentation defines the
CommandLine and CurrentDirectory argument as follows:

1. CommandLine [in]
: {: .meta} Command line to execute. The system adds a null character to the command line, trimming
the string if necessary, to indicate which file was actually used.

1. CurrentDirectory [in]
: {: .meta} Current drive and directory for the child process. The string requires that the current
directory resolves to a known path. A user can specify an absolute path or a path relative to the
current working directory. If this parameter is NULL, the new process will have the same path as the
calling process. This option is provided primarily for shells that must start an application and specify
the application's initial drive and working directory.

So to launch a new notepad process, you would do the following:

```powershell
PS C:\> $CommandLine = 'notepad.exe'
PS C:\> $CurrentDirectory = (Join-Path $env:WINDIR 'System32')
PS C:\> $NPProcess = Invoke-WmiMethod -Class Win32_Process -Name Create -ArgumentList $CommandLine, $CurrentDirectory
```

# Finally

Hopefully the spin we took with `Get-Member` helps demonstrate it's power and usefullness. If I had to
pick a _favorite_ PowerShell, it would be `Get-Member`. No other command has the ability to impact the
way you interact with PowerShell more than this one. It's invaluable for discovering information about
all the information you're getting with `Get-*` commands.

Here's some ideas to get you started playing with `Get-Member`. Leave a comment if you have some tips or
questions.

```powershell
PS C:\> Get-Service Appinfo | Get-Member
PS C:\> Get-CimInstance Win32_ComputerSystem | Get-Member
```

[type accelerators]:https://blogs.technet.microsoft.com/heyscriptingguy/2013/07/08/use-powershell-to-find-powershell-type-accelerators/
[here]:https://msdn.microsoft.com/en-us/library/aa389388(v=vs.85).aspx