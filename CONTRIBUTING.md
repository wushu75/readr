# Contributing to READR

Thanks for your interest in READR ✦ — feedback from people who actually use it is the single most valuable thing for the project.

> **Note:** READR is **source-available, not open-source** (see [LICENSE](LICENSE)). The code is public for transparency and reference, but it isn't licensed for reuse or redistribution. That means this repo doesn't accept code pull requests — but **bug reports, ideas, and feedback are hugely welcome** and genuinely shape what gets built.

## 🐛 Reporting a bug

The most useful thing you can do. Open an [issue](../../issues) and include:

1. **What happened** vs. what you expected.
2. **The exact page URL** where it happened (extraction and PDF issues are almost always site-specific — the URL lets me reproduce it).
3. **Which feature** — reader view, PDF export, theme/font/width, auto-open, sync.
4. **Browser + OS** (e.g. Chrome 140 on macOS).
5. A **screenshot** if it's visual.

Reader-view and PDF bugs depend heavily on the specific site, so a URL is worth more than any description.

## 💡 Requesting a feature

Open an issue describing the problem you're trying to solve (not just the solution you have in mind). "I want to highlight passages and export them" tells me more than "add highlighting." Real use cases win.

## ⭐ Other ways to help

- **Leave an honest review** on the [Chrome Web Store](https://chromewebstore.google.com/detail/acpeognnfhdbfdmdpkfbjgppjpgpekia) — it helps others find READR more than almost anything else.
- **Tell me where it breaks.** A site where the reader view or PDF misbehaves is gold.
- **Star the repo** if you find it interesting.

## Reproducing locally (for reference)

READR is vanilla JS with no build step:

1. Add `ExtPay.js` from [ExtensionPay](https://extensionpay.com) to the project root (not committed — see the README).
2. `chrome://extensions/` → **Developer mode** → **Load unpacked** → select the folder.
3. Test on freshly opened tabs (reloading the extension leaves stale scripts on already-open tabs).

## Contact

Anything not suited to a public issue: **wushumaster75@gmail.com**
