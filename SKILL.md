# 📖 Sistem Analisis Al-Fatihah – SKILL.md

> **Dokumentasi Lengkap Projek Pembelajaran Surah Al-Fatihah**  
> Menggabungkan Tafsir Ibnu Kathir, Analisis Tajwid, Makhraj, Sifat Huruf, dan Makna Per-Kata

---

## 🧠 Gambaran Keseluruhan

Sistem ini adalah pakej pembelajaran digital lengkap untuk **Surah Al-Fatihah** yang merangkumi:

1. **Tafsir Ibnu Kathir** (teks penuh Bahasa Melayu)
2. **Analisis Tajwid Per Ayat** dengan tiga lapisan:
   - 🟥 **Hukum Tajwid** (tempat keluar huruf, mad, idgham, dll.)
   - 🟦 **Makhraj Huruf** (tempat keluar setiap huruf)
   - 🟪 **Sifat Huruf** (sifat berlawanan & tunggal)
3. **Makna Per-Kata** & Terjemahan penuh setiap ayat
4. **Dashboard Interaktif** dengan tab navigasi dan 3 tema warna

---

## 🗂 Struktur Fail

```
📁 Projek Al-Fatihah/
├── 📄 index.html                 # Dashboard utama (tab + 3 tema)
├── 📄 al_fatihah_ayat_1.html     # Analisis lengkap Ayat 1 (Basmalah)
├── 📄 al_fatihah_ayat_2.html     # Analisis lengkap Ayat 2
├── 📄 al_fatihah_ayat_3.html     # Analisis lengkap Ayat 3
├── 📄 al_fatihah_ayat_4.html     # Analisis lengkap Ayat 4
├── 📄 al_fatihah_ayat_5.html     # Analisis lengkap Ayat 5
├── 📄 al_fatihah_ayat_6.html     # Analisis lengkap Ayat 6
├── 📄 al_fatihah_ayat_7.html     # Analisis lengkap Ayat 7
├── 📄 SKILL.md                   # Dokumentasi ini
└── 📄 README.md                  # (Opsional) panduan ringkas
```

---

## 🎯 5 Asas Pembelajaran Quran yang Diterapkan

| Asas | Pelaksanaan dalam Sistem |
|------|--------------------------|
| **1. Makhraj Huruf** | Kotak biru pada setiap kalimah – menyenaraikan tempat keluar setiap huruf (Jauf, Halq, Lisan, Syafatain, Khaisyum) |
| **2. Sifat Huruf** | Kotak ungu pada setiap kalimah – menyenaraikan sifat berlawanan (Hams/Jahr, Syiddah/Rakhawah, Isti'la'/Istifal, dll.) & sifat tunggal (Safir, Qalqalah, Takrir, dll.) |
| **3. Mad** | Kotak merah (Tajwid) – mencatatkan jenis Mad: Thabi'i, 'Arid Lissukun, beserta panjang harakat |
| **4. Hukum Nun Mati & Mim Mati** | Dicatatkan dalam kotak Tajwid – Izhar Halqi, Idgham, dll. |
| **5. Waqaf & Ibtida'** | Dicatatkan dalam kotak Tajwid – Mad 'Arid Lissukun, Hamzatul Wasl, cara memulakan bacaan |

---

## 🧱 Komponen Utama Setiap Fail HTML

### A. Struktur Visual (Setiap Kalimah)

Setiap kalimah dipaparkan dalam **satu kumpulan flexbox** (`kalimah-group`) yang mengandungi:

```
┌─────────────────────────────────────────────────────┐
│  📐 TAJWID      │  🗣️ MAKHRAJ     │  📝 SIFAT      │
│  (Merah)        │  (Biru)         │  (Ungu)        │
├─────────────────┼─────────────────┼────────────────┤
│ • Hukum 1       │ • Tempat huruf  │ • Sifat huruf  │
│ • Hukum 2       │ • Tempat huruf  │ • Sifat huruf  │
│ • ...           │ • ...           │ • ...          │
└─────────────────┴─────────────────┴────────────────┘
│                TEKS ARAB (BESAR)                   │
│                MAKNA PER-KATA (HIJAU)              │
└────────────────────────────────────────────────────┘
```

### B. Elemen Halaman

| Elemen | Keterangan |
|--------|------------|
| **Ayat Penuh** | Teks Arab besar di bahagian atas |
| **Petunjuk Warna** | Legend 3 warna (Tajwid / Makhraj / Sifat) |
| **Kumpulan Kalimah** | Flexbox 3 kotak + teks Arab + makna |
| **Terjemahan Penuh** | Ayat lengkap dalam Bahasa Melayu |
| **Tema Warna** | 3 butang ikon (☀️ Light / 🌙 Dark / ☕ Coffee) |

---

## 🎨 Sistem Tema Warna

| Tema | CSS Class | Latar Belakang | Warna Teks | Warna Aksen |
|------|-----------|----------------|------------|-------------|
| **Day-light** | `body.light` | Putih (#ffffff) | Hitam (#1e1e1e) | Biru gelap (#2c3e50) |
| **Dark-night** | `body.dark` | Hitam (#1e1e1e) | Putih (#e0e0e0) | Biru terang (#a0c4ff) |
| **Beige Coffee** | `body.coffee` | Kuning air (#f5efe0) | Coklat (#4a3728) | Coklat gelap (#6f4e37) |

Pemilihan tema disimpan dalam `localStorage` dengan kunci `alfatihah-theme`.

---

## 📐 Konvensi Penamaan & Kod

### CSS Variables

```css
:root {
    --bg: #ffffff;
    --bg-card: #fafafa;
    --text: #1e1e1e;
    --accent: #2c3e50;
    --tajwid-color: #b34b4b;
    --makhraj-color: #2980b9;
    --sifat-color: #8e44ad;
    --arab-font: 'Scheherazade New', 'Traditional Arabic', serif;
    --ui-font: 'Courier New', Courier, monospace;
}
```

### Font

| Penggunaan | Font |
|------------|------|
| Teks Arab | `Scheherazade New`, `Traditional Arabic` |
| UI (butang, label) | `Courier New` (monospace) |

### Arah Teks

- `direction: rtl` pada `body` untuk layout kanan-ke-kiri
- `direction: ltr` pada `theme-bar` untuk butang tema

---

## 🧩 Cara Menggunakan / Mengubah Suai

### 1. Melihat Dashboard

Buka `index.html` dalam mana-mana pelayar web moden. Semua 7 ayat dimuatkan terus dalam satu halaman dengan sistem tab.

### 2. Melihat Ayat Individu

Buka mana-mana fail `al_fatihah_ayat_X.html` secara langsung.

### 3. Menambah Ayat Baru (Contoh: Surah Lain)

1. Salin salah satu fail `al_fatihah_ayat_X.html`
2. Ubah suai:
   - Tajuk (`<title>`)
   - Ayat penuh (`.ayat-penuh`)
   - Setiap `kalimah-group`:
     - Hukum tajwid (`.tajwid`)
     - Makhraj (`.makhraj`)
     - Sifat (`.sifat`)
     - Teks Arab (`.arab-kalimah`)
     - Makna (`.makna`)
   - Terjemahan penuh (`.terjemahan-penuh`)
3. Tambahkan tab baru dalam `index.html` dan salin kandungan `kalimah-group` ke dalam `ayat-content` yang baru.

---

## 📋 Senarai Hukum Tajwid yang Digunakan

| Hukum | Contoh Ayat |
|-------|-------------|
| Hamzatul Wasl | Ayat 1–7 |
| Idgham Syamsi | Ayat 1–7 |
| Idgham Qamari | Ayat 6, 7 |
| Izhar Halqi | Ayat 7 |
| Izhar (biasa) | Ayat 1, 5 |
| Mad Thabi'i | Ayat 1–7 |
| Mad 'Arid Lissukun | Ayat 2, 4, 5, 6, 7 |
| Harf Lin | Ayat 4, 7 |
| Ra Tafkhim / Tarqiq | Ayat 1, 2, 3, 6, 7 |
| Lam Tarqiq (Lafz Allah) | Ayat 1, 2 |
| Syaddah | Ayat 1–7 |

---

## 📊 Statistik Sistem

| Item | Jumlah |
|------|--------|
| Fail HTML | 8 (7 ayat + 1 indeks) |
| Ayat dianalisis | 7 |
| Kalimah dianalisis | 29 |
| Tema warna | 3 |
| Asas tajwid diterapkan | 5/5 |
| Makhraj huruf | Disebut untuk setiap huruf |
| Sifat huruf | Disebut untuk setiap huruf |

---

## 🚀 Penambahbaikan Masa Depan

- [ ] Tambah audio sebutan untuk setiap kalimah
- [ ] Tambah visualisasi animasi makhraj (gambar keratan mulut)
- [ ] Tambah mod kuiz interaktif
- [ ] Kembangkan ke surah-surah lain
- [ ] Tambah mod cetakan (print-friendly CSS)
- [ ] Tambah Rasm Uthmani penuh dengan tanda waqaf

---

## 📝 Nota Akhir

Sistem ini dibina dengan pendekatan **mobile-first** dan **lightweight**:

- Tiada framework luaran (tiada Bootstrap, jQuery, dll.)
- Tiada JavaScript yang berat
- Hanya HTML + CSS + Vanilla JS
- Serasi dengan semua pelayar moden

Semua analisis makhraj dan sifat huruf dirujuk daripada kitab-kitab tajwid muktabar seperti *al-Jazariyyah*, *Hidayat al-Mustafid*, dan matan-matan tajwid yang lain.

---

*Disediakan untuk tujuan pembelajaran dan dakwah. Semoga bermanfaat.* 🌙
```
