# Books Recomendation Systems Project

## Project Overview
### Latar belakang
Industri buku di Amerika Serikat telah menghadapi berbagai tantangan, mulai dari meningkatnya popularitas media digital hingga kesulitan yang dialami toko buku fisik. Namun, data menunjukkan bahwa buku tetap menjadi bagian penting dalam kehidupan sehari-hari konsumen. Menurut Statista, angka penjualan buku cetak bahkan mengalami perbaikan dan kini secara konsisten melampaui 700 juta unit per tahun. Selain itu, format buku cetak tetap menjadi yang paling populer di antara konsumen AS, dengan 65 persen orang dewasa melaporkan telah membaca buku cetak dalam dua belas bulan terakhir [(Statista, 2024)](https://www.statista.com/topics/1177/book-market/#topicOverview).

Di sisi lain, banyaknya pilihan buku di pasaran membuat konsumen menghadapi **tantangan dalam menemukan buku yang sesuai dengan preferensi mereka**. Sistem rekomendasi hadir sebagai solusi untuk mempersempit pilihan dan membantu pengguna menemukan buku yang paling menarik bagi mereka. Selain itu, sistem ini juga memungkinkan pengguna menemukan konten baru yang mungkin tidak mereka temukan secara mandiri [(Intel, 2024)](https://www.intel.co.id/content/www/id/id/learn/recommendation-systems.html#:~:text=Sistem%20rekomendasi%20membantu%20pengguna%20mempersempit,bisa%20saja%20tidak%20mereka%20temukan)

### Pentingnya Proyek Ini
Menyediakan sistem rekomendasi buku yang tepat sasaran dapat meningkatkan pengalaman membaca pengguna, mendorong loyalitas konsumen terhadap platform distribusi buku, dan meningkatkan angka penjualan. Selain itu, sistem rekomendasi juga menjadi salah satu strategi penting dalam menghadapi persaingan ketat di industri buku yang semakin terdigitalisasi.

---
## Business Understanding
### Problem Statements
Dalam industri buku yang sangat kompetitif dengan ribuan judul baru diterbitkan setiap tahunnya, pengguna seringkali mengalami kesulitan dalam menemukan buku yang sesuai dengan preferensi dan minat pribadi mereka. Banyaknya pilihan yang tersedia menyebabkan pengguna merasa kewalahan, sehingga membutuhkan bantuan sistem untuk mempersempit pilihan dan menemukan buku yang relevan. Tanpa sistem rekomendasi yang efektif, pengalaman pengguna dapat menurun dan berpotensi mengurangi tingkat pembelian atau keterlibatan pengguna.
  
### Goals
- Mengembangkan dua pendekatan sistem rekomendasi, yaitu **Content-Based Filtering** dan **Collaborative Filtering**.
- Membantu pengguna menemukan buku baru yang mungkin belum pernah mereka ketahui.
- Meningkatkan akurasi prediksi rating dan relevansi rekomendasi.
- Meningkatkan potensi penjualan atau keterlibatan pengguna dengan platform buku.
  
### Solution Statements
Untuk mencapai tujuan di atas, proyek ini mengusulkan dua pendekatan sistem rekomendasi:
#### Content-Based Filtering
Pendekatan ini memberikan rekomendasi berdasarkan kesamaan konten antara buku yang sudah disukai pengguna dan buku lainnya. Sistem akan menganalisis atribut seperti genre, deskripsi, atau penulis untuk menemukan buku serupa dengan preferensi pengguna sebelumnya.

Kelebihan:
- Tidak memerlukan data pengguna lain, cukup data preferensi pengguna sendiri.
- Rekomendasi bisa sangat personal.

Kekurangan:
- Terbatas pada item yang mirip dengan yang sudah dikenal pengguna (kurang eksplorasi konten baru).
- Tidak dapat merekomendasikan buku di luar preferensi awal pengguna.

#### Collaborative Filtering
Pendekatan ini memberikan rekomendasi berdasarkan kesamaan perilaku antar pengguna. Sistem akan merekomendasikan buku yang disukai oleh pengguna lain dengan profil atau pola perilaku serupa.

Kelebihan:
- Dapat menemukan buku-buku baru yang tidak mirip secara langsung dengan preferensi awal pengguna.
- Lebih fleksibel dan memperluas cakrawala rekomendasi.

Kekurangan:
- Membutuhkan data interaksi pengguna dalam jumlah besar (seperti rating, review, atau histori pembelian).
---

## Data Understanding
### Informasi Data
Dataset yang digunakan dalam proyek ini adalah Book Recommendation Dataset yang tersedia secara publik di Kaggle. Dataset ini berisi informasi terkait rating buku yang diberikan oleh pengguna, serta detail buku itu sendiri, seperti judul dan penulis. Dataset ini bertujuan untuk mendukung pembangunan sistem rekomendasi berbasis perilaku pengguna dan karakteristik buku.

Dataset ini dapat diunduh melalui tautan berikut:
[Kaggle - Book Recommendation Dataset](https://www.kaggle.com/datasets/arashnic/book-recommendation-dataset)

### Jumlah dan Kondisi Data
Dataset terdiri dari tiga file utama:
- Books.csv — Berisi informasi tentang buku.
- Users.csv — Berisi informasi tentang pengguna.
- Ratings.csv — Berisi informasi tentang rating yang diberikan oleh pengguna terhadap buku.

Secara umum, kondisi dataset adalah sebagai berikut:
- `Books.csv` ➔ berisi 271.360 ISBN dan 242.135 judul buku.
- `Ratings.csv` ➔ berisi 1.149.780 data rating.
- `Users.csv` ➔ berisi 278.858 pengguna.

  
### Variabel dalam Dataset 
Dataset ini berisi informasi tentang buku, pengguna, dan rating yang diberikan oleh pengguna terhadap buku. Dataset terdiri dari tiga file utama:

#### `Books.csv`

Berisi detail informasi mengenai buku.

| Variabel | Deskripsi |
|----------|-----------|
| `ISBN` | Nomor identifikasi unik setiap buku |
| `Book-Title` | Judul buku |
| `Book-Author` | Nama penulis buku |
| `Year-Of-Publication` | Tahun terbit buku |
| `Publisher` | Nama penerbit buku |
| `Image-URL-S` | URL gambar sampul buku (ukuran kecil) |
| `Image-URL-M` | URL gambar sampul buku (ukuran sedang) |
| `Image-URL-L` | URL gambar sampul buku (ukuran besar) |

---

#### `Users.csv`

Berisi informasi pengguna.

| Variabel | Deskripsi |
|----------|-----------|
| `User-ID` | ID unik pengguna |
| `Location` | Lokasi pengguna (format: Kota, Provinsi/Negara Bagian, Negara) |
| `Age` | Umur pengguna (beberapa nilai mungkin kosong atau tidak valid) |

---

#### `Ratings.csv`

Berisi data rating yang diberikan pengguna terhadap buku.

| Variabel | Deskripsi |
|----------|-----------|
| `User-ID` | ID pengguna yang memberikan rating |
| `ISBN` | ID buku yang diberi rating |
| `Book-Rating` | Nilai rating (0–10) <br> `0` berarti pengguna melihat buku tetapi tidak memberi rating eksplisit |

---
### *Exploratory Data Analysis (EDA):**
- Menemukan adanya banyak nilai `Book-Rating` = 0 (belum memberikan rating sesungguhnya).
- Ditemukan missing value di `Users.csv` dan `Books.csv`.
- Tidak semua ISBN di `Ratings.csv` ditemukan di `Books.csv`, perlu data cleaning.
- Buku yang diberi rating >0 hanya sebagian kecil dari total ISBN yang ada.
- Usia pengguna dalam dataset berkisar dari anak-anak hingga lansia, namun terdapat beberapa anomali usia seperti 0 tahun atau lebih dari 100 tahun.

---
## Data Preparation
Data preparation adalah tahapan penting dalam analisis data, yang bertujuan untuk mempersiapkan dataset agar dapat digunakan dalam model analitik yang lebih lanjut. Dalam tahapan ini, dilakukan beberapa proses, seperti pembersihan data (data cleaning), transformasi data (data transformation), dan penyusunan data ke dalam format yang sesuai.

#### Pembersihan Data
Pembersihan data bertujuan untuk mengidentifikasi dan menangani masalah-masalah yang ada dalam dataset, seperti data duplikat, nilai yang hilang, atau inkonsistensi lainnya yang dapat mempengaruhi analisis. 

#### Merged Data
Langkah ini menggabungkan beberapa sumber data yang relevan menjadi satu dataset yang lebih komprehensif. Penggabungan data ini dilakukan agar informasi yang lebih lengkap dapat dianalisis dalam satu waktu.

#### Data Transformation
Transformasi data melibatkan konversi atau perubahan data ke dalam bentuk yang lebih mudah untuk diproses. Dalam hal ini, data yang ada dalam format series diubah menjadi format yang lebih berguna, yaitu list, untuk memudahkan analisis lebih lanjut dan integrasi dengan model rekomendasi.

#### Proses Data Preparation yang Dilakukan
##### Penanganan Missing Values
Missing values atau nilai yang hilang dalam dataset dapat mempengaruhi hasil analisis dan kualitas model. Salah satu teknik yang umum digunakan untuk mengatasi missing values adalah imputasi, yaitu mengganti nilai yang hilang dengan nilai yang relevan berdasarkan distribusi data, seperti menggunakan rata-rata, median, atau mode.
> Implementasi: Pada analisis ini, dilakukan penanganan missing values pada dataset 'Age'. Hal ini telah dipastikan melalui pemeriksaan menggunakan fungsi 'isnull().sum()' yang kemudian untuk menanganinya digunakan fungsi 'users.dropna(inplace=True)'.

##### Merged Data
Langkah ini menggabungkan beberapa sumber data yang relevan menjadi satu dataset yang lebih komprehensif. 
> Dataset yang digunakan melibatkan beberapa tabel terpisah yang perlu digabungkan untuk membentuk satu dataset utuh. Data ratings, books, dan users digabungkan berdasarkan kolom-kolom yang relevan, seperti ISBN dan UserID, untuk memastikan bahwa informasi tentang rating buku dan data buku tersebut tersedia dalam satu dataset.
> Implementasi: merged = pd.merge(ratings, books, on='ISBN', how='inner')

#####  Data Transformation
Transformasi data melibatkan konversi atau perubahan data ke dalam bentuk yang lebih mudah untuk diproses. Dalam hal ini, data yang ada dalam format series diubah menjadi format yang lebih berguna, yaitu list, untuk memudahkan analisis lebih lanjut dan integrasi dengan model rekomendasi.
> Implementasi: Mengonversi Data menjadi List: Kolom ISBN, Book-Title, dan Book-Rating yang sebelumnya berbentuk series diubah menjadi list. Hal ini dilakukan untuk mempermudah proses analisis dan integrasi data ke dalam model rekomendasi berbasis konten atau collaborative filtering.
> rating = preparation['Book-Rating'].tolist()
> books_name = preparation['Book-Title'].tolist()
> books_isbn = preparation['ISBN'].tolist()

---

## Modeling and Result
Pada tahap ini, sistem rekomendasi dibangun untuk memberikan rekomendasi buku berdasarkan data rating yang telah disiapkan. Tujuan utama dari modeling adalah untuk mengidentifikasi buku-buku yang relevan bagi pengguna berdasarkan perilaku mereka sebelumnya atau preferensi yang ada dalam dataset. Sistem rekomendasi dapat mengandalkan berbagai algoritma, dan di sini kita akan menjelaskan dua algoritma yang berbeda: Collaborative Filtering dan Content-Based Filtering.

#### Content Based Filtering
Pada tahap ini, saya membangun sistem rekomendasi menggunakan Content-Based Filtering yang berfokus pada kesamaan antara buku-buku berdasarkan judulnya. Berikut adalah langkah-langkah yang telah dilakukan untuk membangun sistem rekomendasi buku dengan menggunakan teknik ini.

##### Mengambil 10.000 Baris Pertama dari Data
Untuk mengurangi ukuran dataset yang besar dan mempercepat proses, hanya diambil 10.000 baris pertama dari data yang sudah disiapkan.
> data_cut = data_new.head(10000)

#### Konversi Kolom Judul Buku ke dalam Bentuk List
Langkah ini mengubah kolom 'Book-Title' yang berisi judul buku menjadi sebuah list agar mudah diproses lebih lanjut dalam teknik TF-IDF.
> books_title_list = data_cut['Book-Title'].tolist()

####  Inisialisasi TF-IDF Vectorizer
Di sini, saya menggunakan TF-IDF Vectorizer untuk mengubah teks judul buku menjadi representasi numerik yang dapat diproses oleh model. TF-IDF adalah teknik yang mengukur seberapa penting sebuah kata dalam suatu dokumen relatif terhadap seluruh koleksi dokumen (corpus). Kata-kata yang sering muncul dalam satu dokumen tetapi jarang muncul dalam dokumen lainnya akan memiliki bobot tinggi, sementara kata-kata yang umum akan memiliki bobot rendah.
> tfidf = TfidfVectorizer(stop_words='english')
> Catatan: Di sini saya juga menghilangkan kata-kata umum (stop words) seperti "the", "is", dan "a" yang tidak berkontribusi banyak pada analisis.

#### Menghitung Kemiripan Antar Judul Buku (Cosine Similarity)
Kemudian, saya menghitung cosine similarity antara semua judul buku. Cosine similarity adalah ukuran seberapa mirip dua vektor berdasarkan sudut antara mereka. Nilai cosine similarity berkisar antara 0 (tidak mirip sama sekali) hingga 1 (identik). Pada tahapan ini, dihitung cosine similarity pada dataframe tfidf_matrix yang diperoleh pada tahapan TD-IDF Vectorizer sebelumnya. Proses ini menghasilkan output berupa matriks kesamaan dalam bentuk array.
> cosine_sim_matrix = cosine_similarity(tfidf_matrix)

#### Menyajikan Top-N Recommendation
Langkah selanjutnya adalah membuat sebuah fungsi untuk memberi hasil rekomendasi berdasarkan ISBN yang diberikan. Fungsi ini akan menggunakan cosine similarity yang telah dihitung pada langkah sebelumnya untuk menentukan buku-buku yang paling mirip.

Cara Kerja:
- Mengambil Data dengan argpartition(): Fungsi pertama-tama menggunakan argpartition() untuk mengambil index dengan nilai kemiripan tertinggi.
- Mengubah Dataframe Menjadi Numpy: Data kemudian diubah menjadi format numpy untuk memudahkan pengolahan.
- Membuat Range: Fungsi ini akan membuat rentang (range(start, stop, step)) untuk memilih buku-buku dengan kemiripan terbesar.
- Menghapus ISBN Pengguna: Setelah itu, ISBN buku yang dimasukkan oleh pengguna akan dihapus menggunakan fungsi drop(), agar buku tersebut tidak muncul dalam daftar rekomendasi.
- Mengembalikan Data dalam Bentuk DataFrame: Hasilnya akan dikembalikan dalam bentuk DataFrame yang berisi rekomendasi buku yang mirip.

Berikut hasil rekomendasi dari buku dengan ISBN '0449143600':
| ISBN        | Book-Title     | Book-Rating |
|-------------|----------------|-------------|
| 0449143600  | Love by Fire    | 0           |

---

5 Rekomendasi buku berdasarkan ISBN '0449143600':
| No | ISBN        | Book-Title                     | Book-Rating |
|----|-------------|---------------------------------|-------------|
| 1  | 0843928395  | All I Could Do Was Love You     | 9           |
| 2  | 0375409440  | Love                            | 8           |
| 3  | 0373025823  | Perhaps Love                    | 0           |
| 4  | 0440147247  | In the Name of Love              | 0           |
| 5  | 0553275283  | Love Story                      | 8           |




