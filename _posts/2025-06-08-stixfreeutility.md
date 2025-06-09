---
layout: post
title: "Stix Free Utility"
date: 2025-06-08
permalink: /stixfreeutility/
---
This page is currently being built out; not all content is complete

Stix is a YouTuber and optimizer (over 1yr+). All information regarding the free utility comes as of June 3rd, 2025; information is bound to change as he updates his tools. 
<!--more-->
[Youtube Video Summary](https://www.youtube.com/watch?v=LRijhBlQDG4)

I'll start with benchmarks first because the code review will get fairly lengthly; the link to the utility will be at the bottom, make sure to read my warning next to the link if you choose to visit.

### How does it affect PC performance?
It's important to remember that any sorts of gains or losses will vary from one machine to another, as we all have different components; but on my system (3080ti, 5950x, 32gb ddr4) here are how the utility fared against before and after on a clean install of 23h2 Win11 Pro

Starting with driver latency captured with the Windows Performance Toolkit; 

Onto FPS;

### The Code and What it Does

Here is the utility in its entirety as of version 2.7

#### Option 0:
is required for the utility to work for its maximum potential; the code for 0 is 

<details>
  <summary>Show batch code</summary>
  <pre><code>:resources
curl -g -k -L -# -o "%temp%\Stix Free.zip" "https://www.dropbox.com/scl/fi/qdgw7wcn7oesd3rbfu883/Stix-Free.zip?rlkey=6ed88ulyityakfpyv7f0que9d&st=6eeunx33&dl=1" &gt;nul 2&gt;&amp;1
powershell -NoProfile Expand-Archive '%temp%\Stix Free.zip' -DestinationPath 'C:\' &gt;nul 2&gt;&amp;1
</code></pre>
</details>


and the result is the downloading of this file which allows other options to use these programs and resources later on.
### pic here

#### Option 1

<details>
  <summary>Show batch code</summary>
  
  ```nohighlight
echo - Optimizing Boot Config
bcdedit /deletevalue useplatformclock >nul 2>&1
bcdedit /set disabledynamictick yes >nul 2>&1
bcdedit /set useplatformtick yes >nul 2>&1
timeout 2 >nul 2>&1
echo - Disabling ThreadDPC
reg add "HKLM\SYSTEM\CurrentControlSet\Control\Session Manager\kernel" /v "ThreadDpcEnable" /t REG_DWORD /d "0" /f >nul 2>&1
timeout 2 >nul 2>&1
echo - Disabling Fault Tolerant Heap
reg add "HKEY_LOCAL_MACHINE\Software\Microsoft\FTH" /v Enabled /t REG_DWORD /d 0 /f >nul 2>&1
timeout 2 >nul 2>&1
echo - Setting CSRSS IO and CPU Priority
reg add "HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\csrss.exe\PerfOptions" /v "CpuPriorityClass" /t REG_DWORD /d "3" /f >nul 2>&1
reg add "HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\csrss.exe\PerfOptions" /v "IoPriority" /t REG_DWORD /d "3" /f >nul 2>&1
timeout 2 >nul 2>&1
echo - Setting System Responsiveness
reg add "HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Multimedia\SystemProfile" /v "SystemResponsiveness" /t REG_DWORD /d "0" /f >nul 2>&1
timeout 2 >nul 2>&1
echo - Disabling IoLatencyCap
FOR /F "eol=E" %%a in ('REG QUERY "HKLM\SYSTEM\CurrentControlSet\Services" /S /F "IoLatencyCap"^| FINDSTR /V "IoLatencyCap"') DO (
	REG ADD "%%a" /F /V "IoLatencyCap" /T REG_DWORD /d 0 >nul 2>&1

	FOR /F "tokens=*" %%z IN ("%%a") DO (
		SET STR=%%z
		SET STR=!STR:HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\services\=!
		SET STR=!STR:\Parameters=!
	)
)
timeout 2 >nul 2>&1
echo - Enabling Game Mode
reg add "HKCU\SOFTWARE\Microsoft\GameBar" /v "AllowAutoGameMode" /t REG_DWORD /d "1" /f >nul 2>&1
reg add "HKCU\SOFTWARE\Microsoft\GameBar" /v "AutoGameModeEnabled" /t REG_DWORD /d "1" /f >nul 2>&1
timeout 2 >nul 2>&1
echo - Disabling StorPort Idle
for /f "tokens=*" %%s in ('reg query "HKLM\System\CurrentControlSet\Enum" /S /F "StorPort" ^| findstr /e "StorPort"') do reg add "%%s" /v "EnableIdlePowerManagement" /t REG_DWORD /d "0" /f >nul 2>&1
timeout 2 >nul 2>&1
echo - Enabling HAGS
reg add "HKLM\SYSTEM\CurrentControlSet\Control\GraphicsDrivers" /v "HwSchMode" /t REG_DWORD /d 2 /f >nul 2>&1
timeout 2 >nul 2>&1
echo - Disabling Windows Tracking
reg add "HKLM\SOFTWARE\Policies\Microsoft\Windows\System" /v "EnableActivityFeed" /t REG_DWORD /d 0 /f >nul 2>&1
reg add "HKLM\SOFTWARE\Policies\Microsoft\Windows\System" /v "PublishUserActivities" /t REG_DWORD /d 0 /f >nul 2>&1
reg add "HKLM\SOFTWARE\Policies\Microsoft\Windows\System" /v "UploadUserActivities" /t REG_DWORD /d 0 /f >nul 2>&1
reg add "HKLM\SYSTEM\Maps" /v "AutoUpdateEnabled" /t REG_DWORD /d 0 /f >nul 2>&1
reg add "HKCU\Software\Policies\Microsoft\Windows\WindowsCopilot" /v TurnOffWindowsCopilot /t REG_DWORD /d 1 /f >nul 2>&1
reg add "HKCU\Software\Policies\Microsoft\Windows\Explorer" /v "DisableNotificationCenter" /t REG_DWORD /d 1 /f >nul 2>&1
reg add "HKCU\Software\Microsoft\Windows\CurrentVersion\Themes\Personalize" /v "EnableTransparency" /t REG_DWORD /d 0 /f >nul 2>&1
reg add "HKLM\SOFTWARE\Policies\Microsoft\Windows\System" /v "EnableActivityFeed" /t REG_DWORD /d 0 /f >nul 2>&1
reg add "HKLM\SOFTWARE\Policies\Microsoft\Windows\LocationAndSensors" /v "DisableWindowsLocationProvider" /t REG_DWORD /d 1 /f >nul 2>&1
reg add "HKLM\SOFTWARE\Policies\Microsoft\Windows\LocationAndSensors" /v "DisableLocationScripting" /t REG_DWORD /d 1 /f >nul 2>&1
reg add "HKLM\SOFTWARE\Policies\Microsoft\Windows\LocationAndSensors" /v "DisableLocation" /t REG_DWORD /d 1 /f >nul 2>&1
reg add "HKLM\SOFTWARE\Microsoft\Input\TIPC" /v "Enabled" /t REG_DWORD /d 0 /f >nul 2>&1
reg add "HKLM\SOFTWARE\Policies\Microsoft\Biometrics" /v "Enabled" /t REG_DWORD /d 0 /f >nul 2>&1
timeout 2 >nul 2>&1
echo - Optimizing System Profile
reg add "HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Multimedia\SystemProfile" /v "SchedulerPeriod" /t REG_DWORD /d 1 /f >nul 2>&1
reg add "HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Multimedia\SystemProfile" /v "NoLazyMode" /t REG_DWORD /d 1 /f >nul 2>&1
reg add "HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Multimedia\SystemProfile" /v "MaxThreadsTotal" /t REG_DWORD /d 128 /f >nul 2>&1
reg add "HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Multimedia\SystemProfile" /v "MaxThreadsPerProcess" /t REG_DWORD /d 10 /f >nul 2>&1
reg add "HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Multimedia\SystemProfile" /v "LazyModeTimeout" /t REG_DWORD /d 0 /f >nul 2>&1
reg add "HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Multimedia\SystemProfile" /v "IdleDetectionCycles" /t REG_DWORD /d 0 /f >nul 2>&1
timeout 2 >nul 2>&1
echo - Disabling VBS
reg add "HKLM\SYSTEM\CurrentControlSet\Control\DeviceGuard" /v "EnableVirtualizationBasedSecurity" /t REG_DWORD /d 0 /f >nul 2>&1
timeout 2 >nul 2>&1
echo - Disabling Power Throttling & Hibernation
reg add "HKLM\SYSTEM\CurrentControlSet\Control\Power\PowerThrottling" /v "PowerThrottlingOff" /t REG_DWORD /d 1 /f >nul 2>&1
powercfg -h off
reg add "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\Power" /v "HiberBootEnabled" /t REG_DWORD /d 0 /f >nul 2>&1
reg add "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Power" /v "HibernateEnabled" /t REG_DWORD /d 0 /f >nul 2>&1
timeout 2 >nul 2>&1
echo - Disabling Storage Sense
reg add "HKEY_CURRENT_USER\SOFTWARE\Microsoft\Windows\CurrentVersion\StorageSense\Parameters\StoragePolicy" /v "01" /t REG_DWORD /d 0 /f >nul 2>&1
timeout 2 >nul 2>&1
echo - Disabling Sleep Study
reg add "HKLM\SYSTEM\CurrentControlSet\Control\Power" /v "SleepstudyAccountingEnabled" /t REG_DWORD /d "0" /f >nul 2>&1
reg add "HKLM\SYSTEM\CurrentControlSet\Control\Session Manager\Power" /v "SleepStudyDisabled" /t REG_DWORD /d "1" /f >nul 2>&1
reg add "HKLM\SYSTEM\CurrentControlSet\Control\Session Manager\Power" /v "SleepStudyDeviceAccountingLevel" /t REG_DWORD /d "0" /f >nul 2>&1
timeout 2 >nul 2>&1
echo - Disabling Energy Logging
reg add "HKLM\SYSTEM\CurrentControlSet\Control\Power\EnergyEstimation\TaggedEnergy" /v "DisableTaggedEnergyLogging" /t REG_DWORD /d "1" /f >nul 2>&1
reg add "HKLM\SYSTEM\CurrentControlSet\Control\Power\EnergyEstimation\TaggedEnergy" /v "TelemetryMaxApplication" /t REG_DWORD /d "0" /f >nul 2>&1
reg add "HKLM\SYSTEM\CurrentControlSet\Control\Power\EnergyEstimation\TaggedEnergy" /v "TelemetryMaxTagPerApplication" /t REG_DWORD /d "0" /f >nul 2>&1
timeout 2 >nul 2>&1
echo - Disabling MMCSS
reg add "HKLM\SYSTEM\CurrentControlSet\Services\MMCSS" /v "Start" /t REG_DWORD /d "4" /f >nul 2>&1
timeout 2 >nul 2>&1
echo - Setting Win32 Priority Seperation Value
reg add "HKLM\SYSTEM\CurrentControlSet\Control\PriorityControl" /v "Win32PrioritySeparation" /t REG_DWORD /d 42 /f >nul 2>&1
timeout 2 >nul 2>&1
echo - Disabling DMA Remapping
for %%a in (DmaRemappingCompatible) do for /f "delims=" %%b in ('reg query "HKLM\SYSTEM\CurrentControlSet\Services" /s /f "%%a" ^| findstr "HKEY"') do Reg.exe add "%%b" /v "%%a" /t REG_DWORD /d "0" /f >nul 2>&1
timeout 2 >nul 2>&1
echo - Disabling Windows Updates
"C:\Stix Free\Wub.exe"
```
</details>

### Where can you try the utility?
At the time of this article's creation, I have full faith in the legitimacy and product safety of Stix and his free utility. But with anyone, I must urge you to do your own research to ensure the current state of safety for your own system. To try this software for yourself, you can find it within his [discord server](https://discord.gg/UXjTVqJHB3) found under the channel #free-tweaks.

##### End of Article, feel free to reach out to me if you notice any errors or typos and I will gladly adjust. <3 Khorvie
