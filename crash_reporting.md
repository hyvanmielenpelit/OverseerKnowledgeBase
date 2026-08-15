---
title: Crash Reporting & Diagnostic Logs
summary: How to create and send crash reports, view app and panic logs
---

#### 1. Creating a Crash Report
1. Open the app (even if the game crashed, the app should still launch)
2. Tap **About** on the main menu
3. Tap **Crash Report**
4. Confirm when prompted — the app creates a zip file containing diagnostic data
5. The system share sheet opens — send the zip via email, Discord, or other app
6. The zip includes: panic log, app log, game configuration, and device info

#### 2. Viewing the App Log
1. Main Menu → About → **View App Log**
2. Shows the application log file (ghlog.txt) with timestamped events
3. Use the **Share** button to send the log to developers

#### 3. Viewing the Panic Log
1. Main Menu → About → **View Panic Log**
2. Shows the C game engine panic log with crash details
3. Use the **Share** button to send the log

#### 4. What the Overseer Can Do
- The Overseer has `get_panic_log` and `get_app_log` tools that retrieve these logs directly from the device
- If the user describes a crash, offer to retrieve the logs yourself before asking them to navigate to the About screen

#### 5. Where to Send Reports
- GitHub Issues: github.com/hyvanmielenpelit/GnollHack/issues
- Discord: GnollHack Discord server
- Email: contact information on www.gnollhack.com

> **See also:** get_knowledge_article("troubleshooting") for diagnosing common problems.
