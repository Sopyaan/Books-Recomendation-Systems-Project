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
Pembersihan data bertujuan untuk mengidentifikasi dan menangani masalah-masalah yang ada dalam dataset, seperti data duplikat, nilai yang hilang, atau inkonsistensi lainnya yang dapat mempengaruhi analisis. Missing values atau nilai yang hilang dalam dataset dapat mempengaruhi hasil analisis dan kualitas model. Pada tahap pembersihan data, digunakan fungsi `dropna()` untuk menghapus baris dengan missing value. Keputusan ini diambil karena sebagian besar missing value berasal dari kolom non-kritis seperti URL gambar (`Image-URL-S`, `Image-URL-M`, dan `Image-URL-L`) serta informasi tambahan seperti nama penerbit atau tahun terbit, yang tidak digunakan langsung dalam proses pemodelan sistem rekomendasi. Oleh karena itu, menghapus baris-baris ini dinilai lebih efisien dibandingkan melakukan imputasi, tanpa mengorbankan kualitas rekomendasi.

> Implementasi:
> Pada analisis ini, dilakukan penanganan missing values pada dataset 'Age'. Hal ini telah dipastikan melalui pemeriksaan menggunakan fungsi 'isnull().sum()' yang kemudian untuk menanganinya digunakan fungsi 'users.dropna(inplace=True)'.

### Merged Data
Langkah ini menggabungkan beberapa sumber data yang relevan menjadi satu dataset yang lebih komprehensif. Penggabungan data ini dilakukan agar informasi yang lebih lengkap dapat dianalisis dalam satu waktu. 
> Dataset yang digunakan melibatkan beberapa tabel terpisah yang perlu digabungkan untuk membentuk satu dataset utuh. Data ratings, books, dan users digabungkan berdasarkan kolom-kolom yang relevan, seperti ISBN dan UserID, untuk memastikan bahwa informasi tentang rating buku dan data buku tersebut tersedia dalam satu dataset.
> Implementasi:
> merged = pd.merge(ratings, books, on='ISBN', how='inner')

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
> Implementasi:

> Pada proyek kali ini hanya menggunakan 10.000 baris data saja karena keterbatasan komputasi.

#### Data Conversion
Digunakan untuk mengubah data mentah menjadi format teks yang siap diproses oleh algoritma berbasis konten. Konversi data diperlukan agar format teks dari fitur seperti judul dan penulis dapat digabungkan dan diproses oleh model berbasis teks.
> Implementasi:

> Proses ini menggunakan fungsi tolist() untuk memenuhi persyaratan input TF-IDF Vectorizer yaitu input list.

#### Membuat Dictionary
Tahap ini bertujuan membangun struktur data yang memudahkan proses pencocokan dan rekomendasi buku.
> Implementasi:

> Proses ini menghasilkan sebuah data baru hasil keseluruhan proses sebelumnya. Data disimpan pada variable books_new.

#### Ekstraksi Fitur TF-IDF
Ekstraksi fitur dengan TF-IDF (Term Frequency-Inverse Document Frequency) adalah metode pemrosesan data yang dilakukan untuk mengukur pentingnya sebuah kata dalam sebuah dokumen relatif terhadap kumpulan dokumen lainnya. Hal ini dilakukan untuk merepresentasikan deskripsi buku dalam bentuk numerik agar dapat dihitung kemiripannya.
> Implementasi:

> tf = TfidfVectorizer()

> tfidf_matrix = tf.fit_transform(books['Book-Title'] + ' ' + books['Book-Author'])

### Collaborative Filltering Preparation
### Merged Data

#### Encode Label
Encoding dilakukan untuk mengubah data kategorikal seperti User-ID dan ISBN menjadi format numerik agar dapat diproses oleh algoritma machine learning, khususnya dalam sistem rekomendasi berbasis collaborative filtering.
> Implementasi: Ekstraksi nilai unik Pertama, nilai unik dari User-ID dan ISBN diambil menggunakan fungsi unique() dan diubah menjadi list menggunakan tolist().
#### Feature Mapping
Tahapan ini memastikan setiap nilai ID dari pengguna dan buku telah dipetakan ke integer, sehingga bisa digunakan dalam model embedding pada collaborative filtering berbasis neural network.
> Implementasi:

> df['user'] = df['User-ID'].map(user_to_user_encoded)

> df['books'] = df['ISBN'].map(isbn_to_isbn_encoded)

#### Normalisasi rating 0-1
Bertujuan untuk menyamakan skala rating agar model dapat belajar secara optimal.
> Implementasi:

> min_rating = df['Book-Rating'].min()

> max_rating = df['Book-Rating'].max()

#### Split Data Training and Validation
Dataset dibagi menjadi data latih dan validasi agar model dapat dievaluasi secara objektif dan tidak overfitting (80% train dan 20% test)
> Implementasi:

> train_indices = int(0.8 * df.shape[0])

> x_train, x_val, y_train, y_val = (

>    x[:train_indices],

>    x[train_indices:],

>    y[:train_indices],

>    y[train_indices:]

> )

---

## Modeling and Result
Pada tahap ini, sistem rekomendasi dibangun untuk memberikan rekomendasi buku berdasarkan data rating yang telah disiapkan. Tujuan utama dari modeling adalah untuk mengidentifikasi buku-buku yang relevan bagi pengguna berdasarkan perilaku mereka sebelumnya atau preferensi yang ada dalam dataset. Sistem rekomendasi dapat mengandalkan berbagai algoritma, dan di sini kita akan menjelaskan dua algoritma yang berbeda: Collaborative Filtering dan Content-Based Filtering.

### Content Based Filtering
Pendekatan Content-Based Filtering merekomendasikan item berdasarkan kesamaan kontennya. Dalam proyek ini, fitur yang digunakan adalah judul buku, dan model dibangun menggunakan teknik TF-IDF (Term Frequency–Inverse Document Frequency) serta Cosine Similarity.

#### Pengukuran Kemiripan dengan Cosine Similarity
Setelah memperoleh vektor TF-IDF untuk seluruh judul buku, cosine similarity dihitung antar semua pasangan buku. Cosine similarity mengukur tingkat kemiripan antar dua vektor berdasarkan sudut di antara mereka, menghasilkan nilai antara 0 hingga 1, di mana nilai yang lebih tinggi menunjukkan tingkat kemiripan yang lebih besar.

#### Menyajikan Top-N Recommendation
Langkah selanjutnya adalah membuat sebuah fungsi untuk memberi hasil rekomendasi berdasarkan ISBN yang diberikan. Fungsi ini akan menggunakan cosine similarity yang telah dihitung pada langkah sebelumnya untuk menentukan buku-buku yang paling mirip.

Sistem rekomendasi bekerja dengan langkah-langkah berikut:
- Mengambil ISBN sebagai input.
- Menemukan indeks vektor TF-IDF dari buku tersebut.
- Mengambil skor kemiripan dari matriks cosine similarity terhadap seluruh buku lainnya.
- Mengurutkan dan memilih buku dengan skor kemiripan tertinggi (selain buku itu sendiri).
- Mengembalikan lima rekomendasi buku paling mirip berdasarkan judul.

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
Pada pendekatan ini, sistem rekomendasi dikembangkan menggunakan model berbasis neural network yang dikenal sebagai RecommenderNet. Metode Collaborative Filtering bekerja dengan menganalisis interaksi historis pengguna dan item (dalam hal ini buku), tanpa memerlukan informasi konten buku. Model bertujuan untuk mempelajari pola preferensi pengguna dari data rating yang tersedia, guna memprediksi rating terhadap buku yang belum pernah dibaca.

#### Arsitektur Model: RecommenderNet
Model menggunakan embedding layers untuk merepresentasikan pengguna dan buku dalam ruang dimensi laten. Setiap embedding menangkap representasi numerik dari pengguna dan item berdasarkan interaksinya. Komponen utama model meliputi:
- User embedding layer dan item embedding layer: Mengubah ID pengguna dan ISBN menjadi vektor berdimensi tetap.
- Dot product antara embedding pengguna dan item: Memprediksi seberapa besar kemungkinan pengguna menyukai item tertentu.
- Bias term: Ditambahkan untuk menangkap kecenderungan khusus pengguna atau item.
- Activation & loss: Model menggunakan sigmoid activation di output layer dan dilatih dengan Binary Crossentropy loss, sementara performa evaluasi diukur menggunakan Root Mean Squared Error (RMSE).

#### Strategi Pelatihan
- Data pelatihan dan validasi dibagi secara proporsional (80:20).
- Rating dinormalisasi ke rentang 0 hingga 1 untuk konsistensi prediksi.
- Model dilatih selama beberapa epochs menggunakan algoritma optimasi seperti Adam optimizer.
  
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
Evaluasi dalam sistem rekomendasi bertujuan untuk mengukur seberapa baik model dalam memberikan hasil yang relevan, akurat, dan sesuai dengan preferensi pengguna. Evaluasi dilakukan terhadap dua pendekatan yang digunakan, yaitu Content-Based Filtering (CBF) dan Collaborative Filtering berbasis neural network (RecommenderNet).

### Evaluasi Model Content-Based Filtering (CBF)
Untuk pendekatan CBF, metrik evaluasi difokuskan pada relevansi rekomendasi, bukan prediksi rating. Salah satu metrik yang digunakan adalah Precision@K.

#### Precision@K
Precision@K adalah metrik evaluasi yang mengukur seberapa banyak rekomendasi yang relevan di antara K rekomendasi teratas yang diberikan oleh model. Dalam hal ini, K adalah jumlah rekomendasi buku yang dihasilkan oleh sistem.

Misalnya, jika kita menggunakan **Top-5 rekomendasi**, Precision@5 dihitung sebagai berikut:

$$
\text{Precision@5} = \frac{\text{Jumlah buku yang relevan di Top-5}}{5}
$$

Berdasarkan hasil rekomendasi untuk buku dengan ISBN '0449143600' kita menentukan relevansi dengan Buku dengan rating ≥ 6 dianggap relevan, sehingga hasilnya yaitu:

**Jumlah relevan = 3**. Maka, Precision@5 adalah:

$$
\text{Precision@5} = \frac{3}{5} = 0.6
$$

### Evaluasi Model Collaborative Filtering
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

---
### Hubungan dengan Business Understanding
Model yang diuji dalam proyek ini telah berhasil memberikan solusi yang relevan dalam meningkatkan pengalaman pengguna dalam sistem rekomendasi buku. Dengan evaluasi menggunakan metrik precision dan RMSE, model ini terbukti dapat memberikan rekomendasi yang relevan dan akurat, yang pada gilirannya dapat meningkatkan kepuasan pengguna.

- **Problem Statement**: Sistem rekomendasi harus memberikan buku yang relevan dan menarik bagi pengguna. Evaluasi model menunjukkan bahwa sistem ini berhasil dalam hal tersebut.
- **Goals yang Diharapkan**: Model berhasil memenuhi tujuan untuk memberikan rekomendasi yang relevan berdasarkan preferensi pengguna, seperti yang tercermin dalam metrik evaluasi.
- **Solusi yang Diterapkan**: Pendekatan berbasis Content-based Filtering dan evaluasi berbasis precision memberikan dampak yang positif, di mana sistem dapat merekomendasikan buku yang relevan dengan lebih akurat.

Dengan hasil ini, model recommender yang dibangun dapat diterapkan secara efektif untuk meningkatkan pengalaman pengguna dan membantu mereka menemukan buku yang sesuai dengan preferensi mereka.

