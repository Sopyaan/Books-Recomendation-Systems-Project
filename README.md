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
- Books.csv — 271,360 baris, 8 kolom
- Users.csv — 278,858 baris, 3 kolom
- Ratings.csv — 1,149,780 baris, 3 kolom

Secara umum, kondisi dataset adalah sebagai berikut:
- Missing values: pada file 'books.csv' kolom Book-Author, Book-Tittle, Publisher, dan Image-URL memiliki missing values. File 'users.csv' memiliki missing values pada kolom age.
- Duplicate: beberapa duplikat pada data rating dibersihkan.

  
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

### Pembersihan Data
Pembersihan data bertujuan untuk mengidentifikasi dan menangani masalah-masalah yang ada dalam dataset, seperti data duplikat, nilai yang hilang, atau inkonsistensi lainnya yang dapat mempengaruhi analisis. Missing values atau nilai yang hilang dalam dataset dapat mempengaruhi hasil analisis dan kualitas model. Salah satu teknik yang umum digunakan untuk mengatasi missing values adalah imputasi, yaitu mengganti nilai yang hilang dengan nilai yang relevan berdasarkan distribusi data, seperti menggunakan rata-rata, median, atau mode.
> Implementasi: Pada analisis ini, dilakukan penanganan missing values pada dataset 'Age'. Hal ini telah dipastikan melalui pemeriksaan menggunakan fungsi 'isnull().sum()' yang kemudian untuk menanganinya digunakan fungsi 'users.dropna(inplace=True)'.

### Merged Data
Langkah ini menggabungkan beberapa sumber data yang relevan menjadi satu dataset yang lebih komprehensif. Penggabungan data ini dilakukan agar informasi yang lebih lengkap dapat dianalisis dalam satu waktu. 
> Dataset yang digunakan melibatkan beberapa tabel terpisah yang perlu digabungkan untuk membentuk satu dataset utuh. Data ratings, books, dan users digabungkan berdasarkan kolom-kolom yang relevan, seperti ISBN dan UserID, untuk memastikan bahwa informasi tentang rating buku dan data buku tersebut tersedia dalam satu dataset.
> Implementasi: merged = pd.merge(ratings, books, on='ISBN', how='inner')

### Data Transformation
Transformasi data melibatkan konversi atau perubahan data ke dalam bentuk yang lebih mudah untuk diproses. Dalam hal ini, data yang ada dalam format series diubah menjadi format yang lebih berguna, yaitu list, untuk memudahkan analisis lebih lanjut dan integrasi dengan model rekomendasi.  Dalam hal ini, data yang ada dalam format series diubah menjadi format yang lebih berguna, yaitu list, untuk memudahkan analisis lebih lanjut dan integrasi dengan model rekomendasi.
> Implementasi: Mengonversi Data menjadi List: Kolom ISBN, Book-Title, dan Book-Rating yang sebelumnya berbentuk series diubah menjadi list. Hal ini dilakukan untuk mempermudah proses analisis dan integrasi data ke dalam model rekomendasi berbasis konten atau collaborative filtering.
> rating = preparation['Book-Rating'].tolist()
> books_name = preparation['Book-Title'].tolist()
> books_isbn = preparation['ISBN'].tolist()

---

### Content Based Filtering Preparation
#### Cutting Dataset
Tahap ini dilakukan untuk menyederhanakan data agar hanya mencakup informasi yang relevan sebelum proses pemodelan. Pemangkasan dataset dilakukan untuk menyederhanakan data dan hanya menyertakan informasi yang relevan dengan proses pemodelan. Hal ini membantu mempercepat pemrosesan dan mengurangi noise.
> Implementasi: Pada proyek kali ini hanya menggunakan 10.000 baris data saja karena keterbatasan komputasi.

#### Data Conversion
Digunakan untuk mengubah data mentah menjadi format teks yang siap diproses oleh algoritma berbasis konten. Konversi data diperlukan agar format teks dari fitur seperti judul dan penulis dapat digabungkan dan diproses oleh model berbasis teks.
> Implementasi: Proses ini menggunakan fungsi tolist() untuk memenuhi persyaratan input TF-IDF Vectorizer yaitu input list.

#### Membuat Dictionary
Tahap ini bertujuan membangun struktur data yang memudahkan proses pencocokan dan rekomendasi buku.
> Implementasi: Proses ini menghasilkan sebuah data baru hasil keseluruhan proses sebelumnya. Data disimpan pada variable books_new.

#### Ekstraksi Fitur TF-IDF
Ekstraksi fitur dengan TF-IDF (Term Frequency-Inverse Document Frequency) adalah metode pemrosesan data yang dilakukan untuk mengukur pentingnya sebuah kata dalam sebuah dokumen relatif terhadap kumpulan dokumen lainnya. Hal ini dilakukan untuk merepresentasikan deskripsi buku dalam bentuk numerik agar dapat dihitung kemiripannya.
> Implementasi: tf = TfidfVectorizer()
> tfidf_matrix = tf.fit_transform(books['Book-Title'] + ' ' + books['Book-Author'])


#### Cosine Similarity
Cosine similarity digunakan untuk mengukur kesamaan antara dua vektor dan menentukan apakah kedua vektor tersebut menunjuk ke arah yang sama. Cosine similiarity digunakan untuk mengukur tingkat kemiripan antar buku berdasarkan hasil ekstraksi fitur TF-IDF.
> Implementasi: similarity = cosine_similarity(tfidf_matrix)

### Collaborative Filltering Preparation
#### Encode Label
Encoding dilakukan untuk mengubah data kategorikal seperti User-ID dan ISBN menjadi format numerik agar dapat diproses oleh algoritma machine learning, khususnya dalam sistem rekomendasi berbasis collaborative filtering.
> Implementasi: Ekstraksi nilai unik Pertama, nilai unik dari User-ID dan ISBN diambil menggunakan fungsi unique() dan diubah menjadi list menggunakan tolist().
#### Feature Mapping
Tahapan ini memastikan setiap nilai ID dari pengguna dan buku telah dipetakan ke integer, sehingga bisa digunakan dalam model embedding pada collaborative filtering berbasis neural network.
> Implementasi: df['user'] = df['User-ID'].map(user_to_user_encoded)
df['books'] = df['ISBN'].map(isbn_to_isbn_encoded)

#### Normalisasi rating 0-1
Bertujuan untuk menyamakan skala rating agar model dapat belajar secara optimal.
> Implementasi: min_rating = df['Book-Rating'].min()
max_rating = df['Book-Rating'].max()

#### Split Data Training and Validation
Dataset dibagi menjadi data latih dan validasi agar model dapat dievaluasi secara objektif dan tidak overfitting (80% train dan 20% test)
> Implementasi: train_data, val_data = train_test_split(df, test_size=0.2, random_state=42)

---

## Modeling and Result
Pada tahap ini, sistem rekomendasi dibangun untuk memberikan rekomendasi buku berdasarkan data rating yang telah disiapkan. Tujuan utama dari modeling adalah untuk mengidentifikasi buku-buku yang relevan bagi pengguna berdasarkan perilaku mereka sebelumnya atau preferensi yang ada dalam dataset. Sistem rekomendasi dapat mengandalkan berbagai algoritma, dan di sini kita akan menjelaskan dua algoritma yang berbeda: Collaborative Filtering dan Content-Based Filtering.

### Content Based Filtering
Pada tahap ini, saya membangun sistem rekomendasi menggunakan Content-Based Filtering yang berfokus pada kesamaan antara buku-buku berdasarkan judulnya. Berikut adalah langkah-langkah yang telah dilakukan untuk membangun sistem rekomendasi buku dengan menggunakan teknik ini.

#### Mengambil 10.000 Baris Pertama dari Data
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

---
### Collaborative Filtering
Collaborative Filtering berbasis model neural network digunakan untuk membuat sistem rekomendasi buku. Proses ini melibatkan pengkodean ID pengguna dan ISBN, normalisasi rating, pembagian data ke dalam set pelatihan dan validasi, serta pelatihan model dengan menggunakan teknik deep learning.

Model ini bekerja dengan mengidentifikasi buku yang mirip dan tidak pernah dibeli pengguna dengan pertimbangan rating yang telah diberikan sebelumnya. Model ini menjadi solusi dalam menghasilkan sistem rekomendasi yang efektif dan efisien karena mempertimbangkan preferensi pengguna dan hanya hitungan detik dalam memberikan rekomendasi. Adapun langkah-langkah yang dilakukan sebagai berikut:

#### Encoding User dan ISBN
> Saya membuat pemetaan antara ID pengguna (User-ID) dan ISBN buku (ISBN) menjadi ID yang lebih sederhana untuk digunakan dalam model neural network.

#### Normalisasi Rating
> Rating dinormalisasi ke skala antara 0 dan 1, agar lebih konsisten dalam prediksi.

#### Pembagian Data untuk Pelatihan dan Validasi
> Data dibagi menjadi set pelatihan (80%) dan set validasi (20%) untuk melatih dan menguji model.

#### Model RecommenderNet
> Model neural network (RecommenderNet) menggunakan Embedding layers untuk pengguna dan buku. Model ini memprediksi rating yang diberikan oleh pengguna untuk buku tertentu.

#### Pelatihan Model
> Model dilatih dengan menggunakan loss function BinaryCrossentropy dan metrik RootMeanSquaredError untuk menilai seberapa baik model dalam memprediksi rating.

#### Menyajikan Top-N Recommendation
Setelah model selesai dilatih, model dapat memberikan rekomendasi buku berdasarkan prediksi rating yang diberikan oleh pengguna terhadap buku yang belum mereka beri rating. Berikut cara kerja dari proses ini:
- Model memilih secara acak user_id dari dataset rating. Kemudian, model mengambil data buku yang sudah pernah dikunjungi oleh pengguna tersebut.
- Model mengidentifikasi buku yang belum pernah dilihat oleh pengguna tersebut dengan memfilter buku berdasarkan ISBN yang belum ada di data rating pengguna.
- Untuk setiap buku yang belum dilihat oleh pengguna, model memprediksi rating yang mungkin diberikan oleh pengguna menggunakan model yang telah dilatih.
- Rating prediksi dihitung dengan cara menggabungkan embedding dari pengguna dan buku, serta bias masing-masing.
- Setelah mendapatkan prediksi rating untuk semua buku yang belum dilihat, model memilih 10 buku dengan rating tertinggi untuk diberikan sebagai rekomendasi kepada pengguna.
- Buku-buku yang memiliki rating tertinggi oleh pengguna ditampilkan untuk memberi konteks mengenai preferensi pengguna.

Buku dengan Rating Tinggi dari User **278148**:
| No | Judul Buku                                       | Rating |
|----|--------------------------------------------------|--------|
| 1  | Arthur Conan Doyle: A Life                      | 10     |
| 2  | Expression of the Emotions In Man and Anim       | 10     |

---
Top 10 Rekomendasi Buku untuk User 278148:
| No | Judul Buku                                                            |
|----|-----------------------------------------------------------------------|
| 1  | The Watsons Go to Birmingham - 1963 (Yearling Newbery)                |
| 2  | Into the Wild                                                         |
| 3  | Tender at the Bone: Growing Up at the Table                           |
| 4  | Lord of the Flies                                                      |
| 5  | Julia's Last Hope (Oke, Janette, Women of the West.)                  |
| 6  | Night over Water                                                       |
| 7  | Die Wiederkehr Des Königs III                                          |
| 8  | Oceano Mare                                                            |
| 9  | Carolina Moon                                                          |
| 10 | Bias: A CBS Insider Exposes How the Media Distort the News             |

---
## Evaluation
Evaluasi model recommender system bertujuan untuk mengukur seberapa baik model dalam memberikan rekomendasi yang relevan dan akurat sesuai dengan preferensi pengguna. Dalam proyek ini, evaluasi dilakukan menggunakan beberapa metrik yang relevan untuk konteks data dan tujuan model, yang berupa sistem rekomendasi buku.

### Metrik Evaluasi yang Digunakan
#### Root Mean Squared Error (RMSE)
RMSE mengukur seberapa besar perbedaan antara rating yang diprediksi oleh model dan rating yang sebenarnya diberikan oleh pengguna. RMSE merupakan salah satu metrik utama untuk mengukur kesalahan prediksi model rekomendasi.

Formula:
RMSE = √( (1/n) × Σ (y_pred − y_true)² )


> Di mana:  
> - \( y_{pred} \) adalah rating yang diprediksi oleh model.  
> - \( y_{true} \) adalah rating aktual yang diberikan oleh pengguna.  
> - \( n \) adalah jumlah data yang dievaluasi.  

> Cara kerja: Metrik ini dihitung dengan cara mencari rata-rata kuadrat selisih antara rating yang diprediksi dan rating yang sebenarnya, kemudian mengambil akar kuadratnya. Semakin kecil nilai RMSE, semakin akurat prediksi model.

#### Binary Crossentropy Loss (BCE Loss)
BCE Loss digunakan karena model ini memperkirakan rating dalam bentuk probabilitas, yang dihitung dengan fungsi sigmoid. Metrik ini mengukur seberapa baik model dalam memprediksi nilai rating pada skala biner (misalnya: apakah pengguna akan menyukai buku atau tidak).

Formula: 
Binary Crossentropy = - (1/n) × Σ [ y_true * log(y_pred) + (1 - y_true) * log(1 - y_pred) ]

> Di mana:  
> - \( y_{true} \) adalah nilai rating yang sebenarnya (0 atau 1).  
> - \( y_{pred} \) adalah nilai probabilitas yang diprediksi oleh model.

> Cara kerja: Binary crossentropy menghitung perbedaan antara nilai probabilitas yang diprediksi oleh model dan label aktual. Nilai loss yang lebih kecil menunjukkan bahwa model lebih baik dalam memperkirakan kemungkinan rating yang benar.

#### Hasil Proyek Berdasarkan Metrik Evaluasi

Pada hasil pelatihan model, kita memperoleh nilai berikut:

| Metrik                 | Nilai  |
|------------------------|--------|
| **Loss**              | 0.2057 |
| **Root Mean Squared Error (RMSE)** | 0.1500 |
| **Validation Loss**   | 0.4322 |
| **Validation RMSE**   | 0.3108 |

---

Semakin kecil nilai RMSE dan loss, semakin baik model dalam memberikan rekomendasi yang akurat dan sesuai dengan preferensi pengguna.



