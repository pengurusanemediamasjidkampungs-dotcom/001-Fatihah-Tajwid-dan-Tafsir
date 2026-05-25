<p align="center">
  <img src="https://img.shields.io/badge/versi-1.0-blue?style=for-the-badge" alt="Versi 1.0">
  <img src="https://img.shields.io/badge/lesen-MIT-green?style=for-the-badge" alt="Lesen MIT">
  <img src="https://img.shields.io/badge/bahasa-HTML%20%7C%20CSS%20%7C%20JS-orange?style=for-the-badge" alt="HTML+CSS+JS">
  <img src="https://img.shields.io/badge/100%25-Offline-red?style=for-the-badge" alt="100% Offline">
</p>

<h1 align="center">📖 001 – Al‑Fatihah: Tajwid dan Tafsir</h1>

<p align="center"><strong>Sistem Pembelajaran Digital Interaktif untuk Surah Al‑Fatihah</strong><br>
<em>Menggabungkan Tafsir Ibnu Kathir, Analisis Tajwid, Makhraj, Sifat Huruf, dan Makna Per‑Kata</em></p>

---

## 📑 Isi Kandungan

- [🌟 Gambaran Keseluruhan](#-gambaran-keseluruhan)
- [🎯 Lima Asas Pembelajaran Al‑Quran](#-lima-asas-pembelajaran-al-quran)
- [🗂 Struktur Projek](#-struktur-projek)
- [✨ Ciri‑Ciri Utama](#-ciri-ciri-utama)
- [🚀 Panduan Pantas](#-panduan-pantas)
- [📸 Pratonton](#-pratonton)
- [📊 Statistik](#-statistik)
- [🏗 Seni Bina Teknikal](#-seni-bina-teknikal)
- [📚 Dokumentasi](#-dokumentasi)
- [🛠 Penambahbaikan Masa Depan](#-penambahbaikan-masa-depan)
- [📜 Lesen](#-lesen)
- [🙏 Penghargaan](#-penghargaan)

---

## 🌟 Gambaran Keseluruhan

**001 – Al‑Fatihah: Tajwid dan Tafsir** adalah pakej pembelajaran digital **lengkap** untuk Surah Al‑Fatihah. Projek ini dibina bagi memudahkan umat Islam mempelajari bacaan surah paling agung dalam Al‑Quran secara mendalam, merangkumi:

| Lapisan | Penerangan |
|---------|------------|
| 📐 **Tajwid** | Hukum bacaan setiap kalimah (Idgham, Izhar, Mad, dll.) |
| 🗣️ **Makhraj** | Tempat keluar setiap huruf secara terperinci |
| 📝 **Sifat Huruf** | Sifat berlawanan dan sifat tunggal setiap huruf |
| 🈴 **Makna Per‑Kata** | Terjemahan harfiah setiap kalimah dalam Bahasa Melayu |
| 📜 **Tafsir Ibnu Kathir** | Tafsir lengkap Surah Al‑Fatihah dalam Bahasa Melayu |

Semua kandungan dihantar melalui **laman web statik** yang boleh dibuka terus tanpa pelayan (server), tanpa pemasangan, dan tanpa sambungan internet.

---

## 🎯 Lima Asas Pembelajaran Al‑Quran

Projek ini dibina berteraskan **5 tunjang utama Ilmu Tajwid** yang menjadi piawaian dalam mempelajari bacaan Al‑Quran:

| # | Asas | Pelaksanaan dalam Sistem |
|---|------|--------------------------|
| **1** | **Makhraj Huruf** | Kotak 🟦 biru pada setiap kalimah – tempat keluar setiap huruf (Jauf, Halq, Lisan, Syafatain, Khaisyum) |
| **2** | **Sifat Huruf** | Kotak 🟪 ungu – sifat berlawanan (Hams/Jahr, Syiddah/Rakhawah, dll.) & sifat tunggal (Safir, Qalqalah, dll.) |
| **3** | **Mad** | Kotak 🟥 merah (Tajwid) – jenis Mad: Thabi‘i, ‘Arid Lissukun, beserta panjang harakat |
| **4** | **Hukum Nun Mati & Mim Mati** | Dicatatkan dalam kotak Tajwid – Izhar Halqi, Idgham, Ikhfa’, dll. |
| **5** | **Waqaf & Ibtida’** | Dicatatkan – Mad ‘Arid Lissukun, Hamzatul Wasl, cara berhenti dan memulakan bacaan |

---

## 🗂 Struktur Projek

```
001-Fatihah-Tajwid-dan-Tafsir/
├── index.html                  # Papan pemuka utama (tab navigasi + 3 tema)
├── al_fatihah_ayat_1.html      # Analisis lengkap Ayat 1 (Basmalah)
├── al_fatihah_ayat_2.html      # Analisis lengkap Ayat 2
├── al_fatihah_ayat_3.html      # Analisis lengkap Ayat 3
├── al_fatihah_ayat_4.html      # Analisis lengkap Ayat 4
├── al_fatihah_ayat_5.html      # Analisis lengkap Ayat 5
├── al_fatihah_ayat_6.html      # Analisis lengkap Ayat 6
├── al_fatihah_ayat_7.html      # Analisis lengkap Ayat 7
├── API_SPEC.md                 # Spesifikasi endpoint & skema data
├── ARCHITECTURE.md             # Dokumentasi seni bina teknikal
├── DESIGN.md                   # Dokumentasi sistem reka bentuk visual
├── RULES.md                    # Piawaian pengekodan & kekangan
├── SKILL.md                    # Rujukan pedagogi & pengetahuan sistem
├── STRUCTURE.md                # Rujukan struktur fail & kod
└── README.md                   # Fail ini
```

---

## ✨ Ciri‑Ciri Utama

### 🌐 Papan Pemuka Interaktif (`index.html`)
- **7 tab** untuk navigasi pantas antara ayat
- Semua 7 ayat dimuatkan dalam satu halaman – tiada muat semula
- **3 tema warna** boleh tukar dengan satu klik: ☀️ Terang · 🌙 Gelap · ☕ Kopi
- Tema disimpan secara automatik dalam `localStorage`

### 🔍 Analisis Setiap Kalimah
Setiap perkataan dalam Surah Al‑Fatihah dianalisis dalam **tiga kotak sejajar**:

```
┌──────────────┬──────────────┬──────────────┐
│  📐 TAJWID   │  🗣️ MAKHRAJ  │  📝 SIFAT    │
│  (Merah)     │  (Biru)      │  (Ungu)      │
├──────────────┼──────────────┼──────────────┤
│ • Hukum 1    │ • Tempat     │ • Sifat      │
│ • Hukum 2    │ • Tempat     │ • Sifat      │
└──────────────┴──────────────┴──────────────┘
│       TEKS ARAB (BESAR)      │
│       Makna Per-Kata (Hijau) │
```

### 📱 Responsif & Ringan
- **Mobile‑first** – susun atur fleksibel sesuai semua saiz skrin
- Tiada framework luaran – HTML + CSS + Vanilla JS sahaja
- Jumlah saiz halaman individu di bawah **20 KB**
- Serasi dengan semua pelayar moden

### 📖 Halaman Ayat Individu
Setiap fail `al_fatihah_ayat_X.html` boleh dibuka secara berasingan – sesuai untuk:
- Kongsi pautan terus ke analisis ayat tertentu
- Cetakan (print) untuk rujukan fizikal
- Semakan pantas tanpa membuka papan pemuka

---

## 🚀 Panduan Pantas

### Cara Menggunakan

1. **Buka dalam pelayar web:**
   - **Papan pemuka:** Buka `index.html`
   - **Ayat individu:** Buka mana-mana `al_fatihah_ayat_X.html`

2. **Navigasi:**
   - Klik tab `Ayat 1` hingga `Ayat 7` di bahagian atas
   - Setiap tab memaparkan analisis lengkap ayat tersebut

3. **Tukar tema:**
   - Klik ikon ☀️, 🌙, atau ☕ di penjuru kanan atas
   - Tema disimpan secara automatik

### Cara Pasang (Deploy)

Tiada pemasangan diperlukan. Projek ini boleh digunakan melalui:

| Kaedah | Langkah |
|--------|---------|
| **Buka terus** | Muat turun repo, buka mana-mana fail `.html` dengan pelayar |
| **GitHub Pages** | Dayakan GitHub Pages pada branch `main`, folder root |
| **Netlify / Vercel** | Seret (drag) folder projek ke dashboard |
| **Mana-mana pelayan web** | Salin semua fail ke direktori root pelayan |

### Keperluan Sistem

- ✅ Pelayar web moden (Chrome, Firefox, Safari, Edge – versi terkini)
- ✅ Tiada pelayan diperlukan
- ✅ Tiada pangkalan data
- ✅ Tiada sambungan internet (kecuali untuk fon Google – mempunyai fallback)

---

## 📸 Pratonton

### Papan Pemuka – Tema Terang (Light)
Susun atur RTL yang bersih dengan tab navigasi di bahagian atas, ayat penuh dalam tulisan Arab besar, diikuti analisis tiga kotak untuk setiap kalimah, dan terjemahan penuh di bawah.

### Analisis Per‑Kata
Setiap kalimah dipaparkan dengan tiga kotak analisis (Tajwid, Makhraj, Sifat) yang disusun secara mendatar, diikuti oleh teks Arab dan makna dalam Bahasa Melayu.

### Tema Warna
Tiga pilihan tema: ☀️ Terang (putih bersih), 🌙 Gelap (mod malam), dan ☕ Kopi (beige hangat) – semuanya dioptimumkan untuk kontras dan kebolehbacaan.

---

## 📊 Statistik

| Item | Jumlah |
|------|--------|
| **Fail HTML** | 8 (7 ayat + 1 indeks) |
| **Ayat dianalisis** | 7 |
| **Jumlah kalimah** | 29 |
| **Jumlah huruf** | 139 |
| **Tema warna** | 3 (Terang, Gelap, Kopi) |
| **Asas tajwid diterapkan** | 5/5 |
| **Dokumentasi** | 6 fail `.md` |
| **Komitmen** | 27 |

---

## 🏗 Seni Bina Teknikal

| Lapisan | Teknologi |
|---------|-----------|
| **Struktur** | HTML5, elemen semantik, RTL (`dir="rtl"`) |
| **Gaya** | CSS3, *Custom Properties* (pemboleh ubah), Flexbox |
| **Logik** | JavaScript ES6+ vanilla (tanpa framework) |
| **Fon** | `Scheherazade New` (Google Fonts, dengan fallback) |
| **Storan** | `localStorage` untuk keutamaan tema |

### Prinsip Reka Bentuk
- **Tanpa kebergantungan luaran** – tiada jQuery, Bootstrap, React, atau npm
- **Boleh berfungsi luar talian** – semua kandungan statik
- **Mesra mudah alih** – susun atur *flexbox* tanpa *media query*
- **Kandungan dwi-mod** – fail individu dan papan pemuka mengandungi kandungan yang sama (penduaan disengajakan untuk penggunaan luar talian)

Untuk butiran teknikal penuh, rujuk [`ARCHITECTURE.md`](ARCHITECTURE.md).

---

## 📚 Dokumentasi

| Fail | Penerangan |
|------|------------|
| [`SKILL.md`](SKILL.md) | Pengetahuan pedagogi & rujukan 5 asas pembelajaran |
| [`DESIGN.md`](DESIGN.md) | Sistem reka bentuk visual, tema warna, tipografi |
| [`ARCHITECTURE.md`](ARCHITECTURE.md) | Seni bina teknikal, aliran data, strategi tema |
| [`STRUCTURE.md`](STRUCTURE.md) | Rujukan struktur fail & kod, anatomi HTML/CSS/JS |
| [`RULES.md`](RULES.md) | Piawaian pengekodan & kekangan projek |
| [`API_SPEC.md`](API_SPEC.md) | Spesifikasi skema data & endpoint masa depan |

---

## 🛠 Penambahbaikan Masa Depan

- [ ] Audio sebutan untuk setiap kalimah
- [ ] Animasi visual makhraj (keratan rentas mulut)
- [ ] Mod kuiz interaktif (teka hukum tajwid, makhraj, atau sifat)
- [ ] Mod cetakan mesra kertas (*print‑friendly*)
- [ ] Tanda waqaf Rasm Uthmani penuh
- [ ] Kembangkan ke surah‑surah lain (Juzuk 30, Surah pilihan)
- [ ] Skrip binaan untuk segerakkan kandungan antara fail

---

## 📜 Lesen

Projek ini dilesenkan di bawah **[Lesen MIT](LICENSE)**.

Anda bebas untuk:
- ✅ Menggunakan untuk pembelajaran peribadi
- ✅ Mengubah suai untuk keperluan sendiri
- ✅ Mengedarkan semula dengan atribusi
- ✅ Menggunakan dalam projek komersial

---

## 🙏 Penghargaan

- **Tafsir Ibnu Kathir** – sumber utama kandungan tafsir
- **Matan Al‑Jazariyyah** – rujukan utama Ilmu Tajwid
- **Hidayat al‑Mustafid** – rujukan Makhraj dan Sifat Huruf
- **Jemaah Masjid Kampung Sungai Lintang Baru** – inspirasi projek
- Semua yang terlibat secara langsung dan tidak langsung dalam pembangunan sistem ini

---

<p align="center">
  <strong>Disediakan untuk tujuan pembelajaran dan dakwah.</strong><br>
  <em>“Sebaik-baik kalian adalah yang mempelajari Al‑Quran dan mengajarkannya.”</em> – (HR. Al‑Bukhari)<br>
  <br>🌙 Semoga bermanfaat. ✨
</p>
```
