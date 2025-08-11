# Project Fundamental SQL Using FUNCTION and GROUP BY
---
## Latar Belakang Proyek

Setelah menyelesaikan modul pelatihan dan latihan-latihan dengan baik, Aksara menerima tantangan baru dari Senja, atasannya di perusahaan. Senja memberikan proyek analisis penjualan sebagai bentuk kepercayaan atas perkembangan Aksara yang signifikan.

Walaupun proyek ini kadang membuat Aksara pulang lebih larut, ia menyadari bahwa ini adalah bentuk ajakan untuk berkontribusi lebih besar bagi perusahaan. Dengan semangat baru dan segelas boba milk tea favorit di tangan, Aksara membuka email berisi permintaan analisis penjualan dari Senja.

---
## Tujuan dan Permintaan Analisis
Senja meminta Aksara untuk melakukan analisis penjualan pada sebuah store dengan fokus pada metrik-metrik berikut:

1. Total jumlah seluruh penjualan (total/revenue).
2. Total quantity seluruh produk yang terjual.
3. Total quantity dan total revenue untuk setiap kode produk.
4. Rata - Rata total belanja per kode pelanggan.
5. Selain itu,  jangan lupa untuk menambahkan kolom baru dengan nama ‘kategori’ yang mengkategorikan total/revenue ke dalam 3 kategori: High: > 300K; Medium: 100K - 300K; Low: <100K.
---
## Dataset
Dataset tr_penjualan berisi data transaksi penjualan dari sebuah store yang digunakan untuk analisis bisnis.

Kolom	dan Deskripsi : 
- kode_transaksi	: Kode unik untuk setiap transaksi. Satu transaksi bisa memiliki beberapa item.
- kode_pelanggan :	Kode unik pelanggan yang melakukan transaksi.
- no_urut	: Nomor urut item dalam transaksi. Digunakan untuk mengidentifikasi urutan pembelian.
- kode_produk	: Kode unik produk yang dibeli.
- nama_produk	: Nama lengkap produk yang dibeli.
- qty	Jumlah : unit produk yang dibeli dalam baris tersebut.
- total	Total : nilai penjualan (dalam rupiah) untuk produk tersebut.

---
## Hasil Analisis

```
## 1. Total jumlah seluruh penjualan (total/revenue).
SELECT SUM(total) as total 
FROM tr_penjualan;
```
Output : 

| total   |
|---------|
| 3271600 |

```
## 2. Total quantity seluruh produk yang terjual.
SELECT SUM(qty) as qty 
FROM tr_penjualan;
```
Output : 

| qty  |
|------|
|   42 |

```
## 3. Total quantity dan total revenue untuk setiap kode produk.
SELECT kode_produk, SUM(qty) as qty, SUM(total) as total 
FROM tr_penjualan
GROUP BY kode_produk;
```

Output :

| kode_produk | qty  | total   |
|-------------|------|---------|
| prod-01     |    6 |  375000 |
| prod-02     |    2 |  110000 |
| prod-03     |    3 |  300000 |
| prod-04     |    9 |  360000 |
| prod-05     |    4 | 1000000 |
| prod-07     |    1 |   48000 |
| prod-08     |    2 |   31600 |
| prod-09     |    6 |  552000 |
| prod-10     |    9 |  495000 |

```
## 4. Rata - Rata total belanja per kode pelanggan.
SELECT kode_pelanggan, AVG(total) as avg_total 
FROM tr_penjualan
GROUP BY kode_pelanggan;
```
Output :

| kode_pelanggan | avg_total   |
|----------------|-------------|
| dqlabcust01    | 156000.0000 |
| dqlabcust02    | 515800.0000 |
| dqlabcust03    | 181666.6667 |
| dqlabcust05    | 139500.0000 |
| dqlabcust07    | 202125.0000 |

```
## 5. Selain itu,  jangan lupa untuk menambahkan kolom baru dengan nama ‘kategori’ yang mengkategorikan total/revenue ke dalam 3 kategori: High: > 300K; Medium: 100K - 300K; Low: <100K.
SELECT kode_transaksi,kode_pelanggan,no_urut,kode_produk, nama_produk, qty, total,
CASE  
    WHEN total > 300000 THEN 'High'
    WHEN total < 100000 THEN 'Low'   
    ELSE 'Medium'  
END as kategori 
FROM tr_penjualan;
```

Output :
| kode_transaksi | kode_pelanggan | no_urut | kode_produk | nama_produk                   | qty  | total   | kategori |
|----------------|----------------|---------|-------------|-------------------------------|------|---------|----------|
| tr-001         | dqlabcust07    |       1 | prod-01     | Kotak Pensil DQLab            |    5 | 312500  | High     |
| tr-001         | dqlabcust07    |       2 | prod-03     | Flash disk DQLab 32 GB        |    1 | 100000  | Medium   |
| tr-001         | dqlabcust07    |       3 | prod-09     | Buku Planner Agenda DQLab     |    3 | 276000  | Medium   |
| tr-001         | dqlabcust07    |       4 | prod-04     | Flashdisk DQLab 32 GB         |    3 | 120000  | Medium   |
| tr-002         | dqlabcust01    |       1 | prod-03     | Gift Voucher DQLab 100rb      |    2 | 200000  | Medium   |
| tr-002         | dqlabcust01    |       2 | prod-10     | Sticky Notes DQLab 500 sheets |    4 | 220000  | Medium   |
| tr-002         | dqlabcust01    |       3 | prod-07     | Tas Travel Organizer DQLab    |    1 | 48000   | Low      |
| tr-003         | dqlabcust03    |       1 | prod-02     | Flashdisk DQLab 64 GB         |    2 | 110000  | Medium   |
| tr-004         | dqlabcust03    |       1 | prod-10     | Sticky Notes DQLab 500 sheets |    5 | 275000  | Medium   |
| tr-004         | dqlabcust03    |       2 | prod-04     | Flashdisk DQLab 32 GB         |    4 | 160000  | Medium   |
| tr-005         | dqlabcust05    |       1 | prod-09     | Buku Planner Agenda DQLab     |    3 | 276000  | Medium   |
| tr-005         | dqlabcust05    |       2 | prod-01     | Kotak Pensil DQLab            |    1 | 62500   | Low      |
| tr-005         | dqlabcust05    |       3 | prod-04     | Flashdisk DQLab 32 GB         |    2 | 80000   | Low      |
| tr-006         | dqlabcust02    |       1 | prod-05     | Gift Voucher DQLab 250rb      |    4 | 1000000 | High     |
| tr-006         | dqlabcust02    |       2 | prod-08     | Gantungan Kunci DQLab         |    2 | 31600   | Low      |

## Kesimpulan dan Saran 

---

### Kesimpulan

1. **Total Penjualan dan Kuantitas Produk**
   - Total revenue seluruh transaksi mencapai Rp3.271.600.
   - Total kuantitas produk yang terjual sebanyak 42 unit.
     
2. **Performa Produk**
   - Produk dengan revenue tertinggi adalah prod-05 (Gift Voucher DQLab 250rb) dengan total Rp1.000.000
   - Produk dengan kuantitas tertinggi adalah prod-04 (Flashdisk DQLab 32 GB) dan prod-10 (Sticky Notes DQLab 500 sheets), masing-masing terjual sebanyak 9 unit.

4. **Perilaku Pelanggan**
   - Pelanggan dengan rata-rata belanja tertinggi adalah dqlabcust02 dengan Rp515.800 per transaksi.
   - Pelanggan lainnya memiliki rata-rata belanja antara Rp139.500 hingga Rp202.125.

5. **Kategori Transaksi**
   - High: 2 transaksi (nilai > Rp300.000)
   - Medium: 9 transaksi (nilai antara Rp100.000–Rp300.000)
   - Low: 4 transaksi (nilai < Rp100.000)
---

### Saran

1. **Optimasi Produk Unggulan**
   - Fokuskan promosi pada produk dengan kontribusi revenue tinggi seperti `prod-05` dan `prod-09`
   - Evaluasi strategi penjualan untuk produk dengan performa rendah seperti `prod-07` dan `prod-08`

2. **Segmentasi Pelanggan**
   - Pelanggan dengan rata-rata belanja tinggi seperti `dqlabcust02` dapat dijadikan target program loyalitas
   - Lakukan analisis lanjutan terhadap frekuensi dan preferensi pembelian untuk meningkatkan retensi

3. **Strategi Berdasarkan Kategori**
   - Dorong transaksi kategori **Medium** agar naik ke kategori **High** melalui strategi upselling
   - Tinjau kembali nilai tambah dari produk dalam kategori **Low**

4. **Visualisasi dan Monitoring**
   - Buat dashboard interaktif untuk memantau performa produk dan pelanggan secara real-time
   - Gunakan visualisasi seperti bar chart dan heatmap untuk mendukung pengambilan keputusan

---

