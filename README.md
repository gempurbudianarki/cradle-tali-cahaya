# Cyber Cradle - Interactive Hand-Tracking String Physics

**Cyber Cradle** adalah aplikasi web interaktif futuristik berbasis HTML5/JavaScript yang mensimulasikan permainan tradisional tali (Cat's Cradle) menggunakan penjejakan tangan (*hand-tracking*) berbasis kecerdasan buatan (**MediaPipe Hands**) dan visualisasi grafis performa tinggi (**p5.js**). 

Aplikasi ini mendeteksi sendi jari tangan pengguna secara real-time melalui kamera web (*webcam*) dan menghubungkan ujung-ujung jari tangan kiri dan kanan menggunakan tali digital bercahaya neon (seperti laser) yang memiliki efek fisika elastisitas (Verlet Integration) di dalam ruang 3D.

---

## ✨ Fitur Utama

1. **Penjejakan Tangan Real-Time 3D (MediaPipe Hands)**:
   * Deteksi multi-tangan secara simultan (tangan kiri dan kanan).
   * Penjejakan koordinat sendi (landmarks) yang responsif dengan sensitivitas tinggi (faktor *smoothing* default `0.75` untuk respon instan 1-ke-1).

2. **Simulasi Fisika Tali 3D (Verlet Integration)**:
   * Tali digital disimulasikan menggunakan model fisika *Verlet integration* sehingga memiliki efek gravitasi, kelenturan, dan ketegangan (*sag & tension*).
   * Perhitungan posisi tali diselesaikan secara 3D berdasarkan koordinat kedalaman (Z-axis). Ketika tangan didorong mendekat atau menjauh dari kamera, ketebalan dan pancaran cahaya tali akan berskala secara dinamis.
   * Efek plucking/petikan tali: mengibaskan jari dengan cepat di dekat tali akan mentransfer gaya kinetik dan menghasilkan efek getaran gelombang sinus yang berayun elastis.

3. **Desain Visual & Estetika Cyberpunk Premium**:
   * **Double-Helix Laser Beams**: Setiap tali memiliki inti laser putih terang yang dibalut oleh gelombang energi melilit ganda (searah dan berlawanan arah jarum jam) berwarna neon.
   * **Glow & Bloom Effect**: Pencahayaan berpendar (*bloom*) mewah menggunakan teknik penggambaran berlapis (*multi-layer additive blending*) pada kanvas HTML5.
   * **Grid Warping Background**: Latar belakang grid digital bergaya retro yang melengkung secara organik mengikuti posisi tangan pengguna.
   * **CRT Scanline Overlay**: Filter monitor tabung retro untuk memperkuat atmosfer retro-futuristik.

4. **Efek Partikel Interaktif (Kuncup/Pinch Gesture)**:
   * **Gesture Mekar (Pinch & Release)**: Menguncupkan semua jari (pinch) akan mengisi daya bola plasma energi. Saat tangan dibuka kembali, ia akan melepaskan ledakan partikel bola-bola cincin bercahaya (*bubble sparks*) yang berhamburan secara dinamis.
   * **String Friction Sparks**: Persilangan antar tali laser akan mendeteksi titik tabrakan garis segmen dan memercikkan kilatan plasma secara real-time.
   * **Electric Arcs**: Efek petir listrik mini yang menyambar secara acak di antara ujung jari kiri dan kanan ketika kedua tangan berada dalam jarak dekat.

5. **Mesin Audio Sintetis (Web Audio API)**:
   * Suara dengung harmonik dinamis yang frekuensinya berubah sesuai rentang regangan jari.
   * Suara petikan (*pluck zap*) synthesizer retro saat tali dipetik atau ketika partikel meledak, tanpa memerlukan aset file audio eksternal.

6. **Zen Mode & Panel Kontrol Lengkap**:
   * Panel kontrol futuristik untuk mengatur mode latar belakang, pola rajutan tali, warna neon, tingkat ketegangan tali, tingkat dampening getaran, dan keaktifan efek visual.
   * **Zen Mode**: Tekan tombol **"H"** di keyboard atau klik tombol silang (`×`) untuk menyembunyikan semua panel kontrol agar Anda bisa menikmati tampilan penuh tanpa gangguan.

---

## ⚙️ Persyaratan Sistem & Instalasi

Proyek ini dibangun tanpa framework berat (Next.js/React) agar ringan dan dapat dimuat langsung di browser mana pun secara instan. Semua dependensi (*p5.js* dan *MediaPipe*) dimuat langsung melalui CDN.

### Cara Membuka Proyek secara Lokal

1. **Unduh repositori** ini ke komputer Anda.
2. Tempatkan folder proyek di dalam direktori server lokal Anda (misalnya di folder `laragon/www/taliprojek` jika Anda menggunakan Laragon).
3. **Jalankan Server Lokal**:
   Karena fitur akses kamera (*Camera API/getUserMedia*) memerlukan konteks yang aman (*Secure Context*), **Anda tidak dapat membuka file `index.html` secara langsung dengan mengklik ganda file tersebut**. Anda harus membukanya melalui server lokal (`http://localhost` atau `http://127.0.0.1`).
   
   Jika Anda memiliki Python terinstal, jalankan perintah berikut di terminal/PowerShell pada direktori folder Anda:
   ```bash
   python -m http.server 8000
   ```
4. Buka browser Anda dan akses alamat:
   **[http://localhost:8000/](http://localhost:8000/)**

---

## ⚠️ Informasi Penting Tentang Keamanan Browser (Webcam API)

> [!IMPORTANT]
> **Kebijakan Keamanan HTTPS / Localhost**:
> Browser modern secara ketat memblokir fungsi kamera (*getUserMedia*) jika diakses lewat protokol HTTP biasa pada domain kustom (seperti domain virtual Laragon `http://taliprojek.test` atau alamat IP jaringan). 
> 
> Agar kamera Anda menyala dan wajah Anda terlihat:
> 1. Akses aplikasi **wajib** melalui alamat **`http://localhost:8000/`** atau **`http://127.0.0.1:8000/`**.
> 2. Jika Anda ingin menggunakan domain kustom seperti `http://taliprojek.test`, Anda harus mengaktifkan sertifikat SSL (HTTPS) di pengaturan Laragon/Apache Anda.
> 3. Jika izin kamera terblokir secara tidak sengaja, klik ikon gembok/kamera di sebelah kiri kolom alamat URL browser Anda, ubah izin Kamera menjadi **Allow (Izinkan)**, lalu *reload* halaman.

---

## 🎮 Cara Bermain

1. Buka aplikasi di browser (gunakan URL localhost).
2. Izinkan akses kamera saat diminta oleh browser.
3. Berdirilah sekitar 1 hingga 2 meter di depan kamera.
4. Hadapkan **kedua tangan** Anda ke arah kamera.
5. **Regangkan Tali**: Gerakkan tangan kiri dan kanan Anda menjauh atau mendekat untuk menarik dan mengendurkan tali laser.
6. **Ledakan Bola Partikel**: Kuncupkan kelima jari salah satu tangan Anda hingga membentuk bola plasma, lalu buka tangan Anda dengan cepat untuk memicu ledakan partikel bercahaya.
7. **Mainkan Melodi**: Goyangkan jari Anda dengan cepat untuk memetik tali laser dan mendengarkan suara petikan synth yang dinamis.
8. **Zen Mode**: Tekan tombol **"H"** pada keyboard untuk menyembunyikan/menampilkan menu pengaturan visual.

---

## 🛠️ Teknologi yang Digunakan

* **Core Logic**: Vanilla HTML5 & CSS3
* **Rendering Engine**: [p5.js](https://p5js.org/) (Canvas 2D Context dengan Additive Blend Mode)
* **AI hand tracking**: [MediaPipe Hands](https://developers.google.com/mediapipe/solutions/vision/hand_landmarker)
* **Audio Synthesis**: Web Audio API (Oscillators & Custom Gain Nodes)

---

Developed by: **Gempur Budi Anarki**
