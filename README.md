# DS-AI v4.1 ARCHITECT & VISION

## Deskripsi Singkat
DS-AI v4.1 adalah sistem asisten pengembangan perangkat lunak otonom yang dirancang khusus untuk berjalan di lingkungan Termux. Sistem ini mengintegrasikan kecerdasan buatan multimodal (Gemini Vision) dengan kemampuan manajemen file lokal dan eksekusi perintah terminal untuk mempercepat pengembangan aplikasi Flutter dam bahasa pemrograman lainnya.

## Fitur Utama
1. Arsitektur Hybrid: Menggabungkan model Gemini (Vision) untuk analisis gambar dan Groq/Llama untuk kecepatan pemrosesan teks.
2. Analisis Multimodal: Mampu menganalisis tangkapan layar (screenshot) error, sketsa UI, atau foto perangkat keras untuk memberikan solusi koding secara langsung.
3. Manajemen File Otonom: AI dapat membuat, membaca, mengubah, dan menghapus folder atau file di dalam penyimpanan lokal Termux secara mandiri.
4. Integrasi Flutter: Dilengkapi dengan fitur otomatisasi pemeriksaan sintaks (Dart Analyze) dan manajemen build APK.
5. Persistent Logging: Sistem penyimpanan log permanen dalam format JSONL untuk pelacakan percakapan jangka panjang.
6. Auto-Failover: Mekanisme otomatis perpindahan kunci API (API Key Rotation) jika terjadi limitasi kuota (Rate Limit).

## Tahap Instalasi

### 1. Persiapan Lingkungan Termux
Jalankan perintah berikut untuk memastikan repositori dan paket dasar terinstal:

```bash
pkg update && pkg upgrade -y
```
```bash
pkg install python git tmux nano -y'''
```bash
termux-setup-storage```

### 2. Instalasi Dependensi Sistem
Instalasi pustaka pengolah gambar dan pustaka pendukung Python:

```bash
pkg install python-pillow -y```
```bash
pip install flask requests```

### 3. Konfigurasi Proyek
Kloning atau buat direktori kerja dan siapkan struktur folder yang diperlukan:

```mkdir -p ~/build-apk/core ~/build-apk/uploads```
```cd ~/build-apk```

### 4. Pengaturan Variabel Lingkungan (Environment Variables)
Tambahkan kunci API ke dalam konfigurasi shell agar sistem dapat mengakses model AI. Buka file .bashrc:

```nano ~/.bashrc```

Tambahkan baris berikut di akhir file:

export GEMINI_KEYS="kunci_1,kunci_2"
export GROQ_KEY="kunci_anda"
export OPENROUTER_KEY="kunci_anda"

### 5. Menjalankan Sistem
Gunakan Tmux untuk memastikan proses tetap berjalan di latar belakang:

```tmux new -s ai```
```python3 ds_gui.py```

Akses antarmuka web melalui browser pada alamat: ```http://127.0.0.1:5000```

## Struktur File Proyek
- ds_gui.py: Server web Flask dan antarmuka pengguna.
- core/engine.py: Logika utama komunikasi dengan API Model AI.
- core/utils.py: Utilitas untuk kompresi gambar dan validasi kode.
- core/actions.py: Handler untuk operasi file sistem otonom.
- uploads/: Direktori penyimpanan sementara untuk analisis gambar.

## Keamanan dan Pemeliharaan
- Sistem secara otomatis menghapus file gambar setelah dikonversi menjadi data Base64 untuk menghemat ruang penyimpanan.
- Gunakan perintah 'termux-wake-lock' untuk mencegah Android mematikan proses saat perangkat dalam mode siaga.
- Selalu lakukan commit pada repositori git sebelum melakukan perubahan besar melalui AI untuk meminimalisir risiko kehilangan data.
