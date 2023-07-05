# Business Understanding
## Context

Philadelphia Buildings Database ini memuat informasi tentang karakteristik fisik dan lokasi bangunan di kota Philadelphia. Data ini dapat menjadi referensi untuk penyewaan, perencanaan, zonasi dan, pemeliharaan properti.

Dataset ini bersumber dari https://opendataphilly.org/. Situs tersebut adalah portal yang menyediakan akses ke lebih dari 300 set data, aplikasi, dan API yang terkait dengan wilayah Philadelphia. Kemudahan dan kebebasan mengakses data ini bertujuan untuk mendorong kinerja pemerintah yang lebih baik dan juga lebih transparan kepada masyarakat.

`The Office of Property Assessment (OPA)` adalah salah satu departemen dalam pemerintahan Kota Philadelphia yang bertugas untuk menentukan nilai setiap properti di Philadelphia. Asesmen harga dari OPA digunakan untuk menghitung pajak properti yang harus dibayar oleh pemilik.

Dalam skala besar, setiap negara memiliki target pendapatan melalui pajak dengan ketentuan dan sistem yang berbeda-beda. Skala lebih kecilnya, pendapatan dari pajak tersebut dikumpulkan dari region, subregion, maupun kota. Pendapatan ini akan dialokasikan dalam beberapa klasifikasi anggaran sesuai kebutuhan kota, termasuk pembangunan, pendidikan, maupun fasilitas umum. Kota Philadelphia memiliki dataset yang berisi harga pasar (market value) setiap properti di kota yang digunakan untuk perhitungan pajak. Seiring berjalannya waktu, akan ada properti-properti baru yang dibangun di Kota Philadelphia yang harga pasarnya belum ditaksasi. Oleh karena itu, penting bagi pemerintah untuk mengetahui proyeksi nominal pendapatan yang akan diterima sebelum menyusun anggaran agar alokasi anggaran menjadi tepat sasaran sesuai target.

Di tahun 2020, pajak properti di Kota Philadelphia berkontribusi sebesar 14,5% dari pendapatan dana umum, kurang dari separuh median 31,5% dibandingkan 10 kota lainnya. Oleh karena itu, kasus ini menjadi penting karena dengan adanya model yang dapat memprediksi harga pasar properti secara akurat berpotensi mengoptimalisasi pendapatan kota.   

## Problem Statement
1. Bagaimana caranya memprediksi harga properti sehingga perhitungak pajak menjadi akurat?
1. Jenis properti apa yang sebaiknya diprioritaskan terlebih dahulu untuk efisiensi waktu dan biaya dalam pembuatan model machine learning?
1. Model machine learning apa yang sebaiknya digunakan untuk menghitung nilai properti secara akurat?

## Goal
Membuat sebuah model machine learning yang dapat membantu OPA untuk **menentukan harga pasar properti baru (*market value*) yang belum ditaksasi di Kota Philadelphia**.

## Evaluation Metrics
1. MAE (Mean Absolute Error)
2. RMSLE (Root Mean Squared Log Error)
3. MAPE (Mean Absolute Percentage Error)

## Target
|**Metric** | **Target**
|----- | ----- |
|MAPE| <= 42k USD
| MAPE | <= 13%

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
