<<<<<<< HEAD
# RET503 Praktik Terpadu Minggu 4-7: Detektor YOLO (person, cup, laptop)

**NIM / Nama:** 4222401035 / MARIANA LUBIS

## Data
- Sumber: subset COCO val2017 (program 00), kelas pilihan: `person`, `cup`, `laptop`; 200 gambar berobjek + gambar latar 10%.
- Jumlah kotak per kelas: {'person': 679, 'cup': 50, 'laptop': 19}. Kelas paling sedikit: `laptop`.
- Pembagian 70/20/10 (seed 42): train 154, val 44, test 22 gambar.

## Pengaturan
Model yolo26n, epochs 30, imgsz 416, batch 16, seed 0. E3: satu perubahan `imgsz=640`.

## Hasil (data val)
| eksperimen    | perubahan   | pretrained   |   mAP50 |   mAP50-95 |   precision |   recall |   inferensi_ms |   waktu_latih_menit |   imgsz |
|:--------------|:------------|:-------------|--------:|-----------:|------------:|---------:|---------------:|--------------------:|--------:|
| E1_pretrained | -           | True         |  0.6048 |     0.3532 |      0.6295 |   0.6031 |           6.24 |                1.63 |     416 |
| E2_scratch    | -           | False        |  0.005  |     0.0015 |      0.6821 |   0.0453 |           4.23 |                1.31 |     416 |
| E3_tuning     | imgsz=640   | True         |  0.6758 |     0.4674 |      0.8648 |   0.5978 |           8.19 |                1.65 |     640 |

Model terpilih (mAP50-95 val tertinggi): **E3_tuning**.
Hasil di data TEST (sekali saja)       : mAP50 0.783 | mAP50-95 0.624

Grafik: `perbandingan_E1_E2_E3.png`, `E1_pretrained/results.png`, `E2_scratch/results.png`, `E3_tuning/results.png`.

## Analisis
- **Transfer learning (E1 vs E2):** E1 (pretrained) lebih tinggi dari E2 (dari nol) (mAP50-95 val 0.353 vs 0.002, selisih +0.352). Bobot COCO membawa pengetahuan tepi, tekstur, dan bentuk sehingga model cukup menyesuaikan head ke jumlah kelas kita.
- **Tuning (E1 vs E3):** E3 (imgsz=640) lebih baik dari E1, sehingga perubahan **dipertahankan** (mAP50-95 val 0.353 menjadi 0.467, selisih +0.114; waktu inferensi 6.24 ms menjadi 8.19 ms per gambar).
- **Ketidakseimbangan kelas:** *(tulis sendiri: apakah kelas `laptop` lebih lemah dari kelas lain pada tabel per kelas dan confusion matrix.)*
- **Kecepatan vs akurasi:** *(tulis sendiri: apakah kenaikan akurasi sepadan dengan perlambatan.)*

## Catatan kehati-hatian
- Dataset kecil (220 gambar; val 44, test 22). Selisih mAP yang kecil antar-eksperimen bisa hanya kebetulan.
- Data test hanya dipakai satu kali, setelah model dipilih berdasarkan val.
=======
# RET503-Pj1-YOLO
PROJEK 1
>>>>>>> 8e66a62cf8f058b92e8656430f05698bef465f68
