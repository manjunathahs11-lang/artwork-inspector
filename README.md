# Artwork & Packaging Inspector — mobile PWA

A static, mobile-first progressive web app. No Python, PC, account, or server-side image processing is required. Images are handled locally in your browser.

## Features
- Upload approved master and subject artwork from Android files/photos.
- Resize subject to master dimensions and estimate small X/Y translation (±12 pixels).
- Highlight differing regions in red; view master, aligned subject, and binary difference mask.
- OCR text comparison using Tesseract.js (English) with missing/additional word lists.
- Zoom/scroll inspection; PDF, PNG and JSON exports.
- Installable PWA with manifest and service worker.

## Mobile-only deployment (recommended: GitHub Pages)
1. On your phone, open github.com and create a free account or sign in.
2. Create a **public** repository named `artwork-inspector` (public Pages repositories are visible to others; **do not upload confidential artwork**).
3. Open the repository, choose **Add file → Upload files**, and upload **the five files inside this folder** (not the ZIP): `index.html`, `app.js`, `sw.js`, `manifest.webmanifest`, `icon.svg`. On mobile, Chrome's **Desktop site** option may help expose file-upload controls. Alternatively use GitHub's web editor to create each file.
4. In repository **Settings → Pages**, set **Deploy from a branch**, branch **main**, folder **/(root)**, then Save.
5. Wait for the Pages deployment. Open `https://YOUR-USERNAME.github.io/artwork-inspector/` in Chrome on Android.
6. Chrome menu (⋮) → **Add to Home screen** / **Install app**.
7. Tap the app icon, select master and subject images, then **Compare images**. Download the report using **Download PDF report**.

**No PC is required to use or publish this app**, but GitHub's mobile browser interface can be cumbersome. Another static hosting provider supporting ZIP uploads can be used instead; it must serve the site over HTTPS to allow PWA installation.

## Requirements and caveats
- First load needs internet for Tesseract.js and jsPDF JavaScript libraries; OCR also downloads language/engine assets. Offline OCR/PDF are **not guaranteed** because third-party assets are not bundled or cached by this service worker. Visual comparison may still work after the app shell has loaded.
- Images are **not uploaded** by this application. The OCR and PDF scripts are loaded from jsDelivr CDN, so internet access and trust in that provider are required.
- Image registration handles only a small translation, not camera perspective, rotation, different crop, curved packaging, or color-profile calibration.
- OCR compares normalized word counts, **not positions**; text placement changes may be detected visually but not as an OCR text change.
- Large images are downscaled to a maximum 1200-pixel side for mobile performance; fine-print errors can be missed.
- Red regions and changed-pixel percentage are approximate. Inspect manually; do not treat this as certified quality assurance.
- For confidential artwork, consider self-hosting the JS dependencies and private deployment instead of a public repo.
