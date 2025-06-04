# Forecasting Kualitas Udara (ISPU) di Kota Jakarta

Proyek ini bertujuan untuk memprediksi **Indeks Standar Pencemar Udara (ISPU)** di wilayah DKI Jakarta menggunakan data historis kualitas udara. Dengan bantuan algoritma **XGBoost** dan **SARIMAX**, proyek ini mencoba memahami pola polusi udara dan memberikan estimasi akurat terhadap kualitas udara dalam jangka pendek.

---

## Deskripsi Singkat

Kota Jakarta merupakan salah satu kota dengan tingkat pencemaran udara tertinggi di Asia Tenggara. Proyek ini menggunakan data ISPU dari tahun 2021 hingga 2025 untuk:
- Memprediksi kualitas udara
- Menganalisis polutan utama (PM2.5, NO2, PM10)
- Memberikan insight untuk mitigasi dampak pencemaran

---

## Dataset

- **Sumber**: [Satu Data Jakarta](https://satudata.jakarta.go.id)
- **Periode**: Tahun 2021–2025
- **Fitur**:
  - `pm10`, `pm25`, `so2`, `co`, `o3`, `no2`
  - `max`, `critical`, `kategori`
  - `tanggal`, `periode_data`
  - `stasiun`

---

## Metodologi

### Preprocessing
- Pembersihan nilai non-numerik dan karakter seperti `'---'`
- Konversi kolom numerik dan tanggal
- Interpolasi missing values berbasis waktu
- Ekstraksi fitur waktu: `bulan`, `hari`, `hari_dalam_minggu`
- Penambahan fitur lag (`max_lag1`, `max_lag2`, `max_lag7`) dan rolling mean (`max_rolling7`)

### Exploratory Data Analysis (EDA)
- Distribusi polutan
- Tren waktu harian dan musiman
- Korelasi antar polutan
- Visualisasi per stasiun pemantauan

### Modeling
- **XGBoost**: Prediksi ISPU maksimum berdasarkan fitur numerik
- **SARIMAX**: Prediksi time-series dengan dukungan variabel eksternal

---

## Evaluasi Model

| Model     | MAE   | RMSE  | R²    |
|-----------|-------|-------|-------|
| XGBoost   | 3.87  | 5.71  | 0.90  |
| SARIMAX   | 3.51  | 4.83  | 0.93  |

SARIMAX memiliki performa yang lebih baik dalam menangkap pola fluktuasi ISPU.

---

## Fitur Paling Berpengaruh (XGBoost)
1. **pm25** – partikel halus paling berbahaya
2. **pm10**
3. **no2**

## Kesimpulan

- Model **SARIMAX** menunjukkan performa terbaik dalam memprediksi nilai ISPU di Jakarta dibandingkan model XGBoost.
- Berdasarkan metrik evaluasi:
  - **MAE**: 3.51
  - **RMSE**: 4.83
  - **R²**: 0.93
- Fitur polutan yang paling berpengaruh dalam prediksi kualitas udara adalah:
  - **PM2.5** – partikulat halus yang paling berbahaya
  - **PM10**
  - **NO2**
- Polusi udara di Jakarta memiliki tren musiman yang kuat, dengan konsentrasi tinggi pada pertengahan tahun.
- Pre

## Saran dari saya

- Integrasikan **data cuaca** (suhu, kelembaban, kecepatan angin) dan **aktivitas industri** sebagai variabel eksternal untuk meningkatkan akurasi prediksi.
- Gunakan **model SARIMAX** sebagai baseline untuk prediksi jangka pendek ISPU dan perluas dengan pendekatan deep learning seperti **LSTM** untuk prediksi jangka panjang.
- Lakukan **pengawasan intensif terhadap emisi PM2.5, NO2, dan PM10**, terutama dari kendaraan bermotor dan sektor industri.
- Buat sistem **dashboard visual** atau **peringatan dini real-time** untuk memberikan informasi prediktif kepada masyarakat dan pengambil kebijakan.
- Terapkan hasil prediksi sebagai dasar dalam **kebijakan pembatasan aktivitas** (seperti car-free day atau pengendalian industri) saat kualitas udara diperkirakan memburuk.
