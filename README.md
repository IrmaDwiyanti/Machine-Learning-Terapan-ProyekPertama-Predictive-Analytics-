# 🎓 Laporan Proyek Machine Learning - Irma Dwiyanti

## 🌐 Domain Proyek

Pendidikan merupakan aspek fundamental dalam pengembangan kualitas sumber daya manusia suatu bangsa. Keberhasilan sistem pendidikan tidak hanya diukur melalui infrastruktur atau kurikulum, tetapi juga dari kemampuan dalam melakukan evaluasi prestasi belajar siswa secara adil dan objektif. Penilaian prestasi siswa yang berbasis data menjadi semakin penting seiring dengan meningkatnya kebutuhan akan pengambilan keputusan berbasis bukti (evidence-based decision making). Dengan pendekatan ini, pendidik dan pembuat kebijakan dapat merancang intervensi yang tepat sasaran untuk meningkatkan kualitas pembelajaran [1].

Dalam konteks ini, pemanfaatan machine learning memungkinkan pengembangan sistem prediktif berbasis data akademik dan demografis siswa engan data yang tersedia, seperti jenis kelamin, latar belakang pendidikan orang tua, serta nilai ujian, kita dapat membangun model klasifikasi untuk menentukan status prestasi siswa dan model regresi untuk memperkirakan skor akademik secara kuantitatif. Implementasi teknologi ini telah terbukti meningkatkan akurasi penilaian dan mempercepat proses pengambilan keputusan dalam pendidikan [2]. 
kita dapat membangun sistem machine learning yang mampu:

1. Mengklasifikasikan apakah seorang siswa tergolong **berprestasi** atau tidak.
2. Memprediksi nilai **matematika** siswa.
3. Mengestimasi **total skor akademik** siswa berdasarkan fitur demografis.

Masalah ini penting diselesaikan karena dapat membantu sekolah dalam melakukan **intervensi lebih dini**, menyusun strategi pengajaran yang tepat, serta memberikan perhatian lebih kepada siswa yang membutuhkan dukungan akademik.

---

## 🧠 Business Understanding

### Problem Statements:
1. Bagaimana cara mengklasifikasikan siswa apakah mereka berprestasi atau tidak berdasarkan data demografi dan akademik?
2. Bagaimana cara memprediksi skor matematika siswa dari atribut lain?
3. Bagaimana cara mengestimasi total nilai akademik hanya dari faktor demografis?

### Goals:
- Membangun model klasifikasi prestasi siswa (berprestasi atau tidak).
- Membangun model regresi untuk prediksi skor matematika.
- Membangun model regresi untuk estimasi total skor dari fitur demografis.

### Solution Statement:
- **Solusi 1**: Menggunakan **Random Forest Classifier** untuk klasifikasi prestasi siswa.
- **Solusi 2**: Menggunakan **Random Forest Regressor** untuk prediksi skor matematika.
- **Solusi 3**: Menggunakan **Linear Regression** untuk estimasi total skor dari data demografi.
- Setiap solusi dievaluasi menggunakan metrik akurasi (klasifikasi) serta RMSE & R² (regresi).

---

## 📊 Data Understanding

- Jumlah data: **1000 baris**, **8 kolom**.
- Sumber data: [Students Performance Dataset - Kaggle](https://www.kaggle.com/datasets/spscientist/students-performance-in-exams)
- Kolom data:
  - `gender` (L/P)
  - `race/ethnicity` (kelompok etnis siswa)
  - `parental level of education`
  - `lunch` (jenis makanan siang: standard/free)
  - `test preparation course` (complete/none)
  - `math score`
  - `reading score`
  - `writing score`
 
## Informasi Dataset sebagai berikut

![image](https://github.com/user-attachments/assets/d91d09f2-fadb-4618-9daf-ae892187e8f0)


## 📋 Deskripsi Variabel

| Nama Variabel                 | Tipe Data | Keterangan                                                                 | Kode/Nilai                                                                 |
|-------------------------------|-----------|----------------------------------------------------------------------------|----------------------------------------------------------------------------|
| **gender**                    | Kategorik | Jenis kelamin siswa                                                        | `0`: Laki-laki, `1`: Perempuan                                             |
| **race/ethnicity**            | Kategorik | Kelompok etnis siswa                                                       | `0`: Group A, `1`: Group B, `2`: Group C, `3`: Group D, `4`: Group E       |
| **parental level of education**| Kategorik | Tingkat pendidikan orang tua                                               | `0`: Tanpa pendidikan formal, `1`: SD, `2`: SMP, `3`: SMA, `4`: S1, `5`: S2|
| **lunch**                     | Kategorik | Jenis makan siang siswa                                                    | `0`: Free/reduced, `1`: Standard                                           |
| **test preparation course**   | Kategorik | Status persiapan ujian                                                     | `0`: Tidak ikut, `1`: Selesai                                              |
| **math score**                | Numerik   | Nilai ujian matematika (0-100)                                             | -                                                                          |
| **reading score**             | Numerik   | Nilai ujian membaca (0-100)                                                | -                                                                          |
| **writing score**             | Numerik   | Nilai ujian menulis (0-100)                                                | -                                                                          |
| **average_score**             | Numerik   | Rata-rata nilai (matematika, membaca, menulis)                             | Dihitung otomatis                                                          |
| **total_score**               | Numerik   | Total nilai (matematika + membaca + menulis)                               | Dihitung otomatis                                                          |
| **prestasi**                  | Binary    | Status prestasi siswa                                                      | `1`: Berprestasi (average_score ≥ 70), `0`: Tidak berprestasi               |

### Exploratory Data Analysis:
- Tidak ditemukan missing values dan duplikasi.
- Distribusi nilai matematika divisualisasikan dengan histogram.
- Korelasi skor menunjukkan keterkaitan tinggi antar mata pelajaran.

### Distribusi Prestasi Siswa

![image](https://github.com/user-attachments/assets/fa75fc34-9458-4642-9c2d-05426a350b20)

Insight:

- Lebih banyak siswa yang berprestasi dibandingkan yang tidak.

- Ini menunjukkan bahwa mayoritas siswa dalam data ini memiliki capaian prestasi yang diakui.

### Distribusi Math Score

![image](https://github.com/user-attachments/assets/9063a2e4-77d1-4ca7-a9a5-17f81aff4172)

Insight:

- Distribusi nilai matematika cenderung normal tapi sedikit condong ke kiri (negatively skewed).

- Sebagian besar siswa memiliki nilai di kisaran 60–80, menunjukkan performa yang cukup baik di pelajaran matematika.

- Ada sebagian kecil siswa dengan nilai sangat rendah maupun sangat tinggi.

### Distribusi Reading Score

![image](https://github.com/user-attachments/assets/11a4dcfa-52b4-4ad3-b193-d65dfed41ec3)

Insight:

- Outlier rendah: Nilai di bawah 40 mungkin perlu diteliti lebih lanjut (kesalahan input atau siswa dengan kesulitan khusus).

- Kecenderungan positif: Sebagian besar siswa memiliki nilai membaca di atas rata-rata (didominasi nilai 60+).

### Distribusi Writing Score

![image](https://github.com/user-attachments/assets/d0676401-a6ef-43b8-b1c0-467b341f6cfc)

- Outlier rendah menunjukkan kemungkinan siswa dengan kesulitan menulis.

- Kinerja lebih baik dibanding reading score (puncak lebih tinggi dan skew lebih kecil).

- ### Distribusi Average Score

![image](https://github.com/user-attachments/assets/4d4bdc9c-feee-49f5-808d-6c8656b8ad6d)

- Ambang prestasi (70): Sebagian besar siswa berada di sekitar batas ini.

- Konsistensi: Distribusi yang simetris menunjukkan keseimbangan antara mata pelajaran.

- Analisis korelasi dengan variabel seperti parental education atau lunch.

## heatmap korelasi fitur numerik

![image](https://github.com/user-attachments/assets/cd1797fc-0975-4f1c-b2f4-cb2f828d28fb)

Heatmap korelasi menunjukkan hubungan yang sangat kuat antara nilai matematika, membaca, dan menulis (korelasi >0.8), dengan korelasi tertinggi terjadi antara reading score dan writing score (0.95), sementara average_score memiliki korelasi hampir sempurna dengan ketiga nilai ujian (0.92-0.97) karena merupakan rata-ratanya. Variabel prestasi yang dikodekan sebagai binary (0/1) menunjukkan korelasi negatif dengan nilai-nilai ujian, namun sebenarnya memiliki hubungan positif yang kuat (ditunjukkan oleh nilai absolut >0.7), mengindikasikan bahwa siswa dengan nilai tinggi cenderung termasuk dalam kategori berprestasi.



---

## 🧹 Data Preparation

### Teknik yang digunakan:
1. **Feature Engineering**:
   - `average_score` = rata-rata nilai dari 3 mata pelajaran.
   - `total_score` = jumlah dari ketiganya.
   - `prestasi` = 1 jika rata-rata ≥ 70, else 0.

2. **Encoding**:
   - Label Encoding pada fitur kategorikal seperti `gender`, `lunch`, dll.

### Alasan:
- Feature engineering membantu membentuk target variabel baru (`prestasi`, `total_score`).
- Encoding diperlukan agar model machine learning dapat memproses fitur kategorikal.

---

## 🤖 Modeling

### Problem 1: Klasifikasi Prestasi Siswa
- **Model**: `RandomForestClassifier`
- **Input**: Semua fitur kecuali skor & label target.
- **Output**: Label `prestasi` (1 = berprestasi, 0 = tidak)
- **Hasil**: Akurasi: **~0.90**, Confusion Matrix digunakan sebagai visualisasi evaluasi.
- **Kelebihan**: Robust terhadap noise, tidak memerlukan scaling.
- **Kekurangan**: Kurang interpretatif, model kompleks.

### Problem 2: Prediksi Skor Matematika
- **Model**: `RandomForestRegressor`
- **Input**: Semua fitur kecuali `math score` dan turunan label lain.
- **Target**: `math score`
- **Hasil**:
  - RMSE: ~**5.2**
  - R²: ~**0.88**

### Problem 3: Estimasi Total Skor dari Fitur Demografis
- **Model**: `LinearRegression`
- **Input**: Fitur demografis + `test preparation course`
- **Target**: `total_score`
- **Hasil**:
  - RMSE: ~**13.9**
  - R²: ~**0.65**

---

## 📏 Evaluation

### Metrik Evaluasi:

1. **Klasifikasi:**
   - **Accuracy** = (TP + TN) / Total
   - Cocok digunakan karena dataset seimbang antara prestasi dan tidak.
   - Juga digunakan **Confusion Matrix** untuk detail performa.

2. **Regresi:**
   - **RMSE** = √(MSE) → Mengukur deviasi rata-rata prediksi dari nilai sebenarnya.
   - **R² Score** = Prosentase variansi target yang dapat dijelaskan oleh model.

### Hasil evaluasi menunjukkan:
- Model klasifikasi sangat baik dengan akurasi tinggi.
- Model regresi matematika menunjukkan performa prediksi yang sangat baik.
- Model estimasi total skor cukup baik meskipun hanya menggunakan data demografis.

---


## 📝 Penutup

Proyek ini menunjukkan bahwa machine learning mampu membantu dunia pendidikan dalam mengklasifikasikan dan memprediksi prestasi akademik siswa secara otomatis, cepat, dan akurat.

---

