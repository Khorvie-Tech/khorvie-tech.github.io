---
layout: post
title: "How to Import Power Plans"
date: 2025-06-04
permalink: /importpow/
---
*article in progress: not complete yet*
### The process to import a power plan is a simple one, 

1: open command prompt as an administrator

2: ensure that your pow file isn't <!--more--> inside of a zipped folder, if it is in a zipped file, right click on the zip file and extract (a common issue i see is people downloading a .pow file and it comes in a zip file and they forget to extract it which causes the import process to fail)

3: click on your pow file to highlight it in your file explorer and then perform this keyboard shortcut on your device Ctrl Shift C and this will copy the file location of the .pow file

4: move onto the command prompt you opened at the start and type in this command to finish the import process
powercfg -import and then paste the contents of the file location and hit enter

A full example would look something like this
**powercfg -import "C:\Path\To\Plan.pow"**

5. if done correctly; close out of command prompt and hit the keyboard shortcut Windows Key and R, then type in powercfg.cpl to open up the panel to select your new power plan (make sure this panel isn't opened while importing otherwise it won't appear until you relaunch the panel anyways)
   
If following this process perfectly says it is successful in command prompt, but the plan doesn't appear in the list to choose from power plans you can try to disable something called modern standby by searching in your search bar for the registry editor and then making your way to this file path 

HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Power
"PlatformAoAcOverride"=dword:00000000

after setting this value to 0, restart your machine and check again for your power plan

Brief rundown on modern standby: modern standby is a 'low power idle mode' typically used in laptops/tablets. It replaces the older S3 sleep state with an "always on, always connected" behavior, similar to how a smartphone can sleep but stays connected

When you disable modern standby... S3 sleep becomes available, which will affect the features you once had from modern standby like fast resume and potenially sleep funcitonality will be altered too, either taking longer to wake up without modern standby, or not being able to sleep at all

The reason why disabling modern standby can fix hidden power plans is because modern standby assumes the system will manage power automatically, so it hides most advanced power options which includes some power plans. disabling gives full control back to you, the user.


if after all of this if it still doesn't appear, ensure there are no errors in the way you are importing your plan, as these methods should work for anyone in importing a power plan.


(optional/advnaced) To give a custom GUID to the plan the command would be something like this
**powercfg -import "C:\Path\To\Path.pow" {f0e1d2c3-b4a5-6789-0abc-def123456789}**

a proper guid formatting is used with ONLY HEX characters; which includes numbers 0 to 9 and letters a to f, and it follows a character count structure of 8-4-4-4-12; so your final length should match that count. Proper examples can look like anything 0-9 and a-f as long as you follow these formatting rules.

For the general population, you wouldn't have any need making a custom guid; but if you are an optimizer who loves automation, you can write a script to import a powerplan with a custom/predefined guid and then apply it with scripting too instead of opening the power plan control panel and having the user apply it manually.

Additionally you can also change the name of a plan while importing if you use this formatting
powercfg -import "C:\Path\To\Plan.pow" {your-guid-here} "Your Plan Name"

for it to work properly you need to specify the guid otherwise the Name parameter gets ignored

End of Article, feel free to reach out to me if you notice any errors or typos and I will gladly adjust. 
<3 Khorvie
