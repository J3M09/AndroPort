# AndroPort

<p align="center">
  <img src="docs/screenshots/logo.png" width="120" alt="AndroPort logo" />
  <br />
  <strong>Fast file transfer between Windows and Android that bypasses slow Windows MTP.</strong>
  <br />
  <img src="https://img.shields.io/badge/version-2.0.0-blue" alt="Version" />
  <img src="https://img.shields.io/badge/platform-Windows_10_/_11-0078D6?logo=windows&logoColor=white" alt="Platform" />
  <img src="https://img.shields.io/badge/.NET-8-512BD4?logo=dotnet&logoColor=white" alt=".NET" />
  <img src="https://img.shields.io/badge/C%23-512BD4?logo=csharp&logoColor=white" alt="C#" />
  <img src="https://img.shields.io/badge/WinUI-3-0078D4?logo=windows&logoColor=white" alt="WinUI 3" />
  <img src="https://img.shields.io/badge/Platform--Tools-37.0.0-3DDC84?logo=android&logoColor=white" alt="Platform-Tools" />
  <br />
  <a href="https://github.com/J3M09/AndroPort/releases"><strong>Download AndroPort-v2.0.0-win-x64.msi</strong></a>
</p>


## Contents

- [Why AndroPort?](#why-androport)
- [Features](#features)
- [Screenshots](#screenshots)
- [Quick start](#quick-start)
- [Requirements](#requirements)
- [Install](#install-msi)
- [Navigating this repository on GitHub](#navigating-this-repository-on-github)
- [Button reference](#button-reference)
- [ADB setup](#adb-setup)
- [Data and privacy](#data-and-privacy)
- [Troubleshooting](#troubleshooting)

---

## Why AndroPort?

Windows Explorer's MTP is the slowest way to move a photo library. It stalls on big folders, crawls on thousands of small files, and locks Explorer while it works.

AndroPort uses Android Debug Bridge (`adb push` / `adb pull`) over USB debugging instead. One continuous stream per operation, real progress, and you keep browsing your phone while it runs.

| | Windows MTP | AndroPort (ADB) |
|---|---|---|
| Large folders | Stalls, Explorer freeze | Single stream, safe cancel |
| Thousands of small files | Very slow | Batched per item |
| Progress | None / estimate | Live bytes, speed, elapsed, ETA |
| Errors | Dialog spam | Skipped and logged, run continues |
| Needs setup | Nothing | USB debugging once |
| Extra install | Nothing | None — Platform Tools bundled |

- Browse internal storage and removable cards from Windows
- Pull files, folders, or a whole storage root to your PC
- Push multiple PC files or a whole folder to your phone
- Live progress, byte count, speed, elapsed time, and ETA
- Cancel safely, skip recoverable per-item errors, export activity log
- No separate ADB install — Platform Tools 37.0.0 is embedded in the app

## Features

- Phone storage browser with expandable roots and multi-select
- `Pull selected`, `Pull storage`, `Push files`, `Push folder`, `Pull selected to PC`
- `Phone destination` textbox + `Use selected folder` shortcut
- `Folder uploads` toggle: copy the folder, or copy only its contents
- Automatic detection of connected / unauthorized / offline / missing devices
- `Choose ADB` for a custom `adb.exe`, `Auto-detect` to return to bundled tools
- Native Windows light/dark theme + Mica backdrop
- Timestamped activity log with `Export log`
- Self-contained WinUI 3 app — no .NET or Windows App SDK runtime needed

## Screenshots

### Main window — Phone tab

![Phone tab](docs/screenshots/01-main-phone-tab.png)

Top bar: `Detect device`, `Refresh`, `Cancel`, `Choose ADB`, `Auto-detect`. Status card shows `ADB: Bundled platform-tools` and `TRANSFER: Idle`. Left: `Phone storage — Folders and storage roots`, e.g. `Phone Storage (/sdcard)`. Right: `Phone files — /sdcard` with `Select all`.

### Help — connect checklist

![Help dialog](docs/screenshots/03-help-connect.png)

The app's `Help` button walks you through the whole setup:

1. Enable Developer options.
2. Turn on USB debugging.
3. Connect the phone with a data-capable USB cable.
4. Unlock it and approve the debugging prompt.
5. Select Detect device.

### Transfer center

![Transfer center](docs/screenshots/04-transfer-center.png)

`Transfer center — Copy safely in either direction`: `Phone destination` (default `/sdcard`), `Use selected folder`, the `Folder uploads` toggle (`Copy the folder` / `Copy only its contents`), then `Push files`, `Push folder`, and `Pull selected to PC`.

### Activity log

![Activity log](docs/screenshots/05-activity-log.png)

Every ADB command, warning, and error is timestamped in `Activity log`, with `Export log` for troubleshooting.

---

## Quick start

**1. Enable USB debugging on the phone**

- `Settings > About phone > Build number` — tap 7 times until `You are now a developer`
- `Settings > System > Developer options` (Samsung: `Settings > Developer options`)
- Turn on `USB debugging` → `OK`

**2. Connect and approve**

- Use a data-capable cable, unlock the phone
- Approve `Allow USB debugging?` — tick `Always allow from this computer` → `Allow`
- No prompt? Try another cable/port, or toggle USB debugging off and on

**3. Detect the device**

- Open AndroPort, keep `Auto-detect` on, click `Detect device`
- The status card switches from `No Android device detected` to your device

**4. Pull — phone to PC**

- `Phone` tab → select files → `Pull selected` → choose your PC folder
- Or `Pull storage` to copy a full `/sdcard` backup

**5. Push — PC to phone**

- `Transfer` tab → set `Phone destination` (e.g. `/sdcard/DCIM/Camera`)
- `Push files` or `Push folder`, and use `Folder uploads` to copy the folder itself or only its contents

**6. Check the log**

- `Activity` tab → `Export log` if you need help

---

## Requirements

- Windows 10 version 1809 (build 17763) or newer, x64
- Android phone or tablet with USB debugging available
- A data-capable USB cable — charge-only cables will not work

## Install (MSI)

1. Open `Releases` on this repo: [github.com/J3M09/AndroPort/releases](https://github.com/J3M09/AndroPort/releases)
2. Download `AndroPort-v2.0.0-win-x64.msi`
3. Run the wizard — per-user install to `%LOCALAPPDATA%\AndroPort`, no UAC prompt
4. Launch `AndroPort` from the Start Menu

> Unsigned build note: SmartScreen may warn until the app establishes reputation or is signed with a trusted certificate.

## Navigating this repository on GitHub

| Tab | What is there |
|-----|---------------|
| `Code` | This README and `docs/screenshots/` |
| `Releases` | Download the `.msi` installer |
| `Issues` | Report bugs and request features |
| `Commits / Activity` | What changed and when |

## Button reference

| Button | Where | Does |
|--------|-------|------|
| `Detect device` | Top bar | `adb devices`, authorize + list device |
| `Refresh` | Top bar | Re-list the current folder |
| `Cancel` | Top bar | Abort the active transfer |
| `Choose ADB` | Top bar | Use a custom `adb.exe` |
| `Auto-detect` | Top bar | Back to bundled platform-tools |
| `Pull selected` | Phone | Copy checked phone files to the PC |
| `Pull storage` | Phone | Copy a whole storage root to the PC |
| `Select all` | Phone files | Select everything in the folder |
| `Use selected folder` | Transfer | Fill `Phone destination` from the Phone tab |
| `Push files` | Transfer | Send PC files to the phone |
| `Push folder` | Transfer | Send a PC folder to the phone |
| `Pull selected to PC` | Transfer | Same as `Pull selected`, from the Transfer tab |
| `Export log` | Activity | Save a timestamped activity log |
| `Help` / `About` | Footer | Connect checklist / version info |

## ADB setup

The default is correct for almost everyone: `ADB: Bundled platform-tools` with `Auto-detect` on.

- Platform Tools 37.0.0 is embedded in the executable and extracted on first run to `%LOCALAPPDATA%\AdbFileTransferApp\EmbeddedPlatformTools\`
- `Choose ADB` only if you want a specific SDK version — `Auto-detect` switches back
- Manual check: `adb devices` should show `<serial>  device`; `unauthorized` means unlock the phone, approve the prompt, then `Detect device` again

## Data and privacy

Local-only. The app launches its bundled `adb.exe` to talk directly to your device. No uploads, no telemetry.

- Settings: `%LOCALAPPDATA%\AdbFileTransferApp\settings.json`
- Extracted tools: `%LOCALAPPDATA%\AdbFileTransferApp\EmbeddedPlatformTools\`
- Install folder: `%LOCALAPPDATA%\AndroPort\`

## Troubleshooting

<details>
<summary><strong>No Android device detected</strong></summary>

- Use a data cable, not charge-only. Try another cable and port (rear motherboard USB, no hub for large transfers).
- Set the phone's USB mode to one that permits data, unlock it, approve the prompt.
- `Detect device` → `Refresh`, and close other software that may be using ADB.
- If the device never appears in Device Manager, install your phone maker's OEM USB driver.
</details>

<details>
<summary><strong>Device shows <code>unauthorized</code> or <code>offline</code></strong></summary>

- Unlock the phone and approve the `Allow USB debugging?` prompt.
- `Developer options > Revoke USB debugging authorizations`, then reconnect and approve again.
- Unplug and replug, then `Detect device` again.
</details>

<details>
<summary><strong>MTP in Explorer works but ADB shows nothing</strong></summary>

- Normal: MTP and ADB are separate modes. ADB requires USB debugging to be ON.
</details>

<details>
<summary><strong>Push fails or permission denied</strong></summary>

- Stay under `/sdcard/...` — system paths are rejected.
- Check the `Phone destination` spelling, or use `Use selected folder`.
</details>

<details>
<summary><strong>Transfer is slow or stuck</strong></summary>

- Avoid USB hubs for large transfers.
- `Cancel`, `Refresh`, then retry in smaller batches and check `Activity > Export log`.
</details>

---

<p align="center">If AndroPort saves you a slow transfer, give the repo a ⭐ — it helps other people find it.</p>

Android Debug Bridge and Platform Tools are provided by Google under the notices in `platform-tools/NOTICE.txt`.
