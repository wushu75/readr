# READR – Reader Mode & PDF Export

![Manifest](https://img.shields.io/badge/Manifest-V3-blue)
![Version](https://img.shields.io/badge/version-1.2.0-6c63ff)
![Privacy](https://img.shields.io/badge/privacy-no%20data%20collected-green)

**Clean page, one click.** A fast, privacy-first reader-mode Chrome extension that turns any cluttered article into a calm, distraction-free reading view — and (with Pro) exports it as a high-quality PDF that works on every site, even strict ones like Wikipedia.

Everything runs locally in your browser. No accounts, no tracking, no servers.

> **[⭐ Install from the Chrome Web Store →](https://chromewebstore.google.com/detail/acpeognnfhdbfdmdpkfbjgppjpgpekia)**

---

## Features

### Free
- **Distraction-free reader view** on any website — ads, popups, autoplay, and cookie banners fall away, leaving just the article.
- **Dark mode & light theme** for comfortable reading.
- **Adjustable font size and line width.**
- Original page is untouched — press **ESC** to return to it any time.

### Pro — $19.99 one-time, no subscription
- **PDF export** — save any article as a high-quality PDF that keeps your reading style (headings, images, selectable text). Generated privately on your device; works on strict-CSP sites. Not the browser's generic print output.
- **Cross-device reading sync** — pick up where you left off on any computer.
- **Auto-open** reader mode on the sites you choose.
- **Recent reads** history.

---

## How it works

READR extracts the readable content of a page and renders it in a clean, isolated overlay.

- **Extraction** uses Mozilla's [Readability.js](https://github.com/mozilla/readability) (the engine behind Firefox Reader View) on a *clone* of the page, with a lightweight fallback extractor for pages it can't parse. The live page is never modified.
- **Rendering** happens in a full-screen overlay (`all: initial` isolation so host-page styles can't bleed in), themed and sized via CSS classes.
- **PDF export** is generated with [jsPDF](https://github.com/parallax/jsPDF) directly from the extracted text — *not* by rasterizing the page. This is deliberate: page-rasterization (html2canvas) is silently blocked by strict site Content-Security-Policies (Wikipedia, GitHub, news sites) and produces blank output. Text rendering is CSP-independent, works everywhere, and keeps text selectable.
- **Payments** are handled by [ExtensionPay](https://extensionpay.com) (Stripe under the hood) — no backend and no license keys. The extension checks `extpay.getUser().paid`.
- **State** (settings, Pro status, reading history) lives in `chrome.storage.sync`, so it follows the user across devices.

---

## Project structure

```
readr/
├── manifest.json           # MV3 config, permissions
├── Readability.js          # Mozilla reader engine (vendored)
├── contentScript.js        # extraction, overlay, PDF export, prompts
├── overlay.css             # reading overlay styles (scoped)
├── popup.html/.css/.js     # toolbar popup: settings + Pro
├── service_worker.js       # background: routing, lib injection, ExtPay
├── privacy.html            # privacy policy
├── ExtPay.js               # ExtensionPay SDK (see note below)
├── vendor/
│   └── jspdf.umd.min.js    # PDF engine (lazy-loaded)
└── icons/                  # 16 / 48 / 128 px
```

---

## Development

No build step — it's vanilla JavaScript loaded directly by Chrome.

1. Clone the repo.
2. Add the payment SDK: download **ExtPay.js** from [ExtensionPay](https://extensionpay.com) and place it in the project root. *(Kept out of the repo — see Licensing.)*
3. Go to `chrome://extensions/`, enable **Developer mode**, click **Load unpacked**, and select the folder.
4. In dev mode, ExtensionPay runs in **test mode**, so you can test the payment flow without real charges.

To package for the Web Store, zip the **contents** of the folder (so `manifest.json` is at the zip root), including `vendor/` and `icons/`.

---

## Privacy

READR collects no data. There is no analytics, no tracking, and no backend that sees what you read — extraction and PDF generation happen entirely on your device. Payment is processed by Stripe (via ExtensionPay), which only receives what's needed to complete a purchase.

Full policy: <https://wushu75.github.io/readr/readr-privacy.html>

---

## Tech stack

Vanilla JS · Chrome Manifest V3 · [Readability.js](https://github.com/mozilla/readability) · [jsPDF](https://github.com/parallax/jsPDF) · [ExtensionPay](https://extensionpay.com)

---

## Acknowledgements & third-party licenses

- **Readability.js** — © Mozilla, Apache-2.0
- **jsPDF** — MIT
- **ExtensionPay (ExtPay.js)** — AGPL-3.0

> **Note on ExtPay.js:** it is licensed AGPL-3.0. To keep this repository under your own license without AGPL entanglement, `ExtPay.js` is **not committed** here — download it from ExtensionPay when setting up (see Development). It ships inside the packaged extension only.

---

## License

© 2026 wushu75. All rights reserved.

*(This is a source-available default that retains your rights. If you'd prefer an open-source license — MIT, Apache-2.0, etc. — replace this section and add a `LICENSE` file. Keeping ExtPay.js out of the repo, as above, avoids AGPL affecting your choice.)*

---

## Support

Questions or bug reports: **wushumaster75@gmail.com** — or open an issue on this repo.

If READR helps you, an honest review on the Chrome Web Store genuinely helps others find it. ⭐
