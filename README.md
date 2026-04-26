# Prediksi Harga Saham dengan ARIMA dan LSTM

## Deskripsi Proyek
Proyek ini bertujuan untuk memprediksi harga saham (khususnya Apple) menggunakan model Time Series Forecasting yaitu ARIMA dan LSTM. Selain itu, proyek ini juga mencakup ekstraksi data sentimen melalui web scraping untuk mendukung dan melengkapi analisis prediksi.

## Lingkungan Virtual (Virtual Environments)
Karena adanya kebutuhan library yang spesifik dan kompatibilitas dependensi, proyek ini menggunakan dua *virtual environment* terpisah:

1. **`venv` (Python 3.12.4)**
   - **Fungsi:** Digunakan khusus untuk kode scraping sentimen (`Scraping Sentiment.ipynb`).
   - **Alasan:** Versi Python terbaru dioptimalkan untuk menjalankan library web scraping dan automasi (seperti Selenium) dengan performa maksimal.

2. **`venv310` (Python 3.10.0)**
   - **Fungsi:** Digunakan untuk modeling dan evaluasi, meliputi `ARIMA`, `ARIMA 30 RUN`, `ARIMA Ablation`, `LSTM`, `LSTM 30 RUN`, `LSTM Ablation`, serta *generate* visualisasi (`generate visuals ARIMA.ipynb` & `generate visuals LSTM.ipynb`).
   - **Alasan:** Python 3.10.0 sangat stabil dan kompatibel secara penuh dengan *library* Machine Learning & Deep Learning berat seperti TensorFlow/Keras, scikit-learn, dan statsmodels tanpa *issue* dependensi.

## Daftar File & Modul Saat Ini
- **Data Collection (Scraping):**
  - `Scraping Sentiment.ipynb`
  - `selenium-twitter-scraper/` (Modul pendukung)
- **Modeling (ARIMA):**
  - `ARIMA - Apple.ipynb`
  - `ARIMA 30 RUN - Apple.ipynb` (Untuk validasi robustness)
  - `ARIMA Ablation - Apple.ipynb` (Untuk studi ablasi parameter/fitur)
- **Modeling (LSTM):**
  - `LSTM - Apple.ipynb`
  - `LSTM 30 RUN - Apple.ipynb` (Untuk validasi robustness)
  - `LSTM Ablation - Apple.ipynb` (Untuk studi ablasi parameter/fitur)
- **Visualisasi & Analisis:**
  - `generate visuals ARIMA.ipynb`
  - `generate visuals LSTM.ipynb`
  - File *output*: `.pdf` dan `.png` resolusi tinggi
- **Output & Penyimpanan (Artifacts):**
  - `export_arima_results/` & `export_lstm_results/`
  - `saved_models_arima/` & `saved_models_lstm/`
  - `saved_sentiment_scraping/`

## Dependensi dan Requirements Masing-Masing Environment

Proyek ini memiliki dua set *library* utama yang dipisah untuk menghindari bentrok versi (*dependency conflicts*) antara modul *scraping* dan modul *machine learning*.

### 1. `venv` (Python 3.12.4) - Khusus Scraping Sentimen
Environment ini difokuskan pada pengumpulan data mentah dan analisis bahasa natural (NLP). Dependensi utamanya meliputi:
- `snscrape` / `selenium` / `beautifulsoup4` : Digunakan sebagai alat utama ekstraksi atau penarikan data dari situs web maupun media sosial.
- `vaderSentiment` : Digunakan untuk menghasilkan skor sentimen (positif, negatif, netral) pada setiap kalimat teks yang sudah ditarik.
- `pandas` & `numpy` : Digunakan untuk merapikan teks mentah menjadi format tabel atau DataFrame sebelum diekspor.
- `requests` & `curl_cffi` : Untuk menangani koneksi web / HTTP request selama proses *scraping*.
- `notebook` / `jupyter` : Untuk mengeksekusi *cell* pada `Scraping Sentiment.ipynb`.

### 2. `venv310` (Python 3.10.0) - Khusus Machine Learning & Visualisasi
Environment ini memuat *library-library* berat yang membutuhkan kompatibilitas ketat dengan sistem operasi dan versi Python. Dependensi utamanya meliputi:
- `tensorflow` (termasuk Keras) : *Framework Deep Learning* utama untuk mendesain, melatih, dan mengevaluasi arsitektur jaringan saraf **LSTM**.
- `statsmodels` & `pmdarima` : *Library* untuk komputasi statistik yang digunakan untuk melatih model regresi runtun waktu **ARIMA** (serta pencarian hyperparameter *auto-ARIMA*).
- `scikit-learn` : Digunakan untuk preprocessing data harga saham (seperti `MinMaxScaler` untuk normalisasi) dan ekstraksi metrik evaluasi model (RMSE, MAE, dll).
- `yfinance` : Digunakan untuk mengunduh *dataset* pergerakan harga historis saham (contoh: Apple / AAPL) secara langsung via API Yahoo Finance.
- `matplotlib` & `seaborn` : *Library* plotting untuk menghasilkan visualisasi akhir (`.pdf` dan `.png`) terkait perbandingan harga asli vs prediksi ARIMA/LSTM.
- `pandas` & `numpy` : Untuk komputasi matematis vektor, matriks, dan *Time Series Data*.
- `notebook` / `jupyter` : Untuk menjalankan seluruh file `.ipynb` yang berhubungan dengan model dan visualisasi.
