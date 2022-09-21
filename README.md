# Laporan Proyek Akhir - Lalu Habib Satya Wiguna

## Project Overview
Buku merupakan jendela dunia. Dengan membaca buku tentu seseorang dapat memperoleh banyak ilmu yang bermanfaaat. Salah satu manfaat buku yaitu memperluas wawasan kita tentang dunia. Begitu pentingnya buku sehingga di era perkembangan teknologi saat ini kita bisa membaca buku secara online melalui internet[^1]. Namun seringkali setelah selesai membaca suatu buku, seseorang bingung akan membaca buku apa selanjutnya. Tentu tidak mungkin bagi seseorang untuk menelusuri buku satu per satu karena akan membuang-buang waktu. Oleh karena itu diperlukan suatu sistem yang dapat merekomendasikan buku apa yang perlu dibaca selanjutnya dengan cara melihat kemiripan buku yang telah dibaca sebelumnya dengan buku lainnya. Apalagi saat ini banyak sekali perpustakaan berbasis online yang sering dikunjungi oleh mahasiswa untuk mendapatkan referensi terkait dengan tugas atau penelitiannya[^2]. Dengan menggunakan _Machine Learning_, data-data riwayat baca buku pengguna dapat diproses menjadi sebuah sistem rekomendasi yang bisa menghasilkan rekomendasi buku-buku yang relevan kepada pengguna lainnya.  

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
![authors](https://user-images.githubusercontent.com/74854925/191403572-9c7a5a0c-6010-40c1-9a40-50d1d402ad5b.png)

- Vintage merupakan penerbit yang menerbitkan buku terbanyak dengan total 318 buku yang telah diterbitkan di bawah nama Vintage.  
![publisher](https://user-images.githubusercontent.com/74854925/191403597-3a3e24ee-a6f1-489c-b72d-7fefa958a5b4.png)

- Dari total 27 bahasa, Inggris merupakan bahasa yang paling banyak digunakan pada buku yang ada di dataset dengan total 8908 buku yang ditulis dalam bahasa Inggris.  
![language](https://user-images.githubusercontent.com/74854925/191403618-fb39ec22-efa3-406c-ae04-80d5fba31e80.png)

- Tahun 2006 merupakan tahun di mana buku paling banyak diterbitkan dengan total 1700 buku yang diterbitkan pada tahun tersebut.  
![year](https://user-images.githubusercontent.com/74854925/191404064-26611a47-656f-46b8-b7ec-022bc3937845.png)

- Buku dengan judul Twilight menempati posisi teratas untuk buku dengan rating terbanyak yang diberikan.  
![ratingcounts](https://user-images.githubusercontent.com/74854925/191404080-7989645f-3a74-4025-9301-e155d858c266.png)

- Buku dengan judul Harry Potter and the Half-Blood Prince menempati posisi teratas untuk buku dengan rating tertinggi.  
![ratingtop](https://user-images.githubusercontent.com/74854925/191404111-4e8a4780-28c5-40e6-ad44-381ea6873070.png)

- Variabel average_rating dengan variabel language memiliki distribusi penyebaran yang baik sehingga kedua variabel tersebut akan digunakan untuk merekomendasikan buku nanti.  
![corr](https://user-images.githubusercontent.com/74854925/191404122-76e5ec44-afef-4e63-8cc3-f6c3c1306625.png)

## Data Preparation
Untuk mempermudah dalam memproses data ketika tahap pemodelan nanti, maka perlu dilakukan persiapan pada dataset. Berikut proses persiapan data yang dilakukan.  

### Creating New Column
Untuk memudahkan pengelompokan pada rating, akan dibuat kolom baru dengan nama "rating_between" yang berisikan rating-rating yang telah dikelompokkan berdasarkan nilainya yaitu untuk rating antara nilai 0 sampai 1 akan dikelompokkan ke dalam 'between 0 and 1', untuk rating antara nilai 1 sampai 2 akan dikelompokkan ke dalam 'between 1 and 2', untuk rating antara nilai 2 sampai 3 akan dikelompokkan ke dalam 'between 2 and 3', untuk rating antara nilai 3 sampai 4 akan dikelompokkan ke dalam 'between 3 and 4', untuk rating antara nilai 4 sampai 5 akan dikelompokkan ke dalam 'between 4 and 5'. Tujuan dari dilakukannya hal tersebut adalah agar sistem rekomendasi yang dibuat dapat bekerja dengan maksimal untuk menghasilkan rekomendasi yang baik.

### Creating New DataFrame
Pada tahap ini, masing-masing kolom "rating_between" dan kolom "language" akan digunakan untuk membuat sebuah DataFrame baru. Kemudian kedua DataFrame tersebut akan digabungkan dengan kolom "average_rating" dan "ratings_count" untuk menghasilkan sebuah DataFrame baru dengan tujuan agar DataFrame yang diolah berisikan fitur-fitur yang paling berpengaruh dalam proses rekomendasi yaitu rating dan bahasa.

### Normalization
Proses normalisasi dilakukan untuk menskalakan setiap fitur yang ada pada dataset ke dalam rentang tertentu. Penskalaan ini juga berfungsi untuk mengurangi bisa karena beberapa buku memiliki banyak fitur. Secara garis besar, akan dilakukan distribusi dari nilai pada setiap fitur ke dalam rentang nilai 0 sampai 1.

## Modeling and Result
Untuk proyek kali ini, akan digunakan _Content Based Filtering_ pada sistem rekomendasinya. _Content Based Filtering_ akan memberikan rekomendasi buku berdasarkan rating yang telah diberikan sebelumnya untuk suatu buku. Dari data rating buku, kita akan mengidentifikasi buku-buku yang mirip dengan menggunakan algoritma K-Nearest Neighbor (KNN) untuk direkomendasikan ke pengguna. KNN adalah algoritma yang relatif sederhana dibandingkan dengan algoritma lain. Algoritma KNN menggunakan 'kesamaan fitur' untuk memprediksi nilai dari setiap data yang baru. Dengan kata lain, setiap data baru diberi nilai berdasarkan seberapa mirip titik tersebut dalam set pelatihan. KNN bekerja dengan membandingkan jarak satu sampel ke sampel pelatihan lain dengan memilih sejumlah k tetangga terdekat (dengan k adalah sebuah angka positif). Nah, itulah mengapa algoritma ini dinamakan K-nearest neighbor (sejumlah k tetangga terdekat). KNN bisa digunakan untuk kasus klasifikasi dan regresi. Pada kali ini, kita akan menggunakannya untuk membuat sebuah sistem rekomendasi. Penjelasan untuk setiap parameter yang ada pada model KNN sebagai berikut:  
- n_neighbors : merepresentasikan jumlah tetangga terdekat dari titik yang akan dihitung, secara _default_ nilainya adalah 5.  
- weights : fungsi pembobotan yang akan digunakan dalam menghitung jarak antara tetangga terdekat dengan titik yang dimasukkan, bisa diisi dengan _{'uniform', 'distance'} atau callable_, namun secara _default_ menggunakan _'uniform'_.   
- algorithm : jenis algoritma yang akan digunakan untuk proses penghitungan tetangga terdekat, bisa diisi dengan *{'auto', 'ball_tree', 'kd_tree', 'brute'}*, namun secara _default_ menggunakan _'auto'_.  
- leaf_size : ukuran atau size yang mengontrol titik dalam node tertentu, secara _default_ nilainya adalah 30.  
- p : power parameter untuk metrik yang menghitung jarak antara titik tertentu, secara _default_ nilainya adalah 2.  
- metric : metrik yang digunakan pada tree, secara _default_ akan menggunakan metrik _'minkowski'_.  
- metric_params : keyword tambahan untuk metric function, secara _default_ nilainya adalah _None_.  
- n_jobs : banyaknya penugasan parallel untuk menjalankan pencarian tetangga terdekat, secara _default_ nilainya adalah _None_. 

Untuk model yang akan dibuat nanti, parameter yang digunakan adalah n_neighbors saja untuk mengatur berapa banyak jumlah tetangga terdekat yang akan diambil. Untuk parameter yang lain akan digunakan nilai _default_ saja.

### Tuning Parameter
Proses _tuning parameter_ ini akan memasukkan data ke dalam model KNN dengan parameter n_neighbors=11 yang berarti kita akan mengambil 10 buku teratas yang memiliki kemiripan untuk direkomendasikan kepada pengguna. hal ini dilakukan karena buku pertama akan mengarah ke buku itu sendiri, oleh karena itu untuk mengambil 10 buku teratas kita akan melewati 1 buku pertama dan menyimpan 10 buku setelahnya dengan menggunakan nilai 11 pada parameter n_neighbors.
 
### Building Books Recommender Function
Membuat sebuah _function_ yang berfungsi untuk melakukan _filtering_ terhadap buku yang akan direkomendasikan dengan parameter _function_ yaitu judul buku. Dari judul buku tersebut kemudian akan dicari buku lain yang memiliki kemiripan dengan menggunakan model KNN yang telah dibuat sebelumnya. _Function_ ini akan mengembalikan list dengan isi judul-judul buku yang memiliki fitur mirip dengan judul buku yang dimasukkan.

### Testing The Model
Melakukan pengujian terhadap model yang telah dibuat dengan cara memasukkan satu judul buku yang akan menjadi parameter untuk _function_ yang telah dibuat sebelumnya. Pengujian dilakukan dengan memasukkan buku berjudul "The Book Thief". Dari hasil pengujian ini, didapatkan 10 buku yang memiliki kemiripan fitur dengan buku yang dimasukkan sebelumnya.

| Books_Title                    |
|--------------------------------|
| The Giver (The Giver #1)       |
| Jane Eyre                      |
| The Lightning Thief            |
| Little Women                   |
| Charlotte's Web                |
| Memoirs of a Geisha            |
| Water for Elephants            |
| The Notebook (The Notebook #1) |
| Gone with the Wind             |
| The Shining                    |

## Evaluation
Pada tahap ini akan dilakukan evaluasi terhadap model yang telah dibuat. Jika prediksi mendekati nilai sebenarnya, performanya baik. Sedangkan jika tidak, performanya buruk. Oleh karena itu evaluasi perlu dilakukan untuk mengetahui performa dari model yang telah dibuat. Evaluasi ini akan dilakukan dengan menggunakan _cosine similarity_ . _Cosine similarity_ berfungsi untuk melihat apakah ada kemiripan antara buku yang satu dengan yang lainnya dengan menggunakan fitur-fitur yang sebelumnya telah didapatkan. Dengan menggunakan _cosine similarity_ kemiripan akan dilihat berdasarkan nilai pada sudut cosine yang dibentuk dengan cara menghitung _angle_ yang diberikan dari dua buah vektor _items_. Nantinya hasil perhitungan tersebut akan memperlihatkan nilai antara 0-1. Semakin dekat nilai dengan angka 0 maka semakin sedikit kemiripan antara dua buah _items_ tersebut, sebaliknya semakin dekat dengan 1 berarti _items_ tersebut memiliki kemiripan pada fitur-fiturnya. _Output_ akan bernilai 1 apabila sebuah _item_ dibandingkan dengan _item_ itu sendiri.

| Books_Title                    | cosine_similarity |
|--------------------------------|-------------------|
| The Giver (The Giver #1)       | 0.990494          |
| Jane Eyre                      | 0.982311          |
| The Lightning Thief            | 0.987542          |
| Little Women                   | 0.987492          |
| Charlotte's Web                | 0.973157          |
| Memoirs of a Geisha            | 0.969277          |
| Water for Elephants            | 0.980956          |
| The Notebook (The Notebook #1) | 0.983033          |
| Gone with the Wind             | 0.987770          |
| The Shining                    | 0.993691          |

Dari hasil evaluasi di atas, dapat dilihat buku-buku yang direkomendasikan memiliki nilai _cosine similarity_ yang hampir mendekati angka 1. Dapat disimpulkan bahwa sistem rekomendasi yang dibuat sudah bisa memberikan hasil rekomendasi yang relevan.

## Conclusion
Berdasarkan percobaan yang telah dilakukan untuk membangun sebuah sistem rekomendasi, didapatkan kesimpulan sebagai berikut:
1. Rating dan bahasa merupakan fitur yang paling berpengaruh pada dataset yang digunakan dalam membangun sebuah sistem rekomendasi. 
2. Buku-buku yang direkomendasikan telah relevan dengan buku yang dijadikan sebagai acuan karena dari hasil pengujian menggunakan _cosine similarity_, seluruh buku yang direkomendasikan hampir mendekati angka 1 yang berarti buku-buku tersebut memiliki kemiripan dari segi fiturnya.

## References
[^1]: [Pemanfaatan Buku Oleh Mahasiswa Sebagai Penunjang Aktivitas Akademik di Era Generasi Milenial](http://jurnal.uin-antasari.ac.id/index.php/pustakakarya/article/view/3710)  
[^2]: [Model Klasifikasi Analisis Kepuasan Pengguna Perpustakaan Online Menggunakan K-Means dan Decission Tree](https://scholar.google.co.id/scholar_url?url=http://ejurnal.stmik-budidarma.ac.id/index.php/jurikom/article/download/3680/2426&hl=en&sa=X&ei=eHIqY5PfLPuSy9YP1Lyz8AQ&scisig=AAGBfm1NYL2GxbwFk7aY5cWKrf1b8jImVg&oi=scholarr)