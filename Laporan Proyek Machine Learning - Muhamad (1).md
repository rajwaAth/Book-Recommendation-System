# Laporan Proyek Machine Learning - Muhamad Rajwa Athoriq

## Project Overview
Di tengah maraknya platform digital untuk membaca buku, pengguna dihadapkan pada tantangan dalam memilih bacaan yang sesuai dengan preferensi pribadi. Banyaknya pilihan tanpa bantuan sistem yang cerdas sering kali membuat pengguna kewalahan dan menyebabkan pengalaman membaca menjadi kurang optimal.

Proyek ini bertujuan untuk membangun sistem rekomendasi buku berbasis data yang mampu menyarankan judul-judul bacaan secara personal. Sistem ini akan memanfaatkan data historis pengguna seperti riwayat bacaan, genre favorit, dan rating, serta mempertimbangkan faktor tambahan seperti popularitas buku dan ulasan komunitas.

Dengan pendekatan ini, pengguna akan lebih mudah menemukan buku yang sesuai minat mereka, sementara penyedia layanan dapat meningkatkan keterlibatan dan kepuasan pengguna. Proyek ini menggabungkan pendekatan berbasis algoritma modern untuk menciptakan pengalaman membaca yang lebih personal, efisien, dan menyenangkan.

## Business Understanding

Di era digital yang semakin maju, akses terhadap buku menjadi sangat mudah melalui platform-platform digital seperti e-book, perpustakaan online, dan aplikasi baca. Namun, kemudahan ini juga menimbulkan permasalahan baru: banyaknya pilihan membuat pengguna kesulitan dalam memilih buku yang sesuai dengan minat dan kebutuhannya. Dalam konteks inilah, sistem rekomendasi buku menjadi solusi yang sangat relevan.

Sistem rekomendasi buku bertujuan untuk memberikan saran bacaan yang dipersonalisasi berdasarkan preferensi dan kebiasaan pengguna. Sistem ini bekerja dengan menganalisis berbagai faktor seperti riwayat bacaan pengguna, genre favorit, hingga penilaian (rating) yang pernah diberikan. Informasi ini kemudian diproses menggunakan algoritma tertentu agar dapat menghasilkan daftar rekomendasi buku yang relevan (Su & Khoshgoftaar, 2009).

Selain data eksplisit dari pengguna, sistem rekomendasi juga dapat mempertimbangkan aspek lain seperti popularitas buku, rating dari pengguna lain, dan rekomendasi komunitas. Pendekatan ini terbukti dapat meningkatkan akurasi rekomendasi serta memberikan nilai tambah berupa penemuan bacaan baru yang sebelumnya tidak diketahui oleh pengguna (Schafer et al., 2007).

Bagi pembaca, sistem ini membantu menemukan buku yang sesuai selera dan membuka kesempatan untuk mengeksplorasi buku baru. Sementara bagi penyedia layanan digital, sistem ini mampu meningkatkan keterlibatan pengguna, memperpanjang durasi penggunaan platform, serta memberikan wawasan yang lebih mendalam tentang preferensi pengguna (Hariri, Mobasher, & Burke, 2012). Dengan demikian, sistem rekomendasi buku tidak hanya meningkatkan pengalaman membaca pengguna, tetapi juga mendukung pengembangan layanan digital yang lebih adaptif dan efisien.

### Problem Statements
Beberapa masalah utama yang diidentifikasi adalah:
- Pengguna harus menelusuri ribuan judul tanpa bantuan sistem yang memahami preferensi mereka.
- Sistem pencarian dan kategori yang tersedia di sebagian besar platform buku digital masih bersifat umum dan statis.
- Kurangnya personalisasi menyebabkan pengguna kehilangan potensi untuk menemukan buku yang relevan atau menarik.

### Goals
Tujuan dari proyek ini adalah:

- Mengembangkan sistem rekomendasi buku yang mampu memberikan saran bacaan berdasarkan preferensi masing-masing pengguna.
- Meningkatkan efisiensi pengguna dalam menemukan buku yang sesuai dengan selera mereka.
- Meningkatkan pengalaman membaca dan kepuasan pengguna melalui rekomendasi yang akurat dan relevan.

### Solution Approach
Collaborative Filtering (Pilihan yang Digunakan)
Collaborative Filtering merekomendasikan buku berdasarkan kesamaan preferensi antara pengguna yang berbeda. Sistem ini menganalisis pola interaksi (misalnya: rating, ulasan, histori bacaan) dari banyak pengguna untuk menemukan korelasi antar preferensi.

    - Kelebihan: Mampu memberikan rekomendasi yang bersifat eksploratif, termasuk buku yang belum pernah dijelajahi pengguna.
    - Kekurangan: Rentan terhadap masalah cold start untuk pengguna atau buku baru.

## Data Understanding
Pada project kali ini akan digunakan dataset mengenai buku yang berasal dari platform `Kaggle` dengan judul ***Book Recommendation Dataset***. Didalam dataset ini terdapat 3 file csv yang akan digunakan yaitu `Users.csv`, `Books.csv`, & `Ratings.csv`. Link resource: [Book Recommendation Dataset](https://www.kaggle.com/datasets/arashnic/book-recommendation-dataset).

Proyek ini menggunakan tiga file utama dalam bentuk CSV: `Users.csv`, `Books.csv`, dan `Ratings.csv`. Berikut adalah penjelasan struktur kolom pada masing-masing file:

---

### 1. `Users.csv`
Menyimpan informasi dasar mengenai pengguna sistem.
| Kolom      | Tipe Data | Deskripsi |
|------------|-----------|-----------|
| `User-ID`  | integer   | ID unik untuk setiap pengguna |
| `Location` | object    | Lokasi pengguna |
| `Age`      | float   | Usia pengguna. Beberapa nilai mungkin kosong atau tidak valid. |

<br>
<image src='image/decs_users_dataset.png' width= 500/>
<br>

Terdapat 110762 missing values pada kolom `Age`.
---
### 2. `Books.csv`
Menyimpan metadata lengkap mengenai buku.
| Kolom                  | Tipe Data | Deskripsi |
|------------------------|-----------|-----------|
| `ISBN`                 | object    | Nomor unik internasional untuk identifikasi buku. Primary key. |
| `Book-Title`           | object    | Judul buku. |
| `Book-Author`          | object    | Nama penulis buku. |
| `Year-Of-Publication`  | object   | Tahun terbit buku. Validasi diperlukan untuk tahun yang tidak wajar. |
| `Publisher`            | object    | Nama penerbit. |
| `Image-URL-S`          | object    | URL gambar sampul ukuran kecil. |
| `Image-URL-M`          | object    | URL gambar sampul ukuran sedang. |
| `Image-URL-L`          | object    | URL gambar sampul ukuran besar. |

<br>
<image src='image/decs_books_dataset.png' width= 500/>
<br>

Terdapat 2-3 missing value pada kolom `Book-Author`, `Publisher`, & `Image-URL-L`.

---
### 3. `Ratings.csv`
Mencatat interaksi antara pengguna dan buku berupa rating.
| Kolom         | Tipe Data | Deskripsi |
|---------------|-----------|-----------|
| `User-ID`     | integer   | ID pengguna yang memberikan rating. Foreign key ke `Users.csv`. |
| `ISBN`        | object    | ISBN buku yang diberi rating. Foreign key ke `Books.csv`. |
| `Book-Rating` | integer   | Nilai rating dari pengguna untuk buku tersebut (rentang 0–10). Nilai `0` biasanya berarti tidak ada rating eksplisit. |

<br>
<image src='image/decs_ratings_dataset.png' width= 500/>
<br>

Data file ini tidak terdapat null value
---
📌 Dataset ini bersifat relasional. Kunci utama (`User-ID`, `ISBN`) menjadi penghubung antara file `Users.csv`, `Books.csv`, dan `Ratings.csv`. Data ini digunakan sebagai dasar dalam membangun sistem rekomendasi

<br>
<image src='image/top_read_books.png' width= 500/>
<br>



## Data Preparation

Tahapan data preparation sangat penting untuk memastikan kualitas data sebelum digunakan dalam pelatihan model sistem rekomendasi. Di bawah ini adalah tahapan yang dilakukan, lengkap dengan penjelasan dan alasan penerapannya, sesuai dengan urutan yang ada di notebook:

### 1. Merge Dataframe
Menggabungkan ketiga dataset (`Users.csv`, `Books.csv`, dan `Ratings.csv`) menjadi satu DataFrame utama berdasarkan relasi `User-ID` dan `ISBN`. Bertujuan agar informasi lengkap mengenai pengguna, buku, dan rating tersedia dalam satu tabel gabungan sehingga memudahkan proses analisis dan pemodelan.

### 2. Drop Missing Values
Menghapus baris data yang memiliki nilai kosong (missing values) pada kolom penting seperti `Age`, `Book-Title`, atau `Book-Rating`.Data yang hilang dapat menyebabkan bias atau error dalam model. Dengan menghapus missing values, data yang digunakan menjadi lebih bersih dan valid.

### 3. Drop Invalid Values
Pada kolom `Book-Rating`, terdapat nilai 0 yang jumlahnya sangat besar. Nilai tersebut harus dihapus karena beberapa alasan:  
- Merupakan **bukan preferensi nyata** dari pengguna (biasanya menunjukkan bahwa pengguna tidak memberikan rating).  
- **Tidak berguna** dalam sistem rekomendasi berbasis rating.
- Jumlahnya yang sangat dominan dapat **menyebabkan bias** dalam pelatihan model.

## 4. Encoding Data

Melakukan encoding pada kolom `ISBN` dan `User-ID` ke bentuk numerik agar bisa diproses oleh algoritma machine learning.


## 5. Randomising the Dataset

Melakukan pengacakan (shuffling) pada dataset agar distribusi data tidak berurutan berdasarkan user atau buku tertentu. Mencegah bias karena urutan data, serta memastikan bahwa model belajar dari berbagai kombinasi data secara acak.


## 6. Splitting Data Train & Test

Memisahkan dataset menjadi dua bagian: data pelatihan (training set) dan data pengujian (testing set), biasanya dengan rasio 80:20.Memastikan bahwa model dapat diuji secara objektif menggunakan data yang belum pernah dilihat sebelumnya, untuk mengevaluasi performa model secara valid.

---

Dengan melakukan tahapan-tahapan di atas, data menjadi lebih **terstruktur, bersih, dan siap digunakan untuk membangun sistem rekomendasi buku** yang andal dan akurat.

## 🧠 Modeling

Pada tahap ini dibangun model sistem rekomendasi menggunakan metode **Collaborative Filtering**, yang merekomendasikan buku berdasarkan kesamaan preferensi antar pengguna.

### Collaborative Filtering

**Collaborative Filtering** bekerja dengan menganalisis interaksi pengguna (seperti rating atau histori bacaan) untuk menemukan pengguna lain dengan selera serupa, lalu merekomendasikan buku yang disukai oleh pengguna-pengguna tersebut.

#### Kelebihan:
- Mampu merekomendasikan buku yang belum pernah dijelajahi pengguna.
- Tidak memerlukan informasi konten buku (judul, penulis, genre, dll).

#### Kekurangan:
- **Cold Start**: Sulit memberikan rekomendasi bagi pengguna atau buku baru.
- Tergantung pada jumlah data interaksi pengguna.

### Output Model
Contoh dari rekomendasi buku yang dihasilkan dari sistem rekomendasi ini adalah sebagai berikut:

<br>
<image src='image/output.png' width= 500/>
<br>


## Evaluasi Model

Untuk mengukur performa sistem rekomendasi, digunakan metrik **Root Mean Squared Error (RMSE)**, yang mengukur seberapa jauh prediksi rating buku menyimpang dari rating aktual yang diberikan oleh pengguna.

### RMSE (Root Mean Squared Error)

**RMSE** menghitung akar dari rata-rata kuadrat selisih antara nilai prediksi dan nilai aktual. Semakin kecil nilai RMSE, semakin baik performa model.

Rumus RMSE:
<br>
<image src='image/rumus_rmse.png' width= 500/>
<br>

### Hasil Evaluasi

<br>
<image src='image/visual_rmse.png' width= 500/>
<image src='image/visual_loss.png' width= 500/>
<br>

#### Training vs Validation Loss
Grafik *Training and Validation Loss* menunjukkan bahwa nilai *training loss* secara konsisten menurun selama proses pelatihan, mengindikasikan bahwa model berhasil mempelajari pola dari data pelatihan. *Validation loss* juga menurun dan stabil setelah beberapa epoch, yang menunjukkan bahwa model tidak mengalami overfitting secara signifikan dan memiliki kemampuan generalisasi yang baik terhadap data yang belum pernah dilihat.

#### Training vs Validation RMSE
Pada grafik *Training and Validation RMSE*, terlihat bahwa nilai *training RMSE* juga terus menurun, sementara *validation RMSE* menurun di awal dan stabil pada nilai yang cukup rendah. Gap antara RMSE pada data pelatihan dan validasi cukup kecil, menandakan performa model yang seimbang dan akurat baik pada data pelatihan maupun validasi. Hal ini memperkuat kesimpulan bahwa model mampu menghasilkan prediksi dengan kesalahan yang rendah dan dapat diandalkan dalam konteks sistem rekomendasi buku.

## 📚 Referensi

- Hariri, N., Mobasher, B., & Burke, R. (2012). *Context-aware recommendation based on review mining*. Proceedings of the Sixth ACM Conference on Recommender Systems.  
  [https://dl.acm.org/doi/10.1145/2365952.2365982](https://dl.acm.org/doi/10.1145/2365952.2365982)

- Schafer, J. B., Frankowski, D., Herlocker, J., & Sen, S. (2007). *Collaborative filtering recommender systems*. In **The Adaptive Web** (pp. 291–324). Springer.  
  [https://link.springer.com/chapter/10.1007/978-3-540-72079-9_9](https://link.springer.com/chapter/10.1007/978-3-540-72079-9_9)

- Su, X., & Khoshgoftaar, T. M. (2009). *A survey of collaborative filtering techniques*. Advances in Artificial Intelligence, 2009.  
  [https://doi.org/10.1155/2009/421425](https://doi.org/10.1155/2009/421425)

