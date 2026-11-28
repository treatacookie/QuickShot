# Privacy Policy — QuickShot

**Effective Date:** November 2026 | **Last Updated:** November 25, 2026

## 1. Zero Data Collection

**QuickShot** is a local-first desktop screenshot utility. It does **not** include any analytics SDKs, crash reporters, usage telemetry, user accounts, or cloud upload daemons.

- **No Personal Information Collected:** We do not collect names, email addresses, hardware identifiers, or usage statistics.
- **No Automatic Cloud Uploads:** Unlike proprietary cloud-first screenshot tools that upload captures to public URLs by default, QuickShot keeps all screenshots strictly in your computer's volatile RAM, system clipboard, or the local directory you choose (defaulting to `~/Pictures/Screenshots`).

## 2. Optional External Network Requests

QuickShot makes external network connections **only** in the following two circumstances:

1. **SHA-512 Verified Update Checks (`GitHub Releases`, toggleable):**
   - When **"Auto-download & install updates"** is enabled (in **Options → Software Updates**), or when you manually click **Check for Updates…** in the system tray or Options tab, QuickShot queries `https://github.com/treatacookie/QuickShot/releases/latest/download/latest.yml` over HTTPS using Windows' built-in WinHTTP stack and downloads verified updates from GitHub Releases.
   - Standard HTTP request metadata (IP address, User-Agent `QuickShot/<version>`) is handled directly by GitHub under [GitHub's Privacy Statement](https://docs.github.com/en/site-policy/privacy-policies/github-general-privacy-statement).
   - You can disable automatic update checks at any time in **Options → Software Updates** for 100% offline operation.
2. **User-Initiated Visual Search ("Search similar images on Google"):**
   - Strictly **and only** when you explicitly click the **"Search similar images on Google" (`Ctrl+G`)** button on the horizontal toolbar:
     1. QuickShot encodes that single selected region directly in volatile RAM (no temporary disk files and no third-party public image host such as `prnt.sc` or Imgur) and transmits it over HTTPS directly to Google Lens (`https://lens.google.com/v3/upload`), then opens the returned Google Lens visual search results URL in your default web browser.
     2. Your submitted image is handled directly by Google under [Google's Privacy Policy](https://policies.google.com/privacy).
     3. If the direct upload is unavailable (for example, offline or throttled), QuickShot falls back to copying the image to your local clipboard, opening `https://www.google.com/?olud`, and showing a desktop notification so you can paste (`Ctrl+V`) manually.
     4. If you never click the Google button, zero screenshot pixels ever leave your device.
