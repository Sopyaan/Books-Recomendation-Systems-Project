# Books Recomendation Systems Project

## Domain Proyek
### Latar belakang

## Business Understanding
### Problem Statements

### Goals

### Solution Statements

## Data Understanding
### Informasi Data

### Jumlah dan Kondisi Data

### Variabel dalam Dataset 
Dataset ini berisi informasi tentang buku, pengguna, dan rating yang diberikan oleh pengguna terhadap buku. Dataset terdiri dari tiga file utama:

---

### `Books.csv`

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

### `Users.csv`

Berisi informasi pengguna.

| Variabel | Deskripsi |
|----------|-----------|
| `User-ID` | ID unik pengguna |
| `Location` | Lokasi pengguna (format: Kota, Provinsi/Negara Bagian, Negara) |
| `Age` | Umur pengguna (beberapa nilai mungkin kosong atau tidak valid) |

---

### `Ratings.csv`

Berisi data rating yang diberikan pengguna terhadap buku.

| Variabel | Deskripsi |
|----------|-----------|
| `User-ID` | ID pengguna yang memberikan rating |
| `ISBN` | ID buku yang diberi rating |
| `Book-Rating` | Nilai rating (0–10) <br> `0` berarti pengguna melihat buku tetapi tidak memberi rating eksplisit |

---
## Data Preparation
