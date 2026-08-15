---
title: Tech Stack & Repositories
summary: GnollHack technology stack, dependency graph, and GitHub repositories to check for bug reports, fixes, and upstream changes
---
# Tech Stack & Repositories

## GnollHack Repositories (hyvanmielenpelit)

| Repository | Description |
|:---|:---|
| `hyvanmielenpelit/GnollHack` | Main game — C core engine + .NET MAUI frontend |
| `hyvanmielenpelit/GnollHackWiki` | Game wiki (Gollum-style Markdown) |
| `hyvanmielenpelit/MobileGnollHackLogger` | Overseer AI assistant + game log server |
| `hyvanmielenpelit/GnollHackTileSet` | Tile set image assets |
| `hyvanmielenpelit/GnollHackSoundSet` | Sound set audio assets |

## Upstream Dependency Repositories

| Repository | Role in GnollHack | Check When... |
|:---|:---|:---|
| `dotnet/maui` | .NET MAUI UI framework | UI bugs, layout issues, platform-specific crashes, XAML problems |
| `dotnet/android` | Android platform bindings | Android-specific crashes, permission issues, native interop |
| `dotnet/macios` | iOS/macOS platform bindings | iOS/Mac-specific crashes, App Store issues, native interop |
| `dotnet/runtime` | .NET runtime & BCL | Performance issues, GC problems, threading bugs, marshalling |
| `microsoft/microsoft-ui-xaml` | WinUI / XAML framework | Windows desktop UI issues, XAML rendering |
| `mono/SkiaSharp` | 2D graphics rendering library | Rendering bugs, tile/sprite display, canvas drawing issues |

## Technology Stack Overview

- **Game Engine**: C (C89 standard), derived from NetHack 3.6.2
- **Frontend Framework**: .NET MAUI (Android, iOS, Windows)
- **Graphics**: SkiaSharp (SkiaSharp.Views.Maui) for tile rendering
- **Audio**: FMOD for sound effects and music (proprietary, no public GitHub repo)
- **Native Bridge**: P/Invoke between C core and C# frontend
- **Build Utilities**: makedefs, levcomp, dgncomp, dlb (C)

## Troubleshooting Routing Guide

Use this guide to determine which repositories to search when diagnosing issues:

| Problem Area | Primary Repo | Also Check |
|:---|:---|:---|
| Game crashes (C core) | `hyvanmielenpelit/GnollHack` | — |
| Tile rendering issues | `mono/SkiaSharp` | `hyvanmielenpelit/GnollHack`, `dotnet/maui` |
| Sound/music issues | `hyvanmielenpelit/GnollHack` | `hyvanmielenpelit/GnollHackSoundSet` |
| Android-specific crashes | `dotnet/android` | `dotnet/maui`, `hyvanmielenpelit/GnollHack` |
| iOS-specific crashes | `dotnet/macios` | `dotnet/maui`, `hyvanmielenpelit/GnollHack` |
| Windows desktop UI bugs | `microsoft/microsoft-ui-xaml` | `dotnet/maui` |
| XAML layout problems | `dotnet/maui` | `microsoft/microsoft-ui-xaml` |
| Performance / GC issues | `dotnet/runtime` | `dotnet/maui` |
| App startup failures | `dotnet/maui` | `dotnet/android` or `dotnet/macios` |
| Gestures / touch input | `dotnet/maui` | `dotnet/android` or `dotnet/macios` |
| Missing/broken tile assets | `hyvanmielenpelit/GnollHackTileSet` | `hyvanmielenpelit/GnollHack` |
| Game data / wiki content | `hyvanmielenpelit/GnollHackWiki` | `hyvanmielenpelit/GnollHack` |
