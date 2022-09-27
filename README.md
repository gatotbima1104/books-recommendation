# Laporan Proyek Machine Learning - Muhamad Gatot Supiadin

## Domain Proyek

Domain yang dipilih pada proyek ini adalah Film, Entertaiment yang berjudul Movie Recommendation System

## Latar Belakang
Movie atau film sangat populer dikalangan remaja saat ini bahkan sekarang bisa dikatakan semua umur cocok dengan film dengan sesuai genrenya masing masing juga, rata rata Remaja menyukai genre Romance , Adventure dan banyak lainya.

oleh karena itu proyek ini dibuat dengan mengadopsi tingginya tingkat menonton film dalam Indonesia atau bahkan dunia, dimana para penonton akan dapat mudah menemui film film yang bergenre dengan keinginan mereka sehingga mereka akan menonton rekomendasi yang model berikan dan itu akan sangat membantu untuk company maupun user itu sendiri.

## Business Understanding

### Problem Statements

Berdasarkan Latar belakang diatas bisa kita sumpulkan permasalahan dan goal yang akan dicapai pada proyek ini:

- Bagaimana cara analisis data dan pemrosesan data sehingga bisa digunakan pada model rekomendasi?
- Bagaimana sistem memberikan sejumlah rekomendasi movie yang diberikan model oleh pengguna?

### Goals

Goals dari proyek ini :
- Mendapat data yang sudah dianalisis dan bisa digunakan pada model rekomendasi.
- Merekomendasikan Movie kepada user oleh sistem

### Solution statements
Berikut merupakan solusi yang bisa dilakukan guna memenuhi goals:

- Melakukan Eksploratory data dimana didalamnya termasuk seperti, analisa, eksplorasi, processing data, handling missing value, degnga visualisasi data lebih mudah dilihat dan dimengerti, berikut analisa yang bisa dilakukan:

 * Menangalisis pesebaran data pada kolom.
 * Handling Missing value pada data.
 * Membuat sistem rekomendasi yang bisa memberikan rekomendasi movie kepada user.

- Dalam proyek ini saya menggunakan teknik Content-based Filtering dimana teknik ini akan merekomendasika item yang mirip dengan item yang disukai oleh user, kebetulan pada proyek ini kita gunakan Genre sebagai parameter Content basednya dengan memanfaatkan TF-IDF Vectorizer didalamnya.

## Data Understanding
Dataset yang saya gunakan adalah Movie Recommendation yang saya ambil dari kaggle 
[Kaggle](https://www.kaggle.com/datasets/rounakbanik/the-movies-dataset).

Pada dataset ini memiliki 45466 entries dan 24 kolom dimana didalamnya seperti berikut:

- Adult : merupakan informasi bahwa movie diperuntukan untuk dewasa atau tidak
- belong_to_collection : informasi tentang yang dibawakan oleh Movie
- Budget : Biaya pembuatan Movie
- genre : genre dalam movie E.g Adventure, Horror, Thriller  
- id : Id dari movie 
- imbd_id : Id Movie
- original_languages : bahasa yang digunakan dalam Movie
- original_title : judul atau title Movie
- overview : sinopsis dari Movie
- popularity : popularitas dari Movie
- production_companies : Company yang memproduksi Movie
- production_countries : Country yang memperoduksi Movie
- release_date : Waktu rilis movie
- revenue : Pendapatan dari Movie
- runtime : Durasi waktu Movie 
- spoken_languages : bahasa yang dipakai dan diucapkan dalam Movie
- status : status dalam Movie E.g Released etc.                 
- title : Judul general Movie
- vote_average : rata rata Vote dari Movie
- vote_count  : Total vote count dari Movie


## Explatory Data Anlysis
- Drop Colomn
pada tahap ini saya drop beberapa kolom yang dapat mengganggu pada saat pemodelan agar nanti pada tahap pemodelan tidak ada kolom yang menghambat.

- Handling missing value pada dateset

![missing](https://user-images.githubusercontent.com/73319544/192563584-3c90323c-a2dc-46ff-bf7b-f496b73fb3d2.png)


Missing value pada dataset masih sangat banyak dan masih tersebar didalamnya, oleh karena itu kita drop seluruh missing value dalam dataset

![after_missing](https://user-images.githubusercontent.com/73319544/192563619-ba889e29-f1e3-4bae-b9f1-cf0bf3cc8356.png)

Berikut merupakan dataset yang sudah clean tanpa adanya missing value didalamnya dengan total entries berikut

![total](https://user-images.githubusercontent.com/73319544/192564085-2ffe823c-9e3c-4549-85c6-5f80e17781c9.png)

- Visualisasi Setiap Movie kebanyakan memakai bahasa apa yang digunakan oleh Movie

![language_based](https://user-images.githubusercontent.com/73319544/192564574-61e4777f-361e-41ec-b966-bdc4a80347ac.png)

dapat kita lihat diatas bahwa Movie kebanyakan menggunakan bahasa atau subtitle English didalamnya.

## Data Preparation

Berikut tahapan dalam pemrosesan data:

### Menghapus Fitur yang tidak diperlukan
Karena pada proyek ini kita tidak memerluka fitur seperti 'adult', 'budget', 'homepage', 'tagline', 'poster_path', dan 'video' maka kita bisa drop fitur tersebut.

### Handling missing value
pada tahap ini dalamprojek kita melakukan handling missing value dengan drop seluruh data yang memiliki missing value agar pada saat modelling tidak terhabat oleh data yang missing.
ada dua teknik dalam handling missing value diantaranya adalah drop value yang kita gunakan pada proyek ini atau mengisi mising value dengan nilai rata rata.

## Modeling

### Content Based Filtering
Content Based Filtering merekomendasikan item yang mirip dengan item sebelumnya yang disukai atau dipilih oleh pengguna. Kemiripan item dihitung berdasarkan pada fitur-fitur yang ada pada item yang dibandingkan.

disini saya menggunakan TF-IDF Vectorize untuk menemukan representasi dari setiap genre pada movie berikut outputnya :

![genres](https://user-images.githubusercontent.com/73319544/192570237-4f70f30e-3a17-4938-a0fb-dc48575e9e86.png)

selanjutnya melakukan fit dan transformasi kedalam bentuk matriks. dengan teknik kesamaan (similarity degree) antar movie untuk menghitung derajat kesamaan dengan fungsi cosine_similarity dari library sklearn. 

![rumus](https://user-images.githubusercontent.com/73319544/192570880-f316903a-7285-4e9c-b564-b6d12095a251.png)

- berikut outputnya

![sigmoid](https://user-images.githubusercontent.com/73319544/192571066-caf44e98-f06c-44af-b3e9-7e528ab44394.png)

kemudian mengambil sejumlah nilai k tertinggi dari similarity data kemudian mengambil data dari bobot (tingkat kesamaan) tertinggi ke terendah.

kemudia saya menguji akurasi model pada sistem rekomendasi dengan memasukkan judul Jurassic Park sistem akan merekomendasikan film yang mirip dengan Jurassci Park, berikut outputnya :

![jurasik](https://user-images.githubusercontent.com/73319544/192572488-e248f365-0535-416b-b6a6-715926d15354.png)

berdasarkan output diatas yang telah dimasukkan, kita bisa lihat rekomendasi dibawah ini yang diberikan oleh sistem yang diharapkan adalah film yang bergenre sama.

berikut output yang diberikan sistem:

![rekomendasi](https://user-images.githubusercontent.com/73319544/192573534-16a33677-1956-4366-b1e0-f85a140108ed.png)



## Evaluation
Pada bagian ini Anda perlu menyebutkan metrik evaluasi yang digunakan. Kemudian, jelaskan hasil proyek berdasarkan metrik evaluasi tersebut.

Ingatlah, metrik evaluasi yang digunakan harus sesuai dengan konteks data, problem statement, dan solusi yang diinginkan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan formula metrik dan bagaimana metrik tersebut bekerja.

**---Ini adalah bagian akhir laporan---**

_Catatan:_
- _Anda dapat menambahkan gambar, kode, atau tabel ke dalam laporan jika diperlukan. Temukan caranya pada contoh dokumen markdown di situs editor [Dillinger](https://dillinger.io/), [Github Guides: Mastering markdown](https://guides.github.com/features/mastering-markdown/), atau sumber lain di internet. Semangat!_
- Jika terdapat penjelasan yang harus menyertakan code snippet, tuliskan dengan sewajarnya. Tidak perlu menuliskan keseluruhan kode project, cukup bagian yang ingin dijelaskan saja.
