LAPORAN PRAKTIKUM 3 :CSS Dasar
MATA KULIAH :PEMROGRAMAN Web
NAMA:Albert Maulana
NIM:312510162
Struktur repository
Lab3Web/
├── lab2_css_dasar.html     # dokumen HTML (berisi CSS internal + inline)
├── style_eksternal.css     # file CSS eksternal
├── README.md               # laporan ini
└── screenshots/            # tangkapan layar setiap langkah
LANGKAH 1 :Membuat dokumen html 
Pertama saya membuat file baru bernama lab2_css_dasar.html di VSCode, lalu mengisinya dengan struktur dasar HTML dari modul: ada <header> berisi judul <h1>, <nav> berisi tiga tautan, dan <div id="intro"> berisi judul, paragraf, serta tautan bertombol dengan class="button btn-primary". Saat dibuka di browser, tampilannya masih polos karena belum ada CSS sama sekali
<img width="1920" height="1080" alt="Screenshot (122)" src="https://github.com/user-attachments/assets/258d2fee-6bb3-4972-89fc-9e221845e34e" />
Langkah 2:mendeklarasikan CSS internal 
CSS internal di tulis di dalam tag <style>.saya menambahkan aturan body,header,h1,dan h1 i:
<style>
    body { font-family: 'Open Sans', sans-serif; }
    header { min-height: 80px; border-bottom: 1px solid #77CCEF; }
    h1 { font-size: 24px; color: #0F189F; text-align: center; padding: 20px 10px; }
    h1 i { color: #6d6a6b; }
</style>
setelah di simpan dan broswer di refresh,semua judul menjadi biru,rata tengah ,dan kata inline CSS berwarna abu -abu karena kena aturan h1 i.
<img width="1600" height="900" alt="120" src="https://github.com/user-attachments/assets/fcdf0897-6317-4c43-87f2-4cae0babfe91" />
LANGKAH 3:Menambahkan inline CSS
Inline CSS ditulis langsung sebagai atribut style pada tag HTML. Saya menambahkannya pada tag <p>:
<p style="text-align: center; color: #ccd8e4;">
paragraf jadi rata tengah dengan warna .aturan ini berlaku satu paragraf saja .
<img width="1600" height="900" alt="121" src="https://github.com/user-attachments/assets/a0cd192b-86b4-49b6-ba68-6cc89c26abd4" />
  Langkah 4 :membuat CSS eksternal
Saya membuat file baru style_eksternal.css berisi aturan untuk nav, nav a, serta nav .active dan nav a:hover. Setelah itu file dihubungkan ke HTML memakai tag <link> di dalam <head>:
<link rel="stylesheet" href="style_eksternal.css" type="text/css">
Hasilnya menu navigasi berubah menjadi bar hijau dengan teks putih tanpa garis bawah.
<img width="1600" height="900" alt="122" src="https://github.com/user-attachments/assets/7d8bf6a3-5446-4463-affd-a0dae197e88e" />
Langkah 5 Menambahkan CSS Selector (id dan class)
pada style_eskternal.css
-ID selector #intro dan #intro h1, diawali tanda #. Pada HTML dipakai id="intro" tanpa tanda #. Satu id hanya boleh dipakai satu kali dalam satu halaman.
-Class selector .button dan .btn-primary, diawali tanda titik. Pada HTML dipakai class="button btn-primary" tanpa titik, dan satu elemen boleh punya lebih dari satu class.
Hasilnya kotak intro berwarna biru, judul "Hello World" putih rata kiri, dan tautan berubah menjadi tombol merah
<img width="1600" height="900" alt="123" src="https://github.com/user-attachments/assets/7b69b46a-3462-473a-b5a0-80debb5b4533" />
langkah 6 :validasi CSS
File style_eksternal.css saya validasi lewat https://jigsaw.w3.org/css-validator/ (pilih tab By file upload, upload file CSS, lalu klik Check). Hasil yang diharapkan: tidak ada error
JAWABAN PERTANYAAN DAN TUGAS
1. Eksperimen mengubah dan menambah properti CSS
Saya menambahkan beberapa properti baru di style_eksternal.css:

#intro {
    border-radius: 8px;                          /* sudut kotak melengkung */
    box-shadow: 0 4px 10px rgba(0, 0, 0, 0.25);  /* bayangan */
}
.button {
    border-radius: 6px;
    font-weight: bold;
}
.button:hover {
    background: #b01e32;                         /* warna tombol berubah saat kursor di atasnya */
}
Hasilnya kotak intro jadi melengkung dan punya bayangan, tombol menjadi tebal dan melengkung, serta warnanya lebih gelap saat kursor diarahkan ke tombol. Gambar 5 di atas sudah memakai properti-properti ini.

2. Perbedaan h1 { ... } dengan #intro h1 { ... }
h1 { ... } adalah selector elemen. Aturannya berlaku untuk semua tag <h1> di halaman.
#intro h1 { ... } adalah selector turunan (descendant) dengan ID. Aturannya hanya berlaku untuk <h1> yang berada di dalam elemen ber-id="intro".
Karena #intro h1 lebih spesifik, aturannya menang bila bentrok dengan h1 biasa. Di praktikum ini terlihat jelas: h1 di <header> tetap biru dan rata tengah (aturan h1), sedangkan h1 "Hello World" di dalam #intro menjadi putih dan rata kiri (aturan #intro h1), padahal keduanya sama-sama tag <h1>.

3. Internal, eksternal, dan inline CSS pada elemen yang sama
Yang tampil di browser adalah inline CSS. Alasannya, inline punya prioritas tertinggi dibanding internal maupun eksternal.

Untuk internal dan eksternal, bobot (specificity) keduanya sama, sehingga yang menang adalah aturan yang dibaca paling akhir (prinsip cascading). Jadi bila <link> diletakkan sebelum <style>, internal yang menang. Bila <link> diletakkan sesudah <style>, eksternal yang menang.

Contoh:

/* style_eksternal.css */
p { color: green; }
<head>
    <link rel="stylesheet" href="style_eksternal.css">
    <style> p { color: red; } </style>
</head>
<body>
    <p style="color: blue;">Teks ini berwarna biru</p>
    <p>Teks ini berwarna merah</p>
</body>
Paragraf pertama biru (inline menang), paragraf kedua merah (internal menang karena ditulis setelah <link>). Urutan prioritasnya: inline > internal/eksternal (yang terakhir dibaca). Pengecualian: deklarasi yang memakai !important mengalahkan inline sekalipun.

4. Elemen dengan ID dan Class sekaligus: <p id="paragraf-1" class="textparagraf">
Yang tampil adalah deklarasi ID selector, karena ID lebih spesifik daripada class. Bobot specificity: ID bernilai lebih tinggi dari class, dan class lebih tinggi dari selector elemen. Urutannya kira-kira: inline > ID > class > elemen.

Contoh:

.textparagraf { color: red; }
#paragraf-1   { color: green; }
<p id="paragraf-1" class="textparagraf">Paragraf ini berwarna hijau</p>
Paragraf berwarna hijau, walaupun .textparagraf ditulis lebih dulu atau lebih belakang. Hasilnya tidak bergantung pada urutan penulisan, karena bobot ID lebih besar. Properti yang tidak bentrok tetap digabung, misalnya bila class mengatur font-size dan ID mengatur color, kedua aturan itu tetap berlaku.





