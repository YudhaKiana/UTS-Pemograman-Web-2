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

<?php
$conn = mysqli_connect("localhost","root","","security_lab");

$username = $_POST['username'];
$password = $_POST['password'];

$query = "SELECT * FROM users WHERE username='$username' AND password='$password'";
$result = mysqli_query($conn, $query);

if(mysqli_num_rows($result) > 0){
    echo "Login berhasil!";
}else{
    echo "Login gagal!";
}
?>

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

<?php
$conn = mysqli_connect("localhost","root","","security_lab");

$stmt = $conn->prepare("SELECT * FROM users WHERE username=? AND password=?");
$stmt->bind_param("ss", $_POST['username'], $_POST['password']);
$stmt->execute();
$result = $stmt->get_result();

if($result->num_rows > 0){
    echo "Login berhasil!";
}else{
    echo "Login gagal!";
}
?>

🔎 Hasil Setelah Mitigasi
Payload SQL Injection tidak lagi berhasil. ✔️

🧪 Eksperimen 2 — Cross Site Scripting (XSS)
1️⃣ Versi Rentan
File: comment_vulnerable.php

<form method="POST">
<textarea name="comment"></textarea>
<button type="submit">Kirim</button>
</form>

<?php
echo $_POST['comment'];
?>

🧨 Payload XSS

Masukkan komentar:

<script>alert('XSS berhasil')</script>

🔎 Hasil

Popup muncul saat halaman dibuka.
Browser menjalankan script dari user.

✅ XSS berhasil.

2️⃣ Versi Aman

File: comment_secure.php

<form method="POST">
<textarea name="comment"></textarea>
<button type="submit">Kirim</button>
</form>

<?php
if(isset($_POST['comment'])){
    echo htmlspecialchars($_POST['comment'], ENT_QUOTES, 'UTF-8');
}
?>

🔎 Hasil Setelah Mitigasi
Script tidak dijalankan, hanya tampil sebagai teks. ✔️

Disclaimer

Project ini hanya untuk pembelajaran keamanan web secara etis.

 Screenshot hasil plagiasi:
<img width="1859" height="826" alt="Screenshot 2026-04-27 202144" src="https://github.com/user-attachments/assets/802f9bf8-7aa0-4ad9-a715-971339206ed1" />


