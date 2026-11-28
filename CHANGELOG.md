# Changelog

All notable public release changes to **QuickShot** are documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

---

## [0.8.7] - 2026-11-28

### Initial Public Release
- **QuickShot Setup Wizard (`QuickShot-Setup-v0.8.7-x64.exe`) & Portable Bundle (`QuickShot-Portable-v0.8.7-x64.zip`):**
  - Lightweight, instant-startup, 100% offline-first Windows screenshot and in-place annotation utility written from scratch in pure Rust (`~1.1 MB` native executable, zero external runtime DLLs, Per-Monitor V2 High-DPI aware).
  - Hardware-level Win32 GDI `BitBlt` freeze-screen capture (`< 3ms` latency, zero DWM entrance animation) with 8-handle interactive selection and live dimensions badge.
  - In-place vector annotation suite (**Pen**, **Line**, **Stealth Arrow**, **Rectangle**, **Marker / Highlighter**, **Proportional Segoe UI Text**, and **Undo / Redo**) with independent per-tool color memory and 16-color flyout palettes.
  - Human-readable 24-hour local timestamp filenames (`QuickShot_YYYYMMDD_HHMMSS.png` / `.jpg` / `.bmp`) with automatic `_1`/`_2` collision protection across Save As, Quick Save (`Ctrl+Shift+S`), Share, and Instant Fullscreen (`Shift+PrintScreen`).
  - Clean native Win32 desktop notifications (`Shell_NotifyIconW`) with QuickShot branding and embedded PE icon/version metadata.
  - Native Win32 automatic updater (`latest.yml` + Windows CNG SHA-512 verification) with tray menu controls, Options → Software Updates card, and seamless silent install & relaunch to tray.
  - System tray daemon with versioned hover tooltip and low-level keyboard hook (`WH_KEYBOARD_LL`) for `PrintScreen` and `Shift+PrintScreen` instant fullscreen capture.
