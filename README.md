# Income Classification — AI Engineering Study Case

Proyek machine learning untuk memprediksi apakah pendapatan tahunan seorang individu berada pada kategori `<=50K` atau `>50K` berdasarkan karakteristik demografis dan pekerjaan.

## Ringkasan hasil

- Data train: 39.073 observasi
- Data test: 9.769 observasi
- Model final: ensemble 50% HistGradientBoosting ordinal dan 50% HistGradientBoosting target encoding
- Validasi: Stratified 5-Fold Cross-Validation dengan prediksi out-of-fold
- Threshold optimal: 0,450
- F1-macro OOF: 0,8199
- ROC-AUC OOF: 0,9283
- Accuracy OOF: 0,8714
- Balanced accuracy OOF: 0,8140
- Skor evaluasi eksternal: 0,824224

## Metodologi

1. Audit struktur dan kualitas data.
2. Normalisasi target serta kategori null, kosong, dan `?`.
3. Exploratory Data Analysis untuk fitur numerik dan kategorikal.
4. Feature engineering:
   - `capital-balance`
   - `has-capital-gain`
   - `has-capital-loss`
   - `is-married`
   - `is-us`
5. Perbandingan lima model dasar dan dua ensemble.
6. Optimasi threshold berdasarkan F1-macro OOF.
7. Pelatihan ulang model final pada seluruh data train.
8. Validasi format file submission.

## Struktur repositori

```text
.
├── README.md
├── requirements.txt
├── notebooks/
│   └── income_classification.ipynb
├── docs/
│   ├── ai-usage-declaration.md
│   └── technical-report-summary.md
├── data/
│   └── README.md
└── outputs/
    └── README.md
```

Dataset mentah, dokumen soal, dan file submission tidak disertakan karena hak redistribusinya tidak dinyatakan secara eksplisit. Petunjuk penempatan data tersedia di [`data/README.md`](data/README.md).

## Menjalankan notebook

1. Clone repositori dan masuk ke direktori proyek.
2. Buat virtual environment.
3. Instal dependensi:

   ```bash
   python -m pip install -r requirements.txt
   ```

4. Tempatkan `train.csv`, `test.csv`, dan `sample_submission.csv` di folder `data/`.
5. Jalankan Jupyter:

   ```bash
   jupyter lab
   ```

6. Buka `notebooks/income_classification.ipynb`. Jika notebook dijalankan dari folder `notebooks/`, sesuaikan `DATA_DIR` menjadi `Path("../data")`.

Notebook menyimpan output eksperimen yang sudah dijalankan agar hasil utama tetap dapat ditinjau tanpa dataset.

## Catatan evaluasi

Metrik OOF berasal dari data train dan digunakan untuk pemilihan model. Skor 0,824224 berasal dari sistem evaluasi eksternal, sehingga keduanya tidak boleh dibandingkan sebagai pengukuran pada sampel yang sama.

## Penggunaan AI

ChatGPT/Codex digunakan sebagai alat bantu untuk memahami ketentuan, menyusun struktur analisis, memperbaiki kode, melakukan debugging, dan membantu dokumentasi. Seluruh kode dijalankan, ditinjau, dan diverifikasi kembali oleh penulis. Rincian tersedia di [`docs/ai-usage-declaration.md`](docs/ai-usage-declaration.md).

## Pertimbangan etis

Dataset memuat atribut sensitif seperti `sex` dan `race`. Model ini dibuat untuk studi pembelajaran dan tidak boleh digunakan langsung untuk keputusan berdampak tinggi tanpa audit fairness, validasi tambahan, pengawasan manusia, dan kepatuhan terhadap regulasi.

## Lisensi dan penggunaan ulang

Belum ada lisensi penggunaan ulang yang diberikan untuk kode atau konten proyek ini. Dataset mengikuti ketentuan dari penyedia aslinya.
