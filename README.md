# Laporan Proyek Machine Learning - Muhamad Gatot Supiadin

## Domain Proyek

Domain yang dipilih pada proyek ini adalah Film, Entertaiment yang berjudul MovieTV Recommendation System

## Latar Belakang
Movie atau film sangat populer dikalangan remaja saat ini bahkan sekarang bisa dikatakan semua umur cocok dengan film dengan sesuai genrenya masing masing juga, rata rata Remaja menyukai genre Romance , Adventure dan banyak lainya.

oleh karena itu proyek ini dibuat dengan mengadopsi tingginya tingkat menonton film dalam Indonesia atau bahkan dunia, dimana para penonton akan dapat mudah menemui film film yang bergenre dengan keinginan mereka sehingga mereka akan menonton rekomendasi yang model berikan dan itu akan sangat membantu untuk company maupun user itu sendiri.

## Business Understanding

### Problem Statements

Berdasarkan Latar belakang diatas bisa kita sumpulkan permasalahan dan goal yang akan dicapai pada proyek ini:

- Bagaimana cara analisis data dan pemrosesan data sehingga bisa digunakan pada model rekomendasi?
- Bagaimana sistem memberikan sejumlah rekomendasi movieTV yang diberikan model oleh pengguna?

### Goals

Goals dari proyek ini :
- Mendapat data yang sudah dianalisis dan bisa digunakan pada model rekomendasi.
- Merekomendasikan MovieTV kepada user oleh sistem.

### Solution statements
Berikut merupakan solusi yang bisa dilakukan guna memenuhi goals:

- Melakukan Eksploratory data dimana didalamnya termasuk seperti, analisa, eksplorasi, processing data, handling missing value, degnga visualisasi data lebih mudah dilihat dan dimengerti, berikut analisa yang bisa dilakukan:

 * Menangalisis pesebaran data pada kolom.
 * Handling Missing value pada data.
 * Membuat sistem rekomendasi yang bisa memberikan rekomendasi movie kepada user.

- Dalam proyek ini saya menggunakan teknik Content-based Filtering dimana teknik ini akan merekomendasika item yang mirip dengan item yang disukai oleh user, kebetulan pada proyek ini kita gunakan **genre** sebagai parameter Content basednya dengan memanfaatkan 
 - TF-IDF Vectorizer  
 - Cosine similarity
didalamnya.

## Data Understanding
Dataset yang saya gunakan adalah Movie Recommendation yang saya ambil dari kaggle 
[Kaggle](https://www.kaggle.com/datasets/stefanoleone992/filmtv-movies-dataset).

Pada dataset ini memiliki **37711** entries dan **19** kolom dimana didalamnya seperti berikut:

Dataset yang saya ambil adalah dataset publik yang berasal dari kaggle, berikut keterangan mengenai variabel didalmnya :

- filmtv_id : id film
- title : judul film
- year : tahun rilis film
- genre : genre dalam movie E.g Adventure, Horror, Thrille
- duration : durasi film
- country : asal negara film
- director : direktor film
- actors : aktor yang memerankan film
- avg_vote : rata rata vote film
- public_vote : publik vote film
- critic_vote : vote kritik pada film
- total_votes : total vote yang didapat film
- description : deksripsi film
- notes : catatan film

## Explatory Data Anlysis
- Drop Colomn
pada tahap ini saya drop beberapa kolom yang dapat mengganggu pada saat pemodelan agar nanti pada tahap pemodelan tidak ada kolom yang menghambat, diantaranya ada _notes,critic_vote_ dan _description_

- Handling missing value pada dateset

![total_missing](https://user-images.githubusercontent.com/73319544/192696140-0601547a-b8b9-4272-a7df-389dbab2db23.png)

Gambar .1 missing value

Pada Gambar .1 Missing value pada dataset masih sangat banyak dan masih tersebar didalamnya dengan total sebanyak **2213 records**, oleh karena itu kita drop seluruh missing value dalam dataset

![after_missing](https://user-images.githubusercontent.com/73319544/192696504-8501f4be-8245-4e49-a66a-639b5f17e2b7.png)

Gambar .2 after missing value

Pada Gambar .2  merupakan dataset yang sudah clean tanpa adanya missing value didalamnya dengan total entries berikut

![total_clean](https://user-images.githubusercontent.com/73319544/192696755-bb1b6727-7156-4d5f-8fd7-52a011ea324f.png)
Gambar .3 data clean

- Visualisasi Setiap Movie kebanyakan memiliki genre Movie sebagai berikut 

![genre_terbanyak](https://user-images.githubusercontent.com/73319544/192697326-8853e5b3-acf3-4b17-8b4c-f704751cd7b5.png)

Gambar .4 genre TV

Pada Gambar .4 kita bisa lihat bahwa genre terbanyak dalam Movie dimiliki oleh genre **Drama** dan **Comedy** 

- Visualisasi Setiap Movie kapan dirilis 

![tahun_tv](https://user-images.githubusercontent.com/73319544/192697562-00a62b08-0bb2-4b4f-af59-4ac49828085f.png)

Gambar .5 tahun rilis MovieTV

pada Gambar .5 lihat bahwa semakin tahun produksi film semakin meningkat cukup pesat, dengan adanya teknologi khusus tahun demi tahun film menjadi bagian penting dalam peradaban.

## Data Preparation

Berikut tahapan dalam pemrosesan data:

### Menghapus Fitur yang tidak diperlukan
Karena pada proyek ini kita tidak memerluka fitur seperti **'notes' 'critics_vote' 'description'** maka kita bisa drop fitur tersebut.

### Handling missing value
pada tahap ini dalamprojek kita melakukan handling missing value dengan drop seluruh data yang memiliki missing value agar pada saat modelling tidak terhabat oleh data yang missing.
ada dua teknik dalam handling missing value diantaranya adalah drop value yang kita gunakan pada proyek ini atau mengisi mising value dengan nilai rata rata.

## Modeling

### Content Based Filtering
Content Based Filtering merekomendasikan item yang mirip dengan item sebelumnya yang disukai atau dipilih oleh penonton MovieTV, kemiripan item dihitung berdasarkan fitur yang ada dalam item yang dibandingkan, berikut merupakan parameternya :

- movie_name : berisi nama MovieTV yang ingin dicari rekomendasinya.
- similarity_data : berisi dataframe yang berisi similarity yang telah didefinisakan menggunakan cosine similarity.
- items : berisi nama nama fitur yang akan dimunculkan pada saat direkomendasikan, disini saya menaruh fitur **'title', 'year', 'genre', 'year', 'public_vote'**.
- k : banyaknya MovieTV film yang ingin direkomendasikan, disini saya menaruh 10 rekomendasi film yang akan ditampilkan

-kelebihan
 -  mudah digunakan untuk mencari kemiripan pada data untuk rekomendasi.
 
-kekurangan
 - item yang akan dimunculkan terbatas.

### Hasil pemodelan

Berikut saya masukkan beberapa title MovieTV yang akan direkomendasikan:

![dinner](https://user-images.githubusercontent.com/73319544/192699401-63b0413c-a08b-45eb-b538-6e832effbd34.png)

Gambar .6 dinner MovieTV

- berikut outputnya dari rekomendasinya

![dinner_rekom](https://user-images.githubusercontent.com/73319544/192699449-db57f452-a5f1-46c4-9e76-99e9d93637a6.png)

Gambar .7 dinner rekomendasi



## Evaluation
pada bagian ini saya mengambil 2 sampel MovieTV yang akan menampilkan rekomendasinya:

![dinner](https://user-images.githubusercontent.com/73319544/192699401-63b0413c-a08b-45eb-b538-6e832effbd34.png)

Gambar .8 dinner MovieTV

- berikut outputnya dari rekomendasinya

![dinner_rekom](https://user-images.githubusercontent.com/73319544/192699449-db57f452-a5f1-46c4-9e76-99e9d93637a6.png)

Gambar .9 dinner rekomendasi

![deadbang](https://user-images.githubusercontent.com/73319544/192699607-9fdcd3ae-20c4-46c5-a140-be2963b6e13e.png)

Gambar .10 deadbang MovieTV

![deadbang_rekom](https://user-images.githubusercontent.com/73319544/192699660-11677e18-3212-4586-bc5a-7af0c12fc88a.png)

Gambar .11 deadbang rekomendasi

Pada gambar .11 terlihat rekomendasi dari sistem sesuai dengan yang kita ingingkan berdasarkan genre yang pengguna inginkan dengan menampilkan 10 film rekomendasi.

mengingat kita mencari rekomendasi berdasarkan genre yang dimiliki oleh MovieTV, mak bisa kita evaluasi dengan rumus :

![rumus](https://user-images.githubusercontent.com/73319544/192700544-17d470eb-42fd-4d8c-9296-50d2bcbdf5c3.png)

Gambar .12 rumus 

Pada gambar .12 kita bisa mengetahui presisi dari rekomendasi yang kita berikan. kita telah memberikan 10 rekomendasi berdasarkan genre Comedy dan Crime, dan sistem memberikan kita rekomendasi yang sama. 

oleh karena itu dengan rumus perhitungan sederhan pada Gambar .12 sistem bisa memilki 100% dalam presisi nya.

## Referensi
- λ.eranga (Nov 29, 2021), Recommendation System with Content-based Filtering from medium https://medium.com/rahasak/recommendation-system-with-content-based-filtering-500231e31a60
- kunisetti s. (Springer, Singapore), Content-Based Movie Recommendation System Using Genre Correlation, from https://d1wqtxts1xzle7.cloudfront.net/62049148/contentbased20200209-27698-l8hk2i-with-cover-page-v2.pdf?Expires=1664349281&Signature=Odckc84PpURE5-xCpkpqUGGbk2VBLqRu-vBW-MmxGmhZzx4OnEHyY~Z2nQIknqVSeCcZaaufStSZxOsh2hrIayAoxOxmMgC0f7q7FHQprbl4MfYtZXKACJ6thEltg0e-9GoVYle-drD6K47VvA6lE0QnMwiAesyjH4vwDwtjkAOETaW~5~8eCOno7eWKp5koROKmbNgXmIPo593N1nmBjG6G3G9KXzTGxlS0Ek2JmgQl1OzcBz8qJQAj0rGMP4GHF0kgz1AzaanbRRCfEpdumjYbXbz26N5M39GoBRIXPxWdBCSZ6O5pc9oXTtmHt1qB7O8ldBcndN~E6OU-mBSzIQ__&Key-Pair-Id=APKAJLOHF5GGSLRBV4ZA


