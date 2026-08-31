---
title: Platform-Specific Notes
summary: Android, iOS, macOS, Windows, and Steam platform differences and setup notes
---

#### 1. Android
- **Battery Optimization:** Aggressive OS battery management may kill the app while running in the background. Check device settings to exempt GnollHack.
- **Permissions:** Ensure necessary storage permissions are granted for save file management.
- **Store:** Available via the Google Play Store.

#### 2. iOS
- **Storage Management:** Apple devices handle background apps strictly; avoid leaving the game unsaved for long periods while backgrounded.
- **Store:** Available via the Apple App Store.

#### 3. macOS
- **How it is supported:** Macs run the **iOS build** from the App Store. There is no Mac Catalyst version, and none is planned.
- **Hardware:** Apple Silicon only — M1 or later. Intel Macs are not supported.
- **Feature set:** Identical to iOS, including which settings appear. Windows-only and desktop-only settings (Screen Resolution, Windowed Mode, Disable Windows Key, Save File Tracking) are absent.
- **Updates:** Disable Automatic Updates in App Store settings to avoid an update mid-run.

#### 4. Windows
- **Antivirus:** Sometimes antivirus software incorrectly flags the app. You may need to add an exclusion.
- **Display:** Supports windowed mode.
- **Locale Settings:** If the game hangs during loading, try changing the Windows system locale for non-Unicode programs to "English (US)".

#### 5. Steam
- **Sponsor Button:** The in-app sponsor link button is hidden in the Steam build.
- **MSIX:** An alternative MSIX package installer is available for users who prefer not to use Steam.

#### 6. Cross-Platform
- Feature parity is generally maintained across all platforms.
- Save files can be transferred seamlessly between mobile and desktop using the built-in Save Transfer feature.

> **Wiki:** For supported devices and platform-specific troubleshooting, search the wiki for "Overseer References" and see the **platform_differences** section.
