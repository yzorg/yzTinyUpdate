# yzTinyUpdate
yzorg attempts a tiny updater for Win10 and dotnet

## Background

I work for a small trading company, and a few of my users are still on Windows 7.  So I can't use DesktopBridge or AppX to deploy my app.  I'm still doing it the old fashioned way (download zip, unzip to new folder).  

I'm hoping this blog post from 2011 will help when user pins my app to the taskbar that the taskbar **.lnk** can point to the "shim EXE" instead of to the copy of my app in the "versioned folder".

https://blogs.msdn.microsoft.com/oldnewthing/20110601-00/?p=10523

> ...  
> Even better would be to permit pinning, but set the
> `System.AppUserModel.RelaunchCommand`, `.RelaunchDisplayNameResource` 
> and optionally `.RelaunchIconResource` properties so that if the user tries to pin
> the helper, it actually pins the main application.

## Goals

IIUC, if my WinForm app sets these properties (via COM Interop, or via [Windows API Code Pack](https://www.google.com/search?q=WindowsAPICodePack)) then when users pin the app they use every day to the taskbar I can control what the Taskbar **.lnk** file points to.  It can point to a "shim EXE" at the root of my app folder, and I can freely download new versions, that the shim EXE can dynamically find the "best/latest" version of the app each time it is launched.  No asking the user to wait while new versions are installed.

If I get this working we'd like to keep 1 old major version + 1 old minor version of each app (in case something goes wrong), which is another reason to use "versioned folders".
