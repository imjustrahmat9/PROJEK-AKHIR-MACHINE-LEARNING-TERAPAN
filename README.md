## Laporan Proyek Sistem Rekomendasi - RAHMAT HIDAYAT

### Latar Belakang

Seiring berkembangnya era digital, volume informasi yang tersedia meningkat drastis, menimbulkan tantangan besar bagi pengguna dalam menemukan konten yang relevan. Platform seperti Netflix, Spotify, dan Amazon perlu menyaring informasi berdasarkan preferensi pengguna agar dapat memberikan rekomendasi yang tepat sasaran.

Netflix menggunakan sistem rekomendasi berbasis data yang menganalisis pola tontonan pengguna, sehingga dapat menyarankan film yang sesuai selera. Strategi ini terbukti meningkatkan waktu menonton dan memperkuat loyalitas pelanggan. Di bidang musik, Spotify menerapkan pendekatan serupa melalui fitur *Discover Weekly*, yang menyesuaikan daftar putar dengan kebiasaan mendengarkan pengguna, memperluas cakupan lagu yang ditemukan pengguna. Amazon memanfaatkan *collaborative filtering* dalam merekomendasikan produk berdasarkan perilaku belanja pengguna lain, yang terbukti efektif dalam meningkatkan kepuasan pelanggan dan penjualan.

Masalah kelebihan informasi (*information overload*) bisa mengurangi kenyamanan pengguna, membuat mereka enggan menggunakan platform. Sistem rekomendasi yang efisien membantu menyajikan konten yang sesuai kebutuhan tiap individu, sekaligus menjadi strategi bisnis penting untuk mempertahankan pelanggan dan memperluas pasar.

### Pemahaman Bisnis

**Rumusan Masalah:**
1. Bagaimana menyajikan rekomendasi film berdasarkan preferensi pengguna?
2. Bagaimana menghasilkan rekomendasi relevan tanpa hanya bergantung pada rating pengguna?

**Tujuan:**
- Mengembangkan sistem rekomendasi film yang sesuai minat pengguna.
- Membandingkan efektivitas metode *Collaborative Filtering* dan *Content-Based Filtering*.

**Pendekatan Solusi:**

- *Collaborative Filtering*: Menggunakan algoritma SVD (Singular Value Decomposition) untuk mendeteksi pola tersembunyi dalam interaksi pengguna-item. Pendekatan ini cocok saat data konten film minim namun tersedia data perilaku pengguna.
- *Content-Based Filtering*: Menggunakan teknik TF-IDF pada fitur seperti genre, aktor, atau deskripsi film untuk menghitung kemiripan antar film, dilanjutkan dengan *cosine similarity* sebagai metrik kesamaan.

Kedua pendekatan dipilih karena saling melengkapi dalam memberikan personalisasi.

### Pemahaman Data

Dataset yang digunakan adalah MovieLens, terdiri dari *ratings*, *movies*, *tags*, dan *links*. Data ini mencakup informasi film dan rating dari pengguna.

- Tidak ditemukan nilai hilang maupun duplikat.
- Dataset *Movies* berisi ID film, judul, dan genre.
- Dataset *Ratings* mencakup ID pengguna, ID film, rating, dan timestamp.

### Analisis Data Eksploratif

- **Distribusi Rating**: Mayoritas rating berada pada nilai 4, mencerminkan kepuasan pengguna terhadap film yang ditonton.
- **Top 10 Film Rating Tertinggi**: Didominasi oleh film dengan rating sempurna 5.0, meskipun basis penontonnya relatif kecil.
- **Jumlah Rating per Film**: Film populer seperti *Forrest Gump* mendapat rating terbanyak.
- **Distribusi Rating per Pengguna**: Sebagian besar pengguna pasif; sebagian kecil pengguna sangat aktif memberikan banyak rating.
- **Korelasi Rating vs Jumlah Rating**: Terdapat korelasi positif lemah antara popularitas dan rating rata-rata film.

### Persiapan Data

- **Untuk Collaborative Filtering**: Dataset diformat ulang menggunakan pustaka Surprise, lalu dibagi menjadi data pelatihan dan pengujian.
- **Untuk Content-Based Filtering**: Genre diformat ulang dan dikonversi menjadi representasi numerik menggunakan TF-IDF, lalu digunakan cosine similarity untuk mengukur kesamaan antar film.

### Pembuatan Model

**Collaborative Filtering - SVD**
- Menggunakan konfigurasi default Surprise: `n_factors=100`, `n_epochs=20`, `lr_all=0.005`, `reg_all=0.02`.
- Model dilatih pada training set, diuji dengan MAE dan RMSE.
- Rekomendasi untuk User 2 mencakup film seperti *Forrest Gump* dan *Amadeus*.

**Content-Based Filtering**
- Cosine similarity menghitung kemiripan antar film berdasarkan genre.
- Sistem dapat merekomendasikan film serupa berdasarkan input judul.
- Contoh: Film seperti *Jumanji* dan *Toy Story 2* direkomendasikan untuk *Toy Story*.

### Evaluasi Model

**Collaborative Filtering**
- Hasil cross-validation menunjukkan RMSE: 0.8727 dan MAE: 0.6708.
- Model konsisten dan efisien dalam waktu pelatihan dan pengujian.

**Content-Based Filtering**
- Precision dan Recall masing-masing mencapai 1.00 untuk film *Toy Story (1995)*, karena genre dari semua rekomendasi sesuai.

### Kesimpulan

1. Sistem rekomendasi berhasil dikembangkan dengan dua pendekatan utama.
2. *Collaborative Filtering* lebih baik dalam menangkap preferensi kolektif.
3. *Content-Based Filtering* unggul dalam memberikan rekomendasi berdasarkan kesamaan konten eksplisit.
4. Kedua metode dapat dikombinasikan untuk meningkatkan kualitas rekomendasi.

### Referensi
Stratoflow. (2017). How Netflix recommendation algorithm works. Stratoflow. Retrieved from https://stratoflow.com/how-netflix-recommendation-algorithm-work/

Stratoflow. (2018). Spotify recommendation algorithm. Stratoflow. Retrieved from https://stratoflow.com/spotify-recommendation-algorithm/

CloudDevs. (2021). Building personalized recommendation engines. Retrieved from https://clouddevs.com/go/building-personalized-recommendation-engines/

Analytics Vidhya. (2020, December 17). Understanding singular value decomposition. Retrieved from https://www.analyticsvidhya.com/blog/2020/12/understanding-singular-value-decomposition/

GeeksforGeeks. (2023). Content-based filtering recommender system using Python. Retrieved from https://www.geeksforgeeks.org/content-based-filtering-recommender-system-using-python/

Towards Data Science. (2022). How to build a content-based recommendation system using TF-IDF. Retrieved from https://towardsdatascience.com/how-to-build-a-content-based-recommendation-system-using-tf-idf-b419a0424912

GroupLens. (2021). MovieLens dataset. Retrieved from https://grouplens.org/datasets/movielens/



