# 🧠 Adu Otak Berdua — Game Tebak-Tebakan Online Pasangan

Game "Adu Otak Berdua" adalah website game tebak-tebakan jenaka dan mengasah logika yang dimainkan berdua secara online secara realtime. 

Setiap ronde menampilkan teka-teki receh, logika jebakan batman, matematika menjebak, tebak kata dari emoji, susun huruf (anagram), deret pola, hingga teka-teki lateral thinking dengan cerita ber-twist yang mengejutkan!

---

## 🌟 Fitur Utama

- **2 Mode Bermain:**
  1. **Mode Versus ⚔️:** Kedua pemain berlomba menjawab secepat mungkin. Jawaban benar tercepat mendapatkan bonus poin kecepatan ekstra!
  2. **Mode Tim 🤝:** Bekerja sama melawan countdown waktu untuk mengumpulkan skor bersama. Tersedia mini-chat realtime untuk berdiskusi dan saling melempar kode rahasia.
- **Bank Soal Berkualitas (90+ Soal):**
  - Tebak-tebakan receh & plesetan (15 soal)
  - Teka-teki logika "jebakan batman" (15 soal)
  - Matematika & hitung cepat menjebak (10 soal)
  - Tebak kata dari kombinasi emoji (10 soal)
  - Susun huruf acak / anagram (10 soal)
  - Pola deret logika (10 soal)
  - Pikir terbalik / lateral thinking (10 soal)
  - Cerita aneh dengan plot twist mengejutkan (10 soal)
- **3 Level Petunjuk Bertingkat (Hints):**
  - Petunjuk 1: Petunjuk halus (-20% nilai dasar)
  - Petunjuk 2: Petunjuk sedang (-40% nilai dasar)
  - Petunjuk 3: Petunjuk terbuka (-60% nilai dasar)
- **Keamanan Server-Side Evaluation:** Kunci jawaban dan variasi jawaban **tidak pernah dikirim ke browser**. Evaluasi benar/salah 100% diproses di server sebelum ronde ditutup.
- **Sinkronisasi Realtime:** Timer, perolehan skor, status "menunggu pasangan" / "pasangan sudah menjawab" selalu sinkron di kedua layar melalui Supabase Realtime Channels.
- **Rejoin & Auto Reconnect:** Token sesi tersimpan otomatis di `localStorage`. Jika browser ter-refresh atau koneksi terputus, pemain bisa langsung rejoin ke ronde aktif.
- **Papan Hasil & Julukan Lucu:** Gelar unik di akhir permainan berdasarkan performa, seperti *"Duo Otak Kembar Identik"*, *"Duo Jenius Tanpa Tandingan"*, *"Duo Pecinta Bantuan Google"*, atau *"Sama-sama Masih Loading"*.
- **Papan Peringkat (Leaderboard):** Riwayat skor tertinggi pasangan tercatat di database PostgreSQL.
- **Tambah Soal Custom:** Fitur bagi pemain untuk membuat teka-teki rahasia spesial buat pasangannya.

---

## 🛠️ Tech Stack

- **Framework:** Next.js 14+ (App Router, Server Actions & API Route Handlers)
- **Bahasa:** TypeScript
- **Styling & UI:** Tailwind CSS, Framer Motion, Lucide Icons, Canvas Confetti
- **State Management:** Zustand
- **Database & Realtime Backend:** Supabase (PostgreSQL + Realtime Channels + Row Level Security)
- **Hosting / Deployment:** Vercel

---

## 📋 Panduan Setup Supabase (Langkah demi Langkah)

Proyek ini menggunakan Supabase sebagai database PostgreSQL dan Realtime WebSocket. Supabase 100% gratis.

### 1. Buat Proyek Baru di Supabase
1. Buka [https://supabase.com](https://supabase.com) dan login / register.
2. Klik tombol **"New Project"**.
3. Masukkan nama project (misalnya: `adu-otak-berdua`), buat password database, dan pilih Region terdekat (misal: *Singapore*).
4. Klik **"Create new project"** dan tunggu hingga provisioning database selesai (~1-2 menit).

### 2. Eksekusi File Migration & Bank Soal (SQL Editor)
1. Di sidebar dashboard Supabase, buka menu **SQL Editor**.
2. Klik **"New Query"**.
3. Buka file [`supabase/migrations/001_initial_schema.sql`](supabase/migrations/001_initial_schema.sql), salin seluruh isinya, tempel ke SQL Editor Supabase, lalu klik tombol **"Run"** (Ctrl+Enter).
   > *Ini akan membuat tabel `rooms`, `players`, `puzzles`, `rounds`, `answers`, `game_sessions`, `custom_puzzles`, indexes, dan mengaktifkan Row Level Security serta Realtime publication.*
4. Buka kembali **"New Query"**.
5. Buka file [`supabase/migrations/002_seed_puzzles.sql`](supabase/migrations/002_seed_puzzles.sql), salin seluruh 90 soal teka-teki, tempel ke SQL Editor Supabase, lalu klik tombol **"Run"**.
   > *Sekarang database Anda telah terisi dengan 90 soal berkualitas lengkap dengan variasi jawaban, 3 petunjuk, dan penjelasan jenaka!*

### 3. Mengambil API Keys
1. Di dashboard Supabase, buka menu **Project Settings** (ikon gerigi) -> **API**.
2. Salin data berikut:
   - **Project URL** (`https://xxxxxxxxxxxx.supabase.co`)
   - **anon / public key** (untuk akses client)
   - **service_role key** (klik *Reveal*, salin key ini untuk backend server)

---

## 💻 Menjalankan di Komputer Lokal

### 1. Konfigurasi Environment Variable
Salin file `.env.example` menjadi `.env.local`:
```bash
cp .env.example .env.local
```
Lalu buka file `.env.local` dan isi dengan kredensial Supabase Anda:
```env
NEXT_PUBLIC_SUPABASE_URL=https://your-project-id.supabase.co
NEXT_PUBLIC_SUPABASE_ANON_KEY=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
SUPABASE_SERVICE_ROLE_KEY=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
NEXT_PUBLIC_APP_URL=http://localhost:3000
```

### 2. Install Dependensi & Jalankan
```bash
npm install
npm run dev
```
Buka browser di [http://localhost:3000](http://localhost:3000).

---

## 🚀 Panduan Deploy ke Vercel

Aplikasi ini siap di-deploy ke Vercel hanya dalam beberapa langkah:

### Opsi A: Deploy via GitHub (Paling Direkomendasikan)
1. Push repository ini ke akun GitHub Anda.
2. Buka [https://vercel.com](https://vercel.com) dan klik **"Add New..." -> "Project"**.
3. Pilih repository GitHub Anda.
4. Di bagian **Environment Variables**, tambahkan 4 variabel:
   - `NEXT_PUBLIC_SUPABASE_URL` = (URL Supabase Anda)
   - `NEXT_PUBLIC_SUPABASE_ANON_KEY` = (Anon Key Supabase Anda)
   - `SUPABASE_SERVICE_ROLE_KEY` = (Service Role Key Supabase Anda)
   - `NEXT_PUBLIC_APP_URL` = (Domain Vercel Anda, misal `https://adu-otak.vercel.app`)
5. Klik **"Deploy"**. Dalam ~1 menit website Anda sudah online dan bisa diakses dari smartphone maupun laptop via link!

### Opsi B: Deploy via Vercel CLI
```bash
npm install -g vercel
vercel
```
Ikuti petunjuk di terminal untuk menghubungkan project dan memasukkan environment variables.

---

## 🎮 Cara Bermain Bersama Pasangan

1. **Pemain 1 (Host):**
   - Buka website, pilih avatar emoji, ketik nama panggilan, pilih mode (Versus atau Tim), lalu klik **"Buka Room & Ajak Pasangan!"**.
   - Salin **Kode Room (6 digit)** atau klik **"Salin Link Undangan"** dan kirimkan ke pasangan lewat WhatsApp.
2. **Pemain 2:**
   - Buka link undangan, pilih avatar emoji, ketik nama panggilan, dan klik **"Masuk ke Room"**.
3. **Mulai Bertanding:**
   - Begitu kedua pemain terhubung di lobby, Host mengklik **"Mulai Adu Otak Sekarang!"**.
   - Jawab setiap soal sebelum timer habis! Gunakan petunjuk jika buntu, atau saling berbisik di kolom chat jika bermain mode tim.
   - Di akhir ronde, nikmati penjelasan kocak dan rayakan gelar pasangan kalian! 🥳
