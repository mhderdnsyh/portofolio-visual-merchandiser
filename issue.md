# 📋 ISSUE: Implementasi Frontend Portfolio Visual Merchandiser

> **Status:** Open  
> **Tipe:** Feature – Frontend Implementation  
> **Priority:** High  
> **Assignee:** Junior Programmer / AI Model  
> **Estimasi:** 5–8 hari kerja  

---

## 🎯 Deskripsi Proyek

Membangun website **portfolio profesional** untuk seorang **Visual Merchandiser**. Website ini berfungsi sebagai showcase personal brand, menampilkan karya-karya visual merchandising (window display, in-store arrangement, planogram, event visual), keahlian, pengalaman kerja, dan fitur kontak untuk klien/perekrut.

Target audience: HRD/Recruiter Retail, Brand Manager, Store Manager, dan Klien potensial.

---

## 🛠️ Tech Stack & Alasan Pemilihannya

### 1. Core Framework: **Astro.js** + **React** (Islands Architecture)
- **Mengapa Astro.js?**
  - **Zero-JS by Default & Super Cepat:** Portfolio sebagian besar berisi konten visual statis. Astro memutar konten sebagai HTML murni tanpa mengunduh framework JS yang berat, sehingga kecepatan muat (Lighthouse score) mencapai 95-100.
  - **SEO Unggulan:** Karena dirender secara statis di server (SSG), Google dan mesin pencari lain dapat dengan mudah meng-index setiap karya dan deskripsi di dalamnya.
  - **Optimasi Gambar Otomatis (`@astrojs/image`):** Visual Merchandiser mengandalkan banyak foto beresolusi tinggi. Astro secara otomatis mengubah format gambar menjadi `.webp` dan mengompresnya tanpa mengurangi kualitas visual.
  - **Islands Architecture:** Memungkinkan penggunaan komponen interaktif (seperti filter proyek atau lightbox galeri) menggunakan React hanya di komponen yang membutuhkan interaksi saja, tanpa membebani halaman lain.

### 2. Styling: **Tailwind CSS v3** + **Custom Fonts (Playfair Display & Inter)**
- **Mengapa Tailwind CSS?**
  - **Pengembangan Cepat:** Utility-first class mempercepat styling tanpa perlu mengelola ratusan baris file CSS terpisah.
  - **Konsistensi Desain:** Menjaga paduan warna, jarak (spacing), dan ukuran font tetap standar.
  - **Ukuran File Sangat Kecil:** Fitur purge otomatis hanya menyertakan CSS yang benar-benar digunakan.

### 3. Animasi: **Framer Motion**
- **Mengapa Framer Motion?**
  - Memberikan nuansa premium (editorial/luxury vibe) melalui animasi *scroll-triggered*, *fade-in*, dan *hover effects* yang halus pada kartu karya.

### 4. Handling Form Kontak: **Formspree** atau **EmailJS**
- **Mengapa tanpa Backend?**
  - Karena ini website statis, tidak perlu menyewa/membuat server backend Node.js/PHP hanya untuk form kontak. Formspree/EmailJS mengirim pesan pengunjung langsung ke email pemilik portofolio secara gratis.

### 5. Hosting & Deployment: **Vercel** / **Netlify**
- **Mengapa Vercel?**
  - Gratis, terintegrasi langsung dengan GitHub (auto-deploy saat `git push`), dilengkapi SSL (HTTPS) otomatis, dan CDN global super cepat.

---

## 📁 Struktur Folder Proyek

```
portofolio-visual-merchandiser/
├── public/
│   ├── images/
│   │   ├── projects/          ← Foto-foto hasil karya VM
│   │   ├── profile/           ← Foto profil
│   │   └── brands/            ← Logo brand/klien
│   ├── favicon.ico
│   └── og-image.jpg           ← Thumbnail preview saat link dibagikan
│
├── src/
│   ├── components/
│   │   ├── Navbar.astro
│   │   ├── Hero.astro
│   │   ├── About.astro
│   │   ├── ProjectCard.astro
│   │   ├── ProjectFilter.tsx  ← React component (interaktif)
│   │   ├── Skills.astro
│   │   ├── Experience.astro
│   │   ├── Contact.astro
│   │   ├── Footer.astro
│   │   └── GalleryModal.tsx   ← React lightbox untuk detail gambar
│   │
│   ├── layouts/
│   │   └── BaseLayout.astro   ← Meta tag, SEO, Font, Header/Footer
│   │
│   ├── pages/
│   │   ├── index.astro        ← Halaman utama
│   │   └── projects/
│   │       └── [slug].astro   ← Halaman detail tiap proyek
│   │
│   ├── data/
│   │   ├── projects.ts        ← Data array semua proyek & foto
│   │   ├── skills.ts          ← Data keahlian & tools
│   │   └── experience.ts      ← Data riwayat kerja
│   │
│   └── styles/
│       └── global.css         ← Theme colors & custom utility
│
├── astro.config.mjs
├── tailwind.config.mjs
├── tsconfig.json
├── package.json
└── issue.md
```

---

## 🎨 Design System & Visual Palette

### Color Palette (Luxury Dark Mode)
- **Background Utama (`bg-primary`):** `#0A0A0F` (Dark Indigo / Almost Black)
- **Background Card (`bg-secondary`):** `#12121A` (Deep Slate)
- **Aksen Utama (`accent-gold`):** `#C9A84C` (Prestige Gold - kesan profesional & luxury)
- **Aksen Sekunder (`accent-rose`):** `#E8748A` (Rose Gold - kesan fasyen & estetik)
- **Teks Utama (`text-primary`):** `#F0EDE8` (Warm Off-White)
- **Teks Sekunder (`text-secondary`):** `#9A9A9A` (Muted Grey)

### Typography
- **Heading:** `Playfair Display` (Serif - memberikan kesan majalah fashion/editorial)
- **Body:** `Inter` (Sans-serif - bersih, modern, dan sangat mudah dibaca)

---

## 🚀 Tahapan Implementasi (Panduan Step-by-Step untuk Junior / AI)

---

### 🟢 FASE 1: Inisialisasi & Konfigurasi Proyek (Hari 1)

1. **Inisialisasi Astro dalam folder proyek ini:**
   ```bash
   npm create astro@latest . -- --template minimal --typescript strict --no-install --no-git
   npm install
   ```

2. **Install Integrations & Dependencies:**
   ```bash
   npx astro add react tailwind sitemap
   npm install framer-motion yet-another-react-lightbox @astrojs/image sharp
   ```

3. **Setup `tailwind.config.mjs`:**
   Daftarkan warna kustom (`bg-primary`, `accent-gold`, dll) dan font (`font-display`, `font-body`) sesuai spesifikasi Design System di atas.

4. **Setup `src/styles/global.css`:**
   Import Google Fonts (`Playfair Display` & `Inter`), atur warna latar belakang default `body` ke `#0A0A0F` dan warna teks ke `#F0EDE8`.

5. **Uji Coba:**
   Jalankan `npm run dev` dan pastikan server lokal berjalan tanpa error di `http://localhost:4321`.

---

### 🟢 FASE 2: Struktur Layout & Mock Data (Hari 2)

1. **Buat `src/layouts/BaseLayout.astro`:**
   - Menyediakan tag `<head>`, Meta SEO (Title, Description, Open Graph).
   - Mengintegrasikan Google Font dan stylesheet global.
   - Menyediakan `<slot />` untuk menampung isi halaman.

2. **Buat File Data Terstruktur (`src/data/`):**
   - `projects.ts`: Buat array objek berisi data proyek (id, slug, title, brand, category ['Window Display' | 'In-Store' | 'Planogram'], description, fullDescription, coverImage, images[], year, role).
   - `skills.ts`: Buat data kategori skill (Visual Merchandising, Software/Tools, Retail Strategy, Soft Skills).
   - `experience.ts`: Buat data riwayat posisi, nama brand/perusahaan, tahun, dan deskripsi pencapaian.

---

### 🟢 FASE 3: Pembuatan Komponen UI Utama (Hari 3–4)

1. **`Navbar.astro`:**
   - Menyediakan logo/nama personal brand.
   - Navigation links dengan smooth-scrolling (`#about`, `#projects`, `#skills`, `#experience`, `#contact`).
   - Menyediakan toggle menu versi mobile (hamburger).

2. **`Hero.astro`:**
   - Layout 2 kolom (Teks perkenalan + Foto profil utama).
   - Headline menggunakan font serif `Playfair Display`.
   - Tombol CTA: "Lihat Portofolio" (scroll ke `#projects`) dan "Download CV" (link file `.pdf`).

3. **`About.astro`:**
   - Narasi latar belakang profesional sebagai Visual Merchandiser.
   - Highlight statistik ringkas (misal: "5+ Tahun Pengalaman", "30+ Project Handled", "15+ Retail Stores").

4. **`ProjectCard.astro` & `ProjectFilter.tsx`:**
   - Buat komponen filter kategori (All, Window Display, In-Store, Event) menggunakan React (`client:load`).
   - Render kartu proyek dengan efek *hover zoom* pada gambar dan badge nama brand.
   - Tombol "Lihat Detail" mengarah ke `/projects/[slug]`.

5. **`Skills.astro` & `Experience.astro`:**
   - Render daftar skill menggunakan bentuk badge pill modern.
   - Render timeline riwayat kerja secara vertikal.

6. **`Contact.astro`:**
   - Form kontak (Nama, Email, Subjek, Pesan).
   - Hubungkan form `action` ke endpoint Formspree (`https://formspree.io/f/{your_form_id}`).
   - Sertakan tautan media sosial (LinkedIn, Instagram, WhatsApp).

---

### 🟢 FASE 4: Halaman Detail Proyek (`/projects/[slug]`) (Hari 5)

1. **Buat `src/pages/projects/[slug].astro`:**
   - Gunakan fungsi `getStaticPaths()` dari Astro untuk meng-generate halaman statis berdasarkan `projects.ts`.
   - Tampilkan informasi rinci: nama brand, peranan (role), tahun, lokasi, dan penjelasan tantangan/solusi visual merchandising yang dilakukan.

2. **Integrasi Lightbox Galeri Foto:**
   - Implementasikan komponen `GalleryModal.tsx` menggunakan `yet-another-react-lightbox` agar pengunjung bisa mengeklik gambar untuk melihat dalam mode full-screen.

---

### 🟢 FASE 5: Animasi & Polishing UI (Hari 6)

1. **Animasi Smooth Enter:**
   - Tambahkan animasi `framer-motion` saat elemen masuk ke viewport (`whileInView={{ opacity: 1, y: 0 }}`).
2. **Astro View Transitions:**
   - Tambahkan `<ViewTransitions />` di `BaseLayout.astro` untuk efek perpindahan halaman yang mulus tanpa refresh.

---

### 🟢 FASE 6: SEO, Optimasi Gambar & Pengujian (Hari 7)

1. **Kompresi Gambar:**
   - Ubah semua aset foto ke format `.webp` menggunakan Squoosh / TinyPNG.
   - Gunakan tag `<Image />` dari Astro untuk responsif image loading.
2. **Lighthouse Audit:**
   - Jalankan `npm run build` dilanjutkan `npx astro preview`.
   - Buka Chrome DevTools -> Lighthouse. Pastikan skor:
     - Performance: ≥ 90
     - Accessibility: ≥ 90
     - Best Practices: ≥ 90
     - SEO: 100

---

### 🟢 FASE 7: Deployment (Hari 8)

1. Push seluruh source code ke repository GitHub.
2. Hubungkan repository ke dashboard **Vercel** / **Netlify**.
3. Pastikan build command: `astro build` dan output directory: `dist`.
4. Tambahkan custom domain jika sudah tersedia.

---

## 📌 Checklist Verifikasi Akhir (Acceptance Criteria)

- [ ] Website dapat diakses dengan cepat di mobile & desktop tanpa penyusutan tata letak.
- [ ] Semua gambar produk/karya terkompresi dan terbuka jernih saat diklik (lightbox).
- [ ] Filter kategori proyek bekerja secara instan tanpa reload halaman.
- [ ] Form kontak berhasil mengalirkan pesan masuk ke email target.
- [ ] Tombol Download CV dapat mengunduh dokumen PDF.
- [ ] Skor Google Lighthouse Performance minimal 90.

---

*Document issue dibuat untuk panduan mengeksekusi proyek Portofolio Visual Merchandiser.*
