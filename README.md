# AutoScanBug - Pemindai Kerentanan Otomatis

![Keamanan](https://img.shields.io/badge/keamanan-pemindaian%20kerentanan-merah)
![Otomatisasi](https://img.shields.io/badge/otomatis-pemindaian-biru)

AutoScanBug adalah alat pemindaian otomatis yang dirancang untuk mendeteksi berbagai kerentanan keamanan dalam aplikasi web dan sistem.

## 🔍 Fitur Utama

- **Deteksi 30+ Jenis Kerentanan**: Mulai dari OWASP Top 10 hingga miskonfigurasi server
- **Pemindaian Otomatis**: Identifikasi cepat potensi celah keamanan
- **Rekomendasi Perlindungan**: Saran mitigasi untuk setiap jenis kerentanan
- **Cakupan Luas**: Dari injeksi SQL hingga kerentanan autentikasi

## 📋 Kerentanan yang Terdeteksi

### Serangan Injeksi
- SQL Injection (SQLi)
- Command Injection
- XML Injection
- Server-Side Template Injection (SSTI)

### Kerentanan Server-Side
- Eksekusi Kode Jarak Jauh (RCE)
- Local File Inclusion (LFI)
- Remote File Inclusion (RFI)
- Server-Side Request Forgery (SSRF)
- XML External Entity (XXE) Injection

### Kerentanan Client-Side
- Cross-Site Scripting (XSS)
- Cross-Site Request Forgery (CSRF)
- Clickjacking
- Kesalahan Konfigurasi CORS

### Masalah Autentikasi & Sesi
- Authentication Bypass
- Manajemen Sesi yang Lemah
- Session Fixation
- Kerentanan Brute Force

### Masalah File & Konfigurasi
- Directory Listings
- Eksposur File Backup
- File Upload Tidak Aman
- Server Misconfiguration
- Insecure Direct Object Reference (IDOR)

## 🛡️ Rekomendasi Perlindungan

[Setiap deteksi kerentanan disertai saran mitigasi](https://github.com/Y0xDft07/AutoScanbug/blob/main/auto_scan_bug.md)

## 🚀 Instalasi

```bash
# Clone repository
git clone https://github.com/Y09a514/AutoScanBug.git
cd AutoScanBug

# Pasang dependensi
pip install -r requirements.txt

# Jalankan pemindai
python3 autoscanbug.py
```

## 📊 Contoh Output

```
[+] Memindai: http://example.com
[!] Ditemukan: Kerentanan SQL Injection di /search.php
[!] Ditemukan: Kerentanan XSS di /contact.php
[✓] Aman: Tidak ditemukan directory listing

Pemindaian selesai dalam 2m 45s
Ditemukan 3 kerentanan kritis
```

## 🤝 Berkontribusi
Kontribusi terbuka! Silakan ajukan issue atau pull request untuk:
- Detektor kerentanan baru
- Peningkatan algoritma pemindaian
- Tambahan rekomendasi perlindungan

## 📜 Lisensi
MIT License - Lihat [LICENSE](LICENSE) untuk detail

## ⚠️ Penafian
Alat ini hanya untuk pengujian keamanan yang sah. Jangan gunakan pada sistem tanpa izin.
