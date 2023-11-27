
# Data Understanding
## Latar Belakang

- Home Credit saat ini sedang menerapkan berbagai metode statistik dan Machine Learning untuk mengoptimalkan prediksi skor kredit. Tujuan utamanya adalah memastikan bahwa pelanggan yang mampu melunasi pinjaman tidak ditolak saat mengajukan pinjaman, sementara pinjaman yang diberikan disesuaikan dengan jumlah utama (principal), jangka waktu pelunasan (maturity), dan jadwal pembayaran (repayment calendar) yang dapat memotivasi pelanggan untuk mencapai keberhasilan keuangan.
- Dataset yang digunakan adalah application_train.csv 
- Dua Model Machine Learning yang digunakan adalah Logistic Regression, XGBoost Classifier.
## Goal:
Tujuan utama adalah mengurangi jumlah klien yang ditolak oleh kesalahan, padahal sebenarnya mereka memiliki kemampuan untuk membayar kembali.
## Objective:
Membangun model prediktif yang dapat mengidentifikasi klien potensial yang dapat membayar kembali pinjaman, serta mengklasifikasikan klien yang berisiko menjadi calon default.
## Metrik Bisnis:
Penurunan Kerugian yang Diberikan Jika Terjadi Default (Loss Given Default, LGD).

## Read Dataset
`````Python
app_test=pd.read_csv("application_test.csv")
app_train=pd.read_csv("application_train.csv")
`````

![[Pasted image 20231127162104.png]]
## Data Pre-Processing

- Melakukan pemeriksaan missing value dan menghapus variabel yang memiliki missing value.
![[Pasted image 20231127162258.png]]
Berdasarkan hasil diatas dapat dilihat bahwa terdapat missing value pada data training dan testing. Missing value ditangani dengan cara drop variable.
![[Pasted image 20231127162400.png]]
- Memeriksa adanya data duplikat dan tidak menemukan duplikat.
![[Pasted image 20231127162140.png]]
- Mengecek ejaan kata dan menemukan kesalahan pada kolom CODE_GENDER dan NAME_INCOME_TYPE, yang kemudian dihapus.
![[Pasted image 20231127162455.png]]
- Melakukan feature engineering dengan menambahkan kolom AGE yang berisi umur klien dalam tahun (dalam format integer).
![[Pasted image 20231127162601.png]]
- Mengubah data kategorikal menjadi biner.
![[Pasted image 20231127162624.png]]
- Membagi dataset menjadi 70% data training dan 30% data testing.
![[Pasted image 20231127162705.png]]
- Melakukan oversampling (SMOTE) untuk menyeimbangkan data.
![[Pasted image 20231127162736.png]]
DIketahuibahwa data tidak seimbang sehingga dilakukan SMOTE
![[Pasted image 20231127162823.png]]

## Data Visualization and Business Insight

![[Pasted image 20231127163252.png]]

Mayoritas klien (197.056) berhasil membayar pinjaman tepat waktu, sedangkan 98.528 klien mengalami kesulitan dalam pembayaran. Selain itu, jumlah klien perempuan dalam dataset ini lebih banyak daripada klien laki-laki, dan klien perempuan juga memiliki tingkat keberhasilan yang lebih tinggi dalam melunasi pinjaman tepat waktu dibandingkan klien laki-laki.

![[Pasted image 20231127163359.png]]

Informasi yang bisa diterapkan oleh bank adalah bahwa klien yang lebih muda memiliki kecenderungan yang lebih tinggi untuk gagal membayar pinjaman. Tingkat kegagalan pembayaran melebihi 10% untuk kelompok usia termuda, sementara di bawah 5% untuk kelompok usia tertua.

Berdasarkan informasi ini, bank dapat mengambil langkah-langkah pencegahan dengan memberikan panduan atau tips perencanaan keuangan kepada nasabah yang lebih muda. Tujuannya bukan untuk mendiskriminasi nasabah yang lebih muda, tetapi untuk membantu mereka membayar tepat waktu dengan memberikan saran dan dukungan tambahan.

![[Pasted image 20231127163609.png]]

- Lebih banyak clients dengan jenis kelamin perempuan dan tanpa banyak anak
- Lebih banyak clients yang memiliki realty tetapi tidak memiliki mobil
## Machine Learning Implementation and Evaluation

Ada 2 Model Machine Learning menggunakan hyperparameter tuning
1. Logistic Regression
2. XGBoost Classifier 

![[Pasted image 20231127163812.png]]
Setelah menganalisis data Home Credit, ditemukan bahwa model terbaik yang digunakan adalah XGBoost Classifier. Model ini memiliki tingkat akurasi sebesar 0.917690.
## Business Recommendation
- Home Credit Indonesia perlu memberikan perhatian khusus kepada pelanggan yang memenuhi kriteria berikut: memilih pinjaman tunai, memiliki pekerjaan, sudah menikah, dan memiliki rumah atau apartemen. Kelompok pelanggan ini memiliki persentase tertinggi yang tidak mengalami kesulitan dalam pembayaran. Untuk memberikan perhatian khusus, beberapa saran yang dapat dipertimbangkan adalah memberikan kelonggaran dalam jangka waktu pembayaran, mengurangi jumlah angsuran yang harus dibayarkan, atau meningkatkan batas pinjaman yang dapat mereka akses.

- Untuk mengatasi risiko gagal bayar pada klien muda, rekomendasi termasuk meningkatkan penilaian risiko, memberikan edukasi keuangan, menyesuaikan produk pinjaman, meningkatkan pengawasan, dan mengembangkan kemitraan dengan lembaga pendidikan atau organisasi. Ini membantu dalam menawarkan pinjaman yang sesuai, meningkatkan pemahaman keuangan, dan memberikan dukungan tambahan untuk pengelolaan pinjaman klien muda.


