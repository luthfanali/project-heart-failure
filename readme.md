# Prediksi Gagal Jantung

![Jantung](./img/heart.png)

## Pendahuluan

Cardiovascular diseases (CVDs) atau biasa disebut dengan Gagal Jantung adalah penyakit pembunuh nomor 1 di dunia. Gagal jantung menyebabkan 17,9 juta kematian tiap tahunnya, yang mana merupakan 31% dari seluruh kematian di dunia.

Sebagian besar penyakit jantung dapat dicegah dengan gaya hidup yang sehat seperti mengurangi pola makan yang tidak sehat, tidak merokok, dan tidak minum alkohol. Orang yang memiliki penyakit jantung, atau mereka yang memiliki resiko kardivaskular yang tinggi (seperti memiliki penyakit hipertensi, diabetes, hiperlipidemia) memerlukan deteksi dini untuk mencegah terjadinya kegagalan jantung. Oleh karena itu saya mencoba untuk membuat Machine Learning Model yang dapat membantu untuk mewujudkan hal tersebut.

Input dari permasalah ini antara lain:

- Umur
- Jenis Kelamin
- Diabetes
- Anaemia
- Tekanan Darah
- Merokok

Kemudian digunakannya model Random Forest dengan beberapa Hyperparameter Tuning untuk memprediksi Kematian karena Gagal Jantung. Percobaan dengan menggunakan KNN, Logistic Regression, Random Forest, Support Vector Machines, Naive Bayes, dan Decision Tree didapatkan bahwa model Random Forest dapat memprediksi lebih baik dibandingkan model-model lainnya dengan tingkat akurasi sebesar `80.81%` pada Data Training dan `88.00%` pada Data Test.

## Related Work

1. Chicco, D., & Jurman, G. (2020). Machine learning can predict survival of patients with heart failure from serum creatinine and ejection fraction alone. BMC Medical Informatics and Decision Making, 20(1), 16.
2. Meng, F., Zhang, Z., Hou, X., Qian, Z., Wang, Y., Chen, Y., ... Zou, J. (2019). Machine learning for prediction of sudden cardiac death in heart failure patients with low left ventricular ejection fraction: study protocol for a retroprospective multicentre registry in China. BMJ Open, 9(5), e023724.

## Dataset dan Features

### Dataset Source

Dataset yang digunakan didapat dari Kaggle dan Paper [Chicco, D., & Jurman, G. (2020)](https://bmcmedinformdecismak.biomedcentral.com/articles/10.1186/s12911-020-1023-5)

Data ini terdiri dari 229 observasi dan 13 fitur. 13 Fitur tersebut antara lain:

1. `age`: Umur
2. `anaemia` : Penurunan dari sel darah merah
3. `creatinine_phosphokinase` : Level dari Enzim CPK dalam darah (mcg/L)
4. `diabetes` : Punya diabetes atau tidak
5. `ejection_fraction` : Presentase darah keluar dari jantung tiap jantung berkontraksi
6. `high_blood_pressure` : Punya hipertensi atau tidak
7. `platelets` : Jumlah trombosit dalam darah (kiloplatelets/mL)
8. `serum_creatinine` : Tingkat ****************serum creatinine**************** dalam darah (mg/dL)
9. `serum_sodium` : Tingkat ****************serum sodium**************** dalam darah (mEq/L)
10. `sex` : Jenis kelamin
11. `smoking` : Perokok atau tidak
12. `time`: Periode dilaksakannya tindak lanjut
13. `DEATH_EVENT` : Meinggalnya pasien dalam periode dilaksakannya tindak lanjut

### Data Preprocessing

Dilakukan pengecekan atas data Null dan data duplikat. Hasilnya tidak terdapat data Null maupun data duplikat. Kemudian dibagi menjadi 2 set. Sebanyak 75% untuk data training, dan sebanyak 25% untuk data test.

| age | anaemia | creatinine_phosphokinase | diabetes | ejection_fraction | high_blood_pressure | platelets | serum_creatinine | serum_sodium | sex | smoking | time | DEATH_EVENT |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 75 | 0 | 582 | 0 | 20 | 1 | 265000 | 19 | 130 | 1 | 0 | 4 | 1 |
| 55 | 0 | 7861 | 0 | 38 | 0 | 26335803 | 11 | 136 | 1 | 0 | 6 | 1 |
| 65 | 0 | 146 | 0 | 20 | 0 | 162000 | 13 | 129 | 1 | 1 | 7 | 1 |
| 50 | 1 | 111 | 0 | 20 | 0 | 210000 | 19 | 137 | 1 | 0 | 7 | 1 |
| 65 | 1 | 160 | 1 | 20 | 0 | 327000 | 27 | 116 | 0 | 0 | 8 | 1 |

## Metode

1. Logistic Regression: untuk memodelkan hubungan antara variabel independen dan dependen yang bersifat biner (bernilai 0 atau 1). Tujuannya adalah untuk memprediksi probabilitas kelas atau hasil akhir yang diinginkan, berdasarkan variabel independen.
2. KNN (K-Nearest Neighbor): algoritma untuk klasifikasi dan regresi. Konsepnya adalah dengan mencari tetangga terdekat dari data yang akan diprediksi, kemudian mengambil mayoritas kelas dari tetangga terdekat tersebut sebagai hasil prediksi.
3. Random Forest: algoritma yang menggunakan kumpulan *decision trees* untuk melakukan klasifikasi dan regresi. Setiap pohon dihasilkan dari subsample data dan fitur yang dipilih secara acak, sehingga menghasilkan banyak variasi model.
4. SVM (Support Vector Machine): SVM mencari hyperplane (sebuah garis atau permukaan yang memisahkan data) yang memiliki jarak maksimum dari dua kelas yang berbeda. Tujuannya adalah untuk mencaro pemisahan yang optimal antara kelas-kelas tersebut.
5. Naive Bayes: menggunakan teorema Bayes untuk menghitung probabilitas kelas dari suatu data, berdasarkan probabilitas kelas dan probabilitas fitur-fitur pada data tersebut.
6. Decision Tree: menghasilkan model berbentuk pohon, yang menggambarkan klasifikasi atau prediksi yang dilakukan dengan mengikuti serangkaian aturan pemilihan fitur. Setiap node pada pohon mewakili keputusan berdasarkan fitur-fitur tertentu, dan setiap cabang mewakili kemungkinan hasil dari keputusan tersebut.

## Experiments and Results

Ketika melakukan training pada model, diketahui bahwa data training hanya berjumlah 224 observasi. Jumlah data observasi yang sedikit menyebabkan perlu dilakukan ****************Cross Validation**************** untuk mendapatkan perbandingan performa.

Selanjutnya dilihat dari performa yang dihasilkan, KNN, Random Forest dan Decision Tree mengalami overfitting. Tampak dari hasil *****score***** prediksi yang bernilai `1.0` . Kemudian dilakukan Hyperparameter Tuning pada KNN, Random Forest dan Decision Tree. Terlihat pada ketiga model tersebut mengalami perbaikan performa sehingga tidak overfit.

Sebelum Hyperparameter Tuning

```bash
# akurasi knn
knn.score(x_train_clean, y_train)
0.7946428571428571

# akurasi logistic regression
logreg.score(x_train_clean, y_train)
0.8303571428571429

# akurasi random forest
random_forest.score(x_train_clean, y_train)
1.0

# akurasi Support Vector Classifier
svm.score(x_train_clean, y_train)
0.9017857142857143

# akurasi Naive Bayes
naive_bayes.score(x_train_clean, y_train)
0.78125

# akurasi Decision Tree
dtc.score(x_train_clean, y_train)
1.0
```

Setelah Hyperparameter Tuning

```bash
# akurasi knn
knn.score(x_train_clean, y_train)
0.7946428571428571

# akurasi logistic regression
logreg.score(x_train_clean, y_train)
0.8526785714285714

# akurasi random forest
random_forest.score(x_train_clean, y_train)
0.9419642857142857

# akurasi Support Vector Classifier
svm.score(x_train_clean, y_train)
0.8482142857142857

# akurasi Naive Bayes
naive_bayes.score(x_train_clean, y_train)
0.78125

# akurasi Decision Tree
dtc.score(x_train_clean, y_train)
0.8526785714285714
```

Kemudian dilakukannya Cross Validation pada data training dan didapatkan hasil sebagai berikut

```bash
Accuracy Log reg: 79.89% (4.77%)
Accuracy KNN: 72.76% (3.89%)
Accuracy RF: 83.46% (2.41%)
Accuracy SVM: 79.42% (6.22%)
Accuracy Naive Bayes: 76.77% (3.16%)
Accuracy Decision Tree: 79.90% (6.32%)
```

Diujikan pada data test dan didapat hasil sebagai berikut

```bash
Accuracy Log reg: 86.67% (4.22%)
Accuracy KNN: 70.67% (6.80%)
Accuracy RF: 88.00% (6.53%)
Accuracy SVM: 86.67% (5.96%)
Accuracy Naive Bayes: 76.00% (11.62%)
Accuracy Decision Tree: 82.67% (9.98%)
```

### Kesimpulan

Dari seluruh model yang diuji, Random Forest menjadi kandidat yang mumpuni dalam melakukan prediksi dataset Gagal Jantung ini.
