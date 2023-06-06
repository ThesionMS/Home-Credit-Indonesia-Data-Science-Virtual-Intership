# Home-Credit-Indonesia-Data-Science-Virtual-Intership

## Problem Researsch

- Home Credit saat ini sedang menerapkan berbagai metode statistik dan Machine Learning untuk mengoptimalkan prediksi skor kredit. Tujuan utamanya adalah memastikan bahwa pelanggan yang mampu melunasi pinjaman tidak ditolak saat mengajukan pinjaman, sementara pinjaman yang diberikan disesuaikan dengan jumlah utama (principal), jangka waktu pelunasan (maturity), dan jadwal pembayaran (repayment calendar) yang dapat memotivasi pelanggan untuk mencapai keberhasilan keuangan.
- Dataset yang digunakan adalah application_train.csv
- Dua Model Machine Learning yang digunakan adalah Logistic Regression, XGBoost Classifier.

## Data Pre-Processing

- Melakukan pemeriksaan missing value dan menghapus variabel yang memiliki missing value.
- Memeriksa adanya data duplikat dan tidak menemukan duplikat.
- Mengecek ejaan kata dan menemukan kesalahan pada kolom CODE_GENDER dan NAME_INCOME_TYPE, yang kemudian dihapus.
- Melakukan feature engineering dengan menambahkan kolom AGE yang berisi umur klien dalam tahun (dalam format integer).
- Mengubah data kategorikal menjadi biner.
- Membagi dataset menjadi 70% data training dan 30% data testing.
- Melakukan oversampling (SMOTE) untuk menyeimbangkan data.

## Data Visualization and Business Insight

## Data Visualization and Business Insight

## Machine Learning Implementation and Evaluation

Ada 2 Model Machine Learning menggunakan hyperparameter tuning
1. Logistic Regression
2. XGBoost Classifier 

## Business Recommendation



