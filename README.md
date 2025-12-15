# Pilot Study Efektivitas Strategi Promosi pada Produk Berkonsep Donasi

Web survey untuk penelitian Psikologi UGM dengan sistem **stratified random assignment** otomatis yang terintegrasi dengan Google Sheets untuk monitoring real-time.

> 📚 **Penelitian oleh:** Yuniva Putri Adilia  
> 🎓 **Program:** Sarjana Reguler Psikologi Universitas Gadjah Mada  
> 👨‍🏫 **Pembimbing:** Dr. Sumaryono, M. Si., Psikolog

---

## 📖 Panduan Lengkap untuk Pemula

### 🚀 Cara Deploy Website ke Vercel (Gratis!)

**Langkah 1: Persiapan File**
1. Pastikan semua file project ada di folder `iip`:
   - `index.html`
   - `css/style.css`
   - `js/survey.js`
   - `images/` (stimulus-a.png, stimulus-b.png, stimulus-c.png)

**Langkah 2: Buat Akun Vercel**
1. Buka https://vercel.com
2. Klik **Sign Up** (Daftar)
3. Pilih **Continue with GitHub** atau **Continue with Email**
4. Ikuti instruksi untuk verifikasi akun

**Langkah 3: Deploy Project**
1. Login ke Vercel
2. Klik tombol **Add New** → **Project**
3. Pilih **Import Git Repository** ATAU **Upload Files**
4. Jika upload files:
   - Drag & drop folder `iip` ke area upload
   - Atau klik **Select Folder** dan pilih folder `iip`
5. Klik **Deploy**
6. Tunggu ~1-2 menit sampai selesai
7. Vercel akan memberikan URL seperti: `https://iip-survey.vercel.app`

**Langkah 4: Bagikan Link**
- Copy URL yang diberikan Vercel
- Bagikan link tersebut ke partisipan

**Tips:**
- ✅ Vercel gratis untuk unlimited projects
- ✅ Website otomatis update jika file di-upload ulang
- ✅ Bisa custom domain (opsional)

---

### 📊 Setup Google Sheets untuk Menerima Data

**Langkah 1: Buat Google Spreadsheet Baru**
1. Buka https://sheets.google.com
2. Klik **+ Blank** untuk sheet baru
3. Beri nama: **"Survey Responses - Pilot Study"**
4. Copy ID Spreadsheet dari URL:
   ```
   https://docs.google.com/spreadsheets/d/SPREADSHEET_ID_INI/edit
   ```

**Langkah 2: Buka Apps Script**
1. Di Google Sheets, klik **Extensions** → **Apps Script**
2. Hapus code default yang ada
3. Copy SEMUA code dari file `google-script.js`
4. Paste di Apps Script editor

**Langkah 3: Update Spreadsheet ID**
1. Di baris 5 Apps Script, ganti `YOUR_SPREADSHEET_ID_HERE` dengan ID spreadsheet kamu:
   ```javascript
   const SPREADSHEET_ID = 'paste-id-spreadsheet-kamu-disini';
   ```

**Langkah 4: Deploy Web App**
1. Klik **Deploy** (tombol biru) → **New deployment**
2. Di "Select type", klik ⚙️ → Pilih **Web app**
3. Setting:
   - **Description:** "Survey API v1"
   - **Execute as:** Me
   - **Who has access:** **Anyone** (penting!)
4. Klik **Deploy**
5. Klik **Authorize access**
6. Pilih akun Google kamu
7. Klik **Advanced** → **Go to [project name] (unsafe)** → **Allow**
8. Copy **Web app URL** yang diberikan (format: https://script.google.com/macros/s/...)

**Langkah 5: Update URL di Website**
1. Buka file `js/survey.js`
2. Di baris 3, ganti dengan Web app URL kamu:
   ```javascript
   const GOOGLE_SCRIPT_URL = 'paste-url-web-app-kamu-disini';
   ```
3. Save file
4. Upload ulang ke Vercel (deploy otomatis)

**Langkah 6: Test Data Masuk**
1. Buka website survey kamu
2. Isi survey sampai selesai
3. Cek Google Sheets, harusnya ada 2 sheet baru:
   - **Responses** - Data responden
   - **Tracking** - Monitoring assignment kelompok

---

### 🔄 Cara Update Website Setelah Deploy

**Jika ada perubahan di file HTML/CSS/JS:**
1. Buka https://vercel.com dan login
2. Pilih project kamu
3. Klik **Settings** → **Deployments**
4. Upload file yang baru (drag & drop)
5. Vercel akan auto-deploy ~1-2 menit

**Jika ada perubahan di Google Script:**
1. Buka Apps Script editor
2. Edit code yang perlu diubah
3. Klik **Deploy** → **Manage deployments**
4. Klik ✏️ **Edit** di deployment yang aktif
5. Ubah **Version** jadi **New version**
6. Klik **Deploy**
7. URL tetap sama, tidak perlu update di website

---

### ⚠️ Troubleshooting Umum

**Problem: Data tidak masuk ke Google Sheets**
- ✅ Cek Web app URL sudah benar di `survey.js`
- ✅ Pastikan "Who has access" = **Anyone** di Apps Script
- ✅ Test pakai fungsi `testSaveData()` di Apps Script:
  1. Pilih function `testSaveData` di dropdown
  2. Klik **Run** (▶️)
  3. Cek apakah data muncul di Sheets

**Problem: Countdown tidak center**
- ✅ Pastikan file `css/style.css` sudah ter-upload
- ✅ Clear cache browser (Ctrl + Shift + R)

**Problem: Gambar stimulus tidak muncul**
- ✅ Cek folder `images/` sudah ter-upload
- ✅ Cek nama file: `stimulus-a.png`, `stimulus-b.png`, `stimulus-c.png` (lowercase!)

**Problem: Website tidak bisa dibuka**
- ✅ Tunggu 5-10 menit setelah deploy pertama kali
- ✅ Cek status di Vercel dashboard
- ✅ Coba buka di incognito/private window

---

## 📋 Fitur

- ✅ Survey 9 section (Intro, Info Penelitian, Informed Consent, Data Diri, Pengalaman Digital Ads, Stimulus, Skala, Thank You)
- ✅ **Stratified Random Assignment** berdasarkan Jenis Kelamin × Pengalaman Membeli Produk Berkonsep Donasi
- ✅ Balancing otomatis untuk 3 kelompok eksperimen (A, B, C)
- ✅ Integrasi real-time dengan Google Sheets
- ✅ 5 Checkbox Informed Consent + Radio "Bersedia/Tidak Bersedia"
- ✅ 6 pertanyaan tentang exposure iklan digital
- ✅ Purchase Intention Scale (7 poin, 5 item)
- ✅ Screening otomatis (usia, marketing exp, digital active)
- ✅ Timer 30 detik untuk stimulus
- ✅ Countdown 3 detik anti-double-click
- ✅ Responsive design (mobile-friendly)
- ✅ Rujukan UKP UGM di halaman Thank You

## 🎯 Stratifikasi

**4 Strata berdasarkan:**
- **Jenis Kelamin:** Laki-laki / Perempuan
- **Pengalaman Membeli Produk Berkonsep Donasi:** Ya / Tidak

**Strata Codes:**
- `L-Ya` - Laki-laki yang pernah membeli produk berkonsep donasi
- `L-Tidak` - Laki-laki yang belum pernah membeli
- `P-Ya` - Perempuan yang pernah membeli produk berkonsep donasi
- `P-Tidak` - Perempuan yang belum pernah membeli

**Assignment Logic:**
- Setiap responden diassign ke kelompok (A/B/C) yang paling sedikit di strata mereka
- Memastikan distribusi seimbang di setiap kelompok
- Target: 56 responden per kelompok (Total N = 168)

## 📁 Struktur Project

```
iip/
├── index.html              # Main survey page
├── css/
│   └── style.css          # Styling
├── js/
│   └── survey.js          # Logic & randomization
├── images/                # Folder untuk stimulus
│   ├── stimulus-a.png     # Stimulus untuk kelompok A
│   ├── stimulus-b.png     # Stimulus untuk kelompok B
│   └── stimulus-c.png     # Stimulus untuk kelompok C
├── google-script.js       # Google Apps Script code
└── README.md             # Dokumentasi ini
```

## 🚀 Setup Instructions

### 1. Upload Stimulus Images

Upload 3 gambar stimulus kamu ke folder `images/`:
- `stimulus-a.png` - Stimulus untuk kelompok A (Emotional Appeal)
- `stimulus-b.png` - Stimulus untuk kelompok B (Rational Appeal)
- `stimulus-c.png` - Stimulus untuk kelompok C (Kontrol)

**Format yang disarankan:** PNG dengan transparent background, max 2MB per gambar

### 2. Setup Google Sheets & Apps Script

#### A. Buat Google Sheets Baru

1. Buka [Google Sheets](https://sheets.google.com)
2. Buat spreadsheet baru
3. Beri nama (misal: "Survey Data Skripsi")
4. Copy **Spreadsheet ID** dari URL:
   ```
   https://docs.google.com/spreadsheets/d/1AbC123XyZ456.../edit
                                      ^^^^^^^^^^^^^^^^
                                      Ini Spreadsheet ID
   ```

#### B. Setup Google Apps Script

1. Di Google Sheets, klik **Extensions** → **Apps Script**
2. Hapus semua code default
3. Copy semua code dari file `google-script.js`
4. Paste ke Apps Script editor
5. **Ganti `SPREADSHEET_ID`** di baris 4:
   ```javascript
   const SPREADSHEET_ID = 'PASTE_SPREADSHEET_ID_KAMU_DISINI';
   ```
6. Klik **Save** (💾)

#### C. Deploy sebagai Web App

1. Klik **Deploy** → **New deployment**
2. Klik ⚙️ (gear icon) → Pilih **Web app**
3. Isi:
   - **Description:** Survey Web App
   - **Execute as:** Me
   - **Who has access:** Anyone
4. Klik **Deploy**
5. **Authorize** akses (ikuti langkah-langkah authorization)
6. Copy **Web App URL** yang muncul
7. **Save URL ini!** (misal: `https://script.google.com/macros/s/AKfy...`)

#### D. Update survey.js

1. Buka file `js/survey.js`
2. Ganti `GOOGLE_SCRIPT_URL` di baris 3:
   ```javascript
   const GOOGLE_SCRIPT_URL = 'PASTE_WEB_APP_URL_KAMU_DISINI';
   ```
3. Save file

### 3. Test Lokal

1. Buka `index.html` di browser (double-click file)
2. Test isi survey sampai selesai
3. Cek Google Sheets apakah data masuk ke sheet **Responses**
4. Cek sheet **Tracking** untuk melihat distribusi per strata

### 4. Deploy ke Web (Gratis) - Panduan untuk Pemula

Survey ini perlu di-deploy ke internet agar bisa diakses oleh responden. Ada 3 cara mudah dan **GRATIS**:

---

#### 🟢 **CARA PALING MUDAH: Vercel (Recommended)**

**Vercel** adalah platform hosting gratis yang paling mudah untuk pemula. Deploy dalam 2 menit!

##### **Langkah-langkah:**

1. **Buka website Vercel**
   - Kunjungi: [vercel.com](https://vercel.com)
   - Klik tombol **"Sign Up"** atau **"Start Deploying"**

2. **Buat akun (pilih salah satu):**
   - Login dengan **GitHub** (recommended)
   - Login dengan **Google**
   - Login dengan **Email**

3. **Upload project:**
   - Setelah login, klik **"Add New..."** → **"Project"**
   - Klik **"Browse"** atau drag & drop folder `iip` ke halaman
   - Tunggu upload selesai

4. **Deploy:**
   - Vercel akan otomatis detect project kamu
   - Klik **"Deploy"** (tombol biru besar)
   - Tunggu ~30 detik

5. **Selesai! 🎉**
   - Kamu akan dapat URL live, contoh: `https://iip-abc123.vercel.app`
   - Copy URL ini untuk dibagikan ke responden
   - Survey sudah bisa diakses oleh siapa saja!

**💡 Tips:**
- Vercel gratis selamanya untuk project kecil seperti ini
- Tidak perlu install apapun di komputer
- Bisa update project kapan saja dengan upload ulang

---

#### 🔵 **CARA ALTERNATIF 1: Netlify**

**Netlify** juga mudah seperti Vercel, tapi dengan cara sedikit berbeda.

##### **Langkah-langkah:**

1. **Buka website Netlify**
   - Kunjungi: [netlify.com](https://netlify.com)
   - Klik **"Sign Up"** (buat akun dengan email/GitHub/Google)

2. **Deploy dengan Drag & Drop:**
   - Setelah login, kamu akan lihat area yang bertulisan **"Want to deploy a new site without connecting to Git? Drag and drop your site folder here"**
   - **Drag folder `iip` ke area tersebut** (atau klik untuk browse)
   - Tunggu upload & deploy (±1 menit)

3. **Selesai! 🎉**
   - Kamu dapat URL random seperti: `https://random-name-123.netlify.app`
   - Bisa ganti nama domain jika mau:
     - Klik **"Site settings"** → **"Change site name"**
     - Contoh jadi: `https://survey-skripsi-yuniva.netlify.app`

**💡 Kelebihan Netlify:**
- Paling mudah: tinggal drag & drop!
- Bisa ganti nama domain gratis
- Unlimited bandwidth

---

#### 🟣 **CARA ALTERNATIF 2: GitHub Pages**

**GitHub Pages** gratis dari GitHub, tapi butuh langkah lebih banyak. Pilih ini kalau kamu sudah familiar dengan GitHub.

##### **Langkah-langkah:**

1. **Buat akun GitHub** (jika belum punya)
   - Kunjungi: [github.com](https://github.com)
   - Sign up dengan email

2. **Buat repository baru:**
   - Klik **"New"** atau **"+"** → **"New repository"**
   - Nama: `survey-skripsi` (atau nama lain)
   - Pilih **"Public"**
   - Klik **"Create repository"**

3. **Upload files:**
   - Klik **"uploading an existing file"**
   - Drag semua file dari folder `iip` ke halaman
   - Klik **"Commit changes"**

4. **Aktifkan GitHub Pages:**
   - Klik tab **"Settings"**
   - Scroll ke bawah, cari **"Pages"** di sidebar kiri
   - Di bagian **"Source"**, pilih **"main"** branch
   - Klik **"Save"**

5. **Tunggu 2-3 menit**
   - GitHub akan build & deploy otomatis
   - Refresh halaman Settings → Pages
   - URL akan muncul: `https://username.github.io/survey-skripsi`

**💡 Tips:**
- Gratis selamanya
- URL nya lebih "profesional" pakai github.io
- Bisa update dengan upload ulang file

---

#### 📱 **Cara Share Link ke Responden**

Setelah deploy, kamu akan punya URL seperti:
- Vercel: `https://iip-abc123.vercel.app`
- Netlify: `https://survey-yuniva.netlify.app`
- GitHub: `https://username.github.io/survey-skripsi`

**Cara share:**
1. Copy URL lengkap (dengan https://)
2. Share via:
   - WhatsApp
   - Email
   - Instagram/Twitter
   - Google Forms (kalau pakai screening awal)
   - Poster/QR Code

**Buat QR Code (optional):**
- Buka: [qr-code-generator.com](https://www.qr-code-generator.com/)
- Paste URL survey kamu
- Download QR Code
- Print di poster/flyer

---

#### ⚠️ **Hal Penting Setelah Deploy**

1. **Test dulu sebelum share!**
   - Buka URL di browser (desktop & mobile)
   - Isi survey sampai selesai
   - Cek data masuk ke Google Sheets

2. **Cek Google Sheets sudah benar:**
   - Sheet "Responses" ada data test
   - Sheet "Tracking" menghitung assignment
   - Semua kolom terisi (tidak ada yang blank)

3. **Siapkan backup plan:**
   - Save semua URL penting (Vercel, Google Sheets, Apps Script)
   - Backup code di Google Drive/OneDrive
   - Screenshot setup untuk dokumentasi

4. **Monitor rutin:**
   - Cek Google Sheets setiap hari
   - Pastikan assignment seimbang
   - Respons cepat jika ada responden yang komplain

---

#### 🆘 **Troubleshooting Deploy**

**"Website saya tidak bisa dibuka!"**
- ✅ Pastikan semua file sudah di-upload (index.html, css/, js/, images/)
- ✅ Cek nama file exact: `index.html` bukan `Index.html`
- ✅ Tunggu 2-3 menit setelah deploy pertama kali

**"Gambar stimulus tidak muncul!"**
- ✅ Cek file `stimulus-a.png`, `stimulus-b.png`, `stimulus-c.png` ada di folder `images/`
- ✅ Nama file harus lowercase dan exact match
- ✅ Upload ulang gambar jika perlu

**"Data tidak masuk ke Google Sheets!"**
- ✅ Cek Google Apps Script sudah di-deploy dengan "Anyone" access
- ✅ Cek `GOOGLE_SCRIPT_URL` di file `survey.js` sudah benar
- ✅ Test manual di Apps Script dengan function `testSaveData()`

**"Responden tidak bisa isi survey di HP!"**
- ✅ Survey sudah responsive, coba refresh atau clear cache
- ✅ Test di browser lain (Chrome/Firefox/Safari)
- ✅ Pastikan koneksi internet stabil

## 📊 Monitoring Data

### Real-time Monitoring di Google Sheets

Setelah deployment, buka Google Sheets kamu untuk monitoring:

#### Sheet 1: Responses
Berisi semua data responden:
- Timestamp
- Nama/Inisial
- Email aktif
- Data diri (usia, gender)
- Pengalaman marketing & digital
- **6 pertanyaan digital advertising exposure**
- Pengalaman beli produk berkonsep donasi
- **Strata** (L-Ya, L-Tidak, P-Ya, P-Tidak)
- **Kelompok Stimulus** (A, B, C)
- 5 skala Purchase Intention (1-7)

#### Sheet 2: Tracking
Monitoring distribusi assignment:
```
Strata     | Group_A | Group_B | Group_C
-----------|---------|---------|--------
L-Tidak    |    5    |    4    |    4
L-Ya       |    7    |    7    |    6
P-Tidak    |    3    |    4    |    4
P-Ya       |    6    |    5    |    6
```

### Formula untuk Monitoring

Tambahkan sheet baru "Summary" dengan formula:

**Total Responden:**
```
=COUNTA(Responses!A:A)-1
```

**Total per Kelompok:**
```
=COUNTIF(Responses!K:K,"A")  // Kelompok A
=COUNTIF(Responses!K:K,"B")  // Kelompok B
=COUNTIF(Responses!K:K,"C")  // Kelompok C
```

**Progress Target:**
```
=COUNTA(Responses!A:A)-1 & "/168"
```

## 🔧 Troubleshooting

### Data tidak masuk ke Google Sheets

1. **Cek Web App URL sudah benar di `survey.js`**
2. **Cek Spreadsheet ID sudah benar di `google-script.js`**
3. **Pastikan Web App di-deploy dengan "Who has access: Anyone"**
4. **Test manual di Apps Script:**
   ```
   Buka Apps Script → Run function "testSaveData"
   ```

### Stimulus gambar tidak muncul

1. **Cek nama file harus EXACT:**
   - `stimulus-a.jpg` (lowercase)
   - `stimulus-b.jpg`
   - `stimulus-c.jpg`
2. **Cek file ada di folder `images/`**
3. **Bisa ganti format jika perlu di `survey.js` line 112:**
   ```javascript
   stimulusImage.src = `images/stimulus-${assignedGroup.toLowerCase()}.png`;
   ```

### Random assignment tidak seimbang

1. Cek sheet **Tracking** di Google Sheets
2. Jika ada masalah, bisa reset dengan cara:
   - Delete semua row di Tracking (kecuali header)
   - Data akan auto-create ulang saat ada responden baru

### Browser block no-cors request

Jika ada error CORS, bisa pakai mode backup:
1. Data akan otomatis download sebagai JSON
2. Kamu bisa import manual ke Sheets nanti

## 📱 Mobile Optimization

Survey sudah responsive untuk mobile:
- Layout otomatis adjust
- Touch-friendly buttons
- Semantic differential scale readable di mobile

Test di berbagai devices atau pakai Chrome DevTools.

## 🎨 Kustomisasi

### Ganti Warna Theme

Edit `css/style.css` bagian `:root`:
```css
:root {
    --primary-color: #4A90E2;  /* Ganti warna utama */
    --success-color: #28a745;  /* Ganti warna sukses */
}
```

### Tambah Pertanyaan

1. Edit `index.html` di section yang sesuai
2. Tambah input dengan `name` attribute
3. Update `survey.js` di function `submitSurvey()` untuk collect data
4. Update `google-script.js` di `createResponseSheet()` tambah header kolom

### Ganti Semantic Differential Items

Edit `index.html` section `section-scale`, ubah label:
```html
<div class="scale-labels">
    <span class="label-left">Label Kiri</span>
    <span class="label-right">Label Kanan</span>
</div>
```

## 📈 Export Data untuk Analisis

Dari Google Sheets:
1. **File** → **Download** → **CSV** (untuk SPSS/R/Python)
2. Atau **Microsoft Excel (.xlsx)**

Data sudah siap untuk analisis statistik!

## 🔒 Privacy & Security

- Data responden tersimpan aman di Google Sheets milik kamu
- Tidak ada tracking atau analytics pihak ketiga
- Web App URL hanya kamu yang tahu
- Bisa tambah authentication jika perlu

## 📝 Lisensi

Free to use untuk keperluan penelitian akademis.

## 🆘 Support

Jika ada masalah:
1. Cek Troubleshooting section di atas
2. Cek console browser (F12) untuk error messages
3. Cek Execution log di Apps Script

---

**Good luck dengan penelitian skripsimu! 🎓📊**
