# Technical Report Summary

## Tujuan

Membangun model klasifikasi biner untuk memprediksi kategori pendapatan tahunan `<=50K` atau `>50K` dari 14 fitur demografis dan pekerjaan.

## Data dan kualitas data

Data train memiliki 39.073 observasi dengan distribusi target 76,07% `<=50K` dan 23,93% `>50K`. Nilai kategorikal tidak valid ditemukan pada:

| Fitur | Jumlah tidak valid | Persentase |
|---|---:|---:|
| `workclass` | 2.233 | 5,71% |
| `occupation` | 2.241 | 5,74% |
| `native-country` | 688 | 1,76% |

Nilai null, string kosong, dan `?` dinormalisasi menjadi kategori `Unknown`.

## Feature engineering

Lima fitur ditambahkan: `capital-balance`, `has-capital-gain`, `has-capital-loss`, `is-married`, dan `is-us`. Jumlah fitur meningkat dari 14 menjadi 19, terdiri atas delapan fitur kategorikal dan sebelas fitur numerik.

## Eksperimen

Lima kandidat model diuji menggunakan Stratified 5-Fold Cross-Validation dan prediksi out-of-fold:

- Dummy Classifier
- Logistic Regression
- Random Forest
- HistGradientBoosting dengan ordinal encoding
- HistGradientBoosting dengan target encoding

Dua ensemble turut dibandingkan. Threshold probabilitas diuji pada rentang 0,200–0,700 dengan interval 0,002 dan dipilih berdasarkan F1-macro OOF.

## Model final

Model final adalah ensemble 50% HistGradientBoosting ordinal dan 50% HistGradientBoosting target encoding pada threshold 0,450.

| Metrik OOF | Nilai |
|---|---:|
| F1-macro | 0,8199 |
| ROC-AUC | 0,9283 |
| Accuracy | 0,8714 |
| Balanced accuracy | 0,8140 |

Confusion matrix OOF:

| | Prediksi `<=50K` | Prediksi `>50K` |
|---|---:|---:|
| Aktual `<=50K` | 27.465 | 2.259 |
| Aktual `>50K` | 2.767 | 6.582 |

## Submission

File final memiliki 9.769 baris, urutan ID yang sama dengan data test, tanpa nilai kosong atau kolom indeks tambahan. Distribusi prediksi adalah 7.605 label `<=50K` dan 2.164 label `>50K`. Skor evaluasi eksternal yang tercatat adalah 0,824224.

## Insight

- `education-num` memiliki korelasi numerik tertinggi dengan target, yaitu 0,3354.
- `Exec-managerial` memiliki proporsi pendapatan `>50K` tertinggi di antara occupation, sebesar 47,25%.
- `Prof-school` memiliki proporsi pendapatan `>50K` tertinggi di antara tingkat pendidikan, sebesar 74,92%.
- Hubungan tersebut bersifat deskriptif dan tidak membuktikan kausalitas.

## Keterbatasan

Eksperimen belum menggunakan tuning hyperparameter yang ekstensif, repeated/nested cross-validation, atau probability calibration. Karena terdapat atribut sensitif, penggunaan di dunia nyata membutuhkan audit fairness dan validasi tambahan.
