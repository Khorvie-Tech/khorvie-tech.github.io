---
layout: post
title: "Win 32 Priority Separation"
date: 2025-06-04
permalink: /win32priorityseparation/
---
Win32PrioritySeparation is a Windows Registry value that controls how the system prioritizes CPU resources between foreground (active) applications and background services.
<!--more-->

This setting essentially affects how thread scheduling works, especially when the system is under load, by influencing quantum lengths and priority boosts. This can affect frames and responsiveness in video gaming scenarios.

# Casual Breakdown:

It's a registry setting in Windows that controls how your computer splits attention between:
The app you're using right now (foreground); and stuff running in the background (like updates, services)

### Why It Matters?

This setting tells Windows:
How long each app gets to use the CPU before switching, it determines whether your current app gets more love (runs faster/smoother)

### How to change it and recommended Values:

In your search bar type and open up the registry editor.
The value can be located at 
***HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\PriorityControl***
And should be a dword named ***Win32PrioritySeparation***

Through the testing of many optimizers within the community, *recommended values from nearly all good optimizers are* ***1a or 2a***
*(you insert these values as hexadecimal)* But there have been many recorded instances in which other values will work better on some machines; it's important to test these values for yourself and to not blindly trust specific values.

#### Default Value
- for Programs is 26hex/38dec
- for Background Services is 18hex/24dec

### Khorvie Recommendation:
2a is generally more stable for system latency and frames but 1a has the potential on some systems to do this but much better. Try and test 2a for yourself for roughly 30 minutes then do the same with 1a, using capframex for benchmarks would be ideal but if you're unwilling then just go by feel.

| Decimal | Hex  | Binary | Quantum Length | Quantum Type | Foreground Boost | Outcome                                                                 |
| ------- | ---- | ------ | -------------- | ------------ | ---------------- | ----------------------------------------------------------------------- |
| 24      | 0x18 | 011000 | Long           | Fixed        | None             |   **Default for Background Services**; balanced, equal CPU distribution |
| 26      | 0x1A | 011010 | Long           | Fixed        | High             |   Custom; long slices, but boosted active apps                         |
| 38      | 0x26 | 100110 | Short          | Fixed        | High             |   **Default for Programs**; snappy UI, responsive foreground apps       |
| 42      | 0x2A | 101010 | Short          | Fixed        | High             |   Custom; ultra-responsive, aggressive boost to frontmost app          |

### Does it legitimately affect performance
It does but it likely won't be anything super significant, expect results between different values within a 5-10% difference (estimation comes from prior benchmarks from myself, and from me looking at data by FrameSyncLabs, and AlchemyTweaks both of which you can find on youtube)

# The Rock Breakdown:

### Bit Structure:

Win32PrioritySeparation is a REG_DWORD that uses the lowest 6 bits (bits 0–5) to control CPU scheduling behavior. The most important bits are:

- Bits 0–1: Foreground boost level (0 = none, 1 = medium, 2 = high)
- Bit 2: Quantum type (0 = variable, 1 = fixed)
- Bit 3: Quantum length (0 = short, 1 = long)
- Bits 4–5: Reserved/unused by most Windows versions

This means valid values range from 0 to 63 (0x00 to 0x3F in hex), and commonly used values like 0x1A, 0x2A, 0x18, and 0x26 are all valid and meaningful.

### Scheduling Impact:
- Short quantum = faster context switches, more responsive but more overhead
- Long quantum = less switching, better throughput but can make UIs laggy
- Foreground boost = dynamic priority boosts for active app threads
- Variable quantum = adjusts time slice length based on thread priority; foreground apps may get longer quanta, improving responsiveness under load
- Fixed quantum = all threads get equal time slices regardless of priority; more consistent but less responsive to active app needs
  
Windows uses this to modify base scheduling behavior, not override thread priorities.

### Deep Usage Notes:
- Used by kernel scheduler to scale quantum ranges (e.g., 20ms vs 120ms)
- Doesn’t affect real-time classes or explicitly boosted threads
- Greatly influenced by thread priority class (e.g., NORMAL_PRIORITY_CLASS)

| Decimal | Hex  | Binary | Quantum Length | Quantum Type | Foreground Boost | Reserved Bits |
| ------- | ---- | ------ | -------------- | ------------ | ---------------- | ------------- |
| 0       | 0x00 | 000000 | Short          | Variable     | None             | 00            |
| 1       | 0x01 | 000001 | Short          | Variable     | Medium           | 00            |
| 2       | 0x02 | 000010 | Short          | Variable     | High             | 00            |
| 3       | 0x03 | 000011 | Short          | Variable     | Reserved/Unknown | 00            |
| 4       | 0x04 | 000100 | Short          | Variable     | None             | 00            |
| 5       | 0x05 | 000101 | Short          | Variable     | Medium           | 00            |
| 6       | 0x06 | 000110 | Short          | Variable     | High             | 00            |
| 7       | 0x07 | 000111 | Short          | Variable     | Reserved/Unknown | 00            |
| 8       | 0x08 | 001000 | Long           | Variable     | None             | 00            |
| 9       | 0x09 | 001001 | Long           | Variable     | Medium           | 00            |
| 10      | 0x0A | 001010 | Long           | Variable     | High             | 00            |
| 11      | 0x0B | 001011 | Long           | Variable     | Reserved/Unknown | 00            |
| 12      | 0x0C | 001100 | Long           | Fixed        | None             | 00            |
| 13      | 0x0D | 001101 | Long           | Fixed        | Medium           | 00            |
| 14      | 0x0E | 001110 | Long           | Fixed        | High             | 00            |
| 15      | 0x0F | 001111 | Long           | Fixed        | Reserved/Unknown | 00            |
| 16      | 0x10 | 010000 | Short          | Variable     | None             | 01            |
| 17      | 0x11 | 010001 | Short          | Variable     | Medium           | 01            |
| 18      | 0x12 | 010010 | Short          | Variable     | High             | 01            |
| 19      | 0x13 | 010011 | Short          | Variable     | Reserved/Unknown | 01            |
| 20      | 0x14 | 010100 | Short          | Variable     | None             | 01            |
| 21      | 0x15 | 010101 | Short          | Variable     | Medium           | 01            |
| 22      | 0x16 | 010110 | Short          | Variable     | High             | 01            |
| 23      | 0x17 | 010111 | Short          | Variable     | Reserved/Unknown | 01            |
| 24      | 0x18 | 011000 | Long           | Variable     | None             | 01            |
| 25      | 0x19 | 011001 | Long           | Variable     | Medium           | 01            |
| 26      | 0x1A | 011010 | Long           | Variable     | High             | 01            |
| 27      | 0x1B | 011011 | Long           | Variable     | Reserved/Unknown | 01            |
| 28      | 0x1C | 011100 | Long           | Fixed        | None             | 01            |
| 29      | 0x1D | 011101 | Long           | Fixed        | Medium           | 01            |
| 30      | 0x1E | 011110 | Long           | Fixed        | High             | 01            |
| 31      | 0x1F | 011111 | Long           | Fixed        | Reserved/Unknown | 01            |
| 32      | 0x20 | 100000 | Short          | Variable     | None             | 10            |
| 33      | 0x21 | 100001 | Short          | Variable     | Medium           | 10            |
| 34      | 0x22 | 100010 | Short          | Variable     | High             | 10            |
| 35      | 0x23 | 100011 | Short          | Variable     | Reserved/Unknown | 10            |
| 36      | 0x24 | 100100 | Short          | Variable     | None             | 10            |
| 37      | 0x25 | 100101 | Short          | Variable     | Medium           | 10            |
| 38      | 0x26 | 100110 | Short          | Variable     | High             | 10            |
| 39      | 0x27 | 100111 | Short          | Variable     | Reserved/Unknown | 10            |
| 40      | 0x28 | 101000 | Long           | Variable     | None             | 10            |
| 41      | 0x29 | 101001 | Long           | Variable     | Medium           | 10            |
| 42      | 0x2A | 101010 | Long           | Variable     | High             | 10            |
| 43      | 0x2B | 101011 | Long           | Variable     | Reserved/Unknown | 10            |
| 44      | 0x2C | 101100 | Long           | Fixed        | None             | 10            |
| 45      | 0x2D | 101101 | Long           | Fixed        | Medium           | 10            |
| 46      | 0x2E | 101110 | Long           | Fixed        | High             | 10            |
| 47      | 0x2F | 101111 | Long           | Fixed        | Reserved/Unknown | 10            |
| 48      | 0x30 | 110000 | Short          | Variable     | None             | 11            |
| 49      | 0x31 | 110001 | Short          | Variable     | Medium           | 11            |
| 50      | 0x32 | 110010 | Short          | Variable     | High             | 11            |
| 51      | 0x33 | 110011 | Short          | Variable     | Reserved/Unknown | 11            |
| 52      | 0x34 | 110100 | Short          | Variable     | None             | 11            |
| 53      | 0x35 | 110101 | Short          | Variable     | Medium           | 11            |
| 54      | 0x36 | 110110 | Short          | Variable     | High             | 11            |
| 55      | 0x37 | 110111 | Short          | Variable     | Reserved/Unknown | 11            |
| 56      | 0x38 | 111000 | Long           | Variable     | None             | 11            |
| 57      | 0x39 | 111001 | Long           | Variable     | Medium           | 11            |
| 58      | 0x3A | 111010 | Long           | Variable     | High             | 11            |
| 59      | 0x3B | 111011 | Long           | Variable     | Reserved/Unknown | 11            |
| 60      | 0x3C | 111100 | Long           | Fixed        | None             | 11            |
| 61      | 0x3D | 111101 | Long           | Fixed        | Medium           | 11            |
| 62      | 0x3E | 111110 | Long           | Fixed        | High             | 11            |
| 63      | 0x3F | 111111 | Long           | Fixed        | Reserved/Unknown | 11            |

##### End of Article; feel free to reach out if you spot any typos/errors and I will gladly fix them <3 Khorvie
