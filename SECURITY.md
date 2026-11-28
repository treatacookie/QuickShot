# Security Policy & Architecture — QuickShot

**Last Updated:** November 26, 2026

Screen capture utilities operate with access to sensitive desktop display content. QuickShot is engineered from the ground up with a strict local-first, zero-telemetry security model.

---

## 1. Security Architecture Overview

### 1.1 Zero Background Clipboard Snooping
- QuickShot **never monitors, reads, polls, or intercepts** your system clipboard.
- The clipboard subsystem (`arboard`) is accessed **strictly on-demand** when you explicitly trigger a copy action (`Ctrl+C`, `Enter`, or clicking the Copy icon).
- Captured images and annotated bitmaps are never written to any background clipboard history or logging daemon.

### 1.2 Volatile RAM Local-First Guarantee
- When you press `PrintScreen` or `Ctrl+Alt+S`, the frozen screen pixels and annotations reside **exclusively in volatile process RAM**.
- If you cancel the capture (`Esc` or Right-Click), the frame buffer is immediately dropped and zeroed by Rust's RAII memory management.
- QuickShot **never writes hidden scratch files, crash dump logs, or temporary image dumps to disk** without your explicit confirmation — even the built-in **Print (`Ctrl+P`)** workflow streams pixels directly from volatile RAM to the Windows GDI print spooler with zero `%TEMP%` files.
- Screenshots are saved to disk (`~/Pictures/Screenshots/` or custom file path) **only** when you explicitly press Save (`Ctrl+S`) or Quick Save (`Ctrl+Shift+S`).

### 1.3 Zero Telemetry & Cryptographically Verified Updates (`SHA-512`)
- QuickShot contains **zero telemetry, analytics SDKs, crash report uploaders, or cloud capture uploads**.
- Every release publishes a `latest.yml` manifest containing the exact Base64 `sha512` digest of `QuickShot-Setup-vX.Y.Z-x64.exe`.
- When checking for updates (automatically every 6 hours if enabled, or manually via **Check for Updates…**), QuickShot fetches `latest.yml` strictly over HTTPS via Windows native WinHTTP (`winhttp.dll`), verifies the downloaded installer's SHA-512 digest using Windows CNG (`bcrypt.dll`), and **aborts immediately without writing or executing the file** if the digest does not match.
- Automatic update checks can be disabled anytime in **Options → Software Updates**.
- The optional **"Search similar images on Google" (`Ctrl+G`)** action is strictly opt-in on explicit click: it encodes that single selection in RAM (no temp files, no third-party public image host) and POSTs it directly over HTTPS to `https://lens.google.com/v3/upload` via native WinHTTP to open the live visual search results in your browser (falling back automatically to local clipboard copy + `https://www.google.com/?olud` if unreachable). If you never click the Google button, zero screenshot pixels ever leave your PC.

### 1.4 Zero Listening Local Network Ports
- Unlike web-based or Electron capture utilities that run internal HTTP servers, QuickShot **opens zero TCP or UDP listening ports**.
- Other local processes or browser tabs on the computer cannot query or communicate with QuickShot over `localhost`.

### 1.5 Cryptographic Binary Integrity (`SHA-256`) & Zero External Runtime Dependencies
- Every published release on [`treatacookie/QuickShot`](https://github.com/treatacookie/QuickShot/releases/latest) is built in a clean-room Windows CI environment and includes a cryptographic `SHA256SUMS.txt` manifest.
- Both `QuickShot.exe` (compiled with static MSVC CRT linking) and the NSIS Setup installer depend **exclusively on built-in Windows OS DLLs** — zero `VCRUNTIME140.dll`, zero bundled third-party DLLs, and an embedded `asInvoker` Windows Application Manifest (no Administrator privileges required).
- Users and enterprise administrators can verify package authenticity before running installations:
  ```powershell
  Get-FileHash -Algorithm SHA256 .\QuickShot-Setup-v0.8.7-x64.exe
  ```

---

## 2. Supported Versions

Security updates and patches are distributed automatically via the built-in background updater and published to the latest release:

| Version | Supported |
| :--- | :--- |
| **`0.8.x` (Latest Release)** | ✅ Supported |
| `< 0.8.0` | ❌ Please upgrade to the latest release |

---

## 3. Reporting a Vulnerability

If you discover a potential security vulnerability in QuickShot, please report it responsibly:

1. **Private Reporting:** Open an issue marked as a private security advisory on GitHub: [https://github.com/treatacookie/QuickShot/security/advisories](https://github.com/treatacookie/QuickShot/security/advisories).
2. **Details to Include:**
   - Affected version and OS environment.
   - Proof of concept or reproduction steps.
   - Potential impact assessment.
3. **Response Timeline:** We will acknowledge receipt of reports within 48 hours and provide a remediation timeline.
