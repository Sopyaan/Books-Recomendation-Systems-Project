# Books Recomendation Systems Project

## Project Overview
### Latar belakang
Industri buku di Amerika Serikat telah menghadapi berbagai tantangan, mulai dari meningkatnya popularitas media digital hingga kesulitan yang dialami toko buku fisik. Namun, data menunjukkan bahwa buku tetap menjadi bagian penting dalam kehidupan sehari-hari konsumen. Menurut Statista, angka penjualan buku cetak bahkan mengalami perbaikan dan kini secara konsisten melampaui 700 juta unit per tahun. Selain itu, format buku cetak tetap menjadi yang paling populer di antara konsumen AS, dengan 65 persen orang dewasa melaporkan telah membaca buku cetak dalam dua belas bulan terakhir [(Statista, 2024)](https://www.statista.com/topics/1177/book-market/#topicOverview).

Di sisi lain, banyaknya pilihan buku di pasaran membuat konsumen menghadapi **tantangan dalam menemukan buku yang sesuai dengan preferensi mereka**. Sistem rekomendasi hadir sebagai solusi untuk mempersempit pilihan dan membantu pengguna menemukan buku yang paling menarik bagi mereka. Selain itu, sistem ini juga memungkinkan pengguna menemukan konten baru yang mungkin tidak mereka temukan secara mandiri [(Intel, 2024)](https://www.intel.co.id/content/www/id/id/learn/recommendation-systems.html#:~:text=Sistem%20rekomendasi%20membantu%20pengguna%20mempersempit,bisa%20saja%20tidak%20mereka%20temukan)

### Pentingnya Proyek Ini
Menyediakan sistem rekomendasi buku yang tepat sasaran dapat meningkatkan pengalaman membaca pengguna, mendorong loyalitas konsumen terhadap platform distribusi buku, dan meningkatkan angka penjualan. Selain itu, sistem rekomendasi juga menjadi salah satu strategi penting dalam menghadapi persaingan ketat di industri buku yang semakin terdigitalisasi.

## Business Understanding
### Problem Statements
- Bagaimana merekomendasikan buku baru yang kemungkinan disukai pengguna berdasarkan histori interaksi mereka dan pengguna lain?
- Bagaimana mengatasi ketidaksempurnaan data seperti ISBN yang tidak ditemukan?
- Bagaimana menangani permasalahan data terbatas pada pengguna baru (cold-start)?
  
### Goals
- Mengembangkan dua pendekatan sistem rekomendasi, yaitu **Content-Based Filtering** dan **Collaborative Filtering**.
- Meningkatkan akurasi prediksi rating dan relevansi rekomendasi.
- Memberikan rekomendasi Top-N buku untuk masing-masing pengguna.
  
### Solution Statements
- **Content-Based Filtering**:  
  Menggunakan judul buku (`Book-Title`) untuk menghitung kemiripan antar buku dengan TF-IDF dan Cosine Similarity.
- **Collaborative Filtering**:  
  Menggunakan embedding user dan ISBN berbasis TensorFlow (RecommenderNet) untuk memprediksi kemungkinan rating.

---

## Data Understanding
### Informasi Data

### Jumlah dan Kondisi Data
- `Books.csv` ➔ berisi 271.360 ISBN dan 242.135 judul buku.
- `Ratings.csv` ➔ berisi 1.149.780 data rating.
- `Users.csv` ➔ berisi 278.858 pengguna.
- Dataset diambil dari Kaggle: [Kaggle Book Recommendation Dataset](https://www.kaggle.com/datasets/arashnic/book-recommendation-dataset)
  
### Variabel dalam Dataset 
Dataset ini berisi informasi tentang buku, pengguna, dan rating yang diberikan oleh pengguna terhadap buku. Dataset terdiri dari tiga file utama:

---

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

## Data Preparation
**Teknik Data Preparation yang Diterapkan:**
- Menghapus missing value di `Users` dan `Books`.
- Merge `Ratings` dengan `Books` berdasarkan `ISBN`.
- Membatasi data ke 10.000 entri untuk efisiensi pelatihan model.
- Encoding `User-ID` dan `ISBN` ke dalam ID numerik menggunakan `map`.
- Normalisasi rating ke skala 0–1 untuk keperluan training neural network.

**Mengapa Tahapan Ini Diperlukan:**
- Memastikan data bebas dari missing value agar model tidak error.
- Encoding numerik diperlukan karena embedding layer di TensorFlow hanya menerima input integer.
- Normalisasi rating membantu model convergen lebih cepat dan stabil.

---
**Sistem Rekomendasi yang Dibuat:**
1. **Content-Based Filtering:**
   - Menggunakan TF-IDF pada kolom `Book-Title`.
   - Menghitung Cosine Similarity antar buku.
   - Memberikan rekomendasi buku dengan judul yang paling mirip.

2. **Collaborative Filtering:**
   - Membuat model `RecommenderNet` menggunakan TensorFlow.
   - Menggunakan embedding user dan ISBN, lalu menghitung dot product.
   - Loss function: Binary Crossentropy.
   - Optimizer: Adam.

**Top-N Recommendation:**
- Menampilkan **5 buku dengan rating tertinggi** yang pernah dirating user.
- Menampilkan **Top 10 buku rekomendasi baru** untuk user berdasarkan prediksi skor tertinggi.

**Kelebihan dan Kekurangan Pendekatan:**

| Pendekatan | Kelebihan | Kekurangan |
|:--|:--|:--|
| Content-Based Filtering | Tidak butuh banyak data pengguna lain, cepat saat inference | Cenderung rekomendasi buku yang mirip-mirip saja |
| Collaborative Filtering | Mampu menangkap pola preferensi pengguna secara kompleks | Butuh cukup banyak data historis pengguna, rentan cold-start |

---

## 🔯 Evaluation

**Metrik Evaluasi yang Digunakan:**
- **Root Mean Squared Error (RMSE)**

**Formula RMSE:**
\[
\text{RMSE} = \sqrt{\frac{1}{n} \sum_{i=1}^{n}(y_i - \hat{y}_i)^2}
\]

**Penjelasan RMSE:**
- RMSE mengukur rata-rata deviasi kuadrat antara prediksi dan nilai aktual.
- Semakin kecil nilai RMSE, semakin baik prediksi model.

**Hasil Proyek Berdasarkan RMSE:**
- RMSE pada data training dan validation stabil setelah 100 epoch.
- Gap antara RMSE training dan validation kecil, menunjukkan model tidak overfitting.

---
