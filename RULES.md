# 📋 Al‑Fatihah Analysis System – RULES.md

> **Coding Standards & Constraints** for the Al‑Fatihah interactive learning app.  
> All contributors and maintainers must follow these rules to ensure consistency, performance, and maintainability.

---

## 1. General Principles

- **Zero external dependencies** – No JavaScript frameworks (React, Vue, jQuery), no CSS libraries (Bootstrap, Tailwind). Plain HTML, CSS, and vanilla JS only.
- **Offline‑first** – The entire site must work without internet access (except optional Google Font).
- **Static delivery** – All content is pre‑rendered. No server‑side processing required.
- **Minimal duplication** – Content duplication between `index.html` and individual ayah files is allowed but must be kept in sync manually until a build script is introduced.
- **Language** – All code comments and documentation in English (or Bahasa Melayu for content). HTML `lang="ms"`, RTL direction.

---

## 2. HTML Rules

### 2.1 Document Structure
- Every page must have a valid `<!DOCTYPE html>`.
- The `<html>` tag must include `lang="ms"` and `dir="rtl"`.
- The `<head>` must include:
  - `<meta charset="UTF-8">`
  - `<meta name="viewport" content="width=device-width, initial-scale=1.0">`
  - A descriptive `<title>` (e.g., `Al-Fatihah Ayat 1 - Analisis Tajwid Lengkap`).

### 2.2 Semantic Elements
- Use semantic HTML5 elements: `<h1>`, `<h2>`, `<h3>`, `<p>`, `<ul>`, `<li>`, `<button>`, `<div>` for layout only when necessary.
- Avoid `<span>` unless for inline styling.

### 2.3 Content Blocks
- The Arabic verse must be in a `<div class="ayat-penuh">`.
- Each word analysis group must be in a `<div class="kalimah-group">`.
- Inside each group:
  - Tajwid, Makhraj, Sifat boxes must have classes `.kalimah-box`, `.makhraj-box`, `.sifat-box` respectively.
  - Each box must have a title `<div class="box-title">` with an emoji icon (📐, 🗣️, 📝).
  - Hukum list must be `<ul class="tajwid">`, Makhraj list `<ul class="makhraj">`, Sifat list `<ul class="sifat">`.
- The full translation must be a `<div class="terjemahan-penuh">`.

### 2.4 Index‑specific Rules
- The dashboard must have a tab bar with `<button class="tab-btn">` elements, each with a `data-ayat` attribute (1‑7).
- Each ayah section must be a `<div class="ayat-content" id="ayat-X">` where X matches the tab.
- Only one ayah section and one tab button may have the `active` class at any time.

---

## 3. CSS Rules

### 3.1 Theming via Custom Properties
- All colours and theme‑dependent values must be defined as CSS custom properties in `:root` and overridden in body classes (`.light`, `.dark`, `.coffee`).
- Property names must be descriptive and prefixed with `--` (e.g., `--bg`, `--text`, `--accent`, `--tajwid-color`).
- No hard‑coded colours in components; always use variables.

### 3.2 Font Stack
- Arabic text: `font-family: var(--arab-font)` which defaults to `'Scheherazade New', 'Traditional Arabic', serif;`.
- UI text (buttons, labels, hukum lists): `font-family: var(--ui-font)` which defaults to `'Courier New', Courier, monospace;`.
- Body fallback: `'Segoe UI', Tahoma, Geneva, Verdana, sans-serif` for non‑Arabic running text.

### 3.3 Layout
- Use **Flexbox** for all component layouts. No floats, no grid.
- The `.kalimah-group` must be a flex container with `flex-wrap: wrap` and `justify-content: center`.
- Analysis boxes should have `min-width: 140px` and `max-width: 180px` to ensure they wrap cleanly.

### 3.4 Box Styling
- Each analysis box must have a 3px solid top border in its category colour:
  - Tajwid: `var(--tajwid-color)`
  - Makhraj: `var(--makhraj-color)`
  - Sifat: `var(--sifat-color)`
- List items inside boxes must have a font size of `0.7em`, bold, with a line‑height of `1.4`.
- No hover effects on analysis boxes (read‑only displays).

### 3.5 Responsive Design
- Use `em` or `rem` for font sizes, not `px`.
- No media queries; rely on flex wrapping and min/max widths to adapt to screen size.

---

## 4. JavaScript Rules

### 4.1 Theme Switching
- Theme state must be managed by a `setTheme(theme)` function that:
  - Removes `light`, `dark`, `coffee` classes from `<body>`.
  - Adds the chosen class.
  - Saves the choice to `localStorage` with key `'alfatihah-theme'`.
- On page load, check `localStorage` and apply the saved theme (default to `'light'` if none).
- Theme buttons must have IDs `theme-light`, `theme-dark`, `theme-coffee`.

### 4.2 Tab Switching (Index Only)
- Tabs must be activated by a click listener on all `.tab-btn` elements.
- On click: remove `active` class from all tabs and all `.ayat-content` divs, then add `active` to the clicked button and the corresponding `#ayat-{data-ayat}` content div.

### 4.3 General
- All scripts must be placed at the end of `<body>` (inline, no external files).
- Use `const` and `let`; no `var`.
- Use arrow functions for short callbacks, function declarations for named functions.
- No `eval()`, no inline event handlers (use `addEventListener`).

---

## 5. Content Rules

### 5.1 Arabic Text
- Must be fully vocalised with diacritics (tashkeel).
- Use UTF‑8 encoding; special characters like Alif Kecil (ـٰ) must be preserved correctly.
- In lists, letters must be presented in their independent form (e.g., `ب` not `بـ`).

### 5.2 Malay Text
- Use standard Bahasa Melayu spelling (Dewan Bahasa dan Pustaka).
- Tajwid terminology must be transliterated consistently (e.g., `Idgham`, `Izhar`, `Mad Thabi‘i`).
- Makhraj descriptions must be concise: `Halq (tengah kerongkong)`, `Lisan (hujung lidah – gusi)`.

### 5.3 Sifat Lists
- Opposite sifat must be listed in the conventional order: `Hams/Jahr`, `Syiddah/Rakhawah`, `Isti‘la’/Istifal`, `Itbaq/Infitah`, `Idzlaq/Ismat` (where applicable).
- Single sifat (if any) must be listed after the opposite pairs.

---

## 6. Naming Conventions

| Context | Convention |
|---------|------------|
| File names | `al_fatihah_ayat_X.html` (X is 1‑7), `index.html` |
| CSS classes | lowercase with hyphens (`.kalimah-group`, `.ayat-penuh`) |
| CSS variables | `--kebab-case` (e.g., `--bg-card`, `--tajwid-color`) |
| JavaScript variables/functions | camelCase (`setTheme`, `ayatNumber`) |
| HTML IDs | kebab‑case (`theme-light`, `ayat-1`) |
| Commit messages | English, past tense, concise |

---

## 7. Accessibility Constraints

- All interactive elements (buttons) must have `title` attributes.
- Colour contrast must meet WCAG AA minimum (4.5:1 for normal text, 3:1 for large text). Verify with a contrast checker.
- Do not rely solely on colour to convey information; use text labels alongside the colour dots in the legend.
- Use semantic heading hierarchy (h1, h2, h3) without skipping levels.
- Ensure the page is navigable by keyboard (tabindex is natural for buttons).

---

## 8. Performance Constraints

- No external fonts other than `Scheherazade New` (loaded from Google Fonts with `display=swap`). If offline, system Arabic fonts must suffice.
- CSS and JS must be inlined (no separate files) to reduce HTTP requests.
- No large images; emoji and CSS borders serve as UI icons.
- Total page weight of any individual ayah file should stay under 20 KB (uncompressed). Index page weight under 100 KB.

---

## 9. Quality Assurance Checklist

Before committing any changes, verify:

- [ ] HTML valid (no missing closing tags).
- [ ] CSS valid, no unused rules.
- [ ] JavaScript error‑free in browser console.
- [ ] All themes render correctly (light / dark / coffee).
- [ ] All tabs work, no content overlap.
- [ ] Arabic text displays correctly without font issues.
- [ ] RTL layout is intact; theme bar stays LTR.
- [ ] Page works when opened directly from disk (no server required).
- [ ] Content duplication between individual files and index is synchronised.

---

## 10. Contribution Guidelines

- All changes must adhere to the rules above.
- For new ayah additions (e.g., other surahs), follow the exact structure of `al_fatihah_ayat_1.html`.
- If adding new themes, only modify the CSS variable blocks; do not alter HTML structure.
- For major refactoring (e.g., introducing a build step), update `ARCHITECTURE.md` accordingly.
- Keep the `SKILL.md` educational reference up to date with any content additions.

---

*This ruleset ensures the Al‑Fatihah Analysis System remains maintainable, lightweight, and consistent across all its components.*  
📋
```
