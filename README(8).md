# SISTEM REKOMENDASI MOVIE - LAPORAN PROYEK MACHINE LEARNING TERAPAN
Oleh Daffa Akifah Balqis

## Domain Proyek
Dalam beberapa tahun terakhir, industri perfilman mengalami pertumbuhan yang pesat, ditandai dengan meningkatnya jumlah penonton bioskop serta produksi film yang semakin beragam. Setiap tahunnya, ratusan hingga ribuan film baru dengan berbagai alur cerita, genre, dan tema bermunculan, baik dari dalam negeri maupun luar negeri. Keberagaman ini memang memperkaya pilihan hiburan, namun di sisi lain juga menimbulkan tantangan tersendiri bagi para penonton [[1]](https://j-ptiik.ub.ac.id/index.php/j-ptiik/article/view/9163).

Di era digital saat ini, beberapa platform film memang telah menyediakan fitur pencarian dan filter berdasarkan genre atau popularitas. Namun, fitur tersebut belum tentu mampu memberikan rekomendasi yang benar-benar personal dan relevan dengan preferensi masing-masing individu. Setiap orang memiliki selera dan kecenderungan yang unik dalam memilih film, biasanya berdasarkan pengalaman menonton sebelumnya atau genre favorit. Oleh karena itu, dibutuhkan sebuah sistem yang mampu memahami preferensi pengguna dan memberikan rekomendasi film yang sesuai secara otomatis.

## Business Understanding
### Problem Statements
Banyaknya pilihan film sering kali membuat calon penonton merasa kebingungan dan kesulitan dalam menentukan film mana yang layak untuk ditonton berikutnya. Proses pencarian film yang sesuai dengan selera pun menjadi lebih memakan waktu dan tidak jarang membuat penonton merasa kurang puas dengan pilihannya. Berdasarkan latar belakang tersebut, berikut ini merupakan rumusan masalah yang akan diselesaikan dalam proyek ini: <br>
1. Bagaimana sistem dapat merekomendasikan film yang disukai oleh satu pengguna agar juga dapat dinikmati oleh pengguna lain dengan preferensi serupa?

### Goals
Berdasarkan rumusan masalah di atas, maka tujuan yang ingin dicapai adalah:
1. Mengembangkan sistem rekomendasi yang mampu memberikan saran film secara tepat dan relevan berdasarkan preferensi pengguna serta perilaku pengguna sebelumnya.

### Solution Approach
Solusi yang akan digunakan untuk permasalahan di atas adalah:
*   **Content Based Filtering** adalah memanfaatkan informasi yang terdapat pada suatu item sebagai dasar dalam memberikan rekomendasi [[2]](https://scholar.google.com/scholar?hl=id&as_sdt=0%2C5&q=SISTEM+REKOMENDASI+LAPTOP+MENGGUNAKAN++COLLABORATIVE+FILTERING+DAN+CONTENT-BASED++FILTERING+&btnG=). Ini akan digunakan untuk merekomendasikan film berdasarkan kemiripan film yang telah dicari oleh pengguna.
*   **Collaborative Filtering** merupakan suatu pendekatan di mana pendapat atau preferensi dari pengguna lain dimanfaatkan untuk memperkirakan item yang kemungkinan besar akan disukai atau diminati oleh seorang pengguna [[2]](https://scholar.google.com/scholar?hl=id&as_sdt=0%2C5&q=SISTEM+REKOMENDASI+LAPTOP+MENGGUNAKAN++COLLABORATIVE+FILTERING+DAN+CONTENT-BASED++FILTERING+&btnG=). Ini akan digunakan untuk merekomendasikan pengguna terhadap film berdasarkan rating yang juga menghubungkan pengguna serupa dengan kesamaan dalam preferensi dan perilaku.

## Data Understanding
### Penjelasan singkat mengenai dataset
Dataset yang digunakan dalam laporan ini adalah Movie Recommendation Data bersumber dari kaggle yang dapat diakses secara publik pada link: https://www.kaggle.com/datasets/rohan4050/movie-recommendation-data/code . Tidak keseluruhan dataset dari sumber digunakan, dataset yang digunakan yaitu movies, ratings, dan tags. Berikut akan dijelaskan masing-masing secara singkat singkat mengenai dataset. <br>
#### Movies
Memuat data yang terdiri dari: <br>
- movieId: Memuat nilai Id dari film yang bernilai unik (masing-masing film memiliki id yang berbeda). Tipe data integer.
- title: Memuat judul dari film. Tipe data object.
- genres: Memuat genre dari film, nilai genre yang dimiliki masing-masing bisa lebih dari satu. Tipe data object
Dengan keterangan, jumlah data movie :  9742
#### Ratings
Memuat data yang terdiri dari: <br>
- userId: Memuat nilai id unik dari masing-masing user
- movieId: Memuat nilai Id dari filmmovie yang bernilai unik (masing-masing film memiliki id yang berbeda)
- rating: Memuat nilai rating untuk setiap film
- timestamp: Memuat detik Coordinated Universal Time(UTC)
Dengan keterangan, jumlah user unik pada ratings :  610, jumlah movie unik pada ratings :  9724 serta jumlah total data ratings :  100836
#### Tags
Memuat data yang terdiri dari: <br>
- userId: Memuat nilai id unik dari masing-masing user
- movieId: Memuat nilai Id dari filmmovie yang bernilai unik (masing-masing film memiliki id yang berbeda)
- tag: Tag/label yang diberikan oleh seorang pengguna kepada sebuah film.

### Eksploratory Data Analysis (EDA)
- Melihat distribusi data rating dengan histogram
  ![image](https://github.com/user-attachments/assets/c5e69d4a-9d88-45aa-ae09-173a7db792de)
  <br>
  Dari histogram distribusi rating film, diketahui dua rating paling banyak berada di angka 4 diikuti rating 3 serta rating 5.

- Melihat visualisasi genre terpopuler dengan menggunakan bar chart
  ![image](https://github.com/user-attachments/assets/cdb587c4-8fdc-4f87-80f7-cc6b5be64adc)
  <br>
  Visualisasi bar di atas menunjukkan 10 genre film terpopuler berdasarkan jumlah film yang dibuat. Genre Drama paling banyak, diikuti oleh Comedy, Thriller, dan Action. Genre seperti Fantasy dan Horror memiliki jumlah film yang lebih sedikit.

- Melihat distribusi jumlah rating per user dengan histogram
  ![image](https://github.com/user-attachments/assets/e14d5349-f994-41a7-a8fe-394c6e01e1ce)
  <br>
  Histogram di atas menunjukkan distribusi jumlah rating yang diberikan oleh setiap pengguna. Sebagian besar pengguna memberikan rating dalam jumlah yang sedikit, sedangkan hanya sedikit pengguna yang memberikan rating dalam jumlah sangat banyak.

- Melihat hubungan jumlah rating dan rata-rata rating per film dengan menggunakan scatterplot
  ![image](https://github.com/user-attachments/assets/a02959ea-4b9f-4ff5-9362-321076c2d2ce)
  <br>
  Gambar di atas menunjukkan scatterplot yang menggambarkan hubungan antara jumlah rating yang diterima sebuah film dengan rata-rata ratingnya. Terlihat bahwa film dengan jumlah rating sedikit memiliki variasi rata-rata rating yang cukup besar, mulai dari sangat rendah hingga sangat tinggi. Sedangkan film dengan jumlah rating banyak cenderung memiliki rata-rata rating yang stabil di kisaran 3 sampai 4. Jadi, semakin banyak rating yang diterima, rata-rata rating film cenderung lebih konsisten.

## Data Preparation
#### Data Preparation untuk Dataset Film dan Rating
- Menghapus baris dengan judul film duplikat agar setiap film hanya muncul sekali.
- Menghapus baris yang memiliki nilai kosong pada kolom judul film untuk memastikan data lengkap.
- Memfilter hanya baris dengan judul bertipe string untuk menghindari data yang tidak valid.
- Mengubah tipe data kolom movieId pada kedua dataset (film dan rating) menjadi string agar konsisten dan memudahkan pengolahan data selanjutnya.
#### Data Preparation untuk Dataset Tag dan Penggabungan dengan Dataset Film
- Mengelompokkan data tag berdasarkan movieId dan menggabungkan semua tag terkait menjadi satu string per film.
- Menyamakan tipe data kolom movieId pada dataset movies dan tag menjadi string agar penggabungan data dapat dilakukan dengan benar.
- Menggabungkan (merge) data tag yang sudah digabungkan ke dataset film berdasarkan movieId.
- Membuat kolom baru content yang menggabungkan judul film, genre, dan tag menjadi satu teks, yang nantinya digunakan untuk metode content-based filtering dalam rekomendasi film.

## Modeling and Result
### Modeling dengan Content-Based Filtering
#### Penjelasan singkat mengenai model
- **Content-based filtering adalah** sistem rekomendasi yang memanfaatkan informasi konten (juga dikenal sebagai fitur, atribut, atau karakteristik) dari suatu item sebagai dasar untuk memberikan rekomendasi [[2]](https://scholar.google.com/scholar?hl=id&as_sdt=0%2C5&q=SISTEM+REKOMENDASI+LAPTOP+MENGGUNAKAN++COLLABORATIVE+FILTERING+DAN+CONTENT-BASED++FILTERING+&btnG=). <br>
- **Kelebihan Content-based filtering yaitu** mudah dijelaskan karena dapat menunjukkan alasan di balik rekomendasi. Selain itu, sistem ini mampu merekomendasikan item yang belum pernah dinilai oleh pengguna lain [2]. <br>
- **Kekurangan Content-based filtering yaitu** membutuhkan profil pengguna yang berisi minat dan ketertarikan, sehingga kurang efektif untuk pengguna baru yang belum memiliki riwayat aktivitas (cold start problem) [2].

#### Penjelasan tahapan yang digunakan
- Menggunakan metode TF-IDF (Term Frequency-Inverse Document Frequency) untuk mengubah kolom content (gabungan judul, genre, dan tag film) menjadi matriks fitur numerik yang merepresentasikan pentingnya kata dalam setiap film. <br>
- Menghitung matriks kemiripan kosinus antara semua film, yang mengukur tingkat kemiripan konten satu film dengan film lainnya berdasarkan fitur TF-IDF. Matriks kemiripan kosinus ini digunakan sebagai dasar dalam sistem rekomendasi berbasis konten. <br>
- Membuat fungsi  yang akan memeriksa keberadaan judul film dalam dataset, kemudian menghitung dan mengurutkan skor kemiripan kosinus dengan film lain untuk mengembalikan daftar rekomendasi film paling mirip berdasarkan nilai tertinggi (top_n). <br>

### Modeling dengan Collaborative Filtering
#### Penjelasan singkat mengenai model
- **Collaborative filtering adalah** pendekatan di mana pendapat pengguna lain digunakan untuk memprediksi item yang mungkin disukai atau diminati oleh pengguna tertentu [[2]](https://scholar.google.com/scholar?hl=id&as_sdt=0%2C5&q=SISTEM+REKOMENDASI+LAPTOP+MENGGUNAKAN++COLLABORATIVE+FILTERING+DAN+CONTENT-BASED++FILTERING+&btnG=). <br>
- **Kelebihan dari user-based collaborative filtering adalah** kemampuannya menghasilkan rekomendasi berkualitas [2]. <br>
- **Kekurangan collaborative filtering adalah** kompleksitas perhitungan meningkat seiring bertambahnya jumlah pengguna, yang dapat memperlambat proses rekomendasi [2]. <br>

#### Penjelasan tahapan yang digunakan
- Mengonversi ID asli pengguna dan film menjadi indeks numerik berurutan, lalu menambahkan kolom indeks ke data rating untuk persiapan model.
- Menentukan total pengguna dan film serta rentang nilai rating untuk memahami skala data dan mengatur parameter model.
- Mengacak data rating untuk menghindari bias dan menormalisasi nilai rating ke rentang 0–1.
- Membagi data menjadi 80% pelatihan dan 20% validasi, memisahkan fitur (user dan movie) dan target (rating).
- Membangun model RecommenderNet yang menggunakan embedding untuk merepresentasikan pengguna dan film, menghitung interaksi dengan dot product dan bias, serta menghasilkan prediksi rating antara 0 dan 1 menggunakan fungsi sigmoid.
- Menginisialisasi dan mengompilasi model dengan loss function binary crossentropy, optimizer Adam (learning rate 0.001), dan metrik RMSE untuk evaluasi performa.

### TOP-N RECOMMENDATION
- Untuk content-based filtering, menggunakan fungsi yang telah didasari dengan model untuk mencari judul film yang mirip dengan input pengguna dan memberikan rekomendasi film serupa. Jika judul tidak ditemukan, program menyarankan judul yang dekat agar pengguna bisa mencoba lagi.
  Berikut adalah simulasi penggunaan content-based filtering:
  1. Misalkan menggunakan film 'Minions (2015) dan rekomendasi yang diminta 10: 
     ![image](https://github.com/user-attachments/assets/3c2c2f3f-0b29-43d4-8119-ce174009e837) <br>
  2. Berikut merupakan output yang dihasilkan berdasarkan permintaan di atas:
     ![image](https://github.com/user-attachments/assets/6fb2506c-e893-405b-a5f4-505d3def3e5e)
     
     Menampilkan 10 film rekomendasi berdasarkan nama film yang diinput.
     
- Untuk collaborative filtering, menggunakan fungsi yang telah didasari dengan model yang meminta userId dan jumlah rekomendasi, lalu menampilkan daftar film yang direkomendasikan berdasarkan rating yang juga menghubungkan pengguna serupa dengan kesamaan dalam preferensi dan perilaku.
  Berikut adalah simulasi penggunaan collaborative filtering:
  1. Misalkan input id yang digunakan berupa angka 431 dan jumlah rekomendasi yang diminta 10:
     ![image](https://github.com/user-attachments/assets/8f29494e-28bd-4d5f-a971-e9d1f04ac780) <br>
  2. Berikut merupakan output yang dihasilkan berdasarkan permintaan di atas:
     ![image](https://github.com/user-attachments/assets/ddcc564e-aaa9-4023-abf9-a5b01f1b2528)

     Menampilkan 10 film rekomendasi berdasarkan id pengguna yang diinput.

## Evaluation
### Evaluasi Collaborative filtering dengan Plot History Training Model
![image](https://github.com/user-attachments/assets/219cb049-7456-43fc-b4cd-c52e53edd02d)
 <br>
Gambar di atas merupakan plot RMSE dari data pelatihan dan validasi selama 100 epoch. Nilai RMSE ini menjadi nilai yang digunakan untuk mengevaluasi collaborative filtering. Grafik yang dihasilkan menunjukkan RMSE selama pelatihan model, dimana performa dipantau, terakhir diperoleh nilai error akhir sebesar sekitar 0.19 dan error pada data validasi sebesar 0.20. Menunjukkan bahwa prediksi model cukup akurat dengan rata-rata kesalahan kurang dari 0.2 poin pada skala tersebut. <br>
Berikut adalah rumus RMSE yang digunakan dalam perhitungan [[3]](https://ejournal.almaata.ac.id/index.php/IJUBI/article/view/4274): <br>
![image](https://github.com/user-attachments/assets/0f516332-89f5-4bd6-a0c8-511505e2d1bd)
<br>
### Evaluasi Sistem Rekomendasi berdasarkan Content-Based Filtering dengan Precision
Untuk menilai kinerja sistem rekomendasi, dapat dilakukan evaluasi dengan beberapa metrik berikut [[4]](https://mail.ejournal.itn.ac.id/index.php/jati/article/view/13251/7349): <br>
a. Precision: Menghitung persentase rekomendasi film yang sesuai dengan preferensi pengguna. <br>
b. Recall: Mengukur kemampuan sistem dalam merekomendasikan film yang relevan dari seluruh film yang tersedia. <br>
c. F1-Score: Gabungan antara precision dan recall yang memberikan evaluasi seimbang atas akurasi dan kelengkapan rekomendasi. <br>
Metrik yang akan digunakan adalah precision. <br>
Berikut adalah rumus precision [[4]](https://mail.ejournal.itn.ac.id/index.php/jati/article/view/13251/7349): <br>
![image](https://github.com/user-attachments/assets/2fe2e042-a079-440b-ace2-e7384cba37f2) <br>
#### Evaluasi Content-Based
- Hasil pencarian film yang mirip 'Inside Out (2015)':
![image](https://github.com/user-attachments/assets/097bd53f-2852-4e8d-8e6e-5c594d66cebe) <br>
- Kemudian menggunakan cosine similiarity untuk melihat kesamaan film 'Inside Out (2015)' dengan film yang direkomendasikan: <br>
![image](https://github.com/user-attachments/assets/7910e0f4-68a7-4d44-bb23-9c2129c7af15) <br>
- Kesimpulan didapatkan bahwa dengan penyesuaian terhadap genre dan cosine similiarity antara film yang dicari dan film rekomendasi serta genre yang cukup mirip dengan film yang sudah disukai user. Jadi, presisinya adalah 0.7 atau 70%

### Evaluasi Terhadap Business Understanding
- Menjawab Problem Statement
  <br>
  Sistem yang dikembangkan cukup berhasil menjawab permasalahan dengan memberikan rekomendasi film yang sesuai dengan preferensi pengguna berdasarkan data perilaku dan kesamaan preferensi pengguna lain. Dengan menggunakan metode Content Based Filtering dan Collaborative Filtering, sistem mampu merekomendasikan film yang relevan sehingga memudahkan pengguna dalam memilih film yang layak ditonton tanpa kebingungan.

- Mencapai Goals
  <br>
  Sistem rekomendasi yang dibangun berhasil mencapai tujuan utama, yaitu memberikan saran film yang cukup relevan sesuai dengan preferensi pengguna.  Content Based Filtering dan Collaborative Filtering membantu untuk memberikan hasil dalam menyajikan rekomendasi film.
  
- Dampak dari Solution Statement
  <br>
  Penggunaan dua pendekatan dalam sistem rekomendasi yaitu Content Based Filtering dan Collaborative Filtering memberikan dampak positif yang signifikan, antara lain: <br>
  - Efisiensi Pencarian Film: Sistem mampu mempercepat proses pencarian film yang sesuai dengan selera pengguna, sehingga mengurangi waktu dan kebingungan dalam memilih film. <br>
  - Relevansi Rekomendasi: Dengan memanfaatkan informasi item dan preferensi pengguna lain, sistem memberikan rekomendasi yang lebih akurat dan personal, meningkatkan kepuasan pengguna dalam memilih film.
 
### Saran
Untuk mengatasi kelemahan pada metode-metode yang telah diterapkan di atas, dapat digunakan metode hybrid filtering, yaitu dengan menggabungkan Collaborative Filtering (CF) dan Content-Based (CB). Pendekatan ini bertujuan menghasilkan rekomendasi item yang lebih sesuai dengan preferensi pengguna, sekaligus mengatasi masalah sparsity dan meningkatkan akurasi prediksi nilai [[5]](https://citee.ft.ugm.ac.id/download51.php?f=TI-5%20-%20Implementasi%20Metode%20Hybrid%20Filtering.pdf).

## Refrensi
Refrensi: <br>
[[1]](https://j-ptiik.ub.ac.id/index.php/j-ptiik/article/view/9163) Fajriansyah, M., Adikara, P. P., & Widodo, A. W. (2021). Sistem Rekomendasi Film Menggunakan Content Based Filtering. Jurnal Pengembangan Teknologi Informasi Dan Ilmu Komputer, 5(6), 2188–2199. Diambil dari https://j-ptiik.ub.ac.id/index.php/j-ptiik/article/view/9163 <br>
[[2]](https://scholar.google.com/scholar?hl=id&as_sdt=0%2C5&q=SISTEM+REKOMENDASI+LAPTOP+MENGGUNAKAN++COLLABORATIVE+FILTERING+DAN+CONTENT-BASED++FILTERING+&btnG=) Wijaya, A. E., & Alfian, D. (2018). Sistem rekomendasi laptop menggunakan collaborative filtering dan content-based filtering. Jurnal Computech & Bisnis, 12(1), 11–27. <br>
[[3]](https://ejournal.almaata.ac.id/index.php/IJUBI/article/view/4274) Putri, N. M., Prasepitawan, M., & Untoro, M. C. (2024). Analisis model sistem rekomendasi kursus MOOC dengan metode collaborative filtering dan integrasi explainable AI. Indonesian Journal of Business Intelligence, *7*(1). https://ejournal.almaata.ac.id/index.php/IJUBI <br>
[[4]](https://mail.ejournal.itn.ac.id/index.php/jati/article/view/13251/7349) Velamentosa, D., & Zuliarso, E. (2025). Sistem rekomendasi film menggunakan metode content-based filtering. JATI (Jurnal Mahasiswa Teknik Informatika), 9(2), 2918. <br>
[[5]](https://citee.ft.ugm.ac.id/download51.php?f=TI-5%20-%20Implementasi%20Metode%20Hybrid%20Filtering.pdf) Lubis, Y. I., Napitupulu, D. J., & Dharma, A. S. (2020). Implementasi metode hybrid filtering (collaborative dan content-based) untuk sistem rekomendasi pariwisata [Implementation of hybrid filtering (collaborative and content-based) methods for the tourism recommendation system]. Prosiding CITEE 2020, Yogyakarta, 6-8 Oktober 2020












  





