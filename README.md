# Business Understanding
## Context

Philadelphia Buildings Database ini memuat informasi tentang karakteristik fisik dan lokasi bangunan di kota Philadelphia. Data ini dapat menjadi referensi untuk penyewaan, perencanaan, zonasi dan, pemeliharaan properti.

Dataset ini bersumber dari https://opendataphilly.org/. Situs tersebut adalah portal yang menyediakan akses ke lebih dari 300 set data, aplikasi, dan API yang terkait dengan wilayah Philadelphia. Kemudahan dan kebebasan mengakses data ini bertujuan untuk mendorong kinerja pemerintah yang lebih baik dan juga lebih transparan kepada masyarakat.

`The Office of Property Assessment (OPA)` adalah salah satu departemen dalam pemerintahan Kota Philadelphia yang bertugas untuk menentukan nilai setiap properti di Philadelphia. Asesmen harga dari OPA digunakan untuk menghitung pajak properti yang harus dibayar oleh pemilik.

Secara terbuka, OPA menerima pengajuan untuk pengurangan maupun pengecualian yang dapat mengurangi pajak properti. Jika pemilik properti tidak setuju dengan penilaian atau yakin bahwa pengurangan atau pengecualian belum diterapkan dengan benar, OPA menawarkan pilihan untuk meminta peninjauan ulang atau mengajukan banding. Oleh karena itu, sebagai stakeholder, OPA membutuhkan analisis secara mendalam dan sebuah alat atau tool yang dapat membantu OPA dalam menentukan harga properti secara akurat. Kasus ini menjadi sangat penting karena pajak merupakan salah satu sumber pendapatan pemerintah yang akan digunakan untuk perencanaan anggaran kota.

Dalam skala besar, setiap negara memiliki target pendapatan melalui pajak dengan ketentuan dan sistem yang berbeda-beda. Skala lebih kecilnya, pendapatan dari pajak tersebut dikumpulkan dari region, subregion, maupun kota. Pendapatan ini akan dialokasikan dalam beberapa klasifikasi anggaran sesuai kebutuhan kota, termasuk pembangunan, pendidikan, maupun fasilitas umum. Kota Philadelphia memiliki dataset yang berisi harga pasar (market value) setiap properti di kota yang digunakan untuk perhitungan pajak. Seiring berjalannya waktu, akan ada properti-properti baru yang dibangun di Kota Philadelphia yang harga pasarnya belum ditaksasi. Oleh karena itu, penting bagi pemerintah untuk mengetahui proyeksi nominal pendapatan yang akan diterima sebelum menyusun anggaran agar alokasi anggaran menjadi tepat sasaran sesuai target.

Data terbaru di tahun 2020, dilansir pada tautan https://www.pewtrusts.org/en/research-and-analysis/reports/2022/09/how-property-is-taxed-in-philadelphia, total pendapatan (*general revenue*) Kota Philadelphia berjumlah $4,834 M dengan rincian sebagai berikut:
- $  699 M   (14.5%) dari pajak properti
- $2,124  M  (43.9%) dari pajak upah, penghasilan, dan laba bersih
- $1,229 M    (25.4%) dari pajak lainnya
- $  782  M  (16.2%) dari selain pajak

![Tax Property in Philadelphia comapre with other city ](assets/tax.png)

Gambar di atas juga menunjukkan persentase pendapatan yang diwakili oleh pajak properti di Philadelphia dan 10 kota lainnya untuk tahun fiskal 2020, tahun terbaru yang data lengkapnya tersedia. Bagian pendapatan dari pajak properti di Philadelphia sebesar 14,5% dari pendapatan dana umum, kurang dari separuh median 31,5%. Dalam hal pendapatan kota secara keseluruhan, pajak properti memberikan kontribusi sebesar 9,5% di Philadelphia, lebih rendah dibandingkan dengan kota lain yang dipertimbangkan kecuali Columbus, dan juga kurang dari separuh median. 


Dari data di atas dapat dilihat bahwa pajak Kota Philadelphia berkontribusi cukup rendah pada pendapatan kota dibandingkan kota-kota lainnya. Oleh karena itu, kasus ini menjadi penting karena dengan adanya model yang dapat memprediksi harga pasar properti secara akurat berpotensi mengoptimalisasi pendapatan kota.   
   

## Problem Statement
1. Bagaimana caranya memprediksi harga properti sehingga perhitungak pajak menjadi akurat?
1. Jenis properti apa yang sebaiknya diprioritaskan terlebih dahulu untuk efisiensi waktu dan biaya dalam pembuatan model machine learning?
1. Model machine learning apa yang sebaiknya digunakan untuk menghitung nilai properti secara akurat?

## Goal
Membuat sebuah model machine learning yang dapat membantu OPA untuk **menentukan harga pasar properti baru (*market value*) yang belum ditaksasi di Kota Philadelphia**.

## **Analytic Approach**
Jadi dari penjabaran di atas, kami akan menganalisis data untuk dapat menemukan pola dari fitur-fitur yang ada, yang membedakan fitur tertentu seperti lokasi, tanggal, luas dengan yang lainnya dalam hal market value pada jenis gedung perumahan (Residentials atau single Family).

Selanjutnya, kami akan membangun suatu model regresi yang akan membantu perusahaan/badan/lembaga untuk dapat menyediakan 'tool' atau model prediktif yang mampu prediksi market value of property (khususnya jenis perumahan/Residentials) di kota philadelpia di waktu dan lokasi tertentu. Disini kami akan melakukan eksperimen dengan beberapa algoritma model regresi yang sering digunakan seperti Linear Regression, KNN, SGD, Random Forest, XGB, dan LGBM. Dimana kami akan memilih satu model (atau gabungan dari beberapa model) untuk membuat tool tersebut yang sesuai dengan data dari Office of Property Assesment (OPA) https://opendataphilly.org/datasets/philadelphia-properties-and-assessment-history/.

## Evaluation Metrics
1. MAE (Mean Absolute Error)
2. RMSLE (Root Mean Squared Log Error)
3. MAPE (Mean Absolute Percentage Error)

## Target
|**Metric** | **Target**
|----- | ----- |
|MAPE| <= 42,000 USD
| MAPE | <= 13%|

# Data Understanding
## Attributes Information & EDA
1. Terdapat 6 kategori properti: Single Family, Multi Family, Mixed Use, Vacant Land, Commercial, dan Industrial.
2. Kategori Single Family mendominasi hampir 80% dataset.
3. Mayoritas persebaran data pada fitur-fitur diasumsikan tidak terdistribusi normal sehingga interpretasi data akan menggunakan median.
4. Fitur yang merepresentasikan keadaan rumah yaitu luas tanah, luas bangunan, jumlah ruangan, jumlah kamar tidur, jumlah kamar mandi, ada garasi/tidak, jumlah lantai bangunan, kondisi eksterior dan interior, tahun pendirian bangunan, dll.
5. Fitur yang merepresentasikan lokasi seperti kode pos, nama jalan, nomor rumah, kode state, zona, dll.
6. Fitur lainnya mencerminkan nama pemilik, tahun penjualan properti, harga penjualan, dll.

Attributes Information dan EDA secara lengkap dan rinci dapat dilihat pada Notebook.

   
# Preprocessing
Pada tahap ini, kita akan melakukan cleaning pada data yang nantinya data yang sudah dibersihkan akan kita gunakan untuk pemodelan. Beberapa hal yang dilakukan adalah:

1) Data Cleaning
- Drop data duplikat jika ada.
- Cek format penulisan data apakah sudah benar atau belum (jika ada).
- Drop fitur yang tidak memiliki relevansi terhadap harga market properti.
- Melakukan treatment terhadap missing value jika ada. Bisa dengan cara men-drop fiturnya jika memang tidak dibutuhkan atau bisa juga dengan mengimputasi dengan nilai yang paling masuk baik secara *domain knowledge* maupun secara statistik.
- Pengecekan Outliers

2) Feature engineering adalah proses membuat, memilih, atau mengekstraksi fitur (features) yang relevan dari data mentah (raw data) untuk digunakan dalam proses pembelajaran mesin (machine learning). Tujuan utama dari feature engineering adalah meningkatkan kualitas data yang akan digunakan oleh algoritma pembelajaran mesin sehingga menghasilkan model yang lebih baik dan performa yang lebih baik pula. Kita akan melakukan :
   - ekstraksi fitur (**feature extraction**) 
   - konstruksi fitur (**feature construction**) atau pembuatan fitur (**feature creation**)
   
3) Data Transformation
- langkah ini melibatkan pengubahan data ke dalam format yang lebih cocok untuk pemodelan regressi untuk memprediksi harga market properti. Ini dapat mencakup normalisasi data numerik, membuat variabel dummy, dan mengkodekan data kategorikal.

# Modelling
Menggunakan uji RandomForest Regressor, XGBoost Regressor, dan LGBM Regressor. Berikut hasilnya:

|Model|	Mean_MAE	|Std_MAE	|Mean_MAPE	|Std_MAPE|	Mean_RMSLE|	Std_RMSLE|	Mean_R-Squared	|Std_R-Squared|	cv duration (minutes)|
| ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- 
|0	|RandomForest Regressor|	-19523.141701|	407.534850|	-0.135378|	0.001974|	-0.251589|	0.003460|	0.887791	|0.008019	|56.678306|
|1	|XGBoost Regressor|	-30867.305234|	192.172436|	-0.227556|	0.001496|	-0.316739	|0.001408	|0.831060|	0.003824|	2.357592|
|2|	LGBM Regressor	|-33859.142211|	242.295018	|-0.250618|	0.001780|	-0.339415	|0.002176|	0.795538	|0.003642	|0.452971|

Dari hasil Model Benchmarking di atas, dilihat dari semua metrics yang ada maka Model dengan algoritma Random Forest memiliki nilai error yang paling rendah. Tapi kelemahan dari Random Forest adalah waktu/durasi untuk training nya cukup lama jika dibandingkan dengan XGBoost dan LGBM.

Selain itu dari hasil MAPE yang didapatkan bisa dibilang cukup rendah pada ketiga model ini, yang menandakan nilai prediksi yang lebih tinggi jika dibandingkan nilai aktual (overestimation) dapat di handel dengan cukup baik pada prediksi registered users, karea MAPE sensitif terhadap nilai prediksi yang overestimated. Sedangkan untuk RMSLE nya juga nilainya cukup kecil, yang artinya nilai prediksi yang lebih rendah dari nilai aktual nya (underestimation) dapat di handel dengan cukup baik juga, dimana RSMLE sensitif terhadap error pada nilai prediksi yang underestimated.

## Feature Importances
5 fitur terbaik, antara lain:
- `property_age`
- `total_area`
- `overall_condition`
- `total_livable_area`
- `region`

Sesuai dengan pengetahuan umum bahwa kelima fitur ini akan cenderung memiliki pengaruh yang signifikan untuk pemodelan.
Ada beberapa fitur yang tidak penting yang dihapus agar mempercepat waktu pelatihan dan prediksi, mengurangi overfitting, meningkatkan interpretabilitas, mengurangi kompleksitas dan biaya.

## Hyperparameter Tuning
Setelah dilakukan tuning kami mendapatkan best_parameter untuk model terbaik pada dataset ini : 
'model__regressor__n_estimators': 1200, 'model__regressor__min_samples_split': 3, 'model__regressor__min_samples_leaf': 1, 'model__regressor__max_features': 'auto', 'model__regressor__max_depth': 80, 'model__regressor__bootstrap': True}

Testing model terbaik **sebelum** di tuning:
| |	MAE	|MAPE|	RMSLE	|R-Squared|
|-----|-----|-----|-----|-----|
|RandomForest	|17794.461094|	0.122322	|0.240366	|0.894169


Testing model terbaik **setelah** di tuning:
| |	MAE	|MAPE|	RMSLE	|R-Squared|
|-----|-----|-----|-----|-----|
|RandomForest	|17731.06426|	0.121759	|0.239235	|0.895058

Terjadi peningkatan performa pada masing-masing metric sebesar:

- MAE : 0.30%
- MAPE : 0.46%
- RMSLE : 0.47%
- R-Squared : 0.1% 

# Conclusions and Recommendations
## Conclusions
1. Model yang telah dibangun memiliki score MAPE sebesar 12.1%. yang berarti ketika model yang dibuat digunakan untuk memprediksi nilai properti pada rentang nilai seperti yang dilatih terhadap model (market value: 1,000 USD - 4,160,000 USD ) untuk tipe properti residensial di kota Philadelphia, maka hasil prediksi yang dihasilkan oleh model memiliki kemungkinan tingkat kesalahan sebesar 12.1% dari nilai aslinya. Nilai MAPE yang didapat, yaitu sekitar **12,1%** menjadikan model ini dapat dikategorikan ke dalam **'Good forecasting'** (Lewis, 1982).

2. Performa Model yang kami mencapai target yang ditentukan yatu (MAPE <= 13% dan MAE <= 42,000USD)

3. Berdasarkan model yang dibuat (dilihat dari feature importance) fitur-fitur `property_age`, `total_area`, `overall_condition`, `total_livable_area` dan `region` menjadi fitur yang paling berpengaruh terhadap nilai prediksi harga market properti.

4. Dari analisa kesalahan (*error analysis*) yang dilakukan pada 4 fitur terpenting, terdapat beberapa kondisi pada fitur-fitur tersebut yang membuat model memiliki nilai error yang besar :
    - `property_age` pada nilai 95, 100 dan 105 tahun
    - `total_area` atau luas tanah yang memiliki nilai 0 (artinya tanah nya sempit, tapi luas bangunan besar --> rumah susun/apartemen kecil)
    - `overall_condition` atau kondisi rumah (interior dan eksterior) pada nilai 4 (average) --> sebaran nya paling banyak yaitu di atas 70%
    - `total_livable_area` atau luas bangunan pada nilai 0 dan rentang nilai 1200-1210 sqft
    - `region` yaitu di wilayah phiadelphia utara (north) karena sebaran data nya paling banyak dan selatan (south) karena harga nya beragam atau tidak linier (wilayah ini berada tepat di tengah wilayah dengan nilai median market tertinggi dan terendah )

## Recommendations
1. Saat mengecek prediksi mana saja yang memiliki nilai error yang tinggi dan karakteristik untuk 5 fitur terpenting. Pada akhirnya kita dapat mengetahui sebenarnya variabel mana saja dan aspek apa yang menyebabkan model menghasilkan error yang tinggi dengan lebih mendalam, sehingga kita bisa melakukan training ulang dengan penerapan feature engineering lainnya.

2. Jika ada penambahan banyak data, dapat dicoba dengan menggunakan model yang lebih kompleks, seperti recursive neural networks (RNN). Namun, kalau jumlah data dan fiturnya masih seperti dataset ini, kemungkinan besar tidak akan mengubah hasilnya secara signifikan.

3. Model yang sudah dibangun ini bisa dimanfaatkan untuk pengembangan pembuatan model lainnya. Misalkan kita ingin membuat model yang bisa memprediksi properti dengan kategori lain misalkan properti industri maupun apartemen {multi family)

4. Melakukan tuning hyperparameter yang lebih impresif (memperluas parameter space atau menggunakan metodologi lain seperti Bayesian, GridSearch dll), untuk mendapatkan performa terbaik (dan mengurangi overfiiting). Tapi memang dibutuhkan resource/komputer dengan kemampuan komputasi yang lebih tinggi untuk model Random Forest.
