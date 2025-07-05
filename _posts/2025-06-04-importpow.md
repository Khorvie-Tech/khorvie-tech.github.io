---
layout: post
title: "How to Import Power Plans"
date: 2025-06-04
permalink: /importpow/
---
Here is an easy four step guide on how to import power plans into your system
<!--more--> 

1: Open command prompt as an administrator.

2: Ensure that your pow file **isn't** inside of a zipped folder, if it is in a zipped file, right click on the zip file and extract (a common issue I see often is people downloading a .pow file and it comes in a zip file and they forget to extract it which causes the import process to fail)

3: Click on your .pow file to highlight it in your file explorer and then perform this keyboard shortcut on your device ***Ctrl Shift C*** and this will copy the file location of the .pow file. Alternatively, you can try to right click the file and see an option for ***Copy As Path***

4: Move into the command prompt you opened at the start and type in this command to finish the import process;

```nohighlight
powercfg -import
```
make sure there is a space after *-import* and then paste the contents of the file location and then hit enter

A full example would look something like this
**powercfg -import "C:\Path\To\Plan.pow"**

If this was done correctly; close out of command prompt and hit the keyboard shortcut Windows Key and R, then type in ***powercfg.cpl*** to open up the panel to select your new power plan (make sure this panel isn't open while importing otherwise it won't appear until you relaunch the panel anyways)
   
### But if the plan doesn't appear in the list to choose from.. 
You can try to disable something called *modern standby* by searching in your search bar for the registry editor and then making your way to this file path 

```nohighlight
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Power
"PlatformAoAcOverride"=dword:00000000
```

After setting this value to 0, restart your machine and check again for your power plan

### Brief rundown on modern standby:
Modern standby is a 'low power idle mode' typically used in laptops/tablets. It replaces the older S3 sleep state to this new modern standby with an *"always on, always connected"* behavior, similar to how a smartphone can sleep but stays connected.

When you disable modern standby... S3 sleep becomes available, which will affect the features you once had from modern standby like fast resume and potenially sleep funcitonality will be altered too, either taking longer to wake up without modern standby, or not being able to sleep at all

The reason why disabling modern standby can fix hidden power plans is because modern standby assumes the system will manage power automatically, so it hides most advanced power options which includes some power plans. disabling gives full control back to you, the user.

If after all of this if it still doesn't appear, ensure there are no errors in the way you are importing your plan, as these methods should work for anyone in importing a power plan.

Also check [Missing Power Plans](https://khorvie.tech/missingpow/) if this does somehow not work.

### (Optional/advanced) Making a Custom GUID
To give a custom GUID to the plan; the import command would be something like this
**powercfg -import "C:\Path\To\Path.pow" {f0e1d2c3-b4a5-6789-0abc-def123456789}**

A proper GUID formatting is used with ***ONLY HEX*** characters; which *includes numbers 0 to 9 and letters a to f*, and it *follows a character count structure of 8-4-4-4-12*; so your final length should match that count. Proper examples can look like anything given you follow these formatting rules.
- {3f2504e0-4f89-11d3-9a0c-0305e82c3301}
- {a4e7b6c2-1d22-4e5d-8f0a-76a71c933faa}
- {d90f99f7-82b4-4b3f-b93a-5d6733d46c2e}
- {11111111-1111-1111-1111-111111111111}
- {aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa}

Ensure when using or making a GUID that you don't copy a GUID currently in use by your system for another powerplan.

You can check this by opening your command prompt and typing the command ***powercfg -list*** then hit enter

### Should you add your own GUID?
For the general population, you ***wouldn't have any need for making a custom GUID***; but if you are an optimizer who loves automation, this would be very helpful in writing a script to import a power plan with a custom/predefined guid and then apply it with scripting too instead of sending the user to the power plan control panel and having them apply it manually.

Additionally you can also change the name of a plan while importing if you use this formatting
powercfg -import "C:\Path\To\Plan.pow" {your-guid-here} "Your Plan Name"

For it to work properly ***you need to specify the guid*** otherwise the Name parameter gets ignored.




##### End of Article, feel free to reach out to me if you notice any errors or typos and I will gladly adjust. <3 Khorvie
