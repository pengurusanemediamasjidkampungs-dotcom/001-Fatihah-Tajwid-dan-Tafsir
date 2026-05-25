# 🎨 Al‑Fatihah Analysis System – Design Documentation

> **Design System & Visual Language** for the interactive web app analysing Surah Al‑Fatihah (Tajwid, Makhraj, Sifat, Meaning).  
> *Version 1.0 – Lightweight, RTL, Theme‑Aware*

---

## 🧩 Design Philosophy

- **Minimalist & Focused** – Every pixel serves the content. No external CSS frameworks; pure HTML + custom CSS.
- **Mobile‑First** – Layouts adapt from small screens to wide desktops using flexbox wrapping.
- **Accessible** – High contrast, clear typographic hierarchy, and semantic HTML.
- **Cultural Context** – Right‑to‑left (RTL) layout to honour Arabic script, with LTR elements where needed (e.g., theme bar).
- **Modular** – Each ayah is self‑contained (`al_fatihah_ayat_X.html`). The dashboard (`index.html`) aggregates all ayahs with tabbed navigation.

---

## 🏗️ Information Architecture

### Page Structure
1. **Header**: Title, subtitle, theme‑toggle buttons.
2. **Legend**: Coloured dots indicating the three analytical layers (Tajwid, Makhraj, Sifat).
3. **Ayat Penuh** (Full verse): Large Arabic script in the centre.
4. **Kalimah Group** (per word analysis): A horizontal flex row containing three side‑by‑side boxes, followed by the Arabic word and its meaning.
5. **Terjemahan Penuh** (Full translation): A callout box with the complete Malay translation.
6. **Footer**: A subtle line and footnote.

### Navigation (Index only)
- **Tab Bar**: Seven tab buttons, one for each ayah. Active tab has a solid background colour.
- **Content Area**: Only one ayah section is displayed at a time.

---

## 🎨 Colour System

Three themes are provided, each with distinct CSS variables.

| Role               | Light Theme                | Dark Theme                 | Coffee Theme               |
|--------------------|----------------------------|----------------------------|----------------------------|
| Background         | `#ffffff`                  | `#1e1e1e`                  | `#f5efe0`                  |
| Card Surface       | `#fafafa`                  | `#2a2a2a`                  | `#fff8f0`                  |
| Text               | `#1e1e1e`                  | `#e0e0e0`                  | `#4a3728`                  |
| Accent (Headings, Borders) | `#2c3e50`          | `#a0c4ff`                  | `#6f4e37`                  |
| Tajwid Color       | `#b34b4b` (soft red)      | `#ff8c8c` (light red)     | `#9c4f4f` (muted brick)    |
| Makhraj Color      | `#2980b9` (cool blue)     | `#5dade2` (soft blue)     | `#3a6b8c` (deep blue)      |
| Sifat Color        | `#8e44ad` (purple)        | `#c39bd3` (light purple)  | `#7b4f8a` (dusty purple)   |
| Tab Background     | `#e0e0e0`                  | `#3a3a3a`                  | `#e7d7c1`                  |
| Active Tab         | `#2c3e50`                  | `#a0c4ff`                  | `#6f4e37`                  |
| Active Tab Text    | `#ffffff`                  | `#1e1e1e`                  | `#fff8f0`                  |

The colour variables are defined in `:root` and overridden in `body.dark` / `body.coffee`. This ensures a seamless switch without flickering.

---

## 🔤 Typography

- **Arabic Script**: `'Scheherazade New'`, `'Traditional Arabic', serif` – loaded from Google Fonts. Used for the full verse and the per‑word Arabic text.
- **UI & Labels**: `'Courier New', Courier, monospace` – gives a technical, structured feel for hukum, makhraj, sifat lists and tab buttons.
- **System Font Fallback**: `'Segoe UI', Tahoma, Geneva, Verdana, sans-serif` – applied to body for non‑Arabic text like translations and headings.

### Type Scale

| Element              | Font Size (approx) | Weight   |
|----------------------|-------------------|----------|
| Main Title (`h1`)    | `1.8rem`          | bold     |
| Subtitle             | `0.9rem`          | normal   |
| Full Ayah            | `2.8em – 3em`     | normal   |
| Arabic per word      | `2.2em`           | normal   |
| Meaning (makna)      | `0.85em – 0.9em`  | bold     |
| Hukum/Makhraj/Sifat  | `0.7em`           | bold     |
| Translation box      | `1.1rem – 1.2rem` | bold     |

---

## 📐 Layout & Grid

### Master Layout (RTL)
```text
┌──────────────────────────────────────┐
│          Theme Toggle (LTR)          │
│          Title + Subtitle            │
│          Legend (coloured dots)      │
│          [Tab Bar] (index only)      │
├──────────────────────────────────────┤
│          Full Ayah (Arabic)          │
├──────────────────────────────────────┤
│     ╔═════════╦═════════╦═════════╗  │
│     ║ TAJWID  ║ MAKHRAJ ║  SIFAT  ║  │
│     ║  box    ║  box    ║  box    ║  │
│     ╚═════════╩═════════╩═════════╝  │
│        Arabic Word + Meaning         │
├──────────────────────────────────────┤
│     ... (next kalimah group) ...     │
├──────────────────────────────────────┤
│        Full Translation Box          │
├──────────────────────────────────────┤
│        Footer / Divider              │
└──────────────────────────────────────┘
```

### Kalimah Group
Each word is analysed in a `div.kalimah-group` that is a `flex` container:
- 3 analysis boxes (Tajwid, Makhraj, Sifat) side by side on wide screens.
- They wrap below each other on narrow screens (mobile).
- Below them, a full‑width row shows the Arabic word and its Malay meaning.

### Dimensions & Spacing
- **Max width of analysis boxes**: `180px` (prevents overly long lines).
- **Minimum width**: `140px`.
- **Gap between boxes**: `10px`.
- **Section gap**: `15px` between each `kalimah-group`.
- **Border radius**: `8px` for cards, `0.8rem` for translations.
- **Box shadow**: subtle (`rgba(0,0,0,0.06)` in light) to lift cards.

---

## 🧩 Component Library

### 1. Theme Toggle Buttons
- Circular buttons with emoji icons (☀️🌙☕).
- Positioned in a top bar with `direction: ltr`.
- On click, they add/remove CSS classes on `<body>` and store preference in `localStorage`.

### 2. Tab Bar (Index)
- Horizontal flex row of buttons.
- Active tab has contrasting background and white (or dark) text.
- All tabs are rounded (`border-radius: 0.5rem`).

### 3. Analysis Boxes
- Three variants: `.kalimah-box`, `.makhraj-box`, `.sifat-box`.
- Each has a top colour border (3px) to quickly distinguish them.
- Heading (`.box-title`) with an icon (📐 / 🗣️ / 📝) and a dashed bottom border.
- List of items (`.tajwid`, `.makhraj`, `.sifat`) with tight line‑height.

### 4. Ayat Penuh
- Large `font-size` (2.8‑3em) to make the verse stand out.
- No extra decoration – pure Arabic calligraphy.

### 5. Translation Box
- A highlighted container with a right border (4px solid accent colour).
- Background is slightly different from card background to draw attention.

### 6. Legend
- A flex row of colour indicators (small squares) and labels.
- Helps users unfamiliar with the three‑colour system.

---

## 🖱️ Interaction & States

| Element            | Interaction | Visual Feedback |
|--------------------|------------|-----------------|
| Theme buttons      | click      | `transform: scale(1.1)` + theme change |
| Tab buttons        | click      | background fill toggle (`.active` class) |
| Analysis boxes     | none       | static, read‑only |
| `localStorage`     | auto‑save  | theme persists on reload |

No hover effects on analysis boxes to keep the focus on reading.

---

## 📱 Responsive Design

- All containers use `flex-wrap: wrap` and `justify-content: center`.
- Analysis boxes stack vertically on small screens (`max-width` and `min-width` ensure they don't overflow).
- The full ayah uses `em` units for scalability; on mobile, it is still legible.
- Tabs wrap into multiple rows if needed.
- Theme bar stays in the top‑right corner even on RTL layouts.

Breakpoints are not explicitly used; the flex wrapping handles most cases. For extremely small screens (<= 320px), boxes may become a single column, which is acceptable.

---

## ♿ Accessibility

- Sufficient colour contrast ratios in all themes (verified against WCAG AA).
- Buttons have `title` attributes for screen readers.
- All text is real text (not images), allowing screen‑reader access.
- `lang="ms"` and `dir="rtl"` are set appropriately.
- The system uses semantic HTML (`<h1>`, `<h2>`, `<ul>`, `<button>`).

---

## 🔧 Customisation Guide

- To change colours, modify the CSS variables in the three theme blocks.
- To change fonts, replace the font stack in the respective variables (`--arab-font`, `--ui-font`).
- To add a new theme, duplicate the `body.coffee` block and create a new CSS class, then add a button in the theme bar and extend the JavaScript logic.

---

## 📦 Dependencies

- **Zero external JavaScript libraries**.
- **One external font**: `Scheherazade New` from Google Fonts (optional fallback to system Arabic fonts).
- No icons other than emoji.

---

*Design document prepared for developers and maintainers of the Al‑Fatihah Analysis System.*  
🌙
```
