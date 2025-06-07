---
layout: post
title: "Install Group Policy Editor"
date: 2025-06-06
permalink: /installgpedit/
---
You can install group policy editor to your machine using built in Windows DISM Servicing.
<!--more-->
### Step 1: Show File Extensions

You'll want to start off by making sure you have file extensions shown; you can check this by
- opening your file explorer
- in the header, click view
- in the dropdown, click Show, and from that dropdown select ***File Name Extensions***

### Step 2: The Install

- Create a txt file
- Copy and paste this install code into the txt file from "@echo" all the way to "pause"
  
@echo off

for /f %%i in ('dir /b %SystemRoot%\servicing\Packages\Microsoft-Windows-GroupPolicy-Client*.mum') do (
 dism /online /norestart /add-package:"%SystemRoot%\servicing\Packages\%%i"
)

set shortcut="%USERPROFILE%\Desktop\Group Policy Editor.lnk"
powershell "$s=(New-Object -COM WScript.Shell).CreateShortcut(%shortcut%); $s.TargetPath='gpedit.msc'; $s.Save()"

echo Done! You can now launch gpedit from the desktop shortcut or by searching for it.

pause

- Hit the keyboard shortcut Ctrl S to save the txt
- Close out and rename the .txt to a .bat
- Run the batch file as admin and let it proceed with the install

### What the code does

***@echo off***
- Stops the command window from showing each line as it's run. Which makes the output cleaner and easier to read.

***for /f %%i in ('dir /b %SystemRoot%\servicing\Packages\Microsoft-Windows-GroupPolicy-Client*.mum') do (***
- Finds all the necessary files needed to install Group Policy. dir /b lists just the filenames (bare format). The for loop goes through each of those files one by one.

***(dism /online /norestart /add-package:"%SystemRoot%\servicing\Packages\%%i"***
- This line runs once for each file found. DISM is a Windows tool that installs features or updates. It adds each Group Policy-related package into the system.

***)***
- Ends the 'for' loop from the first line of code.

***set shortcut="%USERPROFILE%\Desktop\Group Policy Editor.lnk"***
- Creates a variable called shortcut. It tells the script where to place the shortcut (on the current user's desktop).

***powershell "$s=(New-Object -COM WScript.Shell).CreateShortcut(%shortcut%); $s.TargetPath='gpedit.msc'; $s.Save()"***
- Uses PowerShell to make the shortcut that opens gpedit.msc.

***echo Done! You can now launch gpedit from the desktop shortcut.***
- Shows a friendly message to the user that it’s finished.

***pause***
- Keeps the window open so the user can read the message. Waits for them to press a key before closing.

*End of Article, as always if you see typos or errors reach out to me and let me know <3 Khorvie*

