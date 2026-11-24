## Jarkom-Modul-5-2026-K-28

| Nama | NRP |
|---|---|
| Maitasya Rohmatul Ula | 5027251026 |
| A. Algifari Rantiga Isdar | 5027251084 |

### SOAL 1 — PEMBAGIAN IP ADDRESS MENGGUNAKAN VLSM

Melakukan pembagian alamat IP menggunakan metode Variable Length Subnet Mask (VLSM) pada topologi Geofront. Pembagian dilakukan untuk 17 LAN dan 16 link antar-router dengan menggunakan prefix terkecil sesuai kebutuhan masing-masing subnet agar penggunaan alamat IP lebih efisien.

####  Prefix Induk dan Ketentuan

Prefix induk yang digunakan adalah `192.225.0.0/21`.

- Kapasitas alamat IP: 2.048 alamat.
- Jumlah subnet: 33 subnet.
- Terdiri dari 17 LAN dan 16 link antar-router.
- Pembagian dilakukan dari kebutuhan IP terbesar ke terkecil.
- Gateway LAN menggunakan IP usable pertama.
- Setiap link antar-router membutuhkan 2 IP usable untuk kedua router yang terhubung.
  
TOPOLOGINYA:

<img width="960" height="516" alt="Screenshot 2026-11-23 194206" src="https://github.com/user-attachments/assets/09abe457-296a-4674-b2b1-dd3c9538bc0e" />

LINGKARAN TOPOLOGINYA SESUAI SUBNETTING:

<img width="3840" height="2064" alt="topologi_subnet (1)" src="https://github.com/user-attachments/assets/e7b6709c-9290-4679-ac32-c5afede0bfd3" />

POHON SUBNETTING:

<img width="5175" height="1359" alt="pohon_ip" src="https://github.com/user-attachments/assets/4725af96-0378-4e59-86ff-7c25bdf2f570" />


#### Langkah-Langkah Perhitungan VLSM

Pembagian subnet dilakukan dengan langkah-langkah berikut:

**1. Menghitung kebutuhan IP setiap subnet**

Pertama, menghitung jumlah perangkat yang membutuhkan alamat IP pada setiap LAN. Untuk LAN, kebutuhan IP mencakup alamat gateway dan seluruh perangkat yang terhubung. Sementara itu, setiap link antar-router membutuhkan 2 alamat IP usable.

**2. Mengurutkan kebutuhan subnet**

Seluruh subnet diurutkan berdasarkan kebutuhan IP dari yang terbesar hingga terkecil. Tujuannya agar subnet berukuran besar dialokasikan terlebih dahulu sehingga ruang alamat dapat digunakan secara efisien.

**3. Menentukan prefix menggunakan rumus**

Rumus jumlah alamat IP dalam subnet:

`Jumlah IP = 2^(32 - prefix)`

Rumus jumlah IP usable:

`IP Usable = 2^(32 - prefix) - 2`

Dua alamat dikurangi karena digunakan sebagai network address dan broadcast address.

**4. Menentukan prefix terkecil yang mencukupi**

Pilih prefix dengan kapasitas IP usable yang sama dengan atau lebih besar daripada kebutuhan subnet. Prefix yang dipilih harus menjadi ukuran terkecil yang masih mampu menampung seluruh kebutuhan IP.

**5. Menentukan network dan broadcast**

Setelah prefix ditentukan, tentukan network address berdasarkan blok subnet. Alamat pertama merupakan network address, sedangkan alamat terakhir merupakan broadcast address.

**6. Menentukan gateway dan sisa IP**

Untuk setiap LAN, gateway menggunakan IP usable pertama. Alamat berikutnya digunakan oleh perangkat sesuai urutan pada topologi. Sisa IP dihitung dari jumlah IP usable dikurangi jumlah IP yang terpakai.

#### Contoh Perhitungan Satu Subnet: Switch-Quarters

Subnet Switch-Quarters memiliki kebutuhan sebanyak **501 IP terpakai**, yaitu 500 IP untuk perangkat dan 1 IP untuk gateway.

**1. Menentukan prefix yang sesuai**

Kita mencoba menghitung kapasitas beberapa prefix:

- `/24`:
  - Jumlah IP = 2^(32 − 24) = 256 alamat.
  - IP usable = 256 − 2 = 254 alamat.
  - Tidak mencukupi kebutuhan 501 IP.

- `/23`:
  - Jumlah IP = 2^(32 − 23) = 512 alamat.
  - IP usable = 512 − 2 = 510 alamat.
  - Mencukupi kebutuhan 501 IP.

Karena `/24` tidak mencukupi dan `/23` mencukupi, maka prefix terkecil yang digunakan adalah **/23**.

Subnet mask `/23` adalah `255.255.254.0`.

**2. Menentukan network address**

Prefix induk dimulai dari `192.225.0.0`. Subnet pertama yang dialokasikan adalah Switch-Quarters.

Maka diperoleh:

- Network address: `192.225.0.0`
- Prefix: `/23`

**3. Menentukan rentang IP usable**

Network address adalah `192.225.0.0`, sedangkan alamat broadcast adalah `192.225.1.255`.

Dengan demikian, rentang IP usable adalah:

`192.225.0.1 – 192.225.1.254`

**4. Menentukan gateway**

Gateway menggunakan IP usable pertama, yaitu:

`192.225.0.1`

Alamat berikutnya dapat digunakan untuk perangkat yang terhubung ke Switch-Quarters.

**5. Menghitung sisa IP**

Jumlah IP usable tersedia = 510.

Jumlah IP terpakai = 501.

Sisa IP:

`510 − 501 = 9 IP`

Jadi, subnet Switch-Quarters menggunakan `192.225.0.0/23`, memiliki 501 IP terpakai dan 9 IP usable tersisa.

#### Ringkasan Hasil Pembagian VLSM

| Keterangan | Hasil |
|---|---:|
| Total kebutuhan IP terpakai | 1.003 |
| Total alamat IP yang dialokasikan | 1.196 |
| Prefix induk | `192.225.0.0/21` |
| Kapasitas prefix induk | 2.048 |
| Persentase pemakaian alokasi | 58,40% |
| Sisa alamat IP dari prefix induk | 852 |

#### Kesimpulan

Berdasarkan perhitungan menggunakan metode VLSM, prefix induk `192.225.0.0/21` berhasil dibagi menjadi 33 subnet yang terdiri dari 17 LAN dan 16 link antar-router. Setiap subnet menggunakan prefix terkecil yang mampu memenuhi kebutuhan alamat IP. Dengan demikian, pembagian alamat IP menjadi lebih efisien dan setiap jaringan memperoleh alokasi sesuai kebutuhan perangkatnya.
