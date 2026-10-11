# AndroPort

Fast file transfer between Windows and Android that bypasses slow Windows MTP.

AndroPort is a modern WinUI 3 desktop app for copying folders and files between Windows and Android with the bundled Android Platform Tools.

Created by Jem Hilario.

**Current version:** 2.0

---

## Why AndroPort?

Windows Explorer MTP transfer is slow, stalls on large folders, and often fails on many small files.

AndroPort uses ADB (`adb push` / `adb pull`) over USB debugging instead of MTP, so you get:

- Full USB speed bulk transfer
- Reliable folder copy (no Explorer freeze)
- Browse phone storage (`/sdcard`) directly from Windows
- Push (PC → phone) and Pull (phone → PC) in either direction
- Activity log with export for troubleshooting

No separate ADB install needed — platform-tools are bundled.

## Screenshots

> Save the app screenshots to `docs/screenshots/` with the names below to enable this guided tour.

### 1. Main window — Phone tab

![Phone tab](docs/screenshots/01-main-phone-tab.png)

- Top bar: `Detect device`, `Refresh`, `Cancel`, `Choose ADB`, `Auto-detect`
- Status card: `No Android device detected. Connect your phone and approve USB debugging.` / `ADB: Bundled platform-tools` / `TRANSFER: Idle`
- Tabs: `Phone` | `Transfer` | `Activity`
- Phone tab actions: `Pull selected`, `Pull storage`
- Left: `Phone storage — Folders and storage roots` — e.g. `Phone Storage (/sdcard)`
- Right: `Phone files — /sdcard` + `Select all`
- Footer: `AndroPort 2.0 • Bundled Android Platform Tools` + `Help` / `About`

### 2. About dialog

![About dialog](docs/screenshots/02-about-dialog.png)

`About` button shows:

> AndroPort 2.0 — AndroPort is a modern WinUI 3 desktop app for copying folders and files between Windows and Android with the bundled Android Platform Tools. Created by Jem Hilario.

### 3. Help — Connect your Android device

![Help dialog](docs/screenshots/03-help-connect.png)

`Help` button shows the 5-step connect checklist:

1. Enable Developer options.
2. Turn on USB debugging.
3. Connect the phone with a data-capable USB cable.
4. Unlock it and approve the debugging prompt.
5. Select Detect device.

### 4. Transfer center

![Transfer center](docs/screenshots/04-transfer-center.png)

`Transfer` tab:

- `Transfer center — Copy safely in either direction`
- `Phone destination` textbox (default `/sdcard`)
- `Use selected folder` button
- `Folder uploads` — `Copy the folder` toggle
- `Push files`, `Push folder`, `Pull selected to PC`
- `Ready to transfer — No active item`

### 5. Activity log

![Activity log](docs/screenshots/05-activity-log.png)

`Activity` tab:

- `Activity log` + `Export log` button for diagnostics.

---

## Requirements

- Windows 10 1809+ / Windows 11 x64
- Android phone/tablet with USB cable that supports data (not charge-only)
- USB debugging enabled on the phone
- AndroPort installer: `AndroPort-v2.0.0-win-x64.msi` from GitHub Releases

No manual ADB / driver install in most cases. Windows will use the bundled `platform-tools`.

## Install

1. Go to this repo on GitHub: `https://github.com/J3M09/AndroPort`
2. Open `Releases` (right sidebar on desktop, or `Code ▾` if no release yet).
3. Download `AndroPort-v2.0.0-win-x64.msi`.
4. Double-click the `.msi` and follow the wizard.
5. Launch `AndroPort` from Start Menu.

> For repo navigation: `Code` = files + README, `Releases` = installer download, `Issues` = bug reports, `Activity` = recent history.

## Quick start — first transfer in 5 minutes

### Step 1: Enable USB debugging on Android

1. On phone: `Settings > About phone > Build number` — tap 7 times until `You are now a developer`.
2. Go to `Settings > System > Developer options` (on Samsung: `Settings > Developer options`).
3. Turn on `USB debugging`. Tap `OK` on the warning.

### Step 2: Connect and approve

1. Connect phone to PC with a data-capable USB cable.
2. Unlock the phone.
3. When prompted `Allow USB debugging?` check `Always allow from this computer` → `Allow`.
4. If no prompt appears, unplug/replug and try a different cable/port.

### Step 3: Detect in AndroPort

1. Open AndroPort.
2. Top bar shows `ADB: Bundled platform-tools`. Leave `Auto-detect` on unless you need a custom ADB (see below).
3. Click `Detect device`.
4. Status card changes from `No Android device detected` to connected device.
5. If still not detected, click `Help` and walk the 5-step checklist, then `Refresh`.

### Step 4: Browse phone files

1. Stay on `Phone` tab.
2. Left panel `Phone storage` → select `Phone Storage (/sdcard)`.
3. Right panel `Phone files` lists `/sdcard`. Double-click folders to navigate.
4. Use `Select all` or tick individual files/folders.

### Step 5: Pull (Phone → PC)

Option A — quick buttons on Phone tab:

- Select files → `Pull selected` → choose PC destination folder.
- Full backup: `Pull storage`.

Option B — from Transfer tab:

- Select files on Phone tab first, then open `Transfer` tab.
- Click `Pull selected to PC` → choose destination.

### Step 6: Push (PC → Phone)

1. Open `Transfer` tab.
2. Set `Phone destination`, e.g.:
   - `/sdcard` (root)
   - `/sdcard/Download`
   - `/sdcard/DCIM/Camera`
3. Tip: click `Use selected folder` to fill this from your current Phone-tab folder.
4. `Folder uploads` → `Copy the folder` toggle:
   - ON = copy the folder itself, e.g. `MyPics` → `/sdcard/Download/MyPics`
   - OFF = copy only its contents
5. Click `Push files` (pick one or more files) or `Push folder` (pick a folder).
6. Wait for `Ready to transfer` to go idle. Use `Cancel` to abort.

### Step 7: Verify in Activity log

1. Open `Activity` tab.
2. Check commands and errors.
3. Click `Export log` and attach the file when reporting an issue.

---

## Button reference

| Button | Where | What it does |
|--------|-------|--------------|
| `Detect device` | Top bar | Runs `adb devices`, authorizes and lists device |
| `Refresh` | Top bar | Re-lists current `/sdcard` folder |
| `Cancel` | Top bar | Aborts active push/pull |
| `Choose ADB` | Top bar | Use a custom `adb.exe` instead of bundled |
| `Auto-detect` | Top bar | Switch back to bundled `platform-tools` |
| `Pull selected` | Phone | Copy checked phone files to PC |
| `Pull storage` | Phone | Copy entire `/sdcard` to PC |
| `Select all` | Phone files | Check all files in current folder |
| `Use selected folder` | Transfer | Fill `Phone destination` from Phone-tab selection |
| `Push files` | Transfer | PC files → phone destination |
| `Push folder` | Transfer | PC folder → phone destination |
| `Pull selected to PC` | Transfer | Same as `Pull selected`, from Transfer tab |
| `Export log` | Activity | Save activity log to `.txt`/`.log` |
| `Help` | Footer | Show connect checklist |
| `About` | Footer | Show version + description |

## ADB setup

Default is correct for most users: `ADB: Bundled platform-tools`.

- Keep `Auto-detect` enabled.
- Use `Choose ADB` only if you already have Android SDK Platform-Tools and need a specific version. Point it to your `adb.exe`.
- To revert: click `Auto-detect`.

Verify ADB manually if needed:

```powershell
# bundled adb is alongside the installed app; custom adb example:
adb devices
# expected: <serial>  device
# if `unauthorized`: unlock phone and approve the prompt, then Detect device again
```

## Troubleshooting

**`No Android device detected`**

- Use a data cable, not charge-only. Try another cable/port (prefer rear motherboard USB).
- Unlock phone, approve `Allow USB debugging`.
- Toggle USB debugging off/on, replug, click `Detect device` → `Refresh`.
- Check `Transfer: Idle` — if stuck, click `Cancel` and retry.
- Samsung / others: install OEM USB driver if device never appears in Device Manager.

**Shows `unauthorized`**

- Disconnect, revoke authorizations: `Developer options > Revoke USB debugging authorizations`, reconnect, approve again.

**`adb devices` empty but MTP Explorer works**

- MTP and ADB are different modes. ADB requires USB debugging ON. MTP alone is not enough.

**Push fails / permission denied**

- Don't push to system paths. Stay under `/sdcard/...`.
- Check `Phone destination` spelling — must start with `/sdcard` or full path shown in Phone tab.
- Path with spaces is OK, keep default unless you need a subfolder.

**Slow or stuck transfer**

- Don't use a USB hub for large transfers.
- Use `Cancel`, `Refresh`, retry smaller batch, check `Activity > Export log`.

**App shows `ADB: Custom` and fails after update**

- Click `Auto-detect` to return to bundled platform-tools.

## Reporting issues

1. Reproduce the problem.
2. Open `Activity` tab → `Export log` → save file.
3. On GitHub open `Issues > New issue`.
4. Include: Windows version, phone model + Android version, cable/port, AndroPort version (footer, e.g. `2.0`), steps, expected vs actual, exported log (redact personal filenames if needed), screenshot of status card.

## For maintainers

- Public repo: `https://github.com/J3M09/AndroPort`
- `Code` tab holds `README.md`, `docs/screenshots/`, `.gitattributes`.
- Do not commit the `.msi` to git — upload it to `Releases` instead (61 MB+). Add `*.msi` to `.gitignore` if needed.
- Screenshots in this README are loaded from `docs/screenshots/*.png`. See `docs/screenshots/README.md` for required filenames.

## Credits

AndroPort 2.0 — modern WinUI 3 desktop app for copying folders and files between Windows and Android with the bundled Android Platform Tools.

Created by Jem Hilario.
