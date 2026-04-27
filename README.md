# UTS-Pemograman-Web-2

# Web Security Lab – SQL Injection & XSS Experiment
Deskripsi Project
Repository ini berisi eksperimen pribadi untuk memahami celah keamanan web paling umum:

SQL Injection
Cross-Site Scripting (XSS)

Eksperimen dilakukan menggunakan PHP + MySQL (XAMPP) pada lingkungan lokal.

⚠️ Project ini dibuat hanya untuk tujuan edukasi.

# Tujuan Eksperimen
1. Memahami bagaimana serangan bekerja
2. Mencoba eksploitasi pada aplikasi sederhana
3. Mempelajari cara mitigasi (secure coding)

# Environment
| Tools   | Versi  |
| ------- | ------ |
| PHP     | 8.x    |
| MySQL   | 8.x    |
| Apache  | XAMPP  |
| Browser | Chrome |

# Struktur Project
web-security-lab/
│
├── database.sql
├── login_vulnerable.php
├── login_secure.php
├── comment_vulnerable.php
├── comment_secure.php
└── README.md

# Setup Database
File: database.sql
CREATE DATABASE security_lab;
USE security_lab;

CREATE TABLE users (
  id INT AUTO_INCREMENT PRIMARY KEY,
  username VARCHAR(50),
  password VARCHAR(50)
);

INSERT INTO users VALUES (1,'admin','12345');

# Eksperimen 1 — SQL Injection
1️⃣ Versi Rentan (Vulnerable Login)

File: login_vulnerable.php

<img width="1030" height="430" alt="Screenshot 2026-04-27 203739" src="https://github.com/user-attachments/assets/0e054008-5b54-4db9-aff1-ebb550f37e08" />


🧨 Payload Serangan

Input pada form login:

Username:
admin' --
Password:
bebas

🔎 Hasil Eksperimen

Login berhasil tanpa password.
Query berubah menjadi:

SELECT * FROM users WHERE username='admin' -- ' AND password='bebas'

✅ SQL Injection berhasil.

2️⃣ Versi Aman (Secure Login)

File: login_secure.php

<img width="991" height="412" alt="Screenshot 2026-04-27 203954" src="https://github.com/user-attachments/assets/e73dcb5e-50fc-42c3-a30b-e0cc919ccb12" />


🔎 Hasil Setelah Mitigasi
Payload SQL Injection tidak lagi berhasil. ✔️

🧪 Eksperimen 2 — Cross Site Scripting (XSS)

1️⃣ Versi Rentan

File: comment_vulnerable.php

<img width="650" height="240" alt="Screenshot 2026-04-27 204059" src="https://github.com/user-attachments/assets/62f38998-a4d9-4798-9ad6-f8e468a30337" />


🧨 Payload XSS

Masukkan komentar:

<script>alert('XSS berhasil')</script>

🔎 Hasil

Popup muncul saat halaman dibuka.
Browser menjalankan script dari user.

✅ XSS berhasil.

2️⃣ Versi Aman

File: comment_secure.php

<img width="833" height="296" alt="Screenshot 2026-04-27 204309" src="https://github.com/user-attachments/assets/f89476cc-bb31-4120-b024-b3cf651022ed" />


🔎 Hasil Setelah Mitigasi
Script tidak dijalankan, hanya tampil sebagai teks. ✔️

Disclaimer

Project ini hanya untuk pembelajaran keamanan web secara etis.

 Screenshot hasil plagiasi:
<img width="1859" height="826" alt="Screenshot 2026-04-27 202144" src="https://github.com/user-attachments/assets/802f9bf8-7aa0-4ad9-a715-971339206ed1" />


