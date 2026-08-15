---
title: GnollHack Minimum System Requirements
summary: Minimum and recommended hardware and software requirements for running GnollHack on Android, iOS/iPadOS, and Windows.
---
# GnollHack Minimum System Requirements

These are the current minimum and recommended system requirements for GnollHack.
Note that minimum OS versions may change as the game is updated — when in doubt,
the definitive source is the `GnollHackM.csproj` project file.

## Android

- **Minimum OS:** Android 8.0 (Oreo), API Level 26
- **RAM:** 3 GB minimum (4–6 GB recommended)
- **Storage:** 1–1.5 GB free space (APK, game assets, sound banks, save files)
- **Processor (minimum for 60 FPS at ~2 megapixel resolution):**
  - Qualcomm Snapdragon 660 or better
  - Samsung Exynos 9611 or better
  - Google Tensor (all versions)
  - Unisoc Tiger T618 or better
  - MediaTek Helio G80 / Helio P70 / Helio X30 / Dimensity 700 or better
  - HiSilicon Kirin 960 or better
- **Display:** The game targets 60 FPS at 2.0–2.8 megapixel screen resolutions.
  It works with slower processors but may not reach 60 FPS in zoomed-in mode.
- **Distribution:** Google Play Store

For tested device lists, refer to the wiki article "Supported Android Devices."

## iOS and iPadOS

- **Minimum OS:** iOS / iPadOS 16
- **Fully supported (3 GB+ RAM):** iPhone X (2017) or later, iPhone SE 2nd gen
  (2020) or later, iPad 7th gen (2019) or later, iPad Air 3rd gen (2019) or
  later, iPad Mini 5th gen (2019) or later, all iPad Pro models.
- **Partially supported (2 GB RAM):** Playable with sound banks disabled in
  settings. Includes iPhone 6s/7/8, iPhone SE 1st gen, iPad 5th/6th gen,
  iPad Air 2, iPad Mini 4, iPad Pro 9.7". Restarting the device before
  playing is recommended to free memory.
- **Storage:** 1.5–4 GB free space (app, sound banks, tilesets, game data)
- **Distribution:** Apple App Store

For full device lists, refer to the wiki article "Supported iPhones and iPads."

## Windows

- **Minimum OS:** Windows 10 Version 1809 (Build 17763, October 2018 Update)
- **Recommended OS:** Windows 11
- **RAM:** 8 GB minimum
- **Storage:** 1 GB free disk space
- **Processor:** 5th generation Intel Core (or equivalent) minimum;
  11th generation Intel Core or later recommended
- **Graphics:** Intel HD Graphics (DirectX 11 compatible) minimum;
  Intel UHD Graphics or dedicated GPU recommended
- **Input:** Mouse, keyboard, or touch screen
- **Distribution:** Steam and sideloadable MSIX packages

For more details, refer to the wiki article "System Requirements for Modern
Windows Port (.NET MAUI / WinUI 3)" under Development.

## Additional References

- For CPU rendering performance benchmarks on specific devices, see the wiki
  articles "Game performance in CPU rendering on Android devices" and
  "Game performance in CPU rendering on iPhones and iPads."
- The file `DEVEL/performance.txt` in the GnollHack repository contains an
  infrequently updated record of FPS performance in minimap mode, primarily
  for development purposes.
