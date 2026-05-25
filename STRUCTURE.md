# 📁 Al‑Fatihah Analysis System – Structure

> **File & Code Structure Reference** for the Al‑Fatihah interactive learning app.  
> Covers the directory layout, HTML/CSS/JS anatomy, class naming, and relationships.

---

## 1. Project Tree

```
al-fatihah/
├── index.html                  # Main dashboard (tabs + all ayat + themes)
├── al_fatihah_ayat_1.html      # Ayat 1 – Basmalah
├── al_fatihah_ayat_2.html      # Ayat 2 – Al‑Hamdulillah
├── al_fatihah_ayat_3.html      # Ayat 3 – Ar‑Rahman Ar‑Rahim
├── al_fatihah_ayat_4.html      # Ayat 4 – Maliki Yawmid‑Din
├── al_fatihah_ayat_5.html      # Ayat 5 – Iyyaka Na‘budu
├── al_fatihah_ayat_6.html      # Ayat 6 – Ihdina’s‑Sirat
├── al_fatihah_ayat_7.html      # Ayat 7 – Siratal‑Ladhina…
├── SKILL.md                    # Pedagogical reference & system skills
├── DESIGN.md                   # Visual design system
├── ARCHITECTURE.md             # Technical architecture
├── STRUCTURE.md                # This file
```

---

## 2. HTML Document Anatomy (All Files)

Each file is a standalone HTML5 page. Below is the skeleton used across all ayat files.

### 2.1 `<head>` Section

```html
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Al-Fatihah Ayat X - Analisis Tajwid Lengkap</title>
    <!-- Font: Arabic + monospace -->
    <link href="https://fonts.googleapis.com/css2?family=Scheherazade+New:wght@400;700&display=swap" rel="stylesheet">
    <style>
        /* CSS variables + layout (see Section 4) */
    </style>
</head>
```

### 2.2 `<body>` Structure

```html
<body class="light">  <!-- or dark / coffee -->
    <!-- Theme bar (LTR) -->
    <div class="theme-bar">
        <button class="theme-btn" id="theme-light">☀️</button>
        <button class="theme-btn" id="theme-dark">🌙</button>
        <button class="theme-btn" id="theme-coffee">☕</button>
    </div>

    <!-- Header -->
    <h1>📖 Surah Al-Fatihah – Ayat X</h1>
    <p class="subtitle">Analisis Tajwid · Makhraj · Sifat Huruf</p>

    <!-- Legend -->
    <div class="legend"> ... </div>

    <!-- Full Arabic Verse -->
    <div class="ayat-penuh"> ... </div>

    <hr>

    <!-- Kalimah-by-Kalimah Analysis -->
    <h2>🔍 Analisis Setiap Kalimah</h2>

    <!-- Repeated for each word -->
    <div class="kalimah-group">
        <div class="kalimah-box">  <!-- Tajwid -->
            <div class="box-title">📐 TAJWID</div>
            <ul class="tajwid"> ... </ul>
        </div>
        <div class="makhraj-box">  <!-- Makhraj -->
            <div class="box-title">🗣️ MAKHRAJ</div>
            <ul class="makhraj"> ... </ul>
        </div>
        <div class="sifat-box">    <!-- Sifat -->
            <div class="box-title">📝 SIFAT</div>
            <ul class="sifat"> ... </ul>
        </div>
        <!-- Arabic word + meaning (full width row) -->
        <div style="width:100%; text-align:center;">
            <div class="arab-kalimah"> ... </div>
            <div class="makna"> ... </div>
        </div>
    </div>
    <!-- ... end of kalimah-group ... -->

    <!-- Full translation -->
    <div class="terjemahan-penuh">✨ Terjemahan: ...</div>

    <hr>
    <p class="footnote"> ... </p>

    <!-- JavaScript (theme switching) -->
    <script> ... </script>
</body>
```

---

## 3. Dashboard `index.html` Specifics

The index aggregates all seven ayahs. Its key differences are:

- **Tab navigation** added between the header and content area.
- **Content area** wraps all ayat sections.
- Each ayat is placed in a `.ayat-content` div with an id `ayat-{n}`.
- Tabs are `<button>` elements with `data-ayat` attributes.
- JavaScript controls tab visibility (only one `active` at a time).

The index contains **full inline content** of all ayat (duplicated from the individual files) to avoid loading or iframes. This is a deliberate trade‑off for zero‑dependency delivery.

---

## 4. CSS Architecture

### 4.1 Class Naming Convention

- **Global layout**: `.theme-bar`, `.ayat-penuh`, `.terjemahan-penuh`, `.legend`, `.footnote`
- **Tab system (index)**: `.tabs`, `.tab-btn`, `.content-area`, `.ayat-content`
- **Analysis group**: `.kalimah-group`
- **Analysis boxes**: `.kalimah-box`, `.makhraj-box`, `.sifat-box`
- **Box headers**: `.box-title`
- **List content**: `.tajwid`, `.makhraj`, `.sifat`
- **Word display**: `.arab-kalimah`, `.makna`

All classes are lowercase with hyphens. No BEM or complex nesting is used; simplicity is prioritized.

### 4.2 CSS Custom Properties

All colours, spacing, and font stacks are stored in CSS variables under `:root`. Themes override these variables using body class selectors.

Core variable set:

| Variable | Usage |
|----------|-------|
| `--bg`, `--bg-card` | Page and card backgrounds |
| `--text`, `--accent` | Text colour and highlight |
| `--tab-bg`, `--tab-active`, `--tab-active-text` | Tab button states |
| `--border`, `--shadow` | Borders and box shadows |
| `--tajwid-color`, `--makhraj-color`, `--sifat-color` | Accent colours for analysis boxes |
| `--arab-font`, `--ui-font` | Font stacks |

### 4.3 Box Differentiation

The three analysis boxes share base styles but are distinguished by:

- A 3px solid top border in their theme‑dependent colour.
- A `.box-title` heading with matching colour.
- List items (`.tajwid`, `.makhraj`, `.sifat`) coloured accordingly.

No extra CSS classes are needed; the box type is defined by the container class (e.g., `.makhraj-box`), and its children inherit the styling context.

---

## 5. JavaScript Structure

All interactivity is handled by **inline `<script>` blocks** at the bottom of each file.

### 5.1 Theme Switching (All Pages)

```javascript
const body = document.body;
const lightBtn = document.getElementById('theme-light');
const darkBtn = document.getElementById('theme-dark');
const coffeeBtn = document.getElementById('theme-coffee');

function setTheme(theme) {
    body.classList.remove('dark', 'coffee', 'light');
    body.classList.add(theme);
    localStorage.setItem('alfatihah-theme', theme);
}

lightBtn.addEventListener('click', () => setTheme('light'));
darkBtn.addEventListener('click', () => setTheme('dark'));
coffeeBtn.addEventListener('click', () => setTheme('coffee'));

// Load saved theme on page load
const savedTheme = localStorage.getItem('alfatihah-theme');
if (savedTheme) setTheme(savedTheme);
else setTheme('light');
```

### 5.2 Tab Switching (Index Only)

```javascript
const tabButtons = document.querySelectorAll('.tab-btn');
const ayatContents = document.querySelectorAll('.ayat-content');

tabButtons.forEach(btn => {
    btn.addEventListener('click', () => {
        const ayatNumber = btn.getAttribute('data-ayat');
        tabButtons.forEach(b => b.classList.remove('active'));
        ayatContents.forEach(div => div.classList.remove('active'));
        btn.classList.add('active');
        document.getElementById(`ayat-${ayatNumber}`).classList.add('active');
    });
});
```

State is handled entirely by `active` class toggles. No libraries, no frameworks.

---

## 6. Content Duplication Management

- **Individual files** are the source of truth for each ayah’s analysis.
- **`index.html`** mirrors that content inside `<div class="ayat-content" id="ayat-X">`.
- Updates must be applied to both locations.

To ease maintenance in the future, a simple build script could be introduced, but for the current static project, manual duplication is acceptable due to the small size and infrequent changes.

---

## 7. Naming & ID Rules

- **Ayat IDs**: `ayat-1` through `ayat-7` (used as `id` attributes on content divs and as `data-ayat` values on tab buttons).
- **Theme buttons**: `theme-light`, `theme-dark`, `theme-coffee`.
- **No ID conflicts** across files.
- **Class names** are deliberately generic within the project (no risk of collision in this isolated context).

---

## 8. Relationships Between Files

```
index.html
  ├── contains all ayat content (from individual files)
  ├── uses tab buttons to show/hide ayat sections
  └── shares identical CSS and JS for theming

al_fatihah_ayat_1.html  (standalone, self‑contained)
al_fatihah_ayat_2.html  (standalone)
...
al_fatihah_ayat_7.html  (standalone)

SKILL.md       – references the system as a whole
DESIGN.md      – describes the visual rules used across all pages
ARCHITECTURE.md – describes the technical structure used across all pages
STRUCTURE.md   – this file
```

No runtime dependencies between files. They share the same design and data but operate independently.

---

*Structure reference for maintainers and contributors of the Al‑Fatihah Analysis System.*  
📁
```
