# Dokumentasi Analisis Nutrisi Menu

Dokumen ini menjelaskan cara menyiapkan dan menjalankan notebook analisis nutrisi menu, fungsi pustaka yang digunakan, serta alur analisisnya.

## Gambaran umum

Program membaca data nutrisi dari `menu.csv` dan menganalisis hubungan antara jumlah karbohidrat dan kalori pada setiap menu. Analisis dilakukan di Jupyter Notebook, sehingga kode dan hasilnya dapat dijalankan serta dilihat per langkah.

Data yang tersedia berisi 18 menu, 24 kolom, dan 6 kategori: Breakfast, Chicken, Beef, Sides, Dessert, dan Beverages. Kolom yang digunakan langsung oleh analisis utama adalah:

- `Category`: kategori menu.
- `Item`: nama menu.
- `Carbohydrates`: jumlah karbohidrat.
- `Calories`: jumlah kalori.

Kolom nutrisi lainnya tetap tersedia di CSV, tetapi tidak digunakan dalam analisis hubungan yang dibuat saat ini.

## Isi proyek

```text
.
├── maman12345.ipynb  # Notebook analisis
├── menu.csv          # Data nutrisi menu
├── requirements.txt  # Dependensi Python
└── README.md         # Dokumentasi ini
```

Pastikan `maman12345.ipynb` dan `menu.csv` berada di folder yang sama. Notebook membaca CSV dengan nama relatif `menu.csv`.

## Persyaratan

- Python 3
- Jupyter Notebook
- Dependensi Python tercantum di `requirements.txt` (Jupyter Notebook, `pandas`, `matplotlib`, dan `scipy`)

## Memasang dependensi

Buka terminal pada folder proyek (folder yang berisi `requirements.txt`), lalu jalankan:

```bash
pip install -r requirements.txt
```

Perintah tersebut akan memasang semua pustaka yang tercantum di `requirements.txt`. Jika menggunakan virtual environment, aktifkan terlebih dahulu sebelum menjalankan perintah ini.

## Setup dan menjalankan secara lokal

Buka PowerShell atau terminal pada folder proyek, lalu jalankan:

1. Buat virtual environment:

   ```powershell
   python -m venv .venv
   ```

2. Aktifkan virtual environment di PowerShell:

   ```powershell
   .\.venv\Scripts\Activate.ps1
   ```

   Jika PowerShell menolak menjalankan skrip aktivasi, jalankan perintah berikut hanya untuk jendela terminal saat ini, lalu ulangi aktivasi:

   ```powershell
   Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
   .\.venv\Scripts\Activate.ps1
   ```

3. Pasang semua dependensi:

   ```powershell
   python -m pip install --upgrade pip
   python -m pip install -r requirements.txt
   ```

4. Jalankan Jupyter Notebook:

   ```powershell
   python -m notebook
   ```

5. Di halaman Jupyter yang terbuka di browser, buka `maman12345.ipynb`.
6. Jalankan sel satu per satu menggunakan **Shift+Enter**, atau pilih **Run All** untuk menjalankan seluruh notebook.

Saat notebook berjalan, direktori kerja Jupyter harus merupakan folder yang berisi `menu.csv`. Jika muncul `FileNotFoundError`, pastikan file tersebut ada di folder yang sama dan Jupyter dibuka dari folder proyek.

### Menjalankan di VS Code

1. Buka folder proyek di VS Code.
2. Pastikan ekstensi **Python** dan **Jupyter** tersedia.
3. Buka `maman12345.ipynb` dan pilih kernel Python yang ingin dipakai. Sel pertama notebook menjalankan `%pip install -r requirements.txt` pada kernel aktif, sehingga dependensi dipasang ke environment yang benar. Pastikan terminal kerja/notebook berada di folder proyek agar `requirements.txt` dan `menu.csv` dapat ditemukan.
4. Jalankan sel dengan tombol **Run Cell** atau **Shift+Enter**.

### Menjalankan di Google Colab

Notebook memiliki metadata Google Colab. Unggah `maman12345.ipynb`, `menu.csv`, dan `requirements.txt` ke sesi Colab yang sama, lalu jalankan sel pertama untuk memasang dependensi ke runtime aktif sebelum menjalankan analisis.

Pastikan file CSV berada pada direktori kerja runtime (biasanya `/content`) dan namanya tetap `menu.csv`, karena notebook menggunakan path relatif tersebut.

## Penjelasan pustaka

- **pandas (`pd`)**: membaca CSV menjadi DataFrame, menampilkan data, memeriksa tipe data, menghitung statistik, dan memilih kolom.
- **matplotlib.pyplot (`plt`)**: membuat grafik scatter dan menggambar garis regresi.
- **scipy.stats (`stats`)**: menyediakan `linregress` untuk menghitung model regresi linear dan nilai statistik terkait.
- **Fungsi bawaan Python**: `map` menerapkan fungsi ke nilai-nilai karbohidrat dan `list` mengubah hasilnya menjadi daftar untuk digambar.

## Alur program

1. **Contoh operasi dasar** — sel pertama menjumlahkan `x = 30` dan `y = 20` sebagai contoh sederhana; bagian ini tidak terkait dengan data menu.
2. **Memuat data** — `pd.read_csv('menu.csv')` membaca CSV ke variabel `df`.
3. **Memeriksa data** — `df.head()`, `df.head(10)`, dan `df.tail()` menampilkan baris data; `df.info()` menunjukkan jumlah data dan tipe kolom; `df.describe()` merangkum kolom numerik.
4. **Menghitung kalori** — `df['Calories'].mean()` menghitung rata-rata kalori dan `df['Calories'].max()` mencari nilai kalori tertinggi.
5. **Membandingkan karbohidrat dan kalori** — notebook membuat scatter plot dengan karbohidrat pada sumbu X dan kalori pada sumbu Y.
6. **Menghitung regresi linear** — `stats.linregress(x, y)` menghasilkan kemiringan (`m`), intersep (`c`), korelasi (`r`), p-value, dan standard error. Model garisnya adalah `y = m*x + c`.
7. **Menggambar garis model dan menafsirkan korelasi** — garis merah ditambahkan ke scatter plot. Nilai absolut `r` dipetakan ke label kekuatan hubungan (sangat lemah hingga sangat kuat), dan tanda `r` menentukan arah hubungan.

## Hasil acuan

Dengan versi data yang disertakan:

- Rata-rata kalori: sekitar **316,11**.
- Kalori tertinggi: **650**.
- Korelasi karbohidrat dengan kalori (`r`): sekitar **0,569**, yaitu hubungan linear **positif dan sedang** menurut ambang batas yang ditulis di notebook.
- Persamaan garis hasil regresi: sekitar `kalori = 8,117 × karbohidrat + 19,406`.

Hasil dapat berubah jika isi `menu.csv` diganti.

## Catatan interpretasi

- Korelasi menunjukkan arah dan kekuatan hubungan linear pada data ini; korelasi **tidak membuktikan hubungan sebab-akibat**.
- Dataset hanya mencakup 18 menu, sehingga hasil sebaiknya dipahami sebagai analisis data yang tersedia, bukan kesimpulan umum tentang semua makanan.
- Notebook menghitung prediksi untuk karbohidrat sebesar 100. Nilai karbohidrat pada data yang tersedia hanya berkisar dari 15 sampai 50, sehingga prediksi pada 100 merupakan **ekstrapolasi** dan tidak sebaiknya dianggap sebagai estimasi yang andal.
- Walaupun `linregress` menghasilkan p-value dan standard error, notebook saat ini tidak menampilkan atau membahas keduanya.

## Pemecahan masalah

| Masalah | Solusi |
|---|---|
| `ModuleNotFoundError` untuk pandas, matplotlib, atau scipy | Aktifkan virtual environment proyek dan jalankan perintah instalasi pada bagian setup. |
| `FileNotFoundError: menu.csv` | Letakkan CSV di direktori kerja notebook dan pastikan nama file tepat `menu.csv`. |
| Kernel tidak menemukan pustaka setelah instalasi | Pilih kernel/interpreter yang sama dengan virtual environment tempat pustaka dipasang, lalu mulai ulang kernel. |
