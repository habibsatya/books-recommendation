# Laporan Proyek Akhir - Lalu Habib Satya Wiguna

## Project Overview
Buku merupakan jendela dunia. Dengan membaca buku tentu seseorang dapat memperoleh banyak ilmu yang bermanfaaat. Salah satu manfaat buku yaitu memperluas wawasan kita tentang dunia. Begitu pentingnya buku sehingga di era perkembangan teknologi saat ini kita bisa membaca buku secara online melalui internet[^1]. Namun seringkali setelah selesai membaca suatu buku, seseorang bingung akan membaca buku apa selanjutnya. Tentu tidak mungkin bagi seseorang untuk menelusuri buku satu per satu karena akan membuang-buang waktu. Oleh karena itu diperlukan suatu sistem yang dapat merekomendasikan buku apa yang perlu dibaca selanjutnya dengan cara melihat kemiripan buku yang telah dibaca sebelumnya dengan buku lainnya. Apalagi saat ini banyak sekali perpustakaan berbasis online yang sering dikunjungi oleh mahasiswa untuk mendapatkan referensi terkait dengan tugas atau penelitiannya[^2]. Dengan menggunakan _Machine Learning_, data-data riwayat baca buku pengguna dapat diproses menjadi sebuah sistem rekomendasi yang bisa menghasilkan rekomendasi buku-buku yang relevan kepada pengguna lainnya.  
[^1]: [Pemanfaatan Buku Oleh Mahasiswa Sebagai Penunjang Aktivitas Akademik di Era Generasi Milenial](http://jurnal.uin-antasari.ac.id/index.php/pustakakarya/article/view/3710)  
[^2]: [Model Klasifikasi Analisis Kepuasan Pengguna Perpustakaan Online Menggunakan K-Means dan Decission Tree](https://scholar.google.co.id/scholar_url?url=http://ejurnal.stmik-budidarma.ac.id/index.php/jurikom/article/download/3680/2426&hl=en&sa=X&ei=eHIqY5PfLPuSy9YP1Lyz8AQ&scisig=AAGBfm1NYL2GxbwFk7aY5cWKrf1b8jImVg&oi=scholarr)

## Business Understanding
Saat ini, sistem rekomendasi menjadi teknik dan strategi yang sangat bagus bagi suatu perusahaan untuk mendapatkan profit yang lebih tinggi. Tidak terkecuali bagi perpustakaan online yang dapat menggunakan sistem rekomendasi tersebut untuk meningkatkan kepuasan pembaca dengan tetap memberikan buku-buku yang relevan dengan preferensi pembaca. Semakin puas seorang pengguna maka semakin setia juga pengguna tersebut menggunakan platformnya. Oleh karena itu diperlukan sistem rekomendasi yang bagus demi mengembangkan pelayanan dan kepuasan pengguna. Dengan menggunakan data pengguna yang ada, akan dilakukan proses untuk mengembangkan sebuah sistem rekomendasi yang dapat merekomendasikan buku yang relevan dengan apa yang sudah dibaca oleh pengguna.

### Problem Statement
Berdasarkan kondisi yang telah diuraikan sebelumnya, didapatkan permasalahan sebagai berikut:
- Dari fitur-fitur yang ada pada data, fitur manakah yang paling berpengaruh dalam melakukan rekomendasi buku?
- Apakah buku-buku yang direkomendasikan sudah relevan dengan data yang sudah ada?

### Goals
Untuk menjawab pertanyaan tersebut, dibuuatlah sistem rekomendasi dengan goals sebagai berikut:
- Mengetahui fitur yang paling berpengaruh dalam melakukan rekomendasi buku.
- Membuat sistem rekomendasi yang dapat memberikan hasil paling relevan dengan menggunakan data yang sudah ada.

### Solution Statements
- Untuk mengetahui fitur yang paling berpengaruh terhadap sistem dalam merekomendasikan buku, perlu dilakukan analisis terhadap fitur-fitur yang terdapat pada data yang ada. Setelah mengetahui hal tersebut, barulah akan dilakukan pengembangan sistem rekomendasi untuk memberikan hasil yang maksimal terhadap buku yang relevan dengan buku apa yang telah dibaca oleh pengguna. Oleh karena itu, dengan menggunakan metode _content based filtering_, sistem akan mengetahui buku apa yang paling relevan untuk pengguna.
- Metrik yang akan digunakan untuk mengukur sejauh mana performa sistem rekomendasi adalah Cosine Similarity. Secara garis besar, Cosine Similarity menghitung besar sudut cosine yang terdapat pada dua buah _item_.

## Data Understanding
Dataset yang digunakan untuk mendukung penelitian pada pembuatan sistem rekomendasi ini adalah [Goodreads-books](https://www.kaggle.com/datasets/jealousleopard/goodreadsbooks) yang didapatkan dari situs [kaggle](https://www.kaggle.com). Dataset ini berisi 11123 data buku dengan 12 kolom. Masing-masing kolom tersebut akan dijadikan fitur untuk mendukung pembuatan sistem rekomendasi. Variabel-variabel yang terdapat pada dataset sebagai berikut:
- bookID : kode unik dari setiap buku.
- title : nama atau judul dari buku.
- authors : nama dari penulis buku.
- average_rating : rata-rata penilaian dari setiap buku.
- isbn : kode unik buku yang merujuk pada ISBN (International Standard Book Number).
- isbn13 : 13-digit ISBN untuk mengidentifikasi buku.
- language_code : kode bahasa dari buku, misalnya 'eng' untuk English.
- num_pages : jumlah halaman dari buku.
- ratings_count : total penilaian yang didapatkan dari suatu buku.
- text_reviews_count : total teks review yang diperoleh oleh suatu buku.
- publication_date : tanggal buku dirilis ke publik.
- publisher : nama penerbit yang menerbitkan buku.

### Exploratory Data Analysis
Exploratory Data Analysis atau sering disingkat EDA merupakan proses investigasi awal pada data untuk menganalisis karakteristik, menemukan pola, anomali, dan memeriksa asumsi pada data. Setelah dilakukan Exploratory Data Analysis pada dataset yang digunakan, didapatkan kesimpulan sebagai berikut:
- Dari total 4484 penulis dapat kita lihat Top-10 penulis dengan buku terbanyak yang telah ditulis. Author dengan buku terbanyak yang ditulis adalah Stephen King sebanyak 40 buku.
- Vintage merupakan penerbit yang menerbitkan buku terbanyak dengan total 318 buku yang telah diterbitkan di bawah nama Vintage.
- Dari total 27 bahasa, Inggris merupakan bahasa yang paling banyak digunakan pada buku yang ada di dataset dengan total 8908 buku yang ditulis dalam bahasa Inggris.
- Tahun 2006 merupakan tahun di mana buku paling banyak diterbitkan dengan total 1700 buku yang diterbitkan pada tahun tersebut.
- Buku dengan judul Twilight menempati posisi teratas untuk buku dengan rating terbanyak yang diberikan.
- Buku dengan judul Harry Potter and the Half-Blood Prince menempati posisi teratas untuk buku dengan rating tertinggi.
- Tidak ada korelasi khusus antara variabel average_rating dengan variabel ratings_count, text_reviews_count, dan num_pages.
- Variabel average_rating dengan variabel language memiliki distribusi penyebaran yang baik sehingga kedua variabel tersebut akan digunakan untuk merekomendasikan buku nanti.

