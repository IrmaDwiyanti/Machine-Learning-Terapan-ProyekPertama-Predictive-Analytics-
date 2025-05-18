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

![image](https://github.com/user-attachments/assets/3e27e13d-2eac-4418-a19a-05974d602c42)


Insight:

- Lebih banyak siswa yang tidak berprestasi dibandingkan yang berprestasi.

- Ini menunjukkan bahwa mayoritas siswa dalam data ini memiliki capaian prestasi yang kurang.

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

![image](https://github.com/user-attachments/assets/924e76b8-83e9-4107-ba09-f5a7a7f5e099)

Heatmap di atas menggambarkan korelasi antara variabel-variabel numerik dalam dataset. Warna yang lebih terang (mendekati kuning) menunjukkan korelasi positif yang kuat, sedangkan warna yang lebih gelap (mendekati ungu) menunjukkan korelasi negatif yang kuat. Dari visualisasi ini, terlihat bahwa math score, reading score, dan writing score memiliki korelasi positif yang sangat tinggi satu sama lain, mengindikasikan bahwa siswa yang mendapatkan skor tinggi di salah satu mata pelajaran cenderung mendapatkan skor tinggi di mata pelajaran lainnya. Variabel lain seperti gender, race/ethnicity, parental level of education, lunch, dan test preparation course, setelah di-encode, menunjukkan korelasi yang relatif lemah dengan skor-skor tersebut.

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

-   **Model**: `RandomForestClassifier`
-   **Target**: Kategori prestasi siswa (berprestasi/tidak berprestasi) yang ditentukan berdasarkan rata-rata skor.
-   **Penjelasan Algoritma**:
    -   Random Forest adalah algoritma ensemble yang terdiri dari banyak Decision Tree. Setiap tree memberikan prediksi, dan Random Forest menggabungkan prediksi-prediksi ini (melalui voting untuk klasifikasi) untuk membuat prediksi akhir.
    -   Prinsip dasar dari bagging (Bootstrap Aggregating) digunakan, di mana setiap tree dilatih pada subset data yang di-bootstrap (diambil sampel dengan pengembalian). Ini meningkatkan variasi antar tree dan mengurangi overfitting.
    -   Struktur pohon keputusan melibatkan serangkaian percabangan berdasarkan fitur-fitur input, yang akhirnya mengarah pada prediksi kelas.
-   **Parameter Utama dan Alasan Pemilihan**:
    -   `n_estimators` (100): Jumlah tree dalam forest. 100 tree dipilih sebagai trade-off antara performa dan waktu komputasi. Semakin banyak tree, semakin stabil prediksi, tetapi dengan biaya komputasi yang lebih tinggi.
    -   `max_depth` (10): Kedalaman maksimum setiap tree. Membatasi kedalaman tree membantu mencegah overfitting, di mana model menjadi terlalu kompleks dan menghafal data training. Nilai 10 dipilih setelah eksperimentasi untuk memberikan performa yang baik tanpa overfitting.
    -   `random_state` (42): Seed untuk random generator. Digunakan untuk memastikan hasil yang reproducible.
-   **Hasil**:
    -   Akurasi klasifikasi: 59.00%
    -   Detail performa dapat dilihat pada *Confusion Matrix* berikut:
      
        ![image](https://github.com/user-attachments/assets/5cb06bb4-87d4-4ebc-a2af-7adbf6d19540)

        ![image](https://github.com/user-attachments/assets/2b7d829a-a3e4-40b2-8298-d970deae82d7)

        True Negative (TN): 69 (aktual 0, diprediksi 0)

        False Positive (FP): 41 (aktual 0, diprediksi 1)

        False Negative (FN): 41 (aktual 1, diprediksi 0)

        True Positive (TP): 49 (aktual 1, diprediksi 1)

        Model ini memiliki akurasi sedang, namun terdapat banyak kesalahan klasifikasi (FP & FN = 41), artinya model sering salah dalam membedakan antara dua kelas. Perlu          dievaluasi dengan metrik seperti precision, recall, atau F1-score jika ingin tahu lebih detail.

-   **Kelebihan**:
    -   Robust terhadap overfitting karena menggunakan ensemble.
    -   Dapat menangani fitur dengan berbagai tipe data.
-   **Kekurangan**:
    -   Kurang interpretatif dibandingkan dengan Decision Tree tunggal.
    -   Membutuhkan waktu komputasi yang lebih lama dibandingkan model linier.

### Problem 2: Prediksi Skor Matematika

-   **Model**: `RandomForestRegressor`
-   **Target**: `math score`
-   **Penjelasan Algoritma**:
    -   Random Forest untuk regresi bekerja dengan cara yang sama seperti klasifikasi, tetapi prediksi yang dihasilkan adalah rata-rata dari prediksi setiap tree.
-   **Parameter Utama dan Alasan Pemilihan**:
    -   Parameter yang digunakan sama dengan model klasifikasi (`n_estimators`, `max_depth`, `random_state`) dengan alasan yang sama.
-   **Hasil**:
    - RMSE (Math Score): 4.47
    - R² Score (Math Score): 0.92

### Problem 3: Estimasi Total Skor dari Fitur Demografis

-   **Model**: `LinearRegression`
-   **Input**: Fitur demografis + `test preparation course`
-   **Target**: `total_score`
-   **Penjelasan Algoritma**:
    -   Linear Regression mencari hubungan linier antara fitur-fitur input dan target. Model ini mencoba menemukan garis (atau hyperplane dalam dimensi yang lebih tinggi) yang paling cocok dengan data, meminimalkan jumlah kuadrat error antara prediksi dan nilai sebenarnya.
    -   Asumsi utama Linear Regression adalah hubungan linier antara fitur dan target, independensi error, homoskedastisitas (variansi error konstan), dan normalitas error.
-   **Parameter Utama dan Alasan Pemilihan**:
    -   Dalam implementasi sederhana ini, kita tidak menggunakan regularisasi. Regularisasi (seperti Ridge atau Lasso) dapat ditambahkan untuk mencegah overfitting, tetapi tidak diperlukan di sini karena jumlah fitur relatif kecil.
-   **Hasil**:
    -   RMSE: 41.07
    -   R²: 0.13
-   **Kelebihan**:
    -   Interpretatif (koefisien memberikan informasi tentang hubungan antara fitur dan target).
    -   Komputasi efisien.
-   **Kekurangan**:
    -   Hanya dapat menangkap hubungan linier.
    -   Sensitif terhadap outlier.

---


## 📏 Evaluation

## 📊 Perhitungan Akurasi (Accuracy) - Klasifikasi Prestasi

**Accuracy** = 

![image](https://github.com/user-attachments/assets/8d1fa016-ccec-424d-9e38-bf85054bbf42)


### 📄 Contoh dari Confusion Matrix:

|                 | Predicted 0 | Predicted 1 |
|-----------------|-------------|-------------|
| **Actual 0**    | TN = 69     | FP = 41     |
| **Actual 1**    | FN = 41     | TP = 49     |

### 📌 Perhitungan:
Total sampel = 69 + 41 + 41 + 49 = **200**

Misalnya hasil klasifikasi dari confusion matrix adalah:

- True Positives (TP): 49  
- True Negatives (TN): 69  
- False Positives (FP): 41  
- False Negatives (FN): 41  

Maka:

**Accuracy** = (49 + 69) / (49 + 69 + 41 + 41)  
**Accuracy** = 118 / 200  
**Accuracy** = 0.59 → 59%

### 💡 Interpretasi:
Model berhasil mengklasifikasikan dengan benar sebanyak **59%** dari total data yang tersedia.
"""
    -   Alasan Pemilihan:
        -   Accuracy memberikan gambaran keseluruhan performa model klasifikasi.
        -   Confusion Matrix memberikan detail lebih lanjut tentang performa per kelas.
        -   Classification Report memberikan metrik tambahan yang berguna untuk memahami trade-off antara Precision dan Recall.

# RMSE (Root Mean Squared Error) - Regresi

## Rumus RMSE

**RMSE** = 

![image](https://github.com/user-attachments/assets/a335586b-d926-4b68-bfdf-dcd0e39f9890)


## Contoh Perhitungan RMSE

Misalnya nilai sebenarnya (y\_true):

```
[100, 200, 300]
```

Prediksi (y\_pred):

```
[105, 195, 310]
```

Langkah-langkah:

1. Hitung error kuadrat:

   * (100 - 105)^2 = 25
   * (200 - 195)^2 = 25
   * (300 - 310)^2 = 100

2. Hitung rata-rata error kuadrat:

   * (25 + 25 + 100) / 3 = 50

3. Ambil akar dari hasil rata-rata:

   * RMSE = sqrt(50) ≈ **7.07**

## Interpretasi Hasil

Dari output model saya:

* **RMSE Math Score** = **4.47** → Error kecil, berarti model cukup baik dalam memprediksi nilai matematika.
* **RMSE Total Score** = **41.07** → Error besar, berarti model kurang baik dalam memprediksi nilai total.

Semakin kecil nilai RMSE, semakin baik performa model regresi dalam memprediksi nilai aktual.


# R² Score (Koefisien Determinasi) - Regresi

## Rumus

![image](https://github.com/user-attachments/assets/513e43a8-a2e4-43e0-9fc2-89c7fcc3047d)

* $y_i$ = Nilai aktual
* $\hat{y}_i$ = Nilai prediksi
* $\bar{y}$ = Rata-rata nilai aktual

## Contoh Perhitungan

Misal:

* `y_true` = \[100, 200, 300] → $\bar{y} = 200$
* `y_pred` = \[105, 195, 310]

### Langkah:

1. **Sum of Squared Residuals (SSR):**

$$
(100 - 105)^2 + (200 - 195)^2 + (300 - 310)^2 = 25 + 25 + 100 = 150
$$

2. **Total Sum of Squares (SST):**

$$
(100 - 200)^2 + (200 - 200)^2 + (300 - 200)^2 = 10000 + 0 + 10000 = 20000
$$

3. **Hitung R²:**

$$
R^2 = 1 - \frac{150}{20000} = 1 - 0.0075 = 0.9925
$$

> **Interpretasi:** Model menjelaskan 99.25% variasi data (sangat baik).

---

## Dari Output Model ini:

* **R² Math Score = 0.92** → 92% variasi dijelaskan oleh model (sangat baik)
* **R² Total Score = 0.13** → Hanya 13% variasi dijelaskan (buruk)

---


## 📝 Penutup

Proyek ini menunjukkan bahwa machine learning mampu membantu dunia pendidikan dalam mengklasifikasikan dan memprediksi prestasi akademik siswa secara otomatis, cepat, dan akurat.

---

## Referensi

[1] G. D. Kuh, J. Kinzie, J. H. Schuh, E. J. Whitt, Student Success in College: Creating Conditions That Matter, 1st ed., San Francisco, CA, USA: Jossey-Bass, 2005.

[2] A. Al-Barrak and M. Al-Razgan, "Predicting Students Final GPA Using Decision Trees: A Case Study," International Journal of Information and Education Technology, vol. 6, no. 7, pp. 528-533, 2016.
