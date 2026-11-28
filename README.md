# QuickShot

**Lightweight, Instant-Startup, Local-First Screenshot & In-Place Annotation Utility for Windows.**

[![Latest Release](https://img.shields.io/github/v/release/treatacookie/QuickShot?label=Latest%20Release&color=2b7fff)](https://github.com/treatacookie/QuickShot/releases/latest)
[![Platform: Windows 10/11](https://img.shields.io/badge/Platform-Windows%2010%20%2F%2011%20(x64)-0078D6)](https://github.com/treatacookie/QuickShot/releases/latest)
[![License: MIT](https://img.shields.io/badge/License-MIT-22c55e)](LICENSE)

---

## Overview

**QuickShot** is a fast, native desktop screenshot and in-place annotation utility written from scratch in pure **Rust** (`~0.6 MB` NSIS installer, `~1.4 MB` statically linked native executable, zero external runtime DLLs or VC++ Redistributable required, Per-Monitor V2 High-DPI aware).

Designed around a strict **local-first, zero-telemetry** architecture, QuickShot freezes your screen in under `3 ms`, lets you select and annotate any region directly in volatile PC memory, and exports instantaneously to your clipboard, local disk, or printer — with **no accounts, no cloud uploads, no background telemetry, and no subscriptions**.

---

## Key Features

- **Instant Zero-Animation Freeze-Screen Capture:**
  - Captures multi-monitor High-DPI desktops at 1:1 native hardware pixel accuracy (`< 3 ms` capture latency) with zero DWM slide/entrance animation.
  - High-contrast dashed selection frame with 8 resize handles, drag-to-reposition support, and a live `WxH` dimensions badge.
- **In-Place Annotation Suite with Independent Per-Tool Color Memory:**
  - Every creation tool remembers its own color across sessions (`1st click` selects the tool; `2nd click` or clicking the bottom-right corner flyout triangle opens its 16-color palette directly beside the button):
    1. **Pen (`P`)** — Anti-aliased freehand curve drawing (default: Electric Blue `#1A73E8`).
    2. **Line (`L`)** — Anti-aliased straight line segments (default: Emerald Green `#00A859`).
    3. **Arrow (`A`)** — Axis-locked stealth directional arrows with length-invariant arrowheads (default: Classic Red `#E60000`).
    4. **Rectangle (`R`)** — Crisp hollow box outlines (default: Classic Red `#E60000`).
    5. **Marker / Highlighter (`M` / `H`)** — Uniform-alpha translucent highlight strokes (default: Golden Yellow `#FFD800`).
    6. **Text (`T`)** — Multi-line proportional Segoe UI ClearType text annotations (default: True Black `#000000`).
    7. **Undo / Redo (`Ctrl+Z` / `Ctrl+Y`)** — Full non-destructive annotation history.
  - **Mouse Scroll Wheel** dynamically adjusts stroke thickness (`1.5 px` – `14.0 px`).
- **One-Click Action Bar & Chronological File Naming:**
  - **Copy (`Ctrl+C` or `Enter`)** — Copies the cropped and annotated image directly to the Windows clipboard.
  - **Copy Text — Offline OCR (`Ctrl+T`)** — Extracts all text inside your selected region 100% offline using Windows 10/11's built-in `Windows.Media.Ocr` engine (zero network calls, zero AI model downloads) and copies clean plain text directly to your clipboard with a live toast preview.
  - **Pin to Screen (`Ctrl+Shift+P` or `F3`)** — Lifts the annotated capture into a borderless Always-on-Top floating window at its exact screen position (supports multiple simultaneous pins; left-drag to move, mouse wheel to zoom `35%–300%`, `Ctrl + Wheel` for opacity `25%–100%`, double-click/`Esc` to dismiss, right-click for Copy Image, Copy Text OCR, Save As, Reset Zoom, Opacity presets, or Close All).
  - **Save (`Ctrl+S`)** — Opens the native Save As dialog (`PNG`, `JPEG` with `80% / 90% / 100%` quality, or `BMP`).
  - **Quick Save & Copy Path (`Ctrl+Shift+S`)** — Saves immediately to your configured folder using local 24-hour chronological naming (`QuickShot_YYYYMMDD_HHMMSS.png` / `.jpg` / `.bmp`, with automatic `_1`, `_2` collision protection) and copies the path to the clipboard.
  - **Share (Native Windows 10/11 Share Sheet)** — Saves using your configured format/folder and opens the native Windows Share dialog with a live screenshot thumbnail and attachment — share privately via Nearby Share, Phone Link, Outlook/Mail, WhatsApp, Teams, OneNote, or any installed Windows Share target (zero public cloud links; falls back to File Explorer if unavailable).
  - **Search Similar Images on Google (`Ctrl+G`)** — Directly submits your selection from RAM over HTTPS to Google Lens (with zero third-party image hosts and zero temporary disk files) and opens the live visual search results in your default browser — with automatic clipboard + toast fallback if offline.
  - **Print (`Ctrl+P`)** — Opens QuickShot's built-in **Live Print Preview & Options** dialog (printer selector for all installed local/network & PDF printers, Auto/Portrait/Landscape orientation, Letter/A4/Legal paper size, Fit/Fill/Actual scale, Margins, Color/Grayscale, Copies, and native **More Printer Properties…**) and streams directly from RAM via Win32 GDI with zero temporary files.
  - **Close (`Esc` or `Right-Click`)** — Cancels the capture and clears volatile RAM immediately.
- **System Tray Daemon, Customizable Multi-Hotkeys, Native Notifications & Auto-Updates:**
  - Permanently reserves **`PrintScreen`** for General screenshot (preventing Windows Snipping Tool or OneDrive from reclaiming it), with **`Ctrl + PrintScreen`** and **`Ctrl + Alt + S`** preselected as removable secondary shortcuts and **`Shift + PrintScreen`** for instant fullscreen capture.
  - Built-in **Global Hotkeys** manager (**Options → Global Hotkeys**) supporting up to 4 custom hotkeys per action via live key-press recording (click **`+ Add`** or any empty row space and press keys live), 1-click chip removal (`×`), non-destructive enable/disable for **Instant fullscreen save**, and **`Reset defaults`**.
  - Native Windows desktop notifications with QuickShot's icon and clean formatting.
  - Built-in **SHA-512 verified automatic updater** (`Right-Click Tray Icon → Check for Updates…` or **Options → Software Updates**) — seamlessly checks `latest.yml` on GitHub Releases, verifies cryptographic integrity via Windows CNG, and waits until QuickShot and your PC are idle before silently updating & relaunching to the system tray (can be triggered immediately on demand or toggled off anytime).
  - Built-in **Capture Menu (`•••` left of Share)** on the horizontal capture toolbar to toggle notifications, persistent selection position, cursor capture, or jump straight into **Options…** (pausing and restoring your capture selection & annotations cleanly in RAM).
  - Built-in **Options, Support & About** dialog (`Capture Menu → Options…` or `Right-Click Tray Icon → Options...`) to customize hotkeys, default save folder, image format, JPEG quality, per-tool default colors, toolbar icon color theme, and update preferences.

---

## Downloads & Installation

Download the latest release from [**GitHub Releases**](https://github.com/treatacookie/QuickShot/releases/latest):

| Package | Description |
| :--- | :--- |
| **`QuickShot-Setup-v0.8.7-x64.exe`** | Standard per-user NSIS Windows Setup Wizard (`~0.7 MB`) — zero external dependencies (no VC++ Redistributable, .NET, or WebView2 needed). Installs to `%LOCALAPPDATA%\Programs\QuickShot`, creates Desktop & Start Menu shortcuts, optional Windows Startup (`--tray`), and registers in Windows Installed Apps. Supports silent install via `/S`. |
| **`QuickShot-Portable-v0.8.7-x64.zip`** | Zero-install Portable ZIP bundle with statically linked `QuickShot.exe`, `Start-QuickShot-Tray.bat`, and all legal notices. |
| **`latest.yml`** | Signed-digest (`SHA-512`) release manifest used by QuickShot's built-in auto-updater. |
| **`SHA256SUMS.txt`** | Cryptographic SHA-256 checksums for verifying download integrity (`Get-FileHash -Algorithm SHA256`). |

> **First-Time Windows SmartScreen Notice:** Because QuickShot is currently distributed without a commercial Authenticode code-signing certificate, Windows Defender SmartScreen may display *"Windows protected your PC"* on the initial browser download. Click **More info → Run anyway** (you can verify the file hash against `SHA256SUMS.txt` beforehand). Once installed, future updates apply automatically in the background without manual re-downloads.

### Quick Start & Hotkeys

| Shortcut / Action | Behavior |
| :--- | :--- |
| **`PrintScreen`** *(always reserved)*, **`Ctrl + PrintScreen`**, **`Ctrl + Alt + S`** *(or Left-Click Tray Icon)* | Freeze screen and drag to select a region for annotation *(add/remove custom shortcuts in **Options → Global Hotkeys**)* |
| **`Shift + PrintScreen`** *(customizable / toggleable)* | Instant fullscreen capture saved directly to your Screenshots folder |
| **`P` / `L` / `A` / `R` / `M` / `T`** | Select Pen, Line, Arrow, Rectangle, Marker, or Text tool |
| **`Mouse Scroll Wheel`** | Adjust stroke thickness |
| **`Ctrl + Z` / `Ctrl + Y`** | Undo / Redo annotation |
| **`Ctrl + C`** or **`Enter`** | Copy annotated capture to clipboard |
| **`Ctrl + T`** | Extract & copy text from selection (100% offline Windows OCR) |
| **`Ctrl + Shift + P`** or **`F3`** | Pin selection as a floating Always-on-Top window (drag, wheel zoom, `Ctrl+Wheel` opacity) |
| **`Ctrl + S`** / **`Ctrl + Shift + S`** | Save As dialog / Quick Save & copy file path |
| **`Esc`** or **`Right-Click`** | Clear selection or cancel capture |

---

## Managing or Uninstalling QuickShot

- **Open Options, Support & About:** Right-click the QuickShot icon in the Windows System Tray and choose **Options...**, **Support...**, or **About...**.
- **Settings Storage:** User preferences are stored locally in `%APPDATA%\QuickShot\settings.json`.
- **Command-Line Launch Modes:**
  - `QuickShot.exe --tray` — Start quietly in the background system tray.
  - `QuickShot.exe --once` — Capture a single screenshot and exit immediately afterward.
- **Uninstall:** Remove cleanly via **Windows Settings → Apps → Installed apps → QuickShot**, or run:
  ```powershell
  "%LOCALAPPDATA%\Programs\QuickShot\Uninstall-QuickShot.exe"
  ```
  *(Uninstalling QuickShot never deletes your saved screenshots.)*

---

## Legal, Privacy & Security Documentation

- [**License (`MIT`)**](LICENSE) — Permissive MIT open-source license terms.
- [**End-User License Agreement (`EULA.txt`)**](EULA.txt) — Software license terms and warranty disclaimer.
- [**Privacy Policy (`PRIVACY.md`)**](PRIVACY.md) — Local-first privacy guarantee, zero telemetry, and optional SHA-512 update disclosure.
- [**Security Policy (`SECURITY.md`)**](SECURITY.md) — Volatile RAM isolation, zero clipboard snooping, zero network ports, static CRT isolation, SHA-512 verified updates, and SHA-256 checksums.
- [**Third-Party Notices (`THIRD_PARTY_NOTICES.md`)**](THIRD_PARTY_NOTICES.md) — Open-source Rust crate attributions and licenses.
- [**Changelog (`CHANGELOG.md`)**](CHANGELOG.md) — Public release notes and version history.
