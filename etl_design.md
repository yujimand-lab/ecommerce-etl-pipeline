# ETL Pipeline Design: E-Commerce Orders

## 1. Overview

Pipeline ETL ini dirancang untuk memproses data transaksi e-commerce secara otomatis setiap hari. Proses dimulai dengan mengambil data mentah (Extract), kemudian membersihkan dan memvalidasi data (Transform & Validate), menyimpan hasil data bersih (Load), membuat ringkasan laporan (Report), dan mengirimkan notifikasi ketika seluruh proses selesai (Notify).

Pipeline ini dibuat menggunakan Python dan dirancang agar dapat diorkestrasi menggunakan Apache Airflow.

---

# 2. Extract

### Sumber Data
Pipeline membaca data dari dua file CSV:

- `raw_orders.csv` → berisi data transaksi pelanggan.
- `raw_products.csv` → berisi informasi produk.

### Format Data

CSV (Comma Separated Values)

### Volume Data

Dataset berskala kecil (puluhan hingga ratusan baris) sebagai simulasi pipeline ETL.

### Tujuan Extract

Mengambil seluruh data mentah yang nantinya akan diproses pada tahap transformasi.

---

# 3. Transform

Tahapan transformasi dilakukan untuk meningkatkan kualitas data sebelum digunakan.

### Langkah Transformasi

### 1. Menghapus data duplikat

Menghindari perhitungan transaksi yang berulang sehingga hasil analisis lebih akurat.

### 2. Menangani missing value

Kolom yang memiliki nilai kosong diperbaiki menggunakan nilai default atau metode imputasi agar data tetap lengkap.

### 3. Mengubah tipe data

Kolom tanggal dikonversi menjadi format datetime dan kolom numerik diubah menjadi tipe data numerik agar dapat diproses dengan benar.

### 4. Menggabungkan data

Data transaksi digabungkan dengan data produk berdasarkan Product ID sehingga informasi menjadi lebih lengkap.

### 5. Membuat kolom turunan

Menambahkan informasi seperti total transaksi atau atribut lain yang diperlukan untuk analisis.

### 6. Validasi kualitas data

Pipeline memastikan:

- Tidak ada nilai kosong yang penting.
- Tidak ada data duplikat.
- Jumlah record sesuai.
- Format data valid.

---

# 4. Load

### Tujuan Penyimpanan

Hasil transformasi disimpan dalam bentuk file CSV.

### Output

- `orders_clean.csv`
  
  Berisi data transaksi yang sudah dibersihkan.

- `summary_report.csv`

  Berisi ringkasan hasil ETL seperti jumlah transaksi, total penjualan, dan metrik lainnya.

---

# 5. Orchestration

Pipeline diorkestrasi menggunakan **Apache Airflow**.

### Schedule

```
0 6 * * *
```

Pipeline dijalankan setiap hari pada pukul **06.00**.

### DAG Flow

```
Start
   │
   ▼
Extract
   │
   ▼
Transform
   │
   ▼
Validate
   │
   ▼
Load
   │
   ▼
Report
   │
   ▼
Notify
   │
   ▼
End
```

### Konfigurasi DAG

- Schedule : Daily (06:00)
- Retries : 3 kali
- Retry Delay : 5 menit
- Email on Failure : Aktif
- Catchup : False

---

# 6. Error Handling

Pipeline memiliki mekanisme penanganan error untuk meningkatkan keandalan proses.

### Skenario 1

File sumber tidak ditemukan.

**Penanganan**

- Pipeline mencatat error ke log.
- Melakukan retry hingga 3 kali.
- Mengirim email notifikasi jika tetap gagal.

### Skenario 2

Data tidak valid (missing value berlebihan atau format salah).

**Penanganan**

- Pipeline menghentikan proses.
- Error dicatat pada log.
- Tim mendapatkan notifikasi.

### Skenario 3

Proses transformasi gagal.

**Penanganan**

- Retry otomatis.
- Pipeline tidak melanjutkan ke proses Load sehingga mencegah data yang salah masuk ke output.

---

# 7. Monitoring

Monitoring dilakukan menggunakan log pipeline dan notifikasi.

### Indikator Pipeline Berhasil

- Semua task berstatus **Success**.
- File `orders_clean.csv` berhasil dibuat.
- File `summary_report.csv` berhasil dibuat.
- Log menunjukkan status **Pipeline Completed**.

### Indikator Data Berkualitas

- Tidak ada missing value.
- Tidak ada data duplikat.
- Format data sudah sesuai.
- Jumlah record sesuai hasil validasi.

---

# Kesimpulan

Pipeline ETL ini menerapkan proses Extract, Transform, Load, serta validasi kualitas data secara otomatis. Dengan menggunakan Apache Airflow sebagai orchestrator, pipeline dapat dijalankan secara terjadwal, memiliki mekanisme retry ketika terjadi kegagalan, dan menyediakan monitoring melalui log serta notifikasi sehingga proses pengolahan data menjadi lebih andal dan mudah dipelihara.