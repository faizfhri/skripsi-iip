# Survey Penelitian dengan Stratified Random Assignment

Web survey untuk penelitian eksperimen dengan sistem **stratified random assignment** otomatis yang terintegrasi dengan Google Sheets untuk monitoring real-time.

## 📋 Fitur

- ✅ Survey multi-section (Penjelasan, Consent, Demografi, Pengalaman, Stimulus, Skala Pengukuran)
- ✅ **Stratified Random Assignment** berdasarkan Jenis Kelamin × Pengalaman Membeli
- ✅ Balancing otomatis untuk 3 kelompok eksperimen (A, B, C)
- ✅ Integrasi real-time dengan Google Sheets
- ✅ 5 Checkbox Informed Consent (harus semua di-check)
- ✅ Semantic Differential Scale (7 poin, 7 item)
- ✅ Responsive design (mobile-friendly)
- ✅ Loading indicator dan backup download jika error

## 🎯 Stratifikasi

**4 Strata berdasarkan:**
- Jenis Kelamin: Laki-laki / Perempuan
- Pengalaman Membeli: Belum Pernah / Pernah

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
│   ├── stimulus-a.jpg     # Stimulus untuk kelompok A
│   ├── stimulus-b.jpg     # Stimulus untuk kelompok B
│   └── stimulus-c.jpg     # Stimulus untuk kelompok C
├── google-script.js       # Google Apps Script code
└── README.md             # Dokumentasi ini
```

## 🚀 Setup Instructions

### 1. Upload Stimulus Images

Upload 3 gambar stimulus kamu ke folder `images/`:
- `stimulus-a.jpg` - Stimulus untuk kelompok A
- `stimulus-b.jpg` - Stimulus untuk kelompok B
- `stimulus-c.jpg` - Stimulus untuk kelompok C

**Format yang disarankan:** JPG/PNG, max 2MB per gambar

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

### 4. Deploy ke Web (Gratis)

#### Option A: Deploy ke Vercel (Recommended)

1. Install [Vercel CLI](https://vercel.com/download):
   ```bash
   npm install -g vercel
   ```

2. Di folder `iip`, jalankan:
   ```bash
   vercel
   ```

3. Ikuti langkah-langkah:
   - Login dengan GitHub/GitLab/Email
   - Confirm project setup
   - Deploy!

4. Kamu akan dapat URL live (misal: `https://iip-xyz.vercel.app`)

#### Option B: Deploy ke Netlify

1. Buka [Netlify](https://www.netlify.com)
2. Drag & drop folder `iip` ke Netlify
3. Deploy otomatis!
4. Kamu dapat URL live

#### Option C: Deploy ke GitHub Pages

1. Push folder `iip` ke GitHub repository
2. Buka **Settings** → **Pages**
3. Source: Deploy from branch **main**
4. Folder: **/ (root)**
5. Save
6. URL: `https://username.github.io/repo-name`

## 📊 Monitoring Data

### Real-time Monitoring di Google Sheets

Setelah deployment, buka Google Sheets kamu untuk monitoring:

#### Sheet 1: Responses
Berisi semua data responden:
- Timestamp
- Data diri (nama, usia, gender, pendidikan, pekerjaan)
- Pengalaman membeli
- **Strata** (L-Belum, L-Pernah, P-Belum, P-Pernah)
- **Kelompok Stimulus** (A, B, C)
- 7 skala pengukuran

#### Sheet 2: Tracking
Monitoring distribusi assignment:
```
Strata     | Group_A | Group_B | Group_C
-----------|---------|---------|--------
L-Belum    |    5    |    4    |    4
L-Pernah   |    7    |    7    |    6
P-Belum    |    3    |    4    |    4
P-Pernah   |    6    |    5    |    6
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
