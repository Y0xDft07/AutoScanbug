# AutoScanBug
Berikut adalah cara kerja dan saran perlindungan untuk masing-masing teknik yang disebutkan dalam **AutoScanBug**:

---

### **Injeksi SQL (SQLi)**  
**Cara Kerja:**  
Injeksi SQL memungkinkan penyerang menyisipkan pernyataan SQL berbahaya ke dalam input aplikasi, yang kemudian dieksekusi oleh basis data. Hal ini dapat menyebabkan akses tidak sah ke data, penghapusan data, atau manipulasi basis data.  
**Saran Perlindungan:**  
  - Gunakan prepared statements atau parameterized queries.  
  - Validasi input pengguna untuk mencegah perintah SQL berbahaya.  
  - Batasi hak akses database hanya untuk operasi yang diperlukan.

---

### **Remote Code Execution (RCE)**  
**Cara Kerja:**  
RCE memungkinkan penyerang menjalankan kode arbitrer pada server, sering kali melalui parameter atau file yang tidak tervalidasi.  
**Saran Perlindungan:**  
  - Validasi semua input dan file yang diunggah.  
  - Nonaktifkan eksekusi kode dari direktori unggahan.  
  - Gunakan library dan framework yang aman untuk menghindari eksekusi langsung perintah shell.

---

### **Cross-Site Scripting (XSS)**  
**Cara Kerja:**  
Penyerang menyisipkan skrip berbahaya ke dalam halaman web yang akan dijalankan oleh browser pengguna. Ini dapat mencuri cookie, memanipulasi halaman, atau menyerang pengguna lain.  
**Saran Perlindungan:**  
  - Escape semua input yang ditampilkan di halaman menggunakan fungsi HTML escaping.  
  - Terapkan Content Security Policy (CSP) untuk membatasi sumber skrip.  
  - Validasi dan filter input dari pengguna.

---

### **Local File Inclusion (LFI)**  
**Cara Kerja:**  
LFI memungkinkan penyerang mengakses file lokal server, seperti file konfigurasi atau data sensitif lainnya.  
**Saran Perlindungan:**  
  - Validasi input file dan gunakan whitelist untuk nama file yang diizinkan.  
  - Nonaktifkan pengindeksan direktori di server.  
  - Batasi izin file pada server untuk menghindari akses tidak sah.

---

### **Open Redirect**  
**Cara Kerja:**  
Penyerang mengeksploitasi pengalihan URL yang tidak aman untuk mengarahkan pengguna ke situs phishing atau berbahaya.  
**Saran Perlindungan:**  
  - Gunakan whitelist untuk tujuan URL pengalihan.  
  - Hindari mengambil parameter URL dari input pengguna tanpa validasi.

---

### **Backup Files**  
**Cara Kerja:**  
File cadangan yang terekspos dapat memberikan akses ke konfigurasi sensitif atau kode sumber aplikasi.  
**Saran Perlindungan:**  
  - Hapus file cadangan dari server produksi.  
  - Gunakan mekanisme penyimpanan cadangan yang terenkripsi.

---

### **Database Exposure**  
**Cara Kerja:**  
Informasi basis data yang terekspos dapat digunakan untuk akses tidak sah atau pengumpulan informasi.  
**Saran Perlindungan:**  
  - Pastikan port database hanya dapat diakses dari IP yang diotorisasi.  
  - Gunakan autentikasi yang kuat untuk mengakses database.

---

### **Directory Listings**  
**Cara Kerja:**  
Pengindeksan direktori memungkinkan penyerang melihat isi direktori, termasuk file sensitif.  
**Saran Perlindungan:**  
  - Nonaktifkan directory listing di konfigurasi server (misalnya, di `.htaccess` atau `nginx.conf`).  
  - Gunakan file `index.html` default untuk menutupi direktori kosong.

---

### **Sensitive Information**  
**Cara Kerja:**  
Data sensitif seperti kunci API atau kata sandi yang terekspos dapat digunakan oleh penyerang untuk eskalasi.  
**Saran Perlindungan:**  
  - Hindari menyimpan data sensitif dalam file konfigurasi yang terekspos.  
  - Enkripsi semua data sensitif dalam penyimpanan.

---

### **XML External Entity Injection (XXE)**  
**Cara Kerja:**  
Penyerang menyuntikkan entitas eksternal ke dalam parser XML untuk mengakses file lokal atau melakukan serangan DoS.  
**Saran Perlindungan:**  
  - Nonaktifkan entitas eksternal pada parser XML.  
  - Gunakan library XML yang aman seperti `lxml`.

---

### **Server-Side Request Forgery (SSRF)**  
**Cara Kerja:**  
SSRF memungkinkan penyerang memaksa server melakukan permintaan ke alamat IP atau URL yang dipilih.  
**Saran Perlindungan:**  
  - Validasi URL input dan batasi akses ke internal IP.  
  - Terapkan firewall aplikasi untuk memblokir permintaan SSRF.

---

**Remote File Inclusion (RFI)**  
**Cara Kerja**: Penyerang menyisipkan file berbahaya dari sumber jarak jauh ke dalam aplikasi.  
**Risiko**: Potensi kontrol penuh terhadap server atau pencurian data.  
**Saran Perlindungan**:  
  - Nonaktifkan fungsi file inclusion dari sumber eksternal.  
  - Validasi input file dan gunakan daftar putih (whitelist).  

---

**Log File Disclosure**  
**Cara Kerja**: Pengungkapan log aplikasi berisi informasi sensitif seperti kredensial atau token.  
**Risiko**: Penyerang dapat mengeksploitasi informasi sensitif.  
**Saran Perlindungan**:  
  - Pastikan direktori log tidak dapat diakses publik.  
  - Hindari mencatat informasi sensitif secara langsung. 


---

**Insecure Direct Object Reference (IDOR)**  
**Cara Kerja**: Penyerang mengakses sumber daya dengan memodifikasi parameter ID tanpa otorisasi.  
**Risiko**: Paparan data sensitif dan akses ilegal ke data pengguna.  
**Saran Perlindungan**:  
  - Terapkan kontrol akses berbasis otorisasi.  
  - Gunakan ID objek yang dienkripsi atau diacak.  

---

**Cross-Origin Resource Sharing (CORS)**  
**Cara Kerja**: Konfigurasi CORS yang salah memungkinkan akses tidak sah antar domain.  
**Risiko**: Kebocoran data antar domain.  
**Saran Perlindungan**:  
  - Batasi asal yang diizinkan dalam kebijakan CORS.  
  - Hindari penggunaan wildcard `*` dalam pengaturan CORS.  

---

**Cross-Site Request Forgery (CSRF)**  
**Cara Kerja**: Penyerang mengelabui pengguna untuk mengirimkan permintaan yang tidak sah ke server.  
**Risiko**: Penyerang dapat menjalankan tindakan atas nama pengguna yang sah.  
**Saran Perlindungan**:  
  - Gunakan token CSRF untuk setiap permintaan sensitif.  
  - Validasi asal atau referensi HTTP pada server. 

---

### **Command Injection**  
**Cara Kerja:**  
Penyerang menyisipkan perintah berbahaya ke dalam aplikasi yang memanggil shell sistem.  
**Saran Perlindungan:**  
  - Gunakan library atau fungsi yang menghindari pemanggilan shell.  
  - Escape semua input sebelum diteruskan ke sistem.


---

### **File Upload Vulnerabilities**  
**Cara Kerja:**  
Penyerang dapat mengunggah file berbahaya seperti skrip PHP untuk mendapatkan akses.  
**Saran Perlindungan:**  
  - Validasi ekstensi file unggahan dan gunakan whitelist.  
  - Simpan file di direktori yang tidak dapat dieksekusi.

---

### **Authentication Bypass**  
**Cara Kerja:**  
Penyerang mengeksploitasi kelemahan dalam mekanisme autentikasi untuk mendapatkan akses tanpa otorisasi.  
**Saran Perlindungan:**  
  - Terapkan otentikasi dua faktor (2FA).  
  - Pastikan semua titik akses memerlukan autentikasi.

---

**Insecure Configuration**  
**Cara Kerja**: Konfigurasi server atau aplikasi yang tidak aman memungkinkan eksploitasi.  
**Risiko**: Penyerang dapat memanfaatkan fitur yang tidak perlu atau salah konfigurasi.  
**Saran Perlindungan**:  
  - Terapkan prinsip **least privilege** pada server.  
  - Nonaktifkan fitur dan modul yang tidak diperlukan. 

---

### **Server Misconfiguration**  
**Cara Kerja**: Kesalahan konfigurasi server seperti izin yang terlalu permisif atau fitur yang tidak perlu diaktifkan.  
**Risiko**: Membuka celah keamanan yang dapat dimanfaatkan oleh penyerang.  
**Saran Perlindungan**:  
  - Nonaktifkan fitur atau modul yang tidak diperlukan.  
  - Terapkan prinsip **least privilege** pada izin akses server.  

---

### **Injection Flaws**  
**Cara Kerja**: Penyerang menyisipkan kode atau perintah berbahaya ke dalam input aplikasi (mis. SQL, XSS, XML).  
**Risiko**: Eksploitasi data, kontrol sistem, atau manipulasi aplikasi.  
**Saran Perlindungan**:  
  - Validasi dan sanitasi semua input pengguna.  
  - Gunakan parameterized queries atau prepared statements.  

---

### **Weak Session Management**  
**Cara Kerja**: Pengelolaan sesi yang lemah, seperti ID sesi yang dapat ditebak atau tidak dirotasi.  
**Risiko**: Pengambilalihan akun pengguna.  
**Saran Perlindungan**:  
  - Gunakan ID sesi yang aman dan unik.  
  - Terapkan rotasi ID sesi setelah login.  

---

### **Clickjacking**  
**Cara Kerja**: Penyerang menyematkan halaman target dalam iframe untuk mencuri klik pengguna.  
**Risiko**: Eksekusi tindakan tidak sah atas nama pengguna.  
**Saran Perlindungan**:  
  - Gunakan header `X-Frame-Options: DENY`.  
  - Terapkan kebijakan Content Security Policy (CSP).  

---

### **Host Header Injection**  
**Cara Kerja**: Penyerang memanipulasi header host HTTP untuk mengeksploitasi aplikasi.  
**Risiko**: Pengalihan tidak sah, kebocoran data, atau bypass autentikasi.  
**Saran Perlindungan**:  
  - Validasi header host pada sisi server.  
  - Batasi nilai host hanya pada domain yang diizinkan.  

---

### **Remote File Execution**  
**Cara Kerja**: Penyertaan atau eksekusi file dari sumber jarak jauh melalui input tidak aman.  
**Risiko**: Server dapat dikendalikan oleh penyerang atau diinfeksi malware.  
**Saran Perlindungan**:  
  - Nonaktifkan fungsi penyertaan file dari sumber eksternal.  
  - Validasi dan sanitasi input dengan ketat.  

---

### **Brute Force Attacks**  
**Cara Kerja**: Penyerang mencoba berbagai kombinasi kata sandi hingga berhasil.  
**Risiko**: Akun pengguna dapat diretas.  
**Saran Perlindungan**:  
  - Batasi jumlah percobaan login.  
  - Terapkan autentikasi multi-faktor (MFA).  

---

### **Security Misconfiguration**  
**Cara Kerja**: Konfigurasi keamanan yang salah seperti pengaturan default, modul tidak aman, atau kesalahan izin.  
**Risiko**: Membuka jalan bagi eksploitasi kerentanan.  
**Saran Perlindungan**:  
  - Perbarui konfigurasi dengan praktik terbaik keamanan.  
  - Audit konfigurasi secara berkala.  

---

### **Missing Authentication**  
**Cara Kerja**: Tidak adanya mekanisme autentikasi untuk melindungi sumber daya.  
**Risiko**: Akses tidak sah ke data sensitif atau fitur aplikasi.  
**Saran Perlindungan**:  
  - Terapkan autentikasi berbasis token atau sistem login.  
  - Gunakan metode otorisasi berbasis peran (RBAC).  

---

### **CRLF Injection**
**Cara Kerja**: Penyerang menyisipkan karakter CRLF (Carriage Return Line Feed) ke dalam input pengguna untuk memanipulasi header HTTP atau data log.  
**Risiko**: Memungkinkan penyuntikan header palsu, pengalihan, atau pemalsuan log.  
**Saran Perlindungan**:  
  - Validasi input untuk karakter CR (`\r`) dan LF (`\n`).  
  - Gunakan API yang aman untuk manipulasi header HTTP.  

---
### **Session Fixation**
**Cara Kerja**: Penyerang memaksa pengguna untuk menggunakan ID sesi tertentu sehingga sesi dapat diambil alih setelah autentikasi.  
**Risiko**: Membuka akses tidak sah ke akun pengguna.  
**Saran Perlindungan**:  
  - Hasilkan ID sesi baru setelah login pengguna.  
  - Gunakan cookie dengan atribut `HttpOnly` dan `Secure`.  

---

### **Unvalidated Redirects**
**Cara Kerja**: Pengguna diarahkan ke URL berbahaya karena aplikasi tidak memvalidasi tujuan pengalihan.  
**Risiko**: Membuka pintu untuk serangan phishing dan eksploitasi lainnya.  
**Saran Perlindungan**:  
  - Validasi semua URL pengalihan sebelum digunakan.  
  - Gunakan daftar putih (whitelist) untuk domain yang diizinkan.  

---

### **Command Execution**
**Cara Kerja**: Penyerang menyisipkan dan menjalankan perintah sistem operasi melalui input yang tidak aman.  
**Risiko**: Kontrol penuh atas sistem atau server dapat diambil alih.  
**Saran Perlindungan**:  
  - Validasi dan sanitasi semua input pengguna.  
  - Gunakan API yang mendukung eksekusi perintah dengan parameter terpisah.  

---

### **Cross-Site Tracing (XST)**
**Cara Kerja**: Penyerang memanfaatkan metode HTTP TRACE untuk mencuri cookie atau data sensitif lainnya.  
**Risiko**: Kebocoran informasi sensitif, terutama jika cookie tidak dilindungi dengan atribut `HttpOnly`.  
**Saran Perlindungan**:  
  - Nonaktifkan metode HTTP TRACE pada server web.  
  - Terapkan header `X-Content-Type-Options` dan `X-XSS-Protection`.  

---

### **Server-Side Template Injection (SSTI)**
**Cara Kerja**: Penyerang menyisipkan template berbahaya yang dievaluasi oleh server template.  
**Risiko**: Eksekusi perintah sistem, pencurian data, atau kontrol penuh server.  
**Saran Perlindungan**:  
  - Gunakan mesin template yang aman dan modern.  
  - Validasi dan sanitasi semua input yang diteruskan ke template.  

---

### **File Inclusion**
**Cara Kerja**: Penyerang menyisipkan file lokal atau jarak jauh ke dalam aplikasi melalui input yang tidak aman.  
**Risiko**: Akses tidak sah ke file sensitif atau eksekusi kode berbahaya.  
**Saran Perlindungan**:  
  - Nonaktifkan penyertaan file jarak jauh.  
  - Validasi dan sanitasi semua input file.  

---

### **Privilege Escalation**
**Cara Kerja**: Penyerang mengeksploitasi kelemahan sistem untuk meningkatkan hak akses mereka.  
**Risiko**: Penyerang dapat memperoleh kontrol administrator atau sistem.  
**Saran Perlindungan**:  
  - Audit hak akses secara rutin.  
  - Terapkan patch keamanan pada sistem operasi dan aplikasi.  

---

### **XML Injection**  
**Cara Kerja**: Penyisipan data XML berbahaya ke dalam parser XML.  
**Risiko**: Pengungkapan data atau kontrol sistem melalui parser.  
**Saran Perlindungan**:  
  - Nonaktifkan referensi entitas eksternal (XXE) pada parser XML.  
  - Validasi input XML sebelum diproses.  

---

### **Weak Cryptography**  
**Cara Kerja**: Penggunaan algoritma enkripsi yang lemah atau kunci yang dapat ditebak.  
**Risiko**: Data terenkripsi dapat didekripsi oleh penyerang.  
**Saran Perlindungan**:  
  - Gunakan algoritma enkripsi kuat seperti AES-256.  
  - Terapkan pengelolaan kunci yang aman.  

---

### **Deserialization Vulnerabilities**  
**Cara Kerja**: Objek yang didekodekan dari format serialisasi memuat kode berbahaya.  
**Risiko**: Eksekusi perintah jarak jauh atau akses tidak sah.  
**Saran Perlindungan**:  
  - Validasi data sebelum deserialisasi.  
  - Hindari deserialisasi dari sumber yang tidak tepercaya.  

---

### **Server-Side Request Forgery (SSRF)**
**Cara Kerja**: Penyerang memanfaatkan aplikasi untuk membuat permintaan HTTP ke sumber daya internal atau eksternal tanpa izin.  
**Risiko**: Akses tidak sah ke layanan internal, kebocoran data, atau eksploitasi sistem.  
**Saran Perlindungan**:  
  - Validasi semua URL tujuan pada server.  
  - Gunakan daftar putih (whitelist) untuk domain atau IP yang diizinkan.  
