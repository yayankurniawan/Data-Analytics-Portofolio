## Project INNER JOIN
Dalam database, terdapat tabel ms_pelanggan yang berisi data - data pelanggan yang membeli produk dan tabel tr_penjualan yang berisi data transaksi pembelian di suatu store.

Suatu hari, departemen marketing & promotion meminta bantuan untuk meng-query data-data pelanggan yang membeli produk Kotak Pensil DQLab, Flashdisk DQLab 32 GB, dan Sticky Notes DQLab 500 sheets.

Buatlah query menggunakan tabel ms_pelanggan dan tr_penjualan untuk mendapatkan data - data yang diminta oleh marketing yaitu kode_pelanggan, nama_customer, alamat.
## Dataset

Tabel ms_pelanggan

Tabel ms_pelanggan

| no_urut | kode_pelanggan | nama_customer       | alamat                                   |
|---------|----------------|---------------------|------------------------------------------|
|       1 | dqlabcust01    | Eva Novianti, S.H.  | Vila Sempilan, No. 67 - Kota B           |
|       2 | dqlabcust02    | Heidi Goh           | Vila Sempilan, No. 11 - Kota B           |
|       3 | dqlabcust03    | Unang Handoko       | Vila Sempilan, No. 1 - Kota B            |
|       4 | dqlabcust04    | Jokolono Sukarman   | Vila Permata Intan Berkilau, Blok C5-7   |
|       5 | dqlabcust05    | Tommy Sinaga        | Vila Permata Intan Berkilau, Blok A1/2   |
|       6 | dqlabcust06    | Irwan Setianto      | Vila Gunung Seribu, Blok O1 - No. 1      |
|       7 | dqlabcust07    | Agus Cahyono        | Vila Gunung Seribu, Blok F4 - No. 8      |
|       8 | dqlabcust08    | Maria Sirait        | Vila Bukit Sagitarius, Gang. Sawit No. 3 |
|       9 | dqlabcust09    | Ir. Ita Nugraha     | Vila Bukit Sagitarius, Gang Kelapa No. 6 |
|      10 | dqlabcust10    | Djoko Wardoyo, Drs. | Vila Bukit Sagitarius, Blok A1 No. 1     |
|      11 | dqlabcust11    | Unang Handoko       | Vila Sempilan, No. 1 - Kota B            |
|      12 | dqlabcust12    | Tommy Sinaga        | Vila Permata Intan Berkilau, Blok A1/2   |

Tabel tr_penjualan

| kode_transaksi | kode_pelanggan | no_urut | kode_produk | nama_produk                   | qty  | harga  |
|----------------|----------------|---------|-------------|-------------------------------|------|--------|
| tr-001         | dqlabcust07    |       1 | prod-01     | Kotak Pensil DQLab            |    5 |  62500 |
| tr-001         | dqlabcust07    |       2 | prod-03     | Flash disk DQLab 32 GB        |    1 | 100000 |
| tr-001         | dqlabcust07    |       3 | prod-09     | Buku Planner Agenda DQLab     |    3 |  92000 |
| tr-001         | dqlabcust07    |       4 | prod-04     | Flashdisk DQLab 32 GB         |    3 |  40000 |
| tr-002         | dqlabcust01    |       1 | prod-03     | Gift Voucher DQLab 100rb      |    2 | 100000 |
| tr-002         | dqlabcust01    |       2 | prod-10     | Sticky Notes DQLab 500 sheets |    4 |  55000 |
| tr-002         | dqlabcust01    |       3 | prod-07     | Tas Travel Organizer DQLab    |    1 |  48000 |
| tr-003         | dqlabcust03    |       1 | prod-02     | Flashdisk DQLab 64 GB         |    2 |  55000 |
| tr-004         | dqlabcust03    |       1 | prod-10     | Sticky Notes DQLab 500 sheets |    5 |  55000 |
| tr-004         | dqlabcust03    |       2 | prod-04     | Flashdisk DQLab 32 GB         |    4 |  40000 |
| tr-005         | dqlabcust05    |       1 | prod-09     | Buku Planner Agenda DQLab     |    3 |  92000 |
| tr-005         | dqlabcust05    |       2 | prod-01     | Kotak Pensil DQLab            |    1 |  62500 |
| tr-005         | dqlabcust05    |       3 | prod-04     | Flashdisk DQLab 32 GB         |    2 |  40000 |
| tr-006         | dqlabcust02    |       1 | prod-05     | Gift Voucher DQLab 250rb      |    4 | 250000 |
| tr-006         | dqlabcust02    |       2 | prod-08     | Gantungan Kunci DQLab         |    2 |  15800 |


```
# pelanggan yang membeli produk Kotak Pensil DQLab, Flashdisk DQLab 32 GB, dan Sticky Notes DQLab 500 sheets
SELECT DISTINCT ms_pelanggan.kode_pelanggan, ms_pelanggan.nama_customer, ms_pelanggan.alamat
FROM ms_pelanggan
INNER JOIN tr_penjualan
ON ms_pelanggan.kode_pelanggan = tr_penjualan.kode_pelanggan
WHERE tr_penjualan.nama_produk = 'Kotak Pensil DQLab'
   OR tr_penjualan.nama_produk = 'Flashdisk DQLab 32 GB'
   OR tr_penjualan.nama_produk = 'Sticky Notes DQLab 500 sheets';
```

Output:

| kode_pelanggan | nama_customer      | alamat                                 |
|----------------|--------------------|----------------------------------------|
| dqlabcust01    | Eva Novianti, S.H. | Vila Sempilan, No. 67 - Kota B         |
| dqlabcust03    | Unang Handoko      | Vila Sempilan, No. 1 - Kota B          |
| dqlabcust05    | Tommy Sinaga       | Vila Permata Intan Berkilau, Blok A1/2 |
| dqlabcust07    | Agus Cahyono       | Vila Gunung Seribu, Blok F4 - No. 8    |

## Project UNION
Persiapkanlah data katalog mengenai mengenai nama - nama produk yang akan dijual di suatu store. Data tersebut akan digunakan dalam meeting untuk mereview produk mana saja yang akan dilanjutkan penjualannya dan mana yang tidak akan dilanjutkan.

Siapkan hanya data produk dengan harga di bawah 100K untuk kode produk prod-1 sampai prod-5; dan dibawah 50K untuk kode produk prod-6 sampai prod-10, tanpa mencantumkan kolom no_urut.

Saat mengecek data produk di database, terdapat 2 tabel yang sama - sama berisi data katalog, yaitu:

 
## Dataset
Tabel ms_produk_1

| No | Kode Produk | Nama Produk                    | Harga   |
|----|-------------|----------------------------------|---------|
| 1  | prod-01     | Kotak Pensil DQLab              | 62,500  |
| 2  | prod-02     | Flashdisk DQLab 64 GB           | 55,000  |
| 3  | prod-03     | Gift Voucher DQLab 100rb        | 100,000 |
| 4  | prod-04     | Flashdisk DQLab 32 GB           | 40,000  |
| 5  | prod-05     | Gift Voucher DQLab 250rb        | 250,000 |

Tabel ms_produk_2

| No | Kode Produk | Nama Produk                          | Harga   |
|----|-------------|---------------------------------------|---------|
| 6  | prod-06     | Pulpen Multifunction + Laser DQLab    | 92,500  |
| 7  | prod-07     | Tas Travel Organizer DQLab            | 48,000  |
| 8  | prod-08     | Gantungan Kunci DQLab                 | 15,800  |
| 9  | prod-09     | Buku Planner Agenda DQLab             | 92,000  |
| 10 | prod-10     | Sticky Notes DQLab 500 sheets         | 55,000  |


```
# Produk dengan harga di bawah 100K untuk kode produk prod-1 sampai prod-5; dan dibawah 50K untuk kode produk prod-6 sampai prod-10
SELECT nama_produk, kode_produk, harga
FROM ms_produk_1 WHERE harga < 100000
UNION
SELECT nama_produk, kode_produk, harga
FROM ms_produk_2 WHERE harga < 50000;
```
Output :
| nama_produk                | kode_produk | harga |
|----------------------------|-------------|-------|
| Kotak Pensil DQLab         | prod-01     | 62500 |
| Flashdisk DQLab 64 GB      | prod-02     | 55000 |
| Flashdisk DQLab 32 GB      | prod-04     | 40000 |
| Tas Travel Organizer DQLab | prod-07     | 48000 |
| Gantungan Kunci DQLab      | prod-08     | 15800 |
