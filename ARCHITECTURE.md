# 🏗️ Al‑Fatihah Analysis System – Architecture

> **Technical Architecture & System Design** for the interactive Al‑Fatihah learning app.  
> Covers code organization, data flow, theming, responsiveness, and design decisions.

---

## 1. Overview

The Al‑Fatihah Analysis System is a **client‑side only, static web application** that provides a detailed, per‑word breakdown of Surah Al‑Fatihah. It combines three linguistic layers (Tajwid, Makhraj, Sifat) with translation and tafsir, all delivered through a responsive, theme‑aware interface.

The system consists of:

- **8 static HTML files** (7 individual ayah pages + 1 dashboard index)
- **Vanilla CSS** with custom properties (variables) for theming
- **Vanilla JavaScript** for theme persistence and tab switching

No backend, no build tools, no external frameworks. The entire application can be served from any static web server or opened directly from the file system.

---

## 2. Technology Stack

| Layer          | Technology                           |
|----------------|--------------------------------------|
| **Structure**  | HTML5 semantic elements              |
| **Styling**    | CSS3, CSS Custom Properties, Flexbox |
| **Logic**      | Vanilla JavaScript (ES6+)            |
| **Fonts**      | Google Fonts (`Scheherazade New`)     |
| **Storage**    | `localStorage` for theme persistence |
| **No dependencies** | No jQuery, Bootstrap, or npm packages |

All code is hand‑written without any pre‑processors (Sass/Less) or module bundlers (Webpack/Vite). This keeps the system lightweight and easy to deploy.

---

## 3. File Structure & Responsibilities

```
project-root/
├── index.html                     # Dashboard: tabbed viewer + all ayat content
├── al_fatihah_ayat_1.html         # Standalone analysis for Ayat 1 (Basmalah)
├── al_fatihah_ayat_2.html         # Standalone analysis for Ayat 2
├── al_fatihah_ayat_3.html         # Standalone analysis for Ayat 3
├── al_fatihah_ayat_4.html         # Standalone analysis for Ayat 4
├── al_fatihah_ayat_5.html         # Standalone analysis for Ayat 5
├── al_fatihah_ayat_6.html         # Standalone analysis for Ayat 6
├── al_fatihah_ayat_7.html         # Standalone analysis for Ayat 7
├── SKILL.md                       # Knowledge & pedagogical reference
├── DESIGN.md                      # Visual design system documentation
└── ARCHITECTURE.md                # This file
```

### Responsibilities

- **`index.html`** – The hub; contains all ayat content inline (duplicated from individual files), implements tabs, theme switching, and state persistence. Acts as the main entry point for users.
- **`al_fatihah_ayat_X.html`** – Standalone, self‑contained analysis of a single ayat. Can be viewed independently or linked directly. Each file is a complete HTML document with its own styles (identical to `index.html` for consistency).
- **`.md` files** – Documentation for maintainers, educators, and developers.

The duplication of content between `index.html` and the individual ayat files is intentional to allow both modes of consumption while keeping the entire project dependency‑free.

---

## 4. Component Architecture (Logical View)

Even though the app is built with static HTML, we can abstract its logical components:

```
┌────────────────────────────────────────────┐
│              Theme Manager                  │
│  (JavaScript: setTheme, localStorage)       │
└───────────────────┬────────────────────────┘
                    │
┌───────────────────▼────────────────────────┐
│               UI Shell                      │
│  ┌──────────────────────────────────────┐  │
│  │          Header (title + theme bar)   │  │
│  ├──────────────────────────────────────┤  │
│  │          Tab Navigation (index only)  │  │
│  ├──────────────────────────────────────┤  │
│  │          Content Area                 │  │
│  │  ┌────────────────────────────────┐  │  │
│  │  │   Ayat Content (per ayah)      │  │  │
│  │  │   ┌────────────────────────┐   │  │  │
│  │  │   │   Full Verse (Arabic)   │   │  │  │
│  │  │   ├────────────────────────┤   │  │  │
│  │  │   │   Kalimah Group (word)  │   │  │  │
│  │  │   │   ┌──────┬──────┬──────┐│   │  │  │
│  │  │   │   │Tajwid│Makhraj│Sifat││   │  │  │
│  │  │   │   └──────┴──────┴──────┘│   │  │  │
│  │  │   │   Arabic word + meaning │   │  │  │
│  │  │   └────────────────────────┘   │  │  │
│  │  │   ... (repeat per word)        │  │  │
│  │  │   ┌────────────────────────┐   │  │  │
│  │  │   │  Full Translation      │   │  │  │
│  │  │   └────────────────────────┘   │  │  │
│  │  └────────────────────────────────┘  │  │
│  └──────────────────────────────────────┘  │
└────────────────────────────────────────────┘
```

### Component Breakdown

| Component | Description | HTML Representation |
|-----------|-------------|----------------------|
| **Theme Manager** | Reads/sets theme on body, saves to localStorage | JavaScript functions + `#theme-*` buttons |
| **Tab Navigation** | Toggles visibility of ayat sections | `.tabs` > `.tab-btn` buttons |
| **Ayat Content** | One section per ayah, controlled by tabs | `.ayat-content` div |
| **Kalimah Group** | Per‑word analysis unit, repeated for each word | `.kalimah-group` flex container |
| **Analysis Boxes** | Three boxes (Tajwid, Makhraj, Sifat) showing lists | `.kalimah-box`, `.makhraj-box`, `.sifat-box` |
| **Full Verse** | Large Arabic text of the entire ayah | `.ayat-penuh` |
| **Translation Box** | Malay translation of the whole ayah | `.terjemahan-penuh` |

---

## 5. Data Flow & State Management

### 5.1 Theme State

```
User clicks theme button
        │
        ▼
Button event listener invokes setTheme('light'|'dark'|'coffee')
        │
        ▼
setTheme():
  - Removes all theme classes from <body>
  - Adds the chosen class ('light', 'dark', 'coffee')
  - Saves choice to localStorage('alfatihah-theme')
        │
        ▼
CSS custom properties change → all themed elements re‑render immediately
```

On page load, `localStorage` is checked and the saved theme is applied.

### 5.2 Tab State (Index)

```
User clicks a tab button
        │
        ▼
Click listener on .tab-btn:
  - Removes .active from all tab buttons and .ayat-content divs
  - Adds .active to the clicked button and the corresponding #ayat-{n} div
```

Tab state is not persisted (always defaults to Ayat 1 on reload). This keeps navigation simple and predictable.

### 5.3 Content Data

All analysis data (text of hukum, makhraj, sifat, etc.) is **hard‑coded** directly into the HTML. There is no dynamic data loading or API. This is a deliberate choice to keep the project self‑contained and offline‑capable.

---

## 6. Theming Architecture

Theming is implemented with **CSS Custom Properties** (variables). Each theme defines the same set of variables:

```css
:root {
    --bg: ...;
    --text: ...;
    --accent: ...;
    --tajwid-color: ...;
    --makhraj-color: ...;
    --sifat-color: ...;
    --tab-bg: ...;
    --tab-active: ...;
    /* etc. */
}
```

Theme switchers add a class (`light`, `dark`, `coffee`) to the `<body>`. The classes override the variables:

```css
body.dark {
    --bg: #1e1e1e;
    ...
}
```

All styled elements reference these variables. This provides a clean, scalable way to add new themes in the future without touching existing HTML structure.

---

## 7. Responsive Design Strategy

The layout uses **CSS Flexbox** exclusively, with no media queries. The flex containers have `flex-wrap: wrap` and `justify-content: center`, which naturally:

- Align boxes in a row on wide screens
- Stack them vertically on narrow screens

Key flexible elements:

- `.kalimah-group`: `flex-wrap: wrap`; analysis boxes have `min-width: 140px` and `max-width: 180px` to avoid compression.
- `.tabs`: `flex-wrap: wrap` for the tab bar.
- Font sizes are mostly in `em` or `rem`, scaling with user preferences.

This approach provides a fluid layout that works on mobile, tablet, and desktop without complex breakpoints.

---

## 8. Content Duplication Strategy

**Problem:** We want both a dashboard (single page with all ayat) and individual ayah pages for direct sharing/printing.

**Solution:** The content of each ayah appears twice:

1. In its own `al_fatihah_ayat_X.html` file.
2. Inside the `index.html`, within `#ayat-X` divs.

This duplication is maintained manually (or with a future script). The individual pages are complete HTML documents, while the index embeds only the body content of those pages (without the shared `<head>`).

**Trade‑offs:**

- ✅ No build step or dynamic injection needed.
- ✅ Works offline, easy to deploy.
- ❌ Any update must be made in both places.

Given the stable nature of Quranic analysis content, this duplication is acceptable.

---

## 9. Performance & Accessibility

- **No JavaScript libraries** – minimal parsing and execution time.
- **Single CSS file** per page (styles in `<style>`), no external stylesheets except the optional Google Font.
- **No images** – all icons are emoji, no extra HTTP requests.
- **RTL support** – `dir="rtl"` on `<body>`, with LTR overrides for the theme toggle bar.
- **Accessibility:** Semantic HTML (`<h1>`, `<h2>`, `<ul>`, `<button>`), `title` attributes, high colour contrast.

---

## 10. Future Extension Points

The architecture supports the following enhancements:

- **Adding new surahs:** Duplicate the ayah template files, update content, and add tabs to the index.
- **Integrating audio:** Insert `<audio>` elements into the `.kalimah-group` section.
- **Print stylesheet:** Add a `@media print` block to hide UI elements and adjust fonts.
- **Build automation:** Use a simple Node.js script to inject ayah files into `index.html` at build time, eliminating manual duplication.
- **Interactive quizzes:** Extend the JavaScript to include a quiz mode that hides analysis and asks users to identify hukum/makhraj.

---

*Architecture document prepared for developers and technical maintainers of the Al‑Fatihah Analysis System.*  
📐
```
