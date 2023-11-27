# Home Credit Indonesia Data Science Virtual Intership
## Data Understanding
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

![Gambar5](https://github.com/ThesionMS/Home-Credit-Indonesia-Data-Science-Virtual-Intership/blob/main/gambar/Gambar%204.jpg)

## Data Pre-Processing

- Melakukan pemeriksaan missing value dan menghapus variabel yang memiliki missing value.
![Gambar6]https://github.com/ThesionMS/Home-Credit-Indonesia-Data-Science-Virtual-Intership/blob/main/gambar/Gambar5.jpg

Berdasarkan hasil diatas dapat dilihat bahwa terdapat missing value pada data training dan testing. Missing value ditangani dengan cara drop variable.
```Python
train_pakai = app_train_pakai.dropna()
test_pakai = app_test_pakai.dropna()
```
- Memeriksa adanya data duplikat dan tidak menemukan duplikat.
- 
![Gambar8](https://github.com/ThesionMS/Home-Credit-Indonesia-Data-Science-Virtual-Intership/blob/main/gambar/Gambar6.jpg)

- Mengecek ejaan kata dan menemukan kesalahan pada kolom CODE_GENDER dan NAME_INCOME_TYPE, yang kemudian dihapus.
```Python
train_pakai.drop(train_pakai.index[train_pakai['CODE_GENDER']=='XNA'],inplace=True)
train_pakai.drop(train_pakai.index[train_pakai['NAME_INCOME_TYPE']=='Maternity leave'],inplace=True)
```
- Melakukan feature engineering dengan menambahkan kolom AGE yang berisi umur klien dalam tahun (dalam format integer).
```Python
AGE_TR=(train_pakai['DAYS_BIRTH']/-365).astype(int)
AGE_TS=(test_pakai['DAYS_BIRTH']/-365).astype(int)
```
- Mengubah data kategorikal menjadi biner.
```Python
l = LabelEncoder()
for q in test_pakai.describe(include='object').columns:
    test_pakai[q]=l.fit_transform(test_pakai[q])
app_test.head(3)
```
- Membagi dataset menjadi 70% data training dan 30% data testing.
```Python
# Pembagian data latih dan data uji
from sklearn.model_selection import train_test_split

X = train_pakai.drop(columns = ['TARGET'])
y = train_pakai['TARGET']

# split dataset into training set and test set
X_train, X_test, y_train, y_test = train_test_split(X,
                                                    y,
                                                    test_size=0.3, # 70% training and 30% test
                                                    random_state=109)
```
- Melakukan oversampling (SMOTE) untuk menyeimbangkan data.
- 
![Gambar8](https://github.com/ThesionMS/Home-Credit-Indonesia-Data-Science-Virtual-Intership/blob/main/gambar/Gambar7.jpg)

DIketahuibahwa data tidak seimbang sehingga dilakukan SMOTE

![Gambar9](https://github.com/ThesionMS/Home-Credit-Indonesia-Data-Science-Virtual-Intership/blob/main/gambar/Gambar8.jpg)

## Data Visualization and Business Insight

![Gambar1](https://github.com/ThesionMS/Home-Credit-Indonesia-Data-Science-Virtual-Intership/blob/main/gambar/Picture1.png)

Mayoritas klien (197.056) berhasil membayar pinjaman tepat waktu, sedangkan 98.528 klien mengalami kesulitan dalam pembayaran. Selain itu, jumlah klien perempuan dalam dataset ini lebih banyak daripada klien laki-laki, dan klien perempuan juga memiliki tingkat keberhasilan yang lebih tinggi dalam melunasi pinjaman tepat waktu dibandingkan klien laki-laki.

![Gambar2](https://github.com/ThesionMS/Home-Credit-Indonesia-Data-Science-Virtual-Intership/blob/main/gambar/Picture2.png)

Informasi yang bisa diterapkan oleh bank adalah bahwa klien yang lebih muda memiliki kecenderungan yang lebih tinggi untuk gagal membayar pinjaman. Tingkat kegagalan pembayaran melebihi 10% untuk kelompok usia termuda, sementara di bawah 5% untuk kelompok usia tertua.

Berdasarkan informasi ini, bank dapat mengambil langkah-langkah pencegahan dengan memberikan panduan atau tips perencanaan keuangan kepada nasabah yang lebih muda. Tujuannya bukan untuk mendiskriminasi nasabah yang lebih muda, tetapi untuk membantu mereka membayar tepat waktu dengan memberikan saran dan dukungan tambahan.

![Gambar3](https://github.com/ThesionMS/Home-Credit-Indonesia-Data-Science-Virtual-Intership/blob/main/gambar/Gambar9.jpg)

- Lebih banyak clients dengan jenis kelamin perempuan dan tanpa banyak anak
- Lebih banyak clients yang memiliki realty tetapi tidak memiliki mobil
## Machine Learning Implementation and Evaluation

Ada 2 Model Machine Learning menggunakan hyperparameter tuning
1. Logistic Regression
2. XGBoost Classifier 

![Gambar4](https://github.com/ThesionMS/Home-Credit-Indonesia-Data-Science-Virtual-Intership/blob/main/gambar/Picture3.png)

Setelah menganalisis data Home Credit, ditemukan bahwa model terbaik yang digunakan adalah XGBoost Classifier. Model ini memiliki tingkat akurasi sebesar 0.917690.
## Business Recommendation
- Home Credit Indonesia perlu memberikan perhatian khusus kepada pelanggan yang memenuhi kriteria berikut: memilih pinjaman tunai, memiliki pekerjaan, sudah menikah, dan memiliki rumah atau apartemen. Kelompok pelanggan ini memiliki persentase tertinggi yang tidak mengalami kesulitan dalam pembayaran. Untuk memberikan perhatian khusus, beberapa saran yang dapat dipertimbangkan adalah memberikan kelonggaran dalam jangka waktu pembayaran, mengurangi jumlah angsuran yang harus dibayarkan, atau meningkatkan batas pinjaman yang dapat mereka akses.

- Untuk mengatasi risiko gagal bayar pada klien muda, rekomendasi termasuk meningkatkan penilaian risiko, memberikan edukasi keuangan, menyesuaikan produk pinjaman, meningkatkan pengawasan, dan mengembangkan kemitraan dengan lembaga pendidikan atau organisasi. Ini membantu dalam menawarkan pinjaman yang sesuai, meningkatkan pemahaman keuangan, dan memberikan dukungan tambahan untuk pengelolaan pinjaman klien muda.


