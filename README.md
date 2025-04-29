# LAPORAN PROYEK MACHINE LEARNING TERAPAN
Oleh Rahmat Hidayat

## Domain Proyek
Dalam beberapa tahun terakhir, industri film mengalami perkembangan pesat, terlihat dari peningkatan jumlah penonton bioskop dan keberagaman produksi film. Setiap tahunnya, muncul ratusan hingga ribuan film baru dengan berbagai alur cerita, genre, dan tema, baik dari dalam negeri maupun luar negeri. Keberagaman ini memang memberikan lebih banyak pilihan hiburan, namun di sisi lain, juga menimbulkan tantangan bagi para penonton [1].

Di era digital saat ini, beberapa platform film telah menyediakan fitur pencarian dan filter berdasarkan genre atau popularitas. Meskipun demikian, fitur tersebut belum tentu dapat memberikan rekomendasi yang benar-benar personal dan relevan dengan preferensi individu. Setiap orang memiliki selera dan kecenderungan yang berbeda dalam memilih film, biasanya didasarkan pada pengalaman menonton sebelumnya atau genre favorit. Oleh karena itu, diperlukan sebuah sistem yang dapat memahami preferensi pengguna dan memberikan rekomendasi film yang sesuai secara otomatis.

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
Dataset yang digunakan dalam laporan ini adalah Movie Recommendation Data bersumber dari Movielens yang dapat diakses secara publik pada link berikut ini : https://grouplens.org/datasets/movielens/. Tidak keseluruhan dataset dari sumber digunakan, dataset yang digunakan yaitu movies, ratings, dan tags. Berikut akan dijelaskan masing-masing secara singkat singkat mengenai dataset. <br>
#### Movies
Memuat data yang terdiri dari: <br>
- movie: Memuat nilai Id dari film yang bernilai unik (masing-masing film memiliki id yang berbeda). Tipe data integer.
- rating: Memuat nilai terhadap suatu movie dari urutan (0, 1, 2, 3, 4).

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
![gambar](https://github.com/user-attachments/assets/a30d0bd4-857e-49ae-b924-b5351e83a1f2)

  <br>
  Dari histogram distribusi rating film, diketahui dua rating paling banyak berada di angka 4 diikuti rating 3 serta rating 5.

- Melihat visualisasi genre terpopuler dengan menggunakan bar chart
![gambar](https://github.com/user-attachments/assets/5c2bc1c2-9920-45d5-a7c1-3a5fc8f1299c)

  <br>
  Visualisasi bar di atas menunjukkan 5 genre film terpopuler berdasarkan jumlah film yang dibuat. Genre Drama paling banyak, diikuti oleh Comedy, Thriller, dan Action. Genre seperti Fantasy dan Horror memiliki jumlah film yang lebih sedikit.

- Melihat distribusi jumlah rating per user dengan histogram
![gambar](https://github.com/user-attachments/assets/18704860-7470-442b-ae8f-0a2c658f495b)

  <br>
  Histogram di atas menunjukkan distribusi jumlah rating yang diberikan oleh setiap pengguna. Sebagian besar pengguna memberikan rating dalam jumlah yang sedikit, sedangkan hanya sedikit pengguna yang memberikan rating dalam jumlah sangat banyak.

- Melihat hubungan jumlah rating dan rata-rata rating per film dengan menggunakan scatterplot
![gambar](https://github.com/user-attachments/assets/108f3f5f-c8e7-4852-99c0-f804c72d9cf5)

  <br>
Gambar ini menunjukkan pola menarik antara jumlah rating dan nilai rata-rata rating suatu produk. Terlihat bahwa produk dengan sedikit rating (kurang dari 50) cenderung memiliki nilai rating yang sangat beragam, mulai dari sangat bagus hingga sangat jelek. Hal ini wajar karena dengan sedikit data, rating bisa mudah terpengaruh oleh beberapa penilaian ekstrem. Sebaliknya, produk yang sudah mendapatkan banyak rating (lebih dari 100) menunjukkan nilai rating yang lebih stabil dan cenderung berkumpul di kisaran menengah. Ada kecenderungan menarik di mana produk dengan rating sangat banyak justru memiliki nilai rata-rata yang sedikit lebih rendah dibanding produk dengan rating sedang. Ini mungkin terjadi karena awalnya hanya penggemar berat yang memberi rating tinggi, namun seiring bertambahnya penilaian dari pembeli biasa, nilainya menjadi lebih realistis. Pelajaran pentingnya adalah kita harus lebih berhati-hati dalam menilai produk berdasarkan rating, terutama yang masih memiliki sedikit penilaian. Sebaiknya prioritaskan produk yang sudah mendapatkan banyak rating karena nilainya lebih mencerminkan kualitas sebenarnya. Jika menemukan produk dengan rating sangat tinggi tapi hanya memiliki sedikit penilaian, bisa jadi itu belum menggambarkan kualitas objektif produk tersebut.

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

### Modeling dengan Collaborative Filtering
#### Penjelasan singkat mengenai model
- **Collaborative filtering adalah** pendekatan di mana pendapat pengguna lain digunakan untuk memprediksi item yang mungkin disukai atau diminati oleh pengguna tertentu [[2]](https://scholar.google.com/scholar?hl=id&as_sdt=0%2C5&q=SISTEM+REKOMENDASI+LAPTOP+MENGGUNAKAN++COLLABORATIVE+FILTERING+DAN+CONTENT-BASED++FILTERING+&btnG=). <br>
- **Kelebihan dari user-based collaborative filtering adalah** kemampuannya menghasilkan rekomendasi berkualitas [2]. <br>
- **Kekurangan collaborative filtering adalah** kompleksitas perhitungan meningkat seiring bertambahnya jumlah pengguna, yang dapat memperlambat proses rekomendasi [2]. <br>

### TOP-N RECOMMENDATION
- Untuk content-based filtering, menggunakan fungsi yang telah didasari dengan model untuk mencari judul film yang mirip dengan input pengguna dan memberikan rekomendasi film serupa. Jika judul tidak ditemukan, program menyarankan judul yang dekat agar pengguna bisa mencoba lagi.
  Berikut adalah simulasi penggunaan content-based filtering:
  1. Misalkan menggunakan film Toy Story (1995) dan rekomendasi yang diminta 5: 
![gambar](https://github.com/user-attachments/assets/5a25717b-9672-418f-94d1-6586850e95cf) <br>
  2. Berikut merupakan output yang dihasilkan berdasarkan permintaan di atas:
![gambar](https://github.com/user-attachments/assets/c6f69e39-5f94-4071-b9bd-87d77de45624)     
- Untuk collaborative filtering, menggunakan fungsi yang telah didasari dengan model yang meminta userId dan jumlah rekomendasi, lalu menampilkan daftar film yang direkomendasikan berdasarkan rating yang juga menghubungkan pengguna serupa dengan kesamaan dalam preferensi dan perilaku.
  Berikut adalah simulasi penggunaan collaborative filtering:
  1. Misalkan input id yang digunakan berupa angka 2 dan jumlah rekomendasi yang diminta 5:
![gambar](https://github.com/user-attachments/assets/69b80cc4-5334-420c-9f3c-2d9669b0361d)
<br>

3. Berikut merupakan output yang dihasilkan berdasarkan permintaan di atas:
![gambar](https://github.com/user-attachments/assets/1fceaee7-7990-4476-9edf-a9bbd7b53e7c)

## Evaluation
Evaluasi model dilakukan untuk menilai sejauh mana model SVD (Singular Value Decomposition) mampu memprediksi rating pengguna terhadap item yang belum dilihat. Evaluasi dilakukan menggunakan dua pendekatan: evaluasi terhadap test set dan k-fold cross-validation, dengan metrik utama RMSE (Root Mean Squared Error) dan MAE (Mean Absolute Error). Berikut gambar : 
<img width="809" alt="dos-93dfbee86d454b6cd0f1faa860fea87c20250429044636" src="https://github.com/user-attachments/assets/0aa994c7-f312-41df-8f8c-9b4fb8ea7f50" />

1. Evaluasi terhadap Test Set

Model diuji terhadap data test set, dan hasil evaluasi menunjukkan nilai:

    RMSE: 0.8660
    MAE: 0.6712

Nilai RMSE yang berada di bawah 1 menunjukkan bahwa kesalahan prediksi relatif kecil, menandakan bahwa prediksi rating yang dilakukan oleh model cukup akurat terhadap data aktual. MAE yang rendah juga menunjukkan bahwa deviasi absolut rata-rata antara prediksi dan nilai aktual tergolong kecil.

    Analisis:
    Nilai RMSE yang mendekati nilai MAE menunjukkan bahwa tidak ada kesalahan besar (outlier error) yang mendominasi performa model. Artinya, prediksi cenderung stabil dan tidak terlalu dipengaruhi oleh kesalahan ekstrem.

2. Evaluasi dengan 5-Fold Cross-Validation

Untuk memastikan performa model tidak hanya baik pada satu subset data, dilakukan evaluasi dengan cross-validation sebanyak 5 fold. Hasilnya dirangkum dalam tabel berikut:
| Fold | RMSE   | MAE    |
|------|--------|--------|
| 1    | 0.8718 | 0.6712 |
| 2    | 0.8697 | 0.6708 |
| 3    | 0.8808 | 0.6760 |
| 4    | 0.8731 | 0.6706 |
| 5    | 0.8740 | 0.6714 |
| **Rata-rata** | **0.8739** | **0.6720** |
| **Standar Deviasi** | **0.0038** | **0.0020** |

Analisis:

    Nilai rata-rata RMSE dari cross-validation adalah 0.8739, hanya sedikit lebih tinggi dibanding evaluasi pada test set (0.8660). Hal ini mengindikasikan bahwa model tidak overfit terhadap data pelatihan.

    Standar deviasi yang kecil (0.0038) menunjukkan bahwa model memberikan performa yang konsisten di semua lipatan (fold) data, sehingga stabilitas model sangat baik.

    MAE yang juga stabil di semua fold menguatkan bahwa model memiliki tingkat kesalahan prediksi yang bisa diterima secara praktis.
**
Insight Evaluasi**

Model SVD terbukti memberikan performa yang akurat dan stabil untuk sistem rekomendasi berbasis kolaboratif. Dengan nilai RMSE dan MAE yang rendah serta konsistensi antar fold, model ini layak untuk diterapkan pada sistem rekomendasi nyata. Hasil evaluasi juga menunjukkan bahwa pendekatan yang digunakan telah sesuai dengan prinsip-prinsip validasi model yang baik, seperti menghindari overfitting dan memastikan generalisasi.

## RANGKUMAN 

Hasil Evaluasi menggunakan precision dan recall ini menunjukkan bahwa model Content-Based Filtering sangat efektif dalam merekomendasikan film dengan genre yang sesuai. Hal ini mengindikasikan bahwa pendekatan yang digunakan, yaitu dengan menghitung kemiripan berdasarkan TF-IDF genre, berhasil menangkap hubungan yang relevan di antara film-film dalam dataset. Model sistem rekomendasi dikembangkan dengan dua pendekatan: content-based filtering dan collaborative filtering. Pada pendekatan content-based, sistem menggunakan kesamaan genre untuk merekomendasikan film yang relevan. Contohnya, ketika pengguna memilih "Toy Story (1995)", sistem berhasil merekomendasikan lima film lain yang memiliki genre serupa, seperti "Antz (1998)" dan "Toy Story 2 (1999)", dengan hasil evaluasi precision dan recall sebesar 1.00, menunjukkan bahwa seluruh rekomendasi relevan terhadap preferensi genre pengguna.

Sementara itu, pada pendekatan collaborative filtering menggunakan algoritma SVD, evaluasi dilakukan dengan metrik RMSE, MAE, dan cross-validation. Hasil menunjukkan bahwa model mampu memprediksi rating dengan baik, dengan nilai RMSE sebesar 0.8727 dan MAE sekitar 0.6706. Rata-rata RMSE dari cross-validation sebesar 0.8729 dengan standar deviasi rendah (0.0067), menandakan bahwa model bekerja konsisten pada berbagai subset data. Kedua pendekatan ini menunjukkan performa yang baik dalam memberikan rekomendasi yang akurat dan relevan.


### Saran
Untuk mengatasi kelemahan pada metode-metode yang telah diterapkan di atas, dapat digunakan metode hybrid filtering, yaitu dengan menggabungkan Collaborative Filtering (CF) dan Content-Based (CB). Pendekatan ini bertujuan menghasilkan rekomendasi item yang lebih sesuai dengan preferensi pengguna, sekaligus mengatasi masalah sparsity dan meningkatkan akurasi prediksi nilai [[5]](https://citee.ft.ugm.ac.id/download51.php?f=TI-5%20-%20Implementasi%20Metode%20Hybrid%20Filtering.pdf).

## DAFTAR PUSTAKA
<br>
1. Fajriansyah, M., Adikara, P. P., & Widodo, A. W. (2021). Sistem Rekomendasi Film Menggunakan Content Based Filtering. Jurnal Pengembangan Teknologi Informasi Dan Ilmu Komputer, 5(6), 2188–2199. Diambil dari https://j-ptiik.ub.ac.id/index.php/j-ptiik/article/view/9163

2. Lubis, Y. I., Napitupulu, D. J., & Dharma, A. S. (2020). Implementasi metode hybrid filtering (collaborative dan content-based) untuk sistem rekomendasi pariwisata. Prosiding CITEE 2020, Yogyakarta, 6-8 Oktober 2020. Diambil dari https://citee.ft.ugm.ac.id/download51.php?f=TI-5%20-%20Implementasi%20Metode%20Hybrid%20Filtering.pdf

3. Putri, N. M., Prasepitawan, M., & Untoro, M. C. (2024). Analisis model sistem rekomendasi kursus MOOC dengan metode collaborative filtering dan integrasi explainable AI. Indonesian Journal of Business Intelligence, 7(1). Diambil dari https://ejournal.almaata.ac.id/index.php/IJUBI

4. Velamentosa, D., & Zuliarso, E. (2025). Sistem rekomendasi film menggunakan metode content-based filtering. JATI (Jurnal Mahasiswa Teknik Informatika), 9(2), 2918. Diambil dari https://mail.ejournal.itn.ac.id/index.php/jati/article/view/13251/7349

5. Wijaya, A. E., & Alfian, D. (2018). Sistem rekomendasi laptop menggunakan collaborative filtering dan content-based filtering. Jurnal Computech & Bisnis, 12(1), 11–27. Diambil dari https://scholar.google.com/scholar?hl=id&as_sdt=0%2C5&q=SISTEM+REKOMENDASI+LAPTOP+MENGGUNAKAN++COLLABORATIVE+FILTERING+DAN+CONTENT-BASED++FILTERING+&btnG=


