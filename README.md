# Islamic Shorts Editor

A free, browser-based editor for creating Islamic content — Qur'ān verses and Hadith — in short video and image formats for social media.

---

## Quick Start

```bash
# Clone and serve
git clone https://github.com/theaaa-studio/Islamic-Shorts-Editor.git
cd Islamic-Shorts-Editor

# Serve with Python
py -m http.server 8000    # Windows
python3 -m http.server 8000  # macOS/Linux

# Or with Node.js
npx serve -l 8000
```

Open [http://localhost:8000](http://localhost:8000)

---

## Features

| Quran Editor | Hadith Editor |
|-------------|---------------|
| Verse selection (any Surah/Ayah range) | Book selection (Bukhari, Muslim, etc.) |
| 30+ reciters with audio | Multi-language editions |
| Multi-language translations | Same design tools |
| Video export with synced audio | Image export (PNG) |

**Shared Features:**
- 🎨 Custom backgrounds (color, images, videos)
- 🖋️ Typography controls (fonts, sizes, colors)
- 📱 Aspect ratios: 9:16 (vertical), 1:1 (square)
- 🌓 Light/Dark theme (Material Design 3)
- ✅ Optional credits toggle
- 📱 Fully responsive design

---

## Project Structure

```
Islamic-Shorts-Editor/
├── index.html              # Landing page
├── quran.html              # Quran editor
├── hadith.html             # Hadith editor
│
├── assets/
│   ├── css/
│   │   ├── styles.css      # Main CSS imports
│   │   ├── variables.css   # MD3 design tokens & CSS variables
│   │   ├── base.css        # Base/reset styles
│   │   ├── layout.css      # Main layout structure
│   │   ├── landing.css     # Landing page styles
│   │   ├── panels.css      # Sidebar panels
│   │   ├── forms.css       # Form controls (MD3 buttons, inputs)
│   │   ├── preview.css     # Preview section
│   │   ├── brand.css       # Branding header
│   │   ├── theme.css       # Theme toggle styles
│   │   ├── utilities.css   # Utility classes
│   │   ├── background-panel.css  # Background panel specific
│   │   └── responsive.css  # Mobile responsive breakpoints
│   │
│   ├── html/               # HTML partials (loaded dynamically)
│   │   ├── head.html                 # Shared <head> content
│   │   ├── quran-brand.html          # Quran editor header
│   │   ├── quran-input-panel.html    # Verse selection
│   │   ├── quran-playback-panel.html # Play & export controls
│   │   ├── quran-preview.html        # Preview canvas
│   │   ├── hadith-brand.html         # Hadith editor header
│   │   ├── hadith-input-panel.html   # Hadith selection
│   │   ├── hadith-playback-panel.html# Hadith export controls
│   │   ├── hadith-preview.html       # Hadith preview canvas
│   │   ├── background-panel.html     # Background settings (shared)
│   │   ├── typography-panel.html     # Font settings (shared)
│   │   └── credits-panel.html        # Credits settings (shared)
│   │
│   ├── js/
│   │   ├── quran-app.js          # Quran editor main logic
│   │   ├── quran-html-loader.js  # Quran HTML partial loader
│   │   ├── quran-audio.js        # Audio playback & recording
│   │   ├── quran-drawing.js      # Canvas text rendering
│   │   ├── quran-metadata.js     # Surah/Ayah metadata
│   │   ├── quran-reciters.js     # Reciter list
│   │   ├── quran-translations.js # Translation editions
│   │   ├── hadith-app.js         # Hadith editor main logic
│   │   ├── hadith-html-loader.js # Hadith HTML partial loader
│   │   ├── hadith-metadata.js    # Hadith book metadata
│   │   ├── background.js         # Background management (shared)
│   │   ├── theme.js              # Theme toggle (shared)
│   │   └── utils.js              # Utility functions (shared)
│   │
│   └── background/
│       ├── background.json       # Background media list
│       └── *.jpg, *.mp4          # Media files
```

---

## CSS Architecture

Uses **Material Design 3** design system with CSS custom properties:

| File | Purpose |
|------|---------|
| `variables.css` | MD3 color tokens, elevation, typography scales |
| `forms.css` | MD3 buttons (filled, tonal, outlined), inputs, selects |
| `panels.css` | Collapsible sidebar panels |
| `responsive.css` | Mobile breakpoints (768px, 480px) |

**Key CSS Variables:**
```css
/* Colors */
--md-sys-color-primary        /* Brand green #006135 */
--md-sys-color-surface        /* Background surfaces */
--md-sys-color-on-surface     /* Text on surfaces */

/* Elevation */
--md-sys-elevation-level1     /* Card shadows */
--md-sys-elevation-level2     /* Elevated elements */

/* Shapes */
--md-sys-shape-corner-small   /* 8px */
--md-sys-shape-corner-medium  /* 12px */
```

---

## JavaScript Architecture

**Module Pattern:** Each feature is isolated in its own file.

| Module | Exports/Responsibility |
|--------|------------------------|
| `quran-app.js` | Main app logic, DOM wiring, event handlers |
| `quran-audio.js` | Audio fetch, playback, MediaRecorder |
| `quran-drawing.js` | Canvas rendering (text, backgrounds) |
| `quran-metadata.js` | Surah metadata from API |
| `background.js` | Background loading, selection, uploads |
| `theme.js` | Light/dark theme persistence |

**Data Flow (Quran Editor):**
```
User Input → metadata.js → audio.js → drawing.js → Canvas → Export
```

---

## External APIs

| Service | URL | Purpose |
|---------|-----|---------|
| AlQuran Cloud | `api.alquran.cloud` | Translations, editions |
| Quran.com | `api.quran.com` | Chapter names |
| EveryAyah | `everyayah.com` | Reciter audio (MP3) |
| Hadith API | `cdn.jsdelivr.net/gh/fawazahmed0/hadith-api` | Hadith collections |
| Google Fonts | `fonts.googleapis.com` | Typography |

---

## Adding Content

### Add Background Media

1. Add file to `assets/background/`
2. Update `assets/background/background.json`:
```json
{
  "src": "./assets/background/your-file.jpg",
  "type": "image",
  "name": "Display Name"
}
```

### Add Reciter

Edit `assets/js/quran-reciters.js`:
```javascript
"folder_name_from_everyayah",
```

### Add Font

1. Add Google Fonts link in `assets/html/head.html`
2. Add `<option>` in `assets/html/typography-panel.html`

---

## Browser Support

| Browser | Support |
|---------|---------|
| Chrome 118+ | ✅ Full |
| Edge 118+ | ✅ Full |
| Firefox | ⚠️ Limited (MediaRecorder issues) |
| Safari | ❌ Not recommended |

**Requirements:**
- HTTP server (not `file://`)
- Internet connection for APIs

---

## Export Formats

| Type | Format | Resolution | Naming |
|------|--------|------------|--------|
| Quran Video | WebM (VP9/Opus) | 1080×1920 or 1080×1080 | `Surah-{num}-{name}_Ayah-{from}-{to}_{reciter}_{timestamp}.webm` |
| Hadith Image | PNG | 1080×1920 or 1080×1080 | `{Book}_Hadith-{num}_{ratio}_{edition}_{timestamp}.png` |

**Convert to MP4:**
```bash
ffmpeg -i input.webm -c:v libx264 -c:a aac output.mp4
```

---

## Credits & Attribution

**Data Sources:**
- [EveryAyah.com](https://everyayah.com) — Quran recitations
- [Quran.com](https://quran.com) — Quran metadata
- [AlQuran Cloud](https://alquran.cloud) — Translations
- [Hadith API](https://github.com/fawazahmed0/hadith-api) — Hadith collections

---

## License

Open source. Use it to spread beneficial Islamic knowledge.

---

**Contact:** [TheAAA Portfolio](https://theaaa-studio.github.io/AAA_Personal_Portfolio/)

**May Allah accept this humble effort. Ameen.**
