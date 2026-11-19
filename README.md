# Panduan Setup Firebase & Deploy ke GitHub Pages

Dokumen ini berisi langkah-langkah lengkap untuk menyiapkan **Firebase Firestore** sebagai database *realtime* serta mengunggah aplikasi PWA ke **GitHub Pages**.

---

## Bagian 1: Cara Membuat Project Firebase & Firestore

### 1. Buat Project Baru di Firebase
1. Buka [Firebase Console](https://console.firebase.google.com/) dan masuk menggunakan akun Google Anda.
2. Klik **Add project** (atau **Create a project**).
3. Masukkan nama project (misalnya: `crm-donatur`), lalu klik **Continue**.
4. Matikan atau aktifkan *Google Analytics* sesuai kebutuhan, lalu klik **Create project** dan tunggu hingga selesai.

### 2. Daftarkan Aplikasi Web untuk Mendapatkan `firebaseConfig`
1. Di halaman utama project Firebase, klik ikon **Web (`</>`)** di bawah tulisan *Get started by adding Firebase to your app*.
2. Masukkan nama aplikasi (misalnya: `SapaDonatur Web`), lalu klik **Register app**.
3. Salin kode `const firebaseConfig = { ... };` yang muncul di layar (berisi `apiKey`, `authDomain`, `projectId`, `storageBucket`, `messagingSenderId`, `appId`).
4. Tempelkan `firebaseConfig` tersebut ke dalam file `index.html` (atau kirimkan ke asisten untuk dimasukkan otomatis).

### 3. Aktifkan Cloud Firestore Database
1. Di menu sebelah kiri Firebase Console, pilih **Build → Firestore Database**.
2. Klik **Create database**.
3. Pilih lokasi server terdekat (rekomendasi: `asia-southeast2` untuk Jakarta atau `asia-southeast1` untuk Singapura), lalu klik **Next**.
4. Pilih **Start in test mode** (atau **production mode**), lalu klik **Create**.

### 4. Pasang Coding Rules Firebase (`firestore.rules`)
1. Di halaman **Firestore Database**, buka tab **Rules**.
2. Salin isi file `firestore.rules` yang ada di paket ini, lalu tempel menggantikan isi editor Rules di Firebase Console.
3. Klik **Publish** untuk menyimpan aturan keamanan.

> **Catatan:** Opsi A di `firestore.rules` mengizinkan aplikasi tim bekerja langsung tanpa login sambil tetap memvalidasi tipe data. Jika nanti Anda menambahkan sistem login (Firebase Auth), gunakan Opsi B agar hanya pengguna yang login yang dapat mengakses data.

---

## Bagian 2: Cara Upload ke GitHub & Mengaktifkan GitHub Pages

1. **Buat Repository Baru:** Buka [GitHub](https://github.com/new), beri nama repository (misalnya `sapadonatur-crm`), pilih **Public**, lalu klik **Create repository**.
2. **Unggah File Aplikasi:** Ekstrak file `.zip` aplikasi, lalu unggah `index.html`, `manifest.json`, `sw.js`, dan seluruh file ikon (`.png`) langsung ke root repository (`Add file → Upload files → Commit changes`).
3. **Aktifkan GitHub Pages:**
   - Buka tab **Settings → Pages** di repository GitHub Anda.
   - Pada bagian *Build and deployment*, pilih Source: **Deploy from a branch**.
   - Pilih Branch **`main`** dan folder **`/ (root)`**, lalu klik **Save**.
   - Tunggu 1–2 menit hingga muncul link `https://username.github.io/nama-repo/`.
4. **Pasang di iPhone / Android:**
   - **iPhone (Safari):** Buka link GitHub Pages, ketuk ikon **Share** (kotak dengan panah ke atas), lalu pilih **Add to Home Screen**.
   - **Android (Chrome):** Ketuk banner **Pasang** atau menu titik tiga → **Install app**.
