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
