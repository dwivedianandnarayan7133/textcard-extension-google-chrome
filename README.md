# TextCard – Text to Postcard Chrome Extension

> Select any text on a webpage → generate a beautiful, shareable postcard image instantly.

---

## Features

- 🖱️ **Floating button** appears near any selected text (3+ characters)
- 🃏 **Beautiful postcard** with domain, timestamp, and branding
- 🎨 **5 themes** – Dark Galaxy, Light, Sunset, Ocean, Forest
- ⬇️ **Download as PNG** (2× retina quality)
- 📋 **Copy to clipboard** (paste anywhere)
- ⌨️ **Keyboard shortcut** – `Alt+P`
- 🖱️ **Right-click context menu** → "Generate Postcard"
- ⚙️ **Settings popup** – custom branding name, default theme
- 🔒 **Shadow DOM isolation** – zero style conflicts with host pages
- ✅ Manifest V3 compliant

---

## Installation (Developer / Unpacked)

1. Open Chrome and navigate to `chrome://extensions/`
2. Enable **Developer mode** (top-right toggle)
3. Click **"Load unpacked"**
4. Select the `textcard-extension/` folder
5. The extension icon appears in the toolbar — pin it for easy access

---

## Project Structure

```
textcard-extension/
├── manifest.json          ← MV3 manifest
├── background.js          ← Service worker (context menu, keyboard shortcuts)
├── content.js             ← Injected UI (floating button, modal, postcard)
├── popup.html             ← Settings popup
├── popup.js               ← Settings logic
├── popup.css              ← Settings styles
├── lib/
│   └── html2canvas.min.js ← Bundled (no CDN dependency)
└── icons/
    ├── icon16.png
    ├── icon32.png
    ├── icon48.png
    └── icon128.png
```

---

## Usage

### Method 1 – Floating Button (Primary)
1. Select any text on any webpage
2. A **"Generate Postcard"** button floats near the selection
3. Click it → postcard modal opens
4. Pick a theme, then **Download PNG** or **Copy to Clipboard**

### Method 2 – Keyboard Shortcut
1. Select text
2. Press **`Alt+P`**
3. Postcard modal opens

### Method 3 – Right-Click Context Menu
1. Select text
2. Right-click → **"🃏 Generate Postcard"**

---

## Postcard Layout

```
┌─────────────────────────────────────┐
│ github.com                    ───── │  ← domain (top-left)
│                                 ┌─┐ │
│  "                              │📄│ │  ← stamp decoration
│                                 └─┘ │
│  [Selected text displayed here      │
│   with clean line wrapping and      │
│   elegant typography]               │
│                                     │
│ ─────────────────────────────────── │
│ 🕐 26 Mar 2026 • 10:45 AM  TextCard │  ← meta (bottom)
└─────────────────────────────────────┘
```

---

## Settings (Extension Popup)

| Setting | Default | Description |
|---------|---------|-------------|
| Branding name | `TextCard` | Shows in bottom-right of every postcard |
| Default theme | `Dark Galaxy` | Theme applied on first open |

---

## Themes

| Theme | Description |
|-------|-------------|
| 🌌 Dark Galaxy | Deep purple/blue gradient (default) |
| ☀️ Light | Clean white/grey minimal |
| 🌅 Sunset | Dark rose/crimson |
| 🌊 Ocean | Deep navy/blue |
| 🌿 Forest | Dark emerald green |

---

## Technical Notes

- All injected UI lives in **Shadow DOM** → no CSS conflicts
- **html2canvas 1.4.1** is bundled locally (no network request)
- Images exported at **2× scale** (retina quality)
- Preferences stored in `chrome.storage.sync` (synced across Chrome profiles)
- Service worker is `"type": "module"` for clean ES module support

---

## Permissions

| Permission | Reason |
|------------|--------|
| `activeTab` | Access current tab info |
| `scripting` | Inject content script on-demand (context menu) |
| `storage` | Save user preferences |
| `contextMenus` | Right-click "Generate Postcard" |
| `clipboardWrite` | Copy postcard image to clipboard |
