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
| `hyvanmielenpelit/OverseerKnowledgeBase` | Overseer knowledge base articles |

## Upstream Dependency Repositories

| Repository | Role in GnollHack | Check When... |
|:---|:---|:---|
| `dotnet/maui` | .NET MAUI UI framework | UI bugs, layout issues, platform-specific crashes, XAML problems |
| `dotnet/android` | Android platform bindings | Android-specific crashes, permission issues, native interop |
| `dotnet/macios` | iOS/macOS platform bindings | iOS/Mac-specific crashes, App Store issues, native interop |
| `dotnet/runtime` | .NET runtime & BCL | Performance issues, GC problems, threading bugs, marshalling |
| `microsoft/microsoft-ui-xaml` | WinUI / XAML framework | Windows desktop UI issues, XAML rendering |
| `mono/SkiaSharp` | 2D graphics rendering library | Rendering bugs, tile/sprite display, canvas drawing issues |

## Notable Repository Folders

| Repository | Folder | Description |
|:---|:---|:---|
| `hyvanmielenpelit/GnollHack` | `win/win32` | GnollHack Windows and cross-platform development files |
| `hyvanmielenpelit/GnollHack` | `win/win32/banks` | FMOD sound banks source folder for all versions |
| `hyvanmielenpelit/GnollHack` | `win/win32/tileset` | Tileset source folder for all versions |
| `hyvanmielenpelit/GnollHack` | `win/win32/vs` | Visual Studio solution for GnollHack and GnollHackX (Xamarin) |
| `hyvanmielenpelit/GnollHack` | `win/win32/xpl` | .NET MAUI frontend and its C libraries |
| `hyvanmielenpelit/GnollHack` | `win/win32/xpl/GnollHackM` | Visual Studio solution for GnollHackM (.NET MAUI) |
| `hyvanmielenpelit/MobileGnollHackLogger` | `MobileGnollHackLogger` | GnollHack Account server |
| `hyvanmielenpelit/MobileGnollHackLogger` | `Overseer` | Gnoll Overseer AI assistant |

## Notable Repository Files

| Repository | File | Description |
|:---|:---|:---|
| `hyvanmielenpelit/GnollHack` | `win/win32/xpl/GnollHackX/GnollHackX/Pages/Game/OverseerPage.xaml.cs` | Overseer logic on .NET MAUI side |

## Technology Stack Overview

- **Game Engine**: C (C89 standard), derived from NetHack 3.6.2
- **Frontend Framework**: .NET MAUI (Android, iOS, Windows)
- **Graphics**: SkiaSharp (SkiaSharp.Views.Maui) for tile rendering
- **Audio**: FMOD for sound effects and music (proprietary, no public GitHub repo)
- **Native Bridge**: P/Invoke between C core and C# frontend
- **Build Utilities**: makedefs, levcomp, dgncomp, dlb (C)
- **Overseer**: Angular frontend, ASP.NET Core backend, and SQL Server with Entity Framework Core

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
| Overseer issues | `hyvanmielenpelit/MobileGnollHackLogger` | `hyvanmielenpelit/GnollHack` |
