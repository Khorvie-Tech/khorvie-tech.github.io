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

```nohighlight
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

| **Command**                                      | **Explanation**                                       |
|--------------------------------------------------|--------------------------------------------------------|
| @echo off                                        | Cleaner output (no command echoing)                   |
| dir ...ClientExtensions... >List.txt             | List all Client Extensions package files              |
| dir ...ClientTools... >>List.txt                 | Append all Client Tools package files                 |
| for /f ... do (dism ...)                         | Install each package listed in List.txt               |
| del List.txt                                     | Remove temporary file                                 |
| pause                                            | Wait for user input before closing                    |


##### End of Article, as always if you see typos or errors reach out to me and let me know <3 Khorvie

