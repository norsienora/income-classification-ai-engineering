# Data

Folder ini sengaja tidak menyertakan dataset mentah karena izin redistribusinya tidak dinyatakan secara eksplisit.

Untuk menjalankan notebook, letakkan file berikut di folder ini:

```text
data/
├── train.csv
├── test.csv
└── sample_submission.csv
```

Struktur yang diharapkan:

- `train.csv`: 14 fitur prediktor dan target `income`.
- `test.csv`: kolom `id` dan 14 fitur prediktor.
- `sample_submission.csv`: kolom `id` dan `income`.

File CSV di folder ini diabaikan oleh Git melalui `.gitignore`.
