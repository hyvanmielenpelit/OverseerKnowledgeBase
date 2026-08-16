---
title: Troubleshooting Common Issues
summary: Common problems, error messages, and diagnostic steps organized by symptom
---

#### 1. App Won't Start / Crashes on Launch
- Try disabling GPU acceleration (Settings → General → GPU Acceleration: off)
- Clear cache (Settings → System → Clear Cache)
- Reset core files (About → Manage Files or developer Reset page)
- Check available storage space
- Android: check battery optimization settings (may kill app in background)

#### 2. Game Crashes Mid-Play
- Check the panic log (About → View Panic Log, or Overseer's get_panic_log tool)
- Common causes: out of memory on older devices, corrupted save file
- Try lowering Map FPS (Settings → General)
- Try switching graphics mode (Settings → General → Graphics Mode)

#### 3. Save File Issues
- "Continue" button missing: save may be from incompatible version
- Save corruption: export and re-import (About → Manage Files)
- Version mismatch: check compatibility table
> **See also:** get_knowledge_article("save_management") for full save file guidance.

#### 4. Performance Problems
- Toggle GPU acceleration (Settings → General)
- Lower Map FPS (Settings → General)
- Switch graphics mode (Settings → General → Graphics Mode)

#### 5. Sound Issues
- Check volume settings (Settings → Volume — master, music, SFX, ambient, voice)
- Check Silent Mode (Settings → General → Silent Mode)
- FMOD initialization failures: restart the app

#### 6. Display Problems
- Resolution/scale: Settings → General → Screen Resolution & Scale
- Dark screen on startup: may be disabled animations, reset core files
- GPU rendering glitches: try disabling GPU acceleration

#### 7. Network / Server Issues
- Verify server credentials (Settings → Server Posting → Verify button)
- Check internet connectivity
- Upload failures: retry or check server status
> **See also:** get_knowledge_article("server_account") for account setup.

#### 8. Windows / Steam Specific
- Loading doesn't finish: change system locale for non-Unicode programs to English (US)
- Alternative: install from MSIX package instead of Steam

#### 9. Diagnostic Tools Available
- **In the app:** View Panic Log, View App Log, Crash Report (all in About screen)
- **Via Overseer:** get_panic_log, get_app_log tools can retrieve logs directly
> **See also:** get_knowledge_article("crash_reporting") for creating crash reports.

> **Wiki:** For additional platform-specific troubleshooting details, search the wiki for "Overseer References" and see the **troubleshooting** section.
