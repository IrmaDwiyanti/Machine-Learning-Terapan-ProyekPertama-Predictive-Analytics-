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

-   **Model**: `RandomForestClassifier`
-   **Input**: Fitur demografis siswa, tingkat pendidikan orang tua, jenis makan siang, dan apakah mengikuti kursus persiapan tes.
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
    -   Akurasi: ~0.68
    -   Detail performa dapat dilihat pada *Confusion Matrix* dan *Classification Report* di notebook.
-   **Kelebihan**:
    -   Robust terhadap overfitting karena menggunakan ensemble.
    -   Dapat menangani fitur dengan berbagai tipe data.
-   **Kekurangan**:
    -   Kurang interpretatif dibandingkan dengan Decision Tree tunggal.
    -   Membutuhkan waktu komputasi yang lebih lama dibandingkan model linier.

### Problem 2: Prediksi Skor Matematika

-   **Model**: `RandomForestRegressor`
-   **Input**: Semua fitur kecuali `math score` dan turunan label lain.
-   **Target**: `math score`
-   **Penjelasan Algoritma**:
    -   Random Forest untuk regresi bekerja dengan cara yang sama seperti klasifikasi, tetapi prediksi yang dihasilkan adalah rata-rata dari prediksi setiap tree.
-   **Parameter Utama dan Alasan Pemilihan**:
    -   Parameter yang digunakan sama dengan model klasifikasi (`n_estimators`, `max_depth`, `random_state`) dengan alasan yang sama.
-   **Hasil**:
    -   RMSE: ~20.88
    -   R²: ~0.27

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
    -   RMSE: ~41.07
    -   R²: ~0.13
-   **Kelebihan**:
    -   Interpretatif (koefisien memberikan informasi tentang hubungan antara fitur dan target).
    -   Komputasi efisien.
-   **Kekurangan**:
    -   Hanya dapat menangkap hubungan linier.
    -   Sensitif terhadap outlier.

---


## 📏 Evaluation

### Metrik Evaluasi:

1.  **Klasifikasi:**
    -   **Accuracy**: Mengukur proporsi prediksi yang benar dari total prediksi.
        -   Rumus:  
            ```latex
            \text{Accuracy} = \frac{\text{Jumlah prediksi benar}}{\text{Total jumlah prediksi}}
            ```
        -   Contoh: Jika model memprediksi 80 dari 100 sampel dengan benar, akurasinya adalah 0.8 atau 80%.
    -   **Confusion Matrix**: Tabel yang merangkum hasil prediksi klasifikasi.
        -   Menunjukkan jumlah True Positive (TP), True Negative (TN), False Positive (FP), dan False Negative (FN).
        -   Penting untuk memahami jenis kesalahan yang dibuat oleh model.
    -   **Classification Report**: Menyediakan metrik seperti Precision, Recall, dan F1-score selain Accuracy.
        -   **Precision**: Proporsi prediksi positif yang benar.
            -   Rumus:
                ```latex
                \text{Precision} = \frac{TP}{TP + FP}
                ```
        -   **Recall**: Proporsi aktual positif yang teridentifikasi dengan benar.
            -   Rumus:
                ```latex
                \text{Recall} = \frac{TP}{TP + FN}
                ```
        -   **F1-score**: Rata-rata harmonik dari Precision dan Recall.
            -   Rumus:
                ```latex
                \text{F1-score} = 2 \times \frac{\text{Precision} \times \text{Recall}}{\text{Precision} + \text{Recall}}
                ```
    -   Alasan Pemilihan:
        -   Accuracy memberikan gambaran keseluruhan performa model klasifikasi.
        -   Confusion Matrix memberikan detail lebih lanjut tentang performa per kelas.
        -   Classification Report memberikan metrik tambahan yang berguna untuk memahami trade-off antara Precision dan Recall.

2.  **Regresi:**
    -   **Root Mean Squared Error (RMSE)**: Mengukur rata-rata besarnya error antara prediksi dan nilai aktual.
        -   Rumus:
            ```latex
            \text{RMSE} = \sqrt{\frac{1}{n} \sum_{i=1}^{n} (y_i - \hat{y}_i)^2}
            ```
            -   di mana \( y_i \) adalah nilai aktual, \( \hat{y}_i \) adalah nilai prediksi, dan \( n \) adalah jumlah data.
        -   Interpretasi: RMSE yang lebih rendah menunjukkan model yang lebih baik.
    -   **R-squared (R²)**: Mengukur proporsi variansi dalam variabel dependen yang dapat diprediksi dari variabel independen.
        -   Rumus:
            ```latex
            R^2 = 1 - \frac{\sum_{i=1}^{n} (y_i - \hat{y}_i)^2}{\sum_{i=1}^{n} (y_i - \bar{y})^2}
            ```
            -   di mana \( y_i \) adalah nilai aktual, \( \hat{y}_i \) adalah nilai prediksi, \( \bar{y} \) adalah rata-rata nilai aktual, dan \( n \) adalah jumlah data.
        -   Interpretasi: R² berkisar antara 0 dan 1. R² yang lebih tinggi menunjukkan model yang lebih baik dalam menjelaskan variansi data.

### Hasil Evaluasi:

-   **Klasifikasi Prestasi Siswa**: Model Random Forest mencapai akurasi sekitar 68%. Confusion Matrix dan Classification Report memberikan detail performa per kelas.
-   **Prediksi Skor Matematika**: Model Random Forest menghasilkan RMSE sekitar 20.88 dan R² sekitar 0.27. Ini menunjukkan bahwa model memiliki error rata-rata sekitar 20.88 poin dalam memprediksi skor matematika dan hanya menjelaskan sebagian kecil variansi dalam skor matematika.
-   **Estimasi Total Skor**: Model Linear Regression menghasilkan RMSE sekitar 41.07 dan R² sekitar 0.13. Ini menunjukkan bahwa model memiliki error rata-rata yang cukup tinggi dalam memprediksi total skor dan hanya menjelaskan sebagian kecil variansi dalam total skor.

---
---


## 📝 Penutup

Proyek ini menunjukkan bahwa machine learning mampu membantu dunia pendidikan dalam mengklasifikasikan dan memprediksi prestasi akademik siswa secara otomatis, cepat, dan akurat.

---

## Referensi

[1] G. D. Kuh, J. Kinzie, J. H. Schuh, E. J. Whitt, Student Success in College: Creating Conditions That Matter, 1st ed., San Francisco, CA, USA: Jossey-Bass, 2005.

[2] A. Al-Barrak and M. Al-Razgan, "Predicting Students Final GPA Using Decision Trees: A Case Study," International Journal of Information and Education Technology, vol. 6, no. 7, pp. 528-533, 2016.
