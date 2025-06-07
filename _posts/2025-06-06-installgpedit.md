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

- Right click on the desktop and create a txt file
- Copy and paste this install code into the txt file from *"@echo"* all the way to *"pause"*

```
@echo off

dir /b "%SystemRoot%\servicing\Packages\Microsoft-Windows-GroupPolicy-ClientExtensions-Package~*.mum" >List.txt
dir /b "%SystemRoot%\servicing\Packages\Microsoft-Windows-GroupPolicy-ClientTools-Package~*.mum" >>List.txt

for /f %%i in ('findstr /i . List.txt 2^>nul') do (
    dism /online /norestart /add-package:"%SystemRoot%\servicing\Packages\%%i"
)
del List.txt
pause
```

- Hit the keyboard shortcut Ctrl S to save the txt
- Close out and rename the .txt to a .bat
- Run the batch file as admin and let it proceed with the install
- Reboot machine

### What the code does

***@echo off***
- Turns off command echoing so that commands themselves are not printed to the command prompt, making output cleaner and easier to read.

***dir /b "%SystemRoot%\servicing\Packages\Microsoft-Windows-GroupPolicy-ClientExtensions-Package~*.mum" >List.txt***
- Searches the Windows servicing packages directory for all files that match
Microsoft-Windows-GroupPolicy-ClientExtensions-Package~*.mum
and outputs just the filenames to a file called List.txt.
These files are needed to enable the Group Policy Client Extensions feature.

***dir /b "%SystemRoot%\servicing\Packages\Microsoft-Windows-GroupPolicy-ClientTools-Package~*.mum" >>List.txt***
- Searches the same directory for all files matching
Microsoft-Windows-GroupPolicy-ClientTools-Package~*.mum
and appends the filenames to List.txt.
These files are needed to enable the Group Policy Client Tools feature.

***for /f %%i in ('findstr /i . List.txt 2^>nul') do (
    dism /online /norestart /add-package:"%SystemRoot%\servicing\Packages\%%i"
)***
- Reads each line (filename) from List.txt using findstr (which simply outputs all lines). For each filename, runs the dism command to install the corresponding Windows package:

- /online means it applies to the currently running Windows installation.

- /norestart prevents automatic reboot after installing the package.

- /add-package:"..." specifies the full path to the package file to be installed.

- This loop enables all the necessary Group Policy components on your system.

***del List.txt***
- Deletes the temporary List.txt file to clean up after the script is done.

***pause***
- Pauses the script and displays "Press any key to continue . . ." This gives you a chance to review any messages or errors before the window closes.

##### End of Article, as always if you see typos or errors reach out to me and let me know <3 Khorvie

