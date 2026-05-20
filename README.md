# Watermarking

 Nama: Zahra Zahidah Putri Ruchwijaya
 NIM: 18224058


### Alur Kerja
```
EMBED:  Citra Asli → DCT → Sisipkan Watermark di koefisien DCT → IDCT → Citra Watermarked
        Citra Watermarked → Kompresi JPEG (QF berbeda) → Citra Terkompresi
EXTRACT: Citra Terkompresi → DCT → Ekstrak koefisien → Bandingkan dengan original → Watermark
```

# Bagian 1: Menyiapkan Foto Asli
Mengubah foto asli menjadi grayscale dan pixelnya 256x256. Hal ini dilakukan agar proses penyisipan informasi tersembunyi menjadi lebih ringan secara komputasi dan lebih mudah diimplementasikan. Perubahan kecil pada nilai piksel grayscale cenderung tidak mudah terdeteksi oleh mata manusia sehingga watermark yang disisipkan tetap tersembunyi namun masih bisa diekstrak kembali.

<img width="661" height="641" alt="image" src="https://github.com/user-attachments/assets/340e1309-bc63-459a-be79-e480abdf7c69" />


# Bagian 2: Membuat Watermark
Pada bagian ini dibuat dua jenis watermark yang direpresentasikan dalam nilai biner +1 dan -1, di mana merah melambangkan +1 dan biru melambangkan -1. Watermark pertama adalah Binary Watermark yang dibentuk dari pola inisial "WM" secara visual, artinya piksel diatur secara terstruktur mengikuti bentuk huruf sehingga menghasilkan pola yang bermakna dan bisa dikenali. Watermark kedua adalah Random Watermark yang dibangkitkan secara acak menggunakan seed=2024 sehingga polanya tersebar tidak beraturan di seluruh blok citra.

<img width="1256" height="508" alt="image" src="https://github.com/user-attachments/assets/99caa82f-fad4-4c6c-a63b-4ec06f9858c3" />


# Bagian 3: Menyisipkan Watermark
Pada bagian ini, kedua watermark yang telah dibuat sebelumnya disisipkan ke dalam foto grayscale asli, dan hasilnya dibandingkan secara visual maupun kuantitatif. Secara visual, foto yang telah disisipi watermark baik binary maupun random tampak identik dengan foto aslinya, yang membuktikan bahwa proses watermarking berhasil dilakukan secara imperceptible (tidak kasat mata).

<img width="1067" height="722" alt="image" src="https://github.com/user-attachments/assets/46c747a3-9268-4414-94b6-49fc3ae0e263" />





# Bagian 4: Kompresi dengan QF yang berbeda beda
Pada bagian ini dilakukan pengujian ketahanan watermark terhadap kompresi JPEG dengan berbagai nilai Quality Factor (QF).


<img width="1245" height="542" alt="image" src="https://github.com/user-attachments/assets/4db5ab1d-724a-426d-9f47-2df49cf04f62" />
<img width="1237" height="682" alt="image" src="https://github.com/user-attachments/assets/71e26aed-780a-476b-a4dc-5abd25156c6b" />



Evaluasi Ketahanan Berbagai Quality Factor
---------------------------------------------------------------------------
| QF | PSNR Img | Binary BER | Binary NC | Rand BER | Rand NC |
|---|---|---|---|---|---|
| 95 | 46.5 dB | 0.0000 ✅ | 1.0000 | 0.0000 ✅ | 1.0000 |
| 90 | 43.3 dB | 0.0000 ✅ | 1.0000 | 0.0000 ✅ | 1.0000 |
| 80 | 40.1 dB | 0.0000 ✅ | 1.0000 | 0.0000 ✅ | 1.0000 |
| 70 | 38.3 dB | 0.0000 ✅ | 1.0000 | 0.0000 ✅ | 1.0000 |
| 60 | 36.9 dB | 0.0000 ✅ | 1.0000 | 0.0000 ✅ | 1.0000 |
| 50 | 36.0 dB | 0.0000 ✅ | 1.0000 | 0.0000 ✅ | 1.0000 |
| 40 | 35.1 dB | 0.0000 ✅ | 1.0000 | 0.0000 ✅ | 1.0000 |
| 30 | 34.0 dB | 0.0000 ✅ | 1.0000 | 0.0000 ✅ | 1.0000 |
| 20 | 32.3 dB | 0.2920 ❌ | 0.4160 | 0.3096 ❌ | 0.3809 |
| 10 | 29.8 dB | 0.4424 ❌ | 0.1152 | 0.4775 ❌ | 0.0449 |
| 5  | 26.9 dB | 0.4697 ❌ | 0.0605 | 0.4922 ❌ | 0.0156 |

> ✅ = watermark TERDETEKSI (NC > 0.5) &nbsp;&nbsp; ❌ = watermark GAGAL DIEKSTRAK


<img width="946" height="736" alt="image" src="https://github.com/user-attachments/assets/06387dd1-c0e9-4ad8-80d4-f830d5502d0d" />





# Mengapa Watermark bisa hilang?
Bagian ini menjelaskan secara teknis mengapa watermark hilang saat kompresi JPEG dengan QF rendah. Semakin kecil nilai QF, semakin besar nilai tabel kuantisasi yang digunakan sebagai pembagi koefisien DCT, sehingga koefisien yang menyimpan informasi watermark ikut dibulatkan menjadi 0 dan informasi pun hilang. Hal ini terbukti dari koefisien di posisi (2,1) yang berubah dari nilai 18 pada QF=95 menjadi 0 pada QF=5, serta proporsi koefisien bernilai 0 yang meningkat dari 71.9% hingga 95.9%. Dengan kekuatan alpha=15.0, watermark mulai gagal ketika nilai tabel kuantisasi melampaui angka tersebut karena round(coef/qt) akan menghasilkan 0 dan informasi watermark tidak bisa dipulihkan.

<img width="1472" height="632" alt="image" src="https://github.com/user-attachments/assets/c9076f6c-40f9-4890-8f47-10b488e569f6" />


