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

### SOAL 2 — KONFIGURASI IP ADDRESS, IP FORWARDING, DAN VERIFIKASI LINK

Pada Soal 2 dilakukan konfigurasi alamat IP pada seluruh interface router (17 router) dan host (25 host) berdasarkan hasil perhitungan VLSM pada Soal 1. Selain itu, IP forwarding diaktifkan pada seluruh router agar perangkat dapat meneruskan paket antar-interface.

Konfigurasi dilakukan menggunakan skrip `.sh` pada setiap node yang disimpan di direktori `/root/`. Pengujian dilakukan dengan memeriksa alamat IP, status IP forwarding, serta melakukan ping ke kedua ujung setiap link antar-router dan koneksi lokal.

#### Ketentuan

- **Router:** Setiap interface dikonfigurasi menggunakan alamat IP dan prefix sesuai topologi. IP forwarding diaktifkan dengan nilai `net.ipv4.ip_forward=1`.
- **Host:** Menggunakan IP statis pada interface `eth0` dan default gateway diarahkan ke router yang terhubung melalui switch.
- **Gendo:** Interface `eth0` terhubung ke NAT1 dan memperoleh alamat IP secara dinamis menggunakan DHCP. IP pada interface ini tidak dikonfigurasi secara permanen menggunakan alamat statis.
- **Switch GNS3:** Tidak memerlukan konfigurasi IP.
- **Konektivitas antar-LAN:** Belum dapat dilakukan sebelum konfigurasi routing statis pada Soal 3. Pada Soal 2, pengujian difokuskan pada link yang terhubung langsung dan jaringan lokal.

#### Konfigurasi DHCP pada Gendo

Gendo merupakan satu-satunya router yang terhubung langsung ke NAT1 melalui interface `eth0`. Oleh karena itu, alamat IP pada interface tersebut diperoleh secara otomatis menggunakan DHCP.

**1. Memulihkan koneksi internet sementara**

Pada awal konfigurasi, Gendo belum memiliki alamat IPv4 pada `eth0` dan belum tersedia DHCP Client. Agar dapat mengakses repositori Debian untuk memasang DHCP Client, digunakan alamat IP sementara pada interface `eth0`.

Perintah yang dijalankan:

```bash
ip addr add 192.168.122.2/24 dev eth0
ip route replace default via 192.168.122.1 dev eth0
echo "nameserver 192.168.122.1" > /etc/resolv.conf
```

Alamat `192.168.122.2/24` hanya digunakan sementara untuk memulihkan koneksi ke NAT1. Alamat tersebut bukan alamat IP akhir Gendo.

Konektivitas diuji menggunakan:

```bash
ping -c 4 192.168.122.1
ping -c 4 8.8.8.8
ping -c 4 deb.debian.org
```

Ketiga pengujian berhasil dengan 4 paket terkirim, 4 paket diterima, dan 0% packet loss. Hal ini menunjukkan bahwa koneksi ke NAT1 dan jaringan internet telah tersedia.

**2. Memasang DHCP Client**

Setelah koneksi internet berhasil dipulihkan, DHCP Client dipasang pada Gendo menggunakan perintah:

```bash
apt update
apt install isc-dhcp-client -y
```

Paket `isc-dhcp-client` digunakan agar Gendo dapat meminta dan menerima alamat IP secara otomatis dari DHCP Server NAT1.

**3. Memperoleh alamat IP secara dinamis**

Setelah DHCP Client berhasil dipasang, alamat IP diminta melalui interface `eth0` dengan perintah:

```bash
dhclient -r eth0
dhclient -v eth0
```

Perintah `dhclient -r eth0` digunakan untuk melepaskan lease DHCP sebelumnya, sedangkan `dhclient -v eth0` digunakan untuk meminta alamat IP kembali dari DHCP Server NAT1.

Hasil proses DHCP menunjukkan:

```text
DHCPDISCOVER on eth0
DHCPOFFER of 192.168.122.162 from 192.168.122.1
DHCPREQUEST for 192.168.122.162
DHCPACK of 192.168.122.162 from 192.168.122.1
bound to 192.168.122.162
```

Setelah alamat dinamis berhasil diperoleh, alamat IP sementara `192.168.122.2/24` dihapus menggunakan perintah:

```bash
ip addr del 192.168.122.2/24 dev eth0
```

**4. Memeriksa alamat IP dan default gateway**

Pemeriksaan dilakukan menggunakan:

```bash
ip -4 addr show dev eth0
ip route show default
```

Hasil pemeriksaan menunjukkan:

- IP address: `192.168.122.162/24`
- Status alamat IP: `dynamic`
- Default gateway: `192.168.122.1`
- Interface: `eth0`

Alamat `192.168.122.162` diperoleh secara otomatis melalui DHCP dari NAT1. Dengan demikian, alamat IP sementara `192.168.122.2` sudah tidak digunakan.

**5. Menguji konektivitas NAT1 dan internet**

Pengujian konektivitas dilakukan menggunakan:

```bash
ping -c 4 192.168.122.1
ping -c 4 8.8.8.8
```

HASILNYA:

<img width="960" height="516" alt="image" src="https://github.com/user-attachments/assets/bf3f4239-9eca-4178-b0cc-5541f6f2f050" />

<img width="960" height="516" alt="image" src="https://github.com/user-attachments/assets/f7751d31-2c82-46b5-81d9-a39e07a2c7fa" />


Kedua pengujian berhasil dengan 4 paket terkirim, 4 paket diterima, dan 0% packet loss.

Dengan demikian, Gendo berhasil memperoleh alamat IP secara dinamis dari NAT1 dan dapat mengakses jaringan luar.

#### Cara Menjalankan Skrip

1. Pastikan kabel pada GNS3 sudah sesuai dengan topologi. Switch-Comm harus terhubung ke **Hikari eth2**, bukan ke Kaworu.
2. Jalankan seluruh node, kemudian buka console masing-masing node dengan klik dua kali pada node di GNS3.
3. Salin skrip konfigurasi node yang sesuai, mulai dari perintah `cat > /root/<nama>.sh <<'EOF'` sampai perintah penutup `EOF`.
4. Jalankan perintah `chmod +x /root/<nama>.sh && /root/<nama>.sh` untuk memberikan izin eksekusi dan menjalankan skrip.
5. Skrip disimpan pada direktori `/root/` di masing-masing node.
6. Konfigurasi dilakukan dengan urutan seluruh router terlebih dahulu, dimulai dari Gendo, kemudian dilanjutkan dengan seluruh host.
7. Setelah semua node selesai dikonfigurasi, lakukan pengujian ulang pada setiap link antar-router agar kedua ujung link sudah aktif.

**Catatan khusus Gendo:** Script `/root/gendo.sh` tidak boleh memasang IP statis pada `eth0`. Interface tersebut harus memperoleh alamat IP melalui DHCP. Contoh perintah DHCP yang digunakan pada Gendo:

```bash
ip link set eth0 up
dhclient -4 eth0
```

IP interface internal Gendo (`eth1` sampai `eth8`) tetap dikonfigurasi sesuai hasil VLSM.

#### Daftar Perintah Menjalankan Skrip

Setelah skrip tersimpan, setiap node dapat dikonfigurasi ulang dengan menjalankan perintah `/root/<nama>.sh` pada console node masing-masing.

**Tahap 1 — Router**

| No | Node      | Perintah             |
| -- | --------- | -------------------- |
| 1  | Gendo     | `/root/gendo.sh`     |
| 2  | Yui       | `/root/yui.sh`       |
| 3  | Rei       | `/root/rei.sh`       |
| 4  | Mari      | `/root/mari.sh`      |
| 5  | Shinji    | `/root/shinji.sh`    |
| 6  | Hikari    | `/root/hikari.sh`    |
| 7  | Kaworu    | `/root/kaworu.sh`    |
| 8  | Fuyutsuki | `/root/fuyutsuki.sh` |
| 9  | Maya      | `/root/maya.sh`      |
| 10 | Toji      | `/root/toji.sh`      |
| 11 | Asuka     | `/root/asuka.sh`     |
| 12 | Kensuke   | `/root/kensuke.sh`   |
| 13 | Ritsuko   | `/root/ritsuko.sh`   |
| 14 | Kaji      | `/root/kaji.sh`      |
| 15 | Misato    | `/root/misato.sh`    |
| 16 | Shigeru   | `/root/shigeru.sh`   |
| 17 | Makoto    | `/root/makoto.sh`    |

**Tahap 2 — Host**

| No | Node           | Perintah                  |
| -- | -------------- | ------------------------- |
| 1  | Quarters       | `/root/quarters.sh`       |
| 2  | Comm-Net       | `/root/comm-net.sh`       |
| 3  | Hangar-Crew    | `/root/hangar-crew.sh`    |
| 4  | Sachiel        | `/root/sachiel.sh`        |
| 5  | Medic-Bay      | `/root/medic-bay.sh`      |
| 6  | Pen-Pen        | `/root/pen-pen.sh`        |
| 7  | Relay-Node     | `/root/relay-node.sh`     |
| 8  | Garden-Staff   | `/root/garden-staff.sh`   |
| 9  | Dock-Crew      | `/root/dock-crew.sh`      |
| 10 | Entry-Plug     | `/root/entry-plug.sh`     |
| 11 | Dummy-Plug     | `/root/dummy-plug.sh`     |
| 12 | Magi-Casper    | `/root/magi-casper.sh`    |
| 13 | Magi-Balthasar | `/root/magi-balthasar.sh` |
| 14 | Magi-Melchior  | `/root/magi-melchior.sh`  |
| 15 | Unit-01        | `/root/unit-01.sh`        |
| 16 | Unit-02        | `/root/unit-02.sh`        |
| 17 | Unit-00        | `/root/unit-00.sh`        |
| 18 | Lilith         | `/root/lilith.sh`         |
| 19 | Adam           | `/root/adam.sh`           |
| 20 | Zeruel         | `/root/zeruel.sh`         |
| 21 | Armisael       | `/root/armisael.sh`       |
| 22 | Radar-Array    | `/root/radar-array.sh`    |
| 23 | Archive-Vault  | `/root/archive-vault.sh`  |
| 24 | Spy            | `/root/spy.sh`            |
| 25 | Tokyo3-Core    | `/root/tokyo3-core.sh`    |

**Tahap 3 — Verifikasi ulang router**

Setelah seluruh router dan host selesai dikonfigurasi, jalankan kembali skrip router untuk memastikan link antar-router dapat saling berkomunikasi. Pengujian dilakukan pada kedua ujung setiap link.

Apabila konfigurasi node hilang setelah restart, skrip yang tersimpan dapat dijalankan kembali. Jika file skrip juga hilang, skrip perlu dibuat kembali dari salinan konfigurasi yang telah disimpan.

#### Contoh Skrip: Router Hikari

```sh
cat > /root/hikari.sh <<'EOF'
#!/bin/sh

IF_0=eth0   # Link Gendo-Hikari
IF_1=eth1   # Link Hikari-Kaworu
IF_2=eth2   # Switch-Comm

ip addr flush dev $IF_0
ip addr add 192.225.4.114/30 dev $IF_0
ip link set $IF_0 up

ip addr flush dev $IF_1
ip addr add 192.225.4.129/30 dev $IF_1
ip link set $IF_1 up

ip addr flush dev $IF_2
ip addr add 192.225.2.1/24 dev $IF_2
ip link set $IF_2 up

sysctl -w net.ipv4.ip_forward=1 >/dev/null 2>&1 || echo 1 > /proc/sys/net/ipv4/ip_forward
echo 'net.ipv4.ip_forward=1' > /etc/sysctl.d/99-forward.conf 2>/dev/null

echo "=== IP ADDRESS HIKARI ==="
ip -br addr

echo "=== IP FORWARDING ==="
cat /proc/sys/net/ipv4/ip_forward

ping -c 2 -W 1 192.225.4.113 >/dev/null 2>&1 && echo "OK   192.225.4.113 (Gendo-Hikari)" || echo "GAGAL 192.225.4.113"
ping -c 2 -W 1 192.225.4.130 >/dev/null 2>&1 && echo "OK   192.225.4.130 (Hikari-Kaworu)" || echo "GAGAL 192.225.4.130"
EOF

chmod +x /root/hikari.sh
/root/hikari.sh
```

**Penjelasan skrip:**

- `ip addr flush` menghapus alamat IP lama pada interface agar tidak terjadi konflik.
- `ip addr add` memasang alamat IP dan prefix sesuai hasil VLSM.
- `ip link set ... up` mengaktifkan interface.
- `sysctl -w net.ipv4.ip_forward=1` mengaktifkan IP forwarding agar router dapat meneruskan paket antar-interface.
- Perintah `ping -c 2 -W 1` mengirimkan dua paket ICMP dengan batas waktu tunggu satu detik. Hasilnya ditampilkan sebagai `OK` atau `GAGAL`.

#### Contoh Skrip Host: Comm-Net

Pada host, alamat IP dipasang pada `eth0`, kemudian default gateway diarahkan ke interface router yang terhubung pada switch yang sama.

```sh
ip addr flush dev eth0
ip addr add 192.225.2.2/24 dev eth0
ip link set eth0 up

ip route replace default via 192.225.2.1

ping -c 2 -W 1 192.225.2.1 >/dev/null 2>&1 && echo "OK 192.225.2.1" || echo "GAGAL 192.225.2.1"
```

Skrip router dan host lainnya menggunakan pola yang sama, dengan menyesuaikan nama interface, alamat IP, prefix, default gateway, dan alamat tujuan ping berdasarkan topologi.

#### Tabel IP Link Antar-Router (/30)

| Link            | Router 1 (interface, IP)       | Router 2 (interface, IP)       |
| --------------- | ------------------------------ | ------------------------------ |
| Gendo-Yui       | Gendo eth1 `192.225.4.117`     | Yui eth0 `192.225.4.118`       |
| Gendo-Hikari    | Gendo eth2 `192.225.4.113`     | Hikari eth0 `192.225.4.114`    |
| Gendo-Asuka     | Gendo eth3 `192.225.4.165`     | Asuka eth0 `192.225.4.166`     |
| Gendo-Kaji      | Gendo eth4 `192.225.4.169`     | Kaji eth0 `192.225.4.170`      |
| Gendo-Misato    | Gendo eth5 `192.225.4.149`     | Misato eth0 `192.225.4.150`    |
| Gendo-Shigeru   | Gendo eth6 `192.225.4.157`     | Shigeru eth0 `192.225.4.158`   |
| Gendo-Fuyutsuki | Gendo eth7 `192.225.4.145`     | Fuyutsuki eth0 `192.225.4.146` |
| Yui-Rei         | Yui eth1 `192.225.4.109`       | Rei eth0 `192.225.4.110`       |
| Yui-Mari        | Yui eth2 `192.225.4.137`       | Mari eth0 `192.225.4.138`      |
| Yui-Shinji      | Yui eth3 `192.225.4.133`       | Shinji eth0 `192.225.4.134`    |
| Hikari-Kaworu   | Hikari eth1 `192.225.4.129`    | Kaworu eth0 `192.225.4.130`    |
| Fuyutsuki-Toji  | Fuyutsuki eth1 `192.225.4.153` | Toji eth0 `192.225.4.154`      |
| Fuyutsuki-Maya  | Fuyutsuki eth2 `192.225.4.125` | Maya eth0 `192.225.4.126`      |
| Asuka-Kensuke   | Asuka eth1 `192.225.4.121`     | Kensuke eth0 `192.225.4.122`   |
| Asuka-Ritsuko   | Asuka eth2 `192.225.4.141`     | Ritsuko eth0 `192.225.4.142`   |
| Shigeru-Makoto  | Shigeru eth1 `192.225.4.161`   | Makoto eth0 `192.225.4.162`    |

#### Tabel IP Sisi LAN Router (Gateway)

| Switch   | Router    | Interface | IP Gateway/Prefix  |
| -------- | --------- | --------- | ------------------ |
| Quarters | Rei       | eth1      | `192.225.0.1/23`   |
| Comm     | Hikari    | eth2      | `192.225.2.1/24`   |
| Hangar   | Yui       | eth4      | `192.225.3.1/25`   |
| Bunker   | Kensuke   | eth1      | `192.225.3.129/26` |
| Medic    | Maya      | eth1      | `192.225.3.193/27` |
| Relay    | Kaworu    | eth1      | `192.225.3.225/27` |
| Garden   | Shinji    | eth1      | `192.225.4.1/27`   |
| Dock     | Mari      | eth1      | `192.225.4.33/28`  |
| Lab      | Ritsuko   | eth1      | `192.225.4.49/29`  |
| Terminal | Fuyutsuki | eth3      | `192.225.4.57/29`  |
| Cage     | Misato    | eth1      | `192.225.4.65/29`  |
| Dogma    | Toji      | eth1      | `192.225.4.73/29`  |
| Monolith | Shigeru   | eth2      | `192.225.4.81/29`  |
| Radar    | Makoto    | eth1      | `192.225.4.89/29`  |
| Archive  | Asuka     | eth3      | `192.225.4.97/30`  |
| Intel    | Kaji      | eth1      | `192.225.4.101/30` |
| Cmd      | Gendo     | eth8      | `192.225.4.105/30` |

#### Tabel IP Host

| Host           | Switch   | IP/Prefix          | Gateway         |
| -------------- | -------- | ------------------ | --------------- |
| Quarters       | Quarters | `192.225.0.2/23`   | `192.225.0.1`   |
| Comm-Net       | Comm     | `192.225.2.2/24`   | `192.225.2.1`   |
| Hangar-Crew    | Hangar   | `192.225.3.2/25`   | `192.225.3.1`   |
| Sachiel        | Bunker   | `192.225.3.130/26` | `192.225.3.129` |
| Medic-Bay      | Medic    | `192.225.3.194/27` | `192.225.3.193` |
| Pen-Pen        | Medic    | `192.225.3.195/27` | `192.225.3.193` |
| Relay-Node     | Relay    | `192.225.3.226/27` | `192.225.3.225` |
| Garden-Staff   | Garden   | `192.225.4.2/27`   | `192.225.4.1`   |
| Dock-Crew      | Dock     | `192.225.4.34/28`  | `192.225.4.33`  |
| Entry-Plug     | Lab      | `192.225.4.50/29`  | `192.225.4.49`  |
| Dummy-Plug     | Lab      | `192.225.4.51/29`  | `192.225.4.49`  |
| Magi-Casper    | Terminal | `192.225.4.58/29`  | `192.225.4.57`  |
| Magi-Balthasar | Terminal | `192.225.4.59/29`  | `192.225.4.57`  |
| Magi-Melchior  | Terminal | `192.225.4.60/29`  | `192.225.4.57`  |
| Unit-01        | Cage     | `192.225.4.66/29`  | `192.225.4.65`  |
| Unit-02        | Cage     | `192.225.4.67/29`  | `192.225.4.65`  |
| Unit-00        | Cage     | `192.225.4.68/29`  | `192.225.4.65`  |
| Lilith         | Dogma    | `192.225.4.74/29`  | `192.225.4.73`  |
| Adam           | Dogma    | `192.225.4.75/29`  | `192.225.4.73`  |
| Zeruel         | Monolith | `192.225.4.82/29`  | `192.225.4.81`  |
| Armisael       | Monolith | `192.225.4.83/29`  | `192.225.4.81`  |
| Radar-Array    | Radar    | `192.225.4.90/29`  | `192.225.4.89`  |
| Archive-Vault  | Archive  | `192.225.4.98/30`  | `192.225.4.97`  |
| Spy            | Intel    | `192.225.4.102/30` | `192.225.4.101` |
| Tokyo3-Core    | Cmd      | `192.225.4.106/30` | `192.225.4.105` |

#### Verifikasi

Verifikasi konfigurasi dilakukan melalui beberapa pengujian berikut.

1. **Pemeriksaan alamat IP interface**

   Perintah:

   ```bash
   ip -br addr
   ```

   Perintah dijalankan pada setiap router dan host. Alamat IP yang muncul dicocokkan dengan tabel konfigurasi.

2. **Pemeriksaan IP forwarding**

   Perintah:

   ```bash
   cat /proc/sys/net/ipv4/ip_forward
   ```

   Pada seluruh router, hasil yang diharapkan adalah `1`, yang menunjukkan IP forwarding aktif.

3. **Pengujian ping dua ujung link antar-router**

   Setiap router melakukan ping ke alamat interface router tetangganya yang terhubung langsung. Karena terdapat 16 link antar-router, pengujian dilakukan dari kedua ujung sehingga terdapat 32 pengujian ping.

4. **Pengujian konektivitas host dan gateway**

   Setiap host melakukan ping ke default gateway masing-masing. Selain itu, host yang berada pada switch yang sama diuji agar dapat saling berkomunikasi.

5. **Pengujian router ke host dalam satu LAN**

   Router diuji dengan melakukan ping ke host yang berada pada jaringan lokal yang terhubung langsung.

#### Tabel Tujuan Ping Antar-Router

Seluruh alamat berikut menggunakan prefix `192.225.4.`.

| Router    | Tujuan ping (alamat akhir dan tetangga)                                                                             |
| --------- | ------------------------------------------------------------------------------------------------------------------- |
| Gendo     | `.118` (Yui), `.114` (Hikari), `.166` (Asuka), `.170` (Kaji), `.150` (Misato), `.158` (Shigeru), `.146` (Fuyutsuki) |
| Yui       | `.117` (Gendo), `.110` (Rei), `.138` (Mari), `.134` (Shinji)                                                        |
| Hikari    | `.113` (Gendo), `.130` (Kaworu)                                                                                     |
| Fuyutsuki | `.145` (Gendo), `.154` (Toji), `.126` (Maya)                                                                        |
| Asuka     | `.165` (Gendo), `.122` (Kensuke), `.142` (Ritsuko)                                                                  |
| Shigeru   | `.157` (Gendo), `.162` (Makoto)                                                                                     |
| Rei       | `.109` (Yui)                                                                                                        |
| Mari      | `.137` (Yui)                                                                                                        |
| Shinji    | `.133` (Yui)                                                                                                        |
| Kaworu    | `.129` (Hikari)                                                                                                     |
| Maya      | `.125` (Fuyutsuki)                                                                                                  |
| Toji      | `.153` (Fuyutsuki)                                                                                                  |
| Kensuke   | `.121` (Asuka)                                                                                                      |
| Ritsuko   | `.141` (Asuka)                                                                                                      |
| Kaji      | `.169` (Gendo)                                                                                                      |
| Misato    | `.149` (Gendo)                                                                                                      |
| Makoto    | `.161` (Shigeru)                                                                                                    |

#### Bukti Hasil

**1. Router ke router (Gendo, 7 link langsung)**

Perintah: `/root/gendo.sh`

<img width="960" height="516" alt="Screenshot 2026-11-24 122151" src="https://github.com/user-attachments/assets/b1a4342e-0f4f-41d7-aac6-e4b6e35f46bb" />

**2. Router ke router dan sisi LAN (Hikari)**

Perintah: `/root/hikari.sh`

<img width="960" height="516" alt="Screenshot 2026-11-24 122349" src="https://github.com/user-attachments/assets/beae465a-4c6a-468b-ba22-e77457a712a6" />

**3. Host ke gateway (Comm-Net)**

Perintah: `/root/comm-net.sh`

<img width="960" height="516" alt="image" src="https://github.com/user-attachments/assets/f8628c3f-7336-4aba-b85e-ef9bfe82aaec" />

**4. Host ke host satu switch (Zeruel dan Armisael)**

Perintah: `/root/zeruel.sh`

<img width="960" height="516" alt="image" src="https://github.com/user-attachments/assets/1d6058d2-3d95-4a97-bed0-d406fa167995" />

**5. Router ke host satu LAN (Maya ke Medic-Bay)**

Perintah: `ping -c2 192.225.3.194`

<img width="960" height="516" alt="image" src="https://github.com/user-attachments/assets/f8566fed-6578-4410-818e-21c7489892ed" />

**6. IP dan IP forwarding pada router**

Perintah: `ip -br addr` dan `cat /proc/sys/net/ipv4/ip_forward`

<img width="960" height="516" alt="Screenshot 2026-11-24 123629" src="https://github.com/user-attachments/assets/07af713c-1b68-4908-8ac3-47c96f057a35" />

**7. Konfigurasi DHCP pada Gendo**

Perintah yang digunakan:

```bash
dhclient -v eth0
ip -4 addr show dev eth0
ip route show default
ping -c 4 192.168.122.1
ping -c 4 8.8.8.8
```

Hasil pengujian menunjukkan Gendo berhasil memperoleh IP `192.168.122.162/24` dari NAT1 melalui DHCP. Default gateway menggunakan `192.168.122.1`. Pengujian ping ke gateway NAT1 dan alamat internet `8.8.8.8` juga berhasil tanpa packet loss.

**Dokumentasi hasil konfigurasi DHCP:**

<img width="960" height="516" alt="image" src="https://github.com/user-attachments/assets/36625af1-aaa1-4b87-ac72-63a69563dd07" />

#### Kesimpulan

Berdasarkan konfigurasi yang telah dilakukan, seluruh router dan host dirancang menggunakan pembagian alamat IP sesuai hasil VLSM pada Soal 1. IP forwarding diaktifkan pada router agar dapat meneruskan paket antar-interface.

Khusus Gendo, interface `eth0` memperoleh alamat IP secara otomatis melalui DHCP dari NAT1, yaitu `192.168.122.162/24`, dengan default gateway `192.168.122.1`. Konektivitas ke gateway NAT1 dan jaringan luar berhasil dibuktikan melalui pengujian ping.

Pengujian konektivitas juga dilakukan pada link antar-router dan jaringan lokal untuk memastikan setiap perangkat dapat berkomunikasi dengan perangkat yang terhubung langsung. Routing antar-LAN selanjutnya dikonfigurasi pada Soal 3.


