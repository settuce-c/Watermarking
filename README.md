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
Mengubah foto asli menjadi grayscale
<img width="661" height="641" alt="image" src="https://github.com/user-attachments/assets/340e1309-bc63-459a-be79-e480abdf7c69" />

# Bagian 2: Membuat Watermark
Watermark yang dibuat polanya WM. 
<img width="1256" height="508" alt="image" src="https://github.com/user-attachments/assets/99caa82f-fad4-4c6c-a63b-4ec06f9858c3" />

# Bagian 3: Menyisipkan Watermark
Menyisipkan watermark ke foto asli tadi kita yang udah jadi grayscale
<img width="1067" height="722" alt="image" src="https://github.com/user-attachments/assets/46c747a3-9268-4414-94b6-49fc3ae0e263" />

# Bagian 4: Kompresi dengan QF yang berbeda beda
<img width="1245" height="542" alt="image" src="https://github.com/user-attachments/assets/4db5ab1d-724a-426d-9f47-2df49cf04f62" />
<img width="1237" height="682" alt="image" src="https://github.com/user-attachments/assets/71e26aed-780a-476b-a4dc-5abd25156c6b" />


