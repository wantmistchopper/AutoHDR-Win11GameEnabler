<p align="center">
  <img src="https://i.postimg.cc/zDyBmGs6/banner.png" alt="AutoHDR Force Enabler — Enable Windows 11 Auto HDR on Any DirectX 11 or 12 Game" width="100%">
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Platform-Windows%2010%2F11%20x64-0078D6?style=flat-square&logo=windows" alt="Platform: Windows 10/11 x64">
  <img src="https://img.shields.io/badge/Mode-Win11%20Auto%20HDR%20Enabler-2EA44F?style=flat-square" alt="Mode">
  <img src="https://img.shields.io/badge/Release-autohdr--force--v1.2-5391FE?style=flat-square" alt="Release Tag">
  <img src="https://img.shields.io/badge/License-MIT-8B5CF6?style=flat-square" alt="License: MIT">
</p>

# AutoHDR Force Enabler — Enable Windows 11 Auto HDR on Any DirectX 11 or 12 Game

**Bought an OLED or Mini-LED HDR monitor and frustrated that Windows 11 Auto HDR refuses to turn on in half of your DirectX 11 and DirectX 12 games because they aren't on Microsoft's internal whitelist? Enable per-executable Auto HDR cleanly in one click.**

AutoHDR Force Enabler configures Windows 11's official `Direct3D` application behavior flags (`HKCU\Software\Microsoft\Direct3D`): **applying `BufferUpgradeOverride=1` and `BufferUpgradeEnable=1` per game executable so Windows 11 upgrades SDR 8-bit swapchains into vibrant 10-bit Auto HDR**.

This project is aimed at **Windows 11 (22H2 / 23H2 / 24H2 / 25H2+) PC gamers** with HDR-capable OLED or Mini-LED monitors playing DirectX 11 or DirectX 12 SDR games.

## Quick Use-Case & Troubleshooting Reference

| Scenario / Issue | Cause | Solution |
| --- | --- | --- |
| Windows 11 'Auto HDR was turned on' toast never appears in a DX11/DX12 game | Microsoft only activates Auto HDR for a curated internal game whitelist | Add the game's `.exe` path with `BufferUpgradeOverride=1` in `HKCU\...\Direct3D` |
| Color banding in dark skies or fog on OLED monitors in older DX11 games | 8-bit SDR swapchain limits gradient precision on 10-bit HDR panels | Upgrade swapchain to 10-bit Auto HDR for smoother gradients and bright highlights |
| Game looks washed out or too bright after forcing Auto HDR | Some engines use custom gamma curves that clash with Auto HDR tone mapping | Remove the per-game entry in 1 click or adjust **HDR Intensity** in Xbox Game Bar (`Win+G`) |
| Game uses DirectX 9 or OpenGL/Vulkan | Windows 11 Auto HDR natively supports DirectX 11 and DirectX 12 swapchains | Check renderer API badge (`DX11`/`DX12` supported; use DXVK for DX9 titles) |

## Download for Windows

[**Download AutoHDRForce.zip — Latest GitHub Release (Windows x64)**](../../releases/latest/download/AutoHDRForce.zip)  
[View All Releases & Changelog](../../releases) · [Report an Issue](../../issues)

### Why use `AutoHDRForce.exe`? (Key features)

- Verifies that Windows 11 **HDR** and **Auto HDR** are active on your primary display before applying rules.
- Adds per-executable `BufferUpgradeOverride=1` entries in `HKCU\Software\Microsoft\Direct3D` without touching game files.
- Includes a quick-browse picker that scans running games or Steam/Epic folders for the main `.exe`.
- One-click **Remove Auto HDR Rule** reverts any game back to stock SDR behavior immediately.

### Sample Output

```text
[AutoHDRForce] Windows 11 Display HDR: ENABLED | Global Auto HDR: ENABLED
[OK]   Added Profile    : D:\Games\HollowKnightSilksong\Silksong.exe
[OK]   Registry Key     : HKCU\Software\Microsoft\Direct3D\Application0 (BufferUpgradeOverride=1)
[INFO] Tip              : Press Win+G in-game -> Gaming Features -> Adjust HDR Intensity
```

The release ZIP is named `AutoHDRForce.zip`; the Windows executable inside is named `AutoHDRForce.exe`.

1. Close AutoHDR Force before updating or replacing executable files.
2. Click **Download AutoHDRForce.zip** above.
3. Right-click the downloaded archive and choose **Extract All**.
4. Open the extracted folder and run `AutoHDRForce.exe`.
5. Review the options and output paths before processing files.

**Requirements:** Windows 11 (64-bit) with an HDR-capable display and 'Use HDR' + 'Auto HDR' enabled in Windows Display Settings.

### Verification & Windows SmartScreen Note

- **Offline & standard user permissions:** `AutoHDRForce.exe` runs locally without uploading your personal files and does not require disabling Windows Defender.
- **Windows SmartScreen:** Because this is an independent open-source utility without a commercial EV code-signing certificate, Windows SmartScreen may show *"Windows protected your PC"* on first launch. Click **More info → Run anyway** after verifying the release checksum on the [Releases](../../releases) page.

## Problems this project solves

### Bringing Auto HDR to thousands of unwhitelisted DX11 & DX12 games

Uses Windows 11's own Direct3D swapchain upgrade flag—no ReShade shaders or DLL injection needed.

### 10-bit color precision eliminating sky/shadow banding on OLEDs

Upgrades 8-bit SDR output buffers to 10-bit scRGB HDR.

### Per-game intensity tuning via Xbox Game Bar

Once forced on, Windows 11 lets you tune Auto HDR brightness slider per game with `Win+G`.

### Zero game file modification & 1-click removal

Safe for online and single-player DX11/DX12 titles alike.

## Default folders and configuration paths

AutoHDR Force stores per-application Direct3D flags in the current user registry hive:

```text
HKCU\Software\Microsoft\Direct3D\Application0..N
```

Typical directory layout:

```text
HKCU\Software\Microsoft\Direct3D\Application0
├── Name                  = "C:\Games\YourGame\Game.exe"
├── BufferUpgradeEnable   = 1
└── BufferUpgradeOverride = 1
```

Make sure **Use HDR** and **Auto HDR** are both turned **On** in `Windows Settings -> System -> Display -> HDR` before launching your game.

## Quick start guide

Follow these steps to get started:

1. **Turn on **Use HDR** and **Auto HDR** in Windows 11 Display Settings.** Extract `AutoHDRForce.zip` and launch `AutoHDRForce.exe`.
2. **Click **+ Add Game .exe** and select your DirectX 11 or DirectX 12 game executable.** Verify the `BufferUpgradeOverride = 1` status turns green.
3. **Launch your game—Windows 11 will show the *'Auto HDR was turned on'* notification.** Press `Win+G` in-game to fine-tune the Auto HDR intensity slider.

### Data safety note

AutoHDR Force modifies only `HKCU\Software\Microsoft\Direct3D` user preferences and never alters game files.

## What the status summary shows

AutoHDR Force displays **Windows HDR/AutoHDR system status, configured game `.exe` paths, and registry flag verification**.

## FAQ

**Does AutoHDR Force work on Windows 10?**

No—Auto HDR is a Windows 11 feature. On Windows 11, it works on DirectX 11 and DirectX 12 games.

**Why didn't Auto HDR turn on for an older DirectX 9 or Vulkan game?**

Windows 11 Auto HDR only hooks DirectX 11 and DirectX 12 swapchains. For DX9 games, converting them to DX11/Vulkan or using RTX HDR is required.

**How do I turn off Auto HDR for a specific game?**

Select the game in AutoHDR Force and click 'Remove Rule'.

## Useful reading

- [Microsoft DirectX Blog — Auto HDR Preview for PC](https://devblogs.microsoft.com/directx/auto-hdr-preview-for-pc-available-today/)

## More Windows Gaming Utilities

- [MonitorDim-DDCBrightnessControl](../MonitorDim-DDCBrightnessControl) — Hardware DDC/CI external monitor brightness & contrast slider
- [BorderlessForce-WindowScaler](../BorderlessForce-WindowScaler) — Force borderless windowed fullscreen & dual-monitor cursor lock
- [RefreshLock-HzMonitorSwitcher](../RefreshLock-HzMonitorSwitcher) — Per-game monitor refresh rate (144Hz/240Hz/360Hz) switcher
- [MiniHUD-LightweightFPSOverlay](../MiniHUD-LightweightFPSOverlay) — Compact borderless FPS, frametime & GPU temp overlay

*Independent open-source desktop utility for Windows. Not affiliated with Microsoft Corporation.*
