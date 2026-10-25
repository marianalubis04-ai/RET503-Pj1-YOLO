# RET503 Praktik Minggu 4-7: Detektor YOLO (person, cup, laptop)

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
- **Transfer learning (E1 vs E2):** E1 menggunakan pretrained model dan memperoleh mAP50-95 sebesar 0.3532, sedangkan E2 yang dilatih dari awal hanya memperoleh 0.0015. Nilai recall E1 juga lebih tinggi, yaitu 0.6031 dibandingkan 0.0453 pada E2. Perbedaan ini menunjukkan bahwa pretrained model memberikan hasil yang jauh lebih baik pada eksperimen ini. Model yang sudah memiliki bobot hasil pelatihan sebelumnya dapat dimanfaatkan untuk membantu proses deteksi objek.
- **Tuning (E1 vs E3):** Pada E3, ukuran gambar diubah dari 416 menjadi 640. Hasilnya, mAP50-95 meningkat dari 0.3532 menjadi 0.4674, sedangkan mAP50 meningkat dari 0.6048 menjadi 0.6758. Nilai precision juga naik dari 0.6295 menjadi 0.8648, tetapi recall sedikit turun dari 0.6031 menjadi 0.5978. Dengan hasil tersebut, perubahan ukuran gambar memberikan peningkatan pada beberapa metrik evaluasi. E3 dipilih sebagai model terbaik karena memiliki nilai mAP50-95 tertinggi di antara ketiga eksperimen.
- **Kecepatan vs akurasi:** Waktu inferensi E1 adalah 6.24 ms per gambar, sedangkan E3 membutuhkan 8.19 ms. Artinya, E3 membutuhkan tambahan waktu sekitar 1.95 ms per gambar, dengan peningkatan mAP50-95 sebesar 0.1142. Dalam eksperimen ini, E3 lebih sesuai jika prioritasnya adalah memperoleh hasil deteksi yang lebih baik, sedangkan E1 memiliki keunggulan dari sisi kecepatan inferensi.


