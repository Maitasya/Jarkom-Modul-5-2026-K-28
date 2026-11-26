## Jarkom-Modul-5-2026-K-28

| Nama | NRP |
|---|---|
| Maitasya Rohmatul Ula | 5027251026 |
| A. Algifari Rantiga Isdar | 5027251112|

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

### SOAL 3 — KONFIGURASI ROUTING STATIS

Pada Soal 3 dilakukan konfigurasi routing statis untuk menghubungkan seluruh subnet pada topologi jaringan. Setiap router harus memiliki jalur menuju jaringan lain agar seluruh host dapat saling berkomunikasi.

Konfigurasi dilakukan dengan dua metode, yaitu:
1. Konfigurasi routing secara manual menggunakan perintah `ip route`.
2. Konfigurasi routing menggunakan script Bash agar lebih mudah dijalankan kembali.

Pengujian dilakukan untuk memastikan host Armisael dapat berkomunikasi dengan Lilith, Sachiel, dan Comm-Net.

#### Ketentuan Routing

Ketentuan konfigurasi routing pada Soal 3 adalah sebagai berikut:

1. Router Gendo menjadi router utama yang terhubung ke NAT1.
2. Gendo memiliki default route menuju gateway NAT1 `192.168.122.1`.
3. Router selain Gendo menggunakan satu default route menuju router di atasnya.
4. Router yang memiliki cabang jaringan tambahan harus memiliki static route menuju jaringan tersebut.
5. Menggunakan summarization pada jaringan yang dapat digabungkan tanpa mencakup subnet yang tidak berkaitan.
6. Pengujian menggunakan IP address dan gateway sementara pada setiap host.

#### Konfigurasi Routing Secara Manual

Konfigurasi manual dilakukan terlebih dahulu sebelum menggunakan script. Perintah dijalankan melalui Console masing-masing router GNS3 dengan hak akses root.

#### Konfigurasi Router Gendo

**Langkah 1 — Membuka Console Gendo**

Buka router Gendo pada GNS3, kemudian masuk ke Console dan pastikan menggunakan akun root.

**Langkah 2 — Mengaktifkan IP Forwarding**

Jalankan perintah:

```bash
sysctl -w net.ipv4.ip_forward=1
```

**Langkah 3 — Menambahkan Default Route**

```bash
ip route replace default via 192.168.122.1
```

**Langkah 4 — Menambahkan Static Route**

Jalankan perintah berikut untuk mengarahkan jaringan ke router cabang masing-masing.

```bash
# Cabang Yui
ip route replace 192.225.0.0/23 via 192.225.4.118
ip route replace 192.225.3.0/25 via 192.225.4.118
ip route replace 192.225.4.0/27 via 192.225.4.118
ip route replace 192.225.4.32/28 via 192.225.4.118
ip route replace 192.225.4.108/30 via 192.225.4.118
ip route replace 192.225.4.132/30 via 192.225.4.118
ip route replace 192.225.4.136/30 via 192.225.4.118

# Cabang Hikari
ip route replace 192.225.2.0/24 via 192.225.4.114
ip route replace 192.225.3.224/27 via 192.225.4.114
ip route replace 192.225.4.128/30 via 192.225.4.114

# Cabang Asuka
ip route replace 192.225.3.128/26 via 192.225.4.166
ip route replace 192.225.4.48/29 via 192.225.4.166
ip route replace 192.225.4.96/30 via 192.225.4.166
ip route replace 192.225.4.120/30 via 192.225.4.166
ip route replace 192.225.4.140/30 via 192.225.4.166

# Cabang Kaji
ip route replace 192.225.4.100/30 via 192.225.4.170

# Cabang Misato
ip route replace 192.225.4.64/29 via 192.225.4.150

# Cabang Shigeru
ip route replace 192.225.4.80/28 via 192.225.4.158

# Cabang Fuyutsuki
ip route replace 192.225.3.192/27 via 192.225.4.146
ip route replace 192.225.4.56/29 via 192.225.4.146
ip route replace 192.225.4.72/29 via 192.225.4.146
ip route replace 192.225.4.124/30 via 192.225.4.146
ip route replace 192.225.4.152/30 via 192.225.4.146
```

**Langkah 5 — Memeriksa Routing**

```bash
ip route
```

Pastikan default route dan seluruh static route sudah muncul.

#### Konfigurasi Router Cabang

Setelah Gendo dikonfigurasi, lanjutkan konfigurasi pada router cabang. Setiap router menggunakan default route menuju router induknya.

**A. Router Yui**

```bash
sysctl -w net.ipv4.ip_forward=1
ip route replace default via 192.225.4.117

ip route replace 192.225.0.0/23 via 192.225.4.110
ip route replace 192.225.4.32/28 via 192.225.4.138
ip route replace 192.225.4.0/27 via 192.225.4.134

ip route
```

**B. Router Hikari**

```bash
sysctl -w net.ipv4.ip_forward=1
ip route replace default via 192.225.4.113

ip route replace 192.225.3.224/27 via 192.225.4.130

ip route
```

**C. Router Fuyutsuki**

```bash
sysctl -w net.ipv4.ip_forward=1
ip route replace default via 192.225.4.145

ip route replace 192.225.3.192/27 via 192.225.4.126
ip route replace 192.225.4.72/29 via 192.225.4.154

ip route
```

**D. Router Asuka**

```bash
sysctl -w net.ipv4.ip_forward=1
ip route replace default via 192.225.4.165

ip route replace 192.225.3.128/26 via 192.225.4.122
ip route replace 192.225.4.48/29 via 192.225.4.142

ip route
```

**E. Router Shigeru**

```bash
sysctl -w net.ipv4.ip_forward=1
ip route replace default via 192.225.4.157

ip route replace 192.225.4.88/29 via 192.225.4.162

ip route
```

#### Konfigurasi Router Daun

Router daun tidak memiliki cabang router tambahan sehingga cukup menggunakan default route menuju router induknya.

**A. Router Rei**

```bash
sysctl -w net.ipv4.ip_forward=1
ip route replace default via 192.225.4.109
ip route
```

**B. Router Mari**

```bash
sysctl -w net.ipv4.ip_forward=1
ip route replace default via 192.225.4.137
ip route
```

**C. Router Shinji**

```bash
sysctl -w net.ipv4.ip_forward=1
ip route replace default via 192.225.4.133
ip route
```

**D. Router Kaworu**

```bash
sysctl -w net.ipv4.ip_forward=1
ip route replace default via 192.225.4.129
ip route
```

**E. Router Maya**

```bash
sysctl -w net.ipv4.ip_forward=1
ip route replace default via 192.225.4.125
ip route
```

**F. Router Toji**

```bash
sysctl -w net.ipv4.ip_forward=1
ip route replace default via 192.225.4.153
ip route
```

**G. Router Kensuke**

```bash
sysctl -w net.ipv4.ip_forward=1
ip route replace default via 192.225.4.121
ip route
```

**H. Router Ritsuko**

```bash
sysctl -w net.ipv4.ip_forward=1
ip route replace default via 192.225.4.141
ip route
```

**I. Router Kaji**

```bash
sysctl -w net.ipv4.ip_forward=1
ip route replace default via 192.225.4.169
ip route
```

**J. Router Misato**

```bash
sysctl -w net.ipv4.ip_forward=1
ip route replace default via 192.225.4.149
ip route
```

**K. Router Makoto**

```bash
sysctl -w net.ipv4.ip_forward=1
ip route replace default via 192.225.4.161
ip route
```

#### Penerapan Route Summarization

Route summarization dilakukan untuk menggabungkan beberapa jaringan yang berurutan menjadi satu prefix yang lebih besar.

Pada cabang Shigeru, jaringan Monolith `192.225.4.80/29` dan Radar `192.225.4.88/29` dapat diringkas menjadi:

```text
192.225.4.80/28
```

Konfigurasi pada Shigeru tetap mengarahkan jaringan Radar menuju Makoto:

```bash
ip route replace 192.225.4.88/29 via 192.225.4.162
```

Sementara itu, Gendo cukup mengarahkan seluruh jaringan tersebut melalui Shigeru:

```bash
ip route replace 192.225.4.80/28 via 192.225.4.158
```

Dengan demikian, jumlah route pada Gendo dapat dikurangi tanpa menghilangkan jangkauan jaringan.

#### Konfigurasi Menggunakan Script

Setelah konfigurasi manual dilakukan, konfigurasi dapat diterapkan kembali menggunakan script Bash yang telah dibuat untuk setiap router.

#### Menjalankan Script Router

**Langkah 1 — Membuka Console Router**

Buka Console router yang akan dikonfigurasi.

**Langkah 2 — Memastikan File Script Tersedia**

Contoh untuk Gendo:

```bash
ls -l /root/gendo_route.sh
```

**Langkah 3 — Memberikan Izin Eksekusi**

```bash
chmod +x /root/gendo_route.sh
```

**Langkah 4 — Menjalankan Script**

```bash
/root/gendo_route.sh
```

**Langkah 5 — Memeriksa Hasil**

```bash
ip route
```

Script akan mengaktifkan IP forwarding, menambahkan default route dan static route, kemudian menampilkan tabel routing serta melakukan pengujian ke next-hop.

Lakukan langkah yang sama pada router lainnya dengan nama file masing-masing:

| Router | Nama Script |
|---|---|
| Gendo | `gendo_route.sh` |
| Yui | `yui_route.sh` |
| Rei | `rei_route.sh` |
| Mari | `mari_route.sh` |
| Shinji | `shinji_route.sh` |
| Hikari | `hikari_route.sh` |
| Kaworu | `kaworu_route.sh` |
| Fuyutsuki | `fuyutsuki_route.sh` |
| Maya | `maya_route.sh` |
| Toji | `toji_route.sh` |
| Asuka | `asuka_route.sh` |
| Kensuke | `kensuke_route.sh` |
| Ritsuko | `ritsuko_route.sh` |
| Kaji | `kaji_route.sh` |
| Misato | `misato_route.sh` |
| Shigeru | `shigeru_route.sh` |
| Makoto | `makoto_route.sh` |

**Catatan:** Jalankan script Gendo terlebih dahulu, kemudian router cabang dan router daun. Pastikan IP address pada Soal 2 sudah aktif sebelum menjalankan script.

#### Konfigurasi IP Sementara pada Host

Setelah seluruh router dikonfigurasi, setiap host perlu memiliki IP address dan default gateway agar dapat berkomunikasi melalui router.

Konfigurasi berikut dilakukan pada host pengujian Armisael.

**Langkah 1 — Membuka Console Armisael**

Buka Console host Armisael melalui GNS3.

**Langkah 2 — Mengatur IP Address**

```bash
ip addr flush dev eth0
ip addr add 192.225.4.83/29 dev eth0
ip link set eth0 up
```

**Langkah 3 — Mengatur Default Gateway**

```bash
ip route replace default via 192.225.4.81
```

**Langkah 4 — Memeriksa Konfigurasi**

```bash
ip -br addr
ip route
```

Pastikan Armisael memiliki IP `192.225.4.83/29` dan gateway `192.225.4.81`.

Konfigurasi IP sementara juga diterapkan pada host lainnya sesuai pembagian IP pada Soal 2 dan script host yang telah dibuat.

#### Pengujian Konektivitas

Pengujian dilakukan untuk memastikan routing statis dapat menghubungkan jaringan yang berbeda.

#### Pengujian Gateway Armisael

Jalankan perintah berikut pada Console Armisael:

```bash
ping -c 4 192.225.4.81
```

Alamat tersebut merupakan gateway Armisael pada router Monolith.

#### Pengujian Koneksi Armisael ke Lilith

```bash
ping -c 4 192.225.4.74
```

Pengujian ini memastikan Armisael dapat berkomunikasi dengan host Lilith melalui jaringan yang berbeda.

#### Pengujian Koneksi Armisael ke Sachiel

```bash
ping -c 4 192.225.3.130
```

Pengujian ini memastikan jalur routing dari jaringan Armisael menuju jaringan Sachiel telah tersedia.

#### Pengujian Koneksi Armisael ke Comm-Net

```bash
ping -c 4 192.225.2.2
```

Pengujian ini memastikan Armisael dapat berkomunikasi dengan Comm-Net yang berada pada cabang jaringan Hikari.

Pengujian dinyatakan berhasil apabila mendapatkan balasan `64 bytes from ...` dan hasil akhirnya menunjukkan `0% packet loss`.

#### Bukti Hasil Praktikum

Bukti praktikum berupa screenshot hasil konfigurasi dan pengujian melalui Console GNS3. Setiap screenshot harus memperlihatkan perintah yang dijalankan beserta hasilnya.

#### Bukti 1 — Tabel Routing Router Gendo

**Perintah yang dijalankan:**

```bash
ip route
```

**Tujuan:** Membuktikan bahwa Gendo telah memiliki default route menuju NAT1 dan static route menuju seluruh cabang jaringan.

**Screenshot:**

<img width="960" height="516" alt="image" src="https://github.com/user-attachments/assets/8e5d1ee1-b674-40c1-87fe-457c8a363173" />

#### Bukti 2 — Tabel Routing Router Cabang

**Perintah yang dijalankan pada Shigeru:**

```bash
ip route
```

**Tujuan:** Membuktikan bahwa router cabang memiliki default route menuju Gendo serta route menuju jaringan turunannya.

**Screenshot:**

<img width="960" height="516" alt="image" src="https://github.com/user-attachments/assets/f7bbbb28-b3e2-4937-98d6-fe898d5293f8" />

#### Bukti 3 — Konfigurasi IP dan Gateway Armisael

**Perintah yang dijalankan:**

```bash
ip -br addr
ip route
```

**Tujuan:** Membuktikan bahwa Armisael telah memiliki IP address dan default gateway yang sesuai.

**Screenshot:**

<img width="960" height="516" alt="image" src="https://github.com/user-attachments/assets/e53f970b-befa-46aa-8602-2aa823b458bc" />

#### Bukti 4 — Pengujian Armisael ke Lilith

**Perintah yang dijalankan:**

```bash
ping -c 4 192.225.4.74
```

**Tujuan:** Membuktikan konektivitas Armisael menuju Lilith.

**Screenshot:**

<img width="960" height="516" alt="image" src="https://github.com/user-attachments/assets/4a961155-68b6-4dd6-9d65-03381e64652f" />

#### Bukti 5 — Pengujian Armisael ke Sachiel

**Perintah yang dijalankan:**

```bash
ping -c 4 192.225.3.130
```

**Tujuan:** Membuktikan konektivitas Armisael menuju Sachiel.

**Screenshot:**

<img width="960" height="516" alt="image" src="https://github.com/user-attachments/assets/9afc2a00-29f2-48b7-b623-6efa86a00096" />

#### Bukti 6 — Pengujian Armisael ke Comm-Net

**Perintah yang dijalankan:**

```bash
ping -c 4 192.225.2.2
```

**Tujuan:** Membuktikan konektivitas Armisael menuju Comm-Net.

**Screenshot:**

<img width="960" height="516" alt="image" src="https://github.com/user-attachments/assets/8a18687b-e9a5-4928-be06-49b97d3a80f0" />

HASIL:

<img width="960" height="516" alt="image" src="https://github.com/user-attachments/assets/b37ad9ac-1d32-44c0-bae4-463a52f0e2c9" />

#### Kesimpulan

Berdasarkan  konfigurasi routing statis dilakukan dengan mengatur default route pada setiap router dan menambahkan static route pada router yang memiliki jaringan cabang. Konfigurasi terlebih dahulu dilakukan secara manual, kemudian diterapkan kembali menggunakan script Bash agar lebih praktis.

Route summarization diterapkan pada jaringan cabang Shigeru untuk mengurangi jumlah entri routing pada Gendo. Keberhasilan konfigurasi dibuktikan melalui pemeriksaan tabel routing dan pengujian konektivitas dari Armisael menuju Lilith, Sachiel, dan Comm-Net.

**Catatan hasil:** Praktikum dinyatakan berhasil apabila seluruh pengujian ping mendapatkan balasan dan menunjukkan `0% packet loss`.

### SOAL 4 — KONFIGURASI NAT DAN AKSES INTERNET MELALUI GENDO

Mengonfigurasi Gendo sebagai router NAT agar seluruh jaringan internal dapat mengakses internet melalui NAT1. Konfigurasi menggunakan MASQUERADE agar tetap menyesuaikan alamat IP DHCP pada NAT1.

#### Konfigurasi Manual NAT pada Gendo

Konfigurasi dilakukan pada router Gendo agar seluruh jaringan internal dapat mengakses internet melalui interface NAT1 (`eth0`).

**1. Mengaktifkan IP Forwarding**

Pada Console Gendo, jalankan:

```bash
sysctl -w net.ipv4.ip_forward=1
```

Memastikan IP Forwarding aktif:

```bash
cat /proc/sys/net/ipv4/ip_forward
```

Hasil yang diharapkan adalah `1`.

<img width="952" height="59" alt="image" src="https://github.com/user-attachments/assets/52e89075-5251-4588-89ec-46ea3631c893" />

**2. Menambahkan aturan NAT**

Menambahkan aturan MASQUERADE untuk jaringan internal `192.225.0.0/21` yang keluar melalui `eth0`.

```bash
iptables -t nat -A POSTROUTING \
-s 192.225.0.0/21 \
-o eth0 \
-j MASQUERADE
```

**3. Memeriksa aturan NAT**

```bash
iptables -t nat -L POSTROUTING -n -v
```

Aturan MASQUERADE berhasil ditambahkan dengan source `192.225.0.0/21` dan interface keluar `eth0`.

**Bukti:**

<img width="959" height="70" alt="image" src="https://github.com/user-attachments/assets/d97cdc92-70e3-42cb-8328-f781c223fcc7" />

####  Pengujian Akses Internet dan DNS

Pengujian dilakukan pada Armisael dan Lilith untuk memastikan jaringan internal dapat mengakses internet dan melakukan resolusi domain.

**1. Pengujian pada Armisael**

Memeriksa gateway:

```bash
ping -c 4 192.225.4.81
```

Menguji koneksi internet:

```bash
ping -c 4 8.8.8.8
```

Mengatur DNS karena `/etc/resolv.conf` masih kosong:

```bash
echo "nameserver 192.168.122.1" > /etc/resolv.conf
```

Menguji resolusi dan koneksi domain:

```bash
getent hosts deb.debian.org
ping -4 -c 4 deb.debian.org
```

Hasil pengujian menunjukkan gateway, koneksi internet, dan DNS berhasil.

**Bukti:**

<img width="960" height="516" alt="image" src="https://github.com/user-attachments/assets/6f263dec-233a-4af4-8c94-80061b993d78" />

**2. Pengujian pada Lilith**

Memeriksa gateway:

```bash
ping -c 4 192.225.4.73
```

Menguji koneksi internet:

```bash
ping -c 4 8.8.8.8
```

Mengatur DNS:

```bash
echo "nameserver 192.168.122.1" > /etc/resolv.conf
```

Menguji resolusi dan koneksi domain:

```bash
getent hosts deb.debian.org
ping -4 -c 4 deb.debian.org
```

Hasil pengujian menunjukkan gateway, koneksi internet, dan DNS berhasil.

**Bukti:**

<img width="960" height="516" alt="image" src="https://github.com/user-attachments/assets/33129d79-f97d-4b29-a832-810d715eb95b" />

#### Pembuatan dan Pengujian Script NAT Gendo

Setelah konfigurasi manual berhasil, dibuat script agar konfigurasi NAT dapat diterapkan kembali dengan mudah.

**1. Membuat script**

Pada Console Gendo:

```bash
cat > /root/gendo_nat.sh <<'EOF'
#!/bin/sh

echo "===== AKTIFKAN IP FORWARDING ====="
sysctl -w net.ipv4.ip_forward=1

echo "===== KONFIGURASI NAT ====="
iptables -t nat -C POSTROUTING \
-s 192.225.0.0/21 -o eth0 -j MASQUERADE 2>/dev/null || \
iptables -t nat -A POSTROUTING \
-s 192.225.0.0/21 -o eth0 -j MASQUERADE

echo "===== HASIL NAT ====="
iptables -t nat -L POSTROUTING -n -v

echo "Konfigurasi NAT Gendo selesai."
EOF
```

**2. Menjalankan script**

```bash
chmod +x /root/gendo_nat.sh
/root/gendo_nat.sh
```

Script berhasil dijalankan, IP Forwarding aktif, dan aturan NAT tetap satu sehingga tidak terjadi duplikasi.

**Bukti:**

<img width="959" height="138" alt="image" src="https://github.com/user-attachments/assets/857d8623-b72d-4266-8a77-bacfbac56486" />

#### Verifikasi Counter NAT

Pemeriksaan dilakukan pada Console Gendo untuk memastikan paket dari jaringan internal telah melewati aturan NAT.

```bash
iptables -t nat -L POSTROUTING -n -v
```

Hasil pengujian menunjukkan:

- Paket yang melewati NAT: **11 packets**
- Data yang diproses: **804 bytes**
- Target: `MASQUERADE`
- Interface keluar: `eth0`
- Source: `192.225.0.0/21`

**Bukti:**

<img width="959" height="56" alt="image" src="https://github.com/user-attachments/assets/5ba26b5f-45bb-4c27-b085-d1e08326a548" />

#### Kesimpulan

Konfigurasi NAT pada router Gendo berhasil dilakukan menggunakan MASQUERADE melalui interface NAT1 (`eth0`). IP Forwarding berhasil diaktifkan sehingga jaringan internal dapat mengakses internet.

Pengujian pada Armisael dan Lilith menunjukkan koneksi ke `8.8.8.8` serta domain `deb.debian.org` berhasil tanpa packet loss. Counter NAT juga menunjukkan 11 paket dan 804 bytes telah diproses. Dengan demikian, konfigurasi dan pengujian utama Soal 4 berhasil dilakukan.

### SOAL 5 — KONFIGURASI FIREWALL DAN PEMBATASAN AKSES PADA GENDO

Mengonfigurasi firewall pada router Gendo agar koneksi baru dari NAT1 tidak dapat masuk, tetapi jaringan internal tetap dapat mengakses internet, berkomunikasi antar-LAN, dan mengakses Gendo. Konfigurasi menggunakan policy DROP dengan aturan ACCEPT untuk traffic yang diizinkan.

#### Konfigurasi Manual Firewall pada Gendo

Konfigurasi dilakukan pada Console Gendo dengan mengubah policy INPUT dan FORWARD menjadi DROP serta menambahkan aturan untuk traffic yang diperbolehkan.

**1. Membersihkan aturan filter lama**

```bash
iptables -F INPUT
iptables -F FORWARD
```

**2. Mengizinkan loopback dan koneksi balasan**

```bash
iptables -A INPUT -i lo -j ACCEPT

iptables -A INPUT -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT
iptables -A FORWARD -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT
```

Aturan ini mengizinkan komunikasi loopback serta paket balasan dari koneksi yang sudah terbentuk.

**3. Mengizinkan DHCP dari NAT1**

```bash
iptables -A INPUT -i eth0 -p udp --sport 67 --dport 68 -j ACCEPT
```

Aturan ini mempertahankan penerimaan balasan DHCP dari NAT1 agar alamat IP Gendo tetap dapat diperoleh secara dinamis.

**4. Mengizinkan traffic jaringan internal**

Mengizinkan jaringan internal mengakses internet melalui NAT1:

```bash
iptables -A FORWARD -s 192.225.0.0/21 -o eth0 -j ACCEPT
```

Mengizinkan komunikasi antar-LAN:

```bash
iptables -A FORWARD -s 192.225.0.0/21 -d 192.225.0.0/21 -j ACCEPT
```

Mengizinkan jaringan internal mengakses Gendo:

```bash
iptables -A INPUT -s 192.225.0.0/21 -j ACCEPT
```

**5. Mengubah default policy menjadi DROP**

```bash
iptables -P INPUT DROP
iptables -P FORWARD DROP
iptables -P OUTPUT ACCEPT
```

Dengan konfigurasi tersebut, koneksi baru dari sisi NAT1 ditolak, sedangkan traffic yang telah diizinkan tetap berjalan.

**6. Memeriksa aturan firewall**

```bash
iptables -S
```

Hasil pemeriksaan menunjukkan:

```text
-P INPUT DROP
-P FORWARD DROP
-P OUTPUT ACCEPT
```

Aturan ACCEPT untuk loopback, koneksi balasan, DHCP, dan jaringan internal juga berhasil ditambahkan.

**Bukti:**

<img width="960" height="516" alt="image" src="https://github.com/user-attachments/assets/9c9b1090-70a9-49b4-90ea-de128e2aa732" />

#### Pengujian Firewall dan Koneksi Internet

Pengujian dilakukan untuk memastikan firewall tidak mengganggu akses internet dari jaringan internal.

**1. Pengujian pada Armisael**

Pada Console Armisael, jalankan:

```bash
ping -c 4 8.8.8.8
```

Hasil pengujian menunjukkan koneksi internet tetap berhasil dengan 4 paket diterima dan 0% packet loss.

**Bukti:**

<img width="960" height="516" alt="image" src="https://github.com/user-attachments/assets/da863cae-23e4-44af-bb82-9135b38c134e" />

#### Pembuatan dan Pengujian Script Firewall Gendo

Setelah konfigurasi manual berhasil, konfigurasi firewall dan NAT dimasukkan ke dalam script agar dapat diterapkan kembali dengan mudah.

**1. Membuat script**

Pada Console Gendo, script disimpan dengan nama `/root/gendo-firewall.sh`.

```bash
cat > /root/gendo-firewall.sh <<'EOF'
#!/bin/sh

echo "===== AKTIFKAN IP FORWARDING ====="
sysctl -w net.ipv4.ip_forward=1

echo "===== KONFIGURASI NAT ====="
iptables -t nat -C POSTROUTING \
-s 192.225.0.0/21 -o eth0 -j MASQUERADE 2>/dev/null || \
iptables -t nat -A POSTROUTING \
-s 192.225.0.0/21 -o eth0 -j MASQUERADE

echo "===== RESET FILTER ====="
iptables -F INPUT
iptables -F FORWARD

echo "===== IZINKAN LOOPBACK ====="
iptables -A INPUT -i lo -j ACCEPT

echo "===== IZINKAN KONEKSI BALASAN ====="
iptables -A INPUT -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT
iptables -A FORWARD -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT

echo "===== IZINKAN DHCP NAT1 ====="
iptables -A INPUT -i eth0 -p udp --sport 67 --dport 68 -j ACCEPT

echo "===== IZINKAN INTERNAL KE INTERNET ====="
iptables -A FORWARD -s 192.225.0.0/21 -o eth0 -j ACCEPT

echo "===== IZINKAN ANTAR-LAN ====="
iptables -A FORWARD -s 192.225.0.0/21 -d 192.225.0.0/21 -j ACCEPT

echo "===== IZINKAN INTERNAL KE GENDO ====="
iptables -A INPUT -s 192.225.0.0/21 -j ACCEPT

echo "===== DEFAULT POLICY ====="
iptables -P INPUT DROP
iptables -P FORWARD DROP
iptables -P OUTPUT ACCEPT

echo "===== HASIL FIREWALL ====="
iptables -S

echo "===== HASIL NAT ====="
iptables -t nat -S

echo "Konfigurasi firewall Gendo selesai."
EOF
```

**2. Menjalankan script**

Memberikan izin eksekusi dan menjalankan script:

```bash
chmod +x /root/gendo-firewall.sh
/root/gendo-firewall.sh
```

Script mengaktifkan IP Forwarding, mempertahankan aturan NAT Soal 4, dan menerapkan aturan firewall dengan policy DROP. Konfigurasi IP dan static routing dari soal sebelumnya tetap dipertahankan.

**Bukti:**

<img width="960" height="516" alt="image" src="https://github.com/user-attachments/assets/cdb5ad3f-2848-42a1-bc16-b557058fe078" />

#### Verifikasi Aturan Firewall

Pemeriksaan akhir dilakukan pada Console Gendo menggunakan perintah:

```bash
iptables -S
```

Memeriksa aturan NAT agar konfigurasi Soal 4 tetap berjalan:

```bash
iptables -t nat -L POSTROUTING -n -v
```

Hasil yang diharapkan menunjukkan policy INPUT dan FORWARD tetap DROP, sedangkan aturan MASQUERADE tetap tersedia melalui eth0.

**Bukti:**

<img width="960" height="516" alt="image" src="https://github.com/user-attachments/assets/fb7cd743-3590-4b77-bd93-b77d37019537" />

#### Kesimpulan

Konfigurasi firewall pada router Gendo berhasil dilakukan dengan menerapkan policy DROP pada INPUT dan FORWARD. Aturan ACCEPT ditambahkan untuk mengizinkan loopback, DHCP NAT1, koneksi balasan, akses jaringan internal ke internet, komunikasi antar-LAN, serta akses internal ke Gendo. Pengujian dari Armisael menunjukkan koneksi ke 8.8.8.8 tetap berhasil dengan 0% packet loss. Dengan demikian, firewall berhasil membatasi koneksi baru dari NAT1 tanpa mengganggu akses jaringan internal.

### SOAL 6 — KONFIGURASI IP ADDRESS STATIS DAN DEFAULT GATEWAY PADA SELURUH HOST NON-ROUTER

Mengonfigurasi IP address statis dan default gateway pada 25 node non-router sesuai tabel pengalamatan Soal 2. Konfigurasi disimpan pada `/etc/network/interfaces` agar IP address dan gateway tetap digunakan setelah node dijalankan ulang.

#### Konfigurasi IP Address Secara Manual

Konfigurasi manual dilakukan melalui Console masing-masing node dengan mengatur alamat IP, netmask, dan gateway sesuai tabel pengalamatan.

**1. Memeriksa konfigurasi awal**

```bash
ip -br addr
ip route
cat /etc/network/interfaces
```

**2. Membuat backup konfigurasi**

```bash
cp /etc/network/interfaces /etc/network/interfaces.backup
```

**3. Mengedit konfigurasi jaringan**

```bash
nano /etc/network/interfaces
```

Contoh konfigurasi pada Unit-01:

```text
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
    address 192.225.4.66
    netmask 255.255.255.248
    gateway 192.225.4.65
```

Alamat IP, netmask, dan gateway disesuaikan dengan masing-masing node.

Simpan konfigurasi menggunakan `Ctrl + O`, Enter, kemudian keluar dengan `Ctrl + X`.

**4. Memeriksa hasil konfigurasi**

```bash
ip -br addr
ip route
```

**5. Menguji koneksi ke gateway**

Pada Console Unit-01:

```bash
ping -c 4 192.225.4.65
```

Pengujian manual dilakukan pada Unit-01, Unit-02, Unit-00, Quarters, dan Comm-Net. Hasil pengujian menunjukkan koneksi ke gateway berhasil dengan 4 paket diterima dan 0% packet loss.

**Bukti:**

<img width="960" height="516" alt="image" src="https://github.com/user-attachments/assets/c1de3cc4-86a8-428d-97aa-9f5bb1ffac8d" />

#### Konfigurasi IP Address Menggunakan Script

Setelah konfigurasi manual, digunakan script terpisah untuk setiap node agar proses konfigurasi lebih mudah dan konsisten. Setiap script memiliki nama sesuai node, misalnya `quarters_ip.sh`, `comm-net_ip.sh`, dan `unit-01_ip.sh`.

Script melakukan tiga proses utama, yaitu menyimpan konfigurasi ke `/etc/network/interfaces`, memasang IP address dan default gateway secara langsung, serta menampilkan hasil pemeriksaan IP dan ping gateway.

**1. Membuat script konfigurasi**

Contoh pada Console Quarters:

```bash
cat > /root/quarters_ip.sh <<'EOF'
#!/bin/sh
printf 'auto lo\niface lo inet loopback\nauto eth0\niface eth0 inet static\n    address 192.225.0.2\n    netmask 255.255.254.0\n    gateway 192.225.0.1\n' > /etc/network/interfaces

ip addr flush dev eth0
ip addr add 192.225.0.2/23 dev eth0
ip link set eth0 up
ip route replace default via 192.225.0.1

echo "== ip -br =="
ip -br addr

echo "== ping gateway =="
ping -c 2 -W 1 192.225.0.1 && echo "OK" || echo "GAGAL"
EOF
```

Script serupa dibuat pada setiap node dengan menyesuaikan nama file, alamat IP, prefix, netmask, dan gateway.

**2. Memberikan izin eksekusi dan menjalankan script**

Contoh pada Quarters:

```bash
chmod +x /root/quarters_ip.sh
/root/quarters_ip.sh
```

Perintah tersebut juga diterapkan pada script node lainnya dengan menyesuaikan nama file.

**3. Memeriksa hasil konfigurasi**

```bash
ip -br addr
ip route
```

Hasil pemeriksaan menampilkan alamat IP pada interface `eth0` dan default gateway sesuai tabel pengalamatan.

**Bukti:**

<img width="960" height="516" alt="image" src="https://github.com/user-attachments/assets/b129aa5b-abfa-4497-8552-41e9d444ebc2" />

#### Pengujian Konektivitas dan Ketahanan Konfigurasi

Pengujian dilakukan untuk memastikan alamat IP dan gateway telah terpasang serta konfigurasi tetap tersedia setelah node dijalankan ulang.

**1. Pengujian IP address dan gateway Unit-01**

```bash
ip -br addr
ip route
ping -c 2 192.225.4.65
```

Hasil yang diharapkan adalah Unit-01 memiliki IP `192.225.4.66/29` dan dapat terhubung ke gateway `192.225.4.65`.

**2. Pengujian setelah restart node**

Node Unit-01 dihentikan dengan memilih **Stop**, kemudian dijalankan kembali menggunakan **Start** pada GNS3.

Setelah node aktif, jalankan:

```bash
ip -br addr
ping -c 2 192.225.4.65
```

Pengujian ini memastikan IP address tetap terpasang dan koneksi ke gateway tetap berhasil setelah node dijalankan ulang.

Jika konfigurasi tidak bertahan setelah restart, konfigurasi jaringan dapat dimasukkan melalui menu **Edit config** pada node Docker GNS3.

**Bukti:**

<img width="960" height="516" alt="image" src="https://github.com/user-attachments/assets/c33e461e-7d89-439f-8314-798514a84b21" />

#### Kesimpulan

Konfigurasi IP address statis dan default gateway dilakukan pada 25 node non-router sesuai tabel pengalamatan Soal 2. Pengerjaan dilakukan secara manual dan menggunakan 25 script terpisah sesuai nama masing-masing node. Setiap script menyimpan konfigurasi ke `/etc/network/interfaces`, menerapkan IP address dan gateway secara langsung, serta melakukan pemeriksaan menggunakan `ip -br addr` dan `ping`. Pengujian pada Unit-01 setelah Stop dan Start digunakan untuk memastikan konfigurasi tetap tersedia setelah node dijalankan ulang.

### SOAL 7 — INSTALASI IPTABLES, NETCAT-TRADITIONAL, DAN AKTIVASI LISTENER PADA MAGI

Mengaktifkan MAGI-Casper, MAGI-Balthasar, dan MAGI-Melchior pada Switch Terminal agar dapat menerima pesan dari Lilith. Pengerjaan dilakukan dengan memasang `iptables` dan `netcat-traditional`, kemudian menjalankan TCP listener sesuai port pada glosarium. Pada tahap ini belum diterapkan aturan keamanan firewall karena pembahasan keamanan dilakukan pada soal berikutnya.

#### Instalasi Paket Secara Manual

Instalasi dilakukan melalui Console masing-masing node MAGI. Paket yang dipasang adalah `iptables` dan `netcat-traditional`.

**1. Mengatur DNS**

Sebelum instalasi, DNS diperiksa terlebih dahulu. Jika `/etc/resolv.conf` kosong, DNS diatur menggunakan:

```bash
cat > /etc/resolv.conf <<'EOF'
nameserver 1.1.1.1
nameserver 8.8.8.8
EOF
```

**2. Memeriksa koneksi internet**

```bash
ping -c 3 192.168.122.1
ping -c 3 1.1.1.1
getent hosts deb.debian.org
```

Pengujian dilakukan untuk memastikan gateway, koneksi internet, dan resolusi DNS berjalan dengan baik.

**3. Memasang paket pada setiap MAGI**

Perintah berikut dijalankan pada Console MAGI-Casper, MAGI-Balthasar, dan MAGI-Melchior:

```bash
apt-get update
apt-get install -y iptables netcat-traditional
```

**4. Memeriksa hasil instalasi**

```bash
iptables --version
nc.traditional -h
```

Hasil pemeriksaan menunjukkan `iptables` versi 1.8.11 dan `netcat-traditional` versi 1.10-50 berhasil terpasang pada ketiga MAGI.

**Bukti:**

MAGI-CASPER

<img width="960" height="516" alt="image" src="https://github.com/user-attachments/assets/6cff64a2-4a6e-46b6-9dd4-1625fced374a" />

<img width="960" height="516" alt="image" src="https://github.com/user-attachments/assets/6b665beb-2b2b-44d6-9d60-77ced282f26b" />


MAGI-BALTHASAR

<img width="960" height="516" alt="image" src="https://github.com/user-attachments/assets/1551215c-c18b-408a-8266-f17d805369da" />

<img width="960" height="516" alt="image" src="https://github.com/user-attachments/assets/9c412577-f5cf-4944-a71d-9a3a70a1cad1" />

MAGI-MELCHIOR

<img width="960" height="516" alt="image" src="https://github.com/user-attachments/assets/73283e8f-2d69-4f63-b4f8-7576ed82e514" />

<img width="960" height="516" alt="image" src="https://github.com/user-attachments/assets/cd3d6dc3-ba35-4164-a326-f67496db83da" />

#### Aktivasi Listener Secara Manual

Setelah instalasi paket berhasil, listener dijalankan pada masing-masing MAGI menggunakan `netcat-traditional`.

**1. Mengaktifkan listener MAGI-Casper**

Pada Console MAGI-Casper, listener dijalankan pada port 5000:

```bash
nohup sh -c 'while true; do nc.traditional -l -v -n -p 5000 >> /root/nc_5000.log 2>&1; done' >/dev/null 2>&1 &
```

**2. Mengaktifkan listener MAGI-Balthasar**

Pada Console MAGI-Balthasar, listener dijalankan pada port 5000 dan 5001:

```bash
nohup sh -c 'while true; do nc.traditional -l -v -n -p 5000 >> /root/nc_5000.log 2>&1; done' >/dev/null 2>&1 &

nohup sh -c 'while true; do nc.traditional -l -v -n -p 5001 >> /root/nc_5001.log 2>&1; done' >/dev/null 2>&1 &
```

**3. Mengaktifkan listener MAGI-Melchior**

Pada Console MAGI-Melchior, listener dijalankan pada port 5000:

```bash
nohup sh -c 'while true; do nc.traditional -l -v -n -p 5000 >> /root/nc_5000.log 2>&1; done' >/dev/null 2>&1 &
```

**4. Memeriksa status listener**

Pada masing-masing MAGI, status port diperiksa menggunakan:

```bash
ss -ltn
```

Hasil pemeriksaan menunjukkan port 5000 aktif pada Casper dan Melchior, sedangkan Balthasar menggunakan port 5000 dan 5001.

**Bukti:**

[LISTENER_CASPER]

<img width="960" height="516" alt="image" src="https://github.com/user-attachments/assets/0436ac4b-f63a-4660-8b47-9dd0ededfea8" />

[LISTENER_BALTHASAR]

<img width="960" height="516" alt="image" src="https://github.com/user-attachments/assets/a0b435cf-fdc1-484c-926d-02fde7860b5e" />

[LISTENER_MELCHIOR]

<img width="960" height="516" alt="image" src="https://github.com/user-attachments/assets/e62eaf97-8132-432d-a942-a3982708ce24" />

#### Konfigurasi Menggunakan Script

Setelah pengujian manual, konfigurasi dibuat menggunakan script terpisah agar instalasi paket dan aktivasi listener lebih mudah dijalankan kembali. Script disimpan pada direktori `/root/` dengan nama sesuai node dan fungsi masing-masing.

**1. Membuat script instalasi paket**

Contoh pada MAGI-Casper:

```bash
cat > /root/magi-casper_install.sh <<'EOF'
#!/bin/sh
export DEBIAN_FRONTEND=noninteractive

apt-get update -qq
apt-get install -y iptables netcat-traditional
update-alternatives --set nc /bin/nc.traditional

echo "=== CEK IPTABLES ==="
iptables --version

echo "=== CEK NETCAT ==="
nc.traditional -h 2>&1 | head -n 2

echo "Instalasi MAGI-Casper selesai"
EOF
```

Script serupa dibuat pada MAGI-Balthasar dan MAGI-Melchior dengan menyesuaikan nama file dan pesan node.

Nama script instalasi:

- `magi-casper_install.sh`
- `magi-balthasar_install.sh`
- `magi-melchior_install.sh`

**2. Membuat script listener**

Contoh pada MAGI-Casper:

```bash
cat > /root/magi-casper_listener.sh <<'EOF'
#!/bin/sh
PORTS="5000"

stop_listener() {
  for d in /proc/[0-9]*; do
    c=$(tr '\0' ' ' < "$d/cmdline" 2>/dev/null)
    case "$c" in
      *"while true; do nc -l"*" -p $1 "*)
        kill "${d#/proc/}" 2>/dev/null
        ;;
    esac
  done
}

start_listener() {
  stop_listener "$1"
  nohup sh -c "while true; do nc -l -v -n -p $1 >> /root/nc_$1.log 2>&1; done" >/dev/null 2>&1 &
}

for p in $PORTS; do
  start_listener "$p"
done

sleep 1
echo "=== LISTENER CASPER ==="
ss -ltn | grep ':5000'
echo "=== LOG PESAN ==="
tail -n 5 /root/nc_5000.log 2>/dev/null
EOF
```

Script listener dibuat terpisah pada ketiga MAGI dengan pengaturan port sesuai kebutuhan:

| Node | Nama script | Port |
|---|---|---|
| MAGI-Casper | `magi-casper_listener.sh` | 5000 |
| MAGI-Balthasar | `magi-balthasar_listener.sh` | 5000 dan 5001 |
| MAGI-Melchior | `magi-melchior_listener.sh` | 5000 |

**3. Memberikan izin eksekusi dan menjalankan script**

Contoh pada MAGI-Casper:

```bash
chmod +x /root/magi-casper_install.sh
/root/magi-casper_install.sh

chmod +x /root/magi-casper_listener.sh
/root/magi-casper_listener.sh
```

Perintah yang sama diterapkan pada Balthasar dan Melchior dengan menyesuaikan nama script masing-masing.

**Bukti:**

MAGI-Casper

<img width="960" height="516" alt="image" src="https://github.com/user-attachments/assets/300b932f-1b56-42d9-b561-e42ff02e2b79" />

Magi-Balthasar

<img width="960" height="516" alt="image" src="https://github.com/user-attachments/assets/a929c68c-da06-4217-8307-bbba01f82d25" />

Magi-Melchior

<img width="960" height="516" alt="image" src="https://github.com/user-attachments/assets/f653b9c5-e453-4e1b-bf9c-18b305f47bc5" />

#### Pengiriman Pesan dari Lilith

Setelah ketiga listener aktif, Lilith digunakan untuk mengirim pesan ke seluruh MAGI melalui alamat IP dan port yang telah ditentukan.

**1. Membuat script pengiriman pesan**

Pada Console Lilith dibuat script `/root/lilith_kirim-pesan.sh`:

```bash
cat > /root/lilith_kirim-pesan.sh <<'EOF'
#!/bin/sh

export DEBIAN_FRONTEND=noninteractive
apt-get update -qq
apt-get install -y netcat-traditional

update-alternatives --set nc /bin/nc.traditional

kirim() {
  echo "$3" | nc -w 2 "$1" "$2"
  echo "exit=$? -> $1:$2"
}

echo "=== PENGIRIMAN PESAN DARI LILITH ==="

kirim 192.225.4.58 5000 "Halo Magi-Casper, ini pesan dari Lilith"

kirim 192.225.4.59 5000 "Halo Magi-Balthasar port 5000, ini pesan dari Lilith"

kirim 192.225.4.59 5001 "Halo Magi-Balthasar port 5001, ini pesan dari Lilith"

kirim 192.225.4.60 5000 "Halo Magi-Melchior, ini pesan dari Lilith"

echo "=== PENGIRIMAN SELESAI ==="
EOF
```

**2. Memberikan izin eksekusi dan menjalankan script**

```bash
chmod +x /root/lilith_kirim-pesan.sh
/root/lilith_kirim-pesan.sh
```

Hasil pengujian menunjukkan keempat pengiriman berhasil dengan status `exit=0`.

**Bukti:**

<img width="960" height="516" alt="image" src="https://github.com/user-attachments/assets/3226e8db-646c-4885-81c7-aea4f2e0c627" />

#### Pengujian Listener dan Pesan yang Diterima

Pengujian dilakukan pada setiap MAGI untuk memastikan listener aktif dan pesan dari Lilith berhasil diterima.

**1. Pengujian MAGI-Casper**

```bash
ss -ltn | grep ':5000'
tail -n 5 /root/nc_5000.log
```

Hasil menunjukkan port 5000 berstatus `LISTEN` dan pesan dari Lilith berhasil diterima.

<img width="960" height="516" alt="image" src="https://github.com/user-attachments/assets/04f686ae-b1b0-4ccf-ad7d-73201e6d8516" />

**2. Pengujian MAGI-Balthasar**

```bash
ss -ltn | grep -E ':5000|:5001'
tail -n 5 /root/nc_5000.log /root/nc_5001.log
```

Hasil menunjukkan port 5000 dan 5001 berstatus `LISTEN`. Kedua port berhasil menerima pesan dari Lilith.

<img width="960" height="516" alt="image" src="https://github.com/user-attachments/assets/a10af17c-cda1-4307-8bf0-709902dc9a43" />

**3. Pengujian MAGI-Melchior**

```bash
ss -ltn | grep ':5000'
tail -n 5 /root/nc_5000.log
```

Hasil menunjukkan port 5000 berstatus `LISTEN` dan pesan dari Lilith berhasil diterima.

<img width="960" height="516" alt="image" src="https://github.com/user-attachments/assets/7c7867a5-f67d-47da-a18f-73e1f4ad6179" />

#### Kesimpulan

Aktivasi MAGI-Casper, MAGI-Balthasar, dan MAGI-Melchior berhasil dilakukan melalui instalasi `iptables` dan `netcat-traditional`, kemudian menjalankan TCP listener sesuai port yang ditentukan. Pengerjaan dilakukan secara manual dan dilanjutkan menggunakan script terpisah untuk instalasi serta aktivasi listener pada setiap node. Lilith berhasil mengirimkan empat pesan ke ketiga MAGI, termasuk dua pesan ke MAGI-Balthasar melalui port 5000 dan 5001. Seluruh pengiriman menghasilkan `exit=0` dan pesan berhasil ditampilkan pada log masing-masing node. Dengan demikian, seluruh tahapan Soal 7 berhasil diselesaikan tanpa menerapkan aturan firewall, sesuai instruksi soal.

### SOAL 8 — KONFIGURASI LAYANAN TCP MENGGUNAKAN NETCAT PADA PEN-PEN DAN TOKYO3-CORE

Mengonfigurasi layanan TCP menggunakan Netcat pada node Pen-Pen dan Tokyo3-Core. Pen-Pen menyediakan layanan pada port 80 dengan pesan `Welcome to Pen-Pen`, sedangkan Tokyo3-Core menyediakan layanan pada port 80 dengan pesan `Welcome to Tokyo3-Core` dan port 8080 dengan pesan `syifa imutz`. Pengujian dilakukan dari node Lilith menggunakan Netcat. Selain itu, port 22 diuji untuk memastikan koneksi langsung ditolak karena tidak menyediakan layanan.

#### Konfigurasi Layanan TCP Secara Manual

Konfigurasi manual dilakukan melalui Console masing-masing node dengan menjalankan Netcat sebagai listener pada port yang ditentukan.

**1. Memeriksa Netcat**

Pada Console Pen-Pen dan Tokyo3-Core:

```bash
command -v nc
command -v nc.openbsd
command -v nc.traditional
```

Hasil pemeriksaan menunjukkan kedua node memiliki Netcat OpenBSD (`/usr/bin/nc.openbsd`), sehingga tidak perlu menginstal Netcat tambahan.

**2. Menjalankan layanan pada Pen-Pen**

Pada Console Pen-Pen, jalankan:

```bash
while true; do
    printf "Welcome to Pen-Pen\n" | nc.openbsd -l -n -p 80
done
```

Perintah tersebut menjalankan listener pada port 80 dan mengirimkan pesan `Welcome to Pen-Pen` ketika menerima koneksi.

**3. Menjalankan layanan pada Tokyo3-Core**

Pada Console Tokyo3-Core, jalankan layanan port 80:

```bash
while true; do
    printf "Welcome to Tokyo3-Core\n" | nc.openbsd -l -n -p 80
done
```

Kemudian, jalankan layanan port 8080:

```bash
while true; do
    printf "syifa imutz\n" | nc.openbsd -l -n -p 8080
done
```

Kedua layanan dijalankan secara terpisah agar masing-masing port dapat menerima koneksi.

**4. Memeriksa status listener**

Pada Pen-Pen:

```bash
ss -ltn | grep ':80 '
```

Pada Tokyo3-Core:

```bash
ss -ltn | grep -E ':80 |:8080 '
```

Hasil pemeriksaan menunjukkan port 80 pada Pen-Pen serta port 80 dan 8080 pada Tokyo3-Core berstatus `LISTEN`.

**Bukti:**

[konfigurasi manual dan status listener Pen-Pen]

<img width="960" height="516" alt="image" src="https://github.com/user-attachments/assets/9b56bed4-c71a-44c9-8b0a-6ad418761768" />

[konfigurasi manual dan status listener Tokyo3-Core]

<img width="960" height="516" alt="image" src="https://github.com/user-attachments/assets/b834a405-05a9-4b4f-8009-5a0454880711" />

#### Konfigurasi Layanan TCP Menggunakan Script

Setelah konfigurasi manual, dibuat script terpisah agar layanan dapat dijalankan dengan lebih mudah dan konsisten. Script menggunakan `nc.openbsd` yang telah tersedia pada masing-masing node.

**1. Membuat script layanan Pen-Pen**

Pada Console Pen-Pen:

```bash
cat > /root/pen-pen_service.sh <<'EOF'
#!/bin/sh

NC="/usr/bin/nc.openbsd"

echo "=== LAYANAN PEN-PEN ==="

if [ ! -x "$NC" ]; then
    echo "ERROR: Netcat tidak ditemukan"
    exit 1
fi

if ss -ltn | grep -qE ':80[[:space:]]'; then
    echo "Port 80 sudah digunakan!"
    exit 1
fi

nohup sh -c '
while true; do
    printf "Welcome to Pen-Pen\n" |
    /usr/bin/nc.openbsd -l -n -p 80
done
' >/root/penpen-port80.log 2>&1 </dev/null &

sleep 2

echo "=== STATUS PORT 80 ==="
ss -ltn | grep ':80 '

echo "Layanan Pen-Pen selesai."
EOF
```

**2. Membuat script layanan Tokyo3-Core**

Pada Console Tokyo3-Core:

```bash
cat > /root/tokyo3-core_service.sh <<'EOF'
#!/bin/sh

NC="/usr/bin/nc.openbsd"

echo "=== LAYANAN TOKYO3-CORE ==="

if [ ! -x "$NC" ]; then
    echo "ERROR: Netcat tidak ditemukan"
    exit 1
fi

if ! ss -ltn | grep -qE ':80[[:space:]]'; then
    nohup sh -c '
    while true; do
        printf "Welcome to Tokyo3-Core\n" |
        /usr/bin/nc.openbsd -l -n -p 80
    done
    ' >/root/tokyo-port80.log 2>&1 </dev/null &
fi

if ! ss -ltn | grep -qE ':8080[[:space:]]'; then
    nohup sh -c '
    while true; do
        printf "syifa imutz\n" |
        /usr/bin/nc.openbsd -l -n -p 8080
    done
    ' >/root/tokyo-port8080.log 2>&1 </dev/null &
fi

sleep 2

echo "=== STATUS PORT 80 DAN 8080 ==="
ss -ltn | grep -E ':80[[:space:]]|:8080[[:space:]]'

echo "Layanan Tokyo3-Core selesai."
EOF
```

**3. Memberikan izin eksekusi dan menjalankan script**

Pada Pen-Pen:

```bash
chmod +x /root/pen-pen_service.sh
/root/pen-pen_service.sh
```

Pada Tokyo3-Core:

```bash
chmod +x /root/tokyo3-core_service.sh
/root/tokyo3-core_service.sh
```

Script menjalankan listener di latar belakang menggunakan `nohup`, sehingga layanan tetap berjalan meskipun console ditinggalkan.

**4. Memeriksa hasil konfigurasi**

Pada Pen-Pen:

```bash
ss -ltn | grep ':80 '
```

Pada Tokyo3-Core:

```bash
ss -ltn | grep -E ':80 |:8080 '
```

Hasil pemeriksaan menunjukkan seluruh port layanan berstatus `LISTEN`.

**Bukti:**

[hasil eksekusi Pen-Pen]

<img width="960" height="516" alt="image" src="https://github.com/user-attachments/assets/0716b2cf-be2d-4f07-9680-59e78c014269" />

[hasil eksekusi Tokyo3-Core]

<img width="960" height="516" alt="image" src="https://github.com/user-attachments/assets/717ee72c-db93-4831-af0a-df382e2afe67" />

#### Pengujian Layanan TCP dari Lilith

Pengujian dilakukan melalui Console Lilith menggunakan script `/root/lilith_test_soal8.sh`. Pengujian bertujuan memastikan ketiga layanan dapat diakses dan port 22 tidak menerima koneksi.

**1. Menjalankan script pengujian**

Pada Console Lilith:

```bash
chmod +x /root/lilith_test_soal8.sh
/root/lilith_test_soal8.sh
```

**2. Hasil pengujian layanan Pen-Pen**

Pengujian dilakukan menuju alamat `192.225.3.195` pada port 80.

Hasil yang diperoleh:

```text
(UNKNOWN) [192.225.3.195] 80 (http) open
Welcome to Pen-Pen
Status koneksi: 0
```

**3. Hasil pengujian layanan Tokyo3-Core**

Pengujian menuju alamat `192.225.4.106` pada port 80 dan 8080.

Hasil yang diperoleh:

```text
(UNKNOWN) [192.225.4.106] 80 (http) open
Welcome to Tokyo3-Core
Status koneksi: 0
```

```text
(UNKNOWN) [192.225.4.106] 8080 (http-alt) open
syifa imutz
Status koneksi: 0
```

**4. Pengujian port 22**

Pengujian dilakukan pada port 22 Pen-Pen dan Tokyo3-Core untuk memastikan port yang tidak menyediakan layanan langsung menolak koneksi.

Hasil pengujian:

```text
192.225.3.195 port 22:
Connection refused

192.225.4.106 port 22:
Connection refused
```

Kedua hasil menunjukkan bahwa port 22 tidak menyediakan layanan dan koneksi langsung ditolak.

**Bukti:**

[hasil pengujian lengkap dari Console Lilith]

<img width="960" height="516" alt="image" src="https://github.com/user-attachments/assets/304dccf9-950e-4aec-8773-39c96230912b" />

#### Kesimpulan

Konfigurasi layanan TCP pada Pen-Pen dan Tokyo3-Core berhasil dilakukan secara manual dan menggunakan script. Pen-Pen berhasil menyediakan layanan port 80 dengan pesan `Welcome to Pen-Pen`. Tokyo3-Core berhasil menyediakan layanan port 80 dengan pesan `Welcome to Tokyo3-Core` dan port 8080 dengan pesan `syifa imutz`. Seluruh layanan berhasil diuji dari Lilith dengan status koneksi berhasil. Pengujian port 22 pada kedua node menghasilkan `Connection refused`, sesuai dengan ketentuan soal. Dengan demikian, seluruh konfigurasi dan pengujian Soal 8 berhasil diselesaikan.

### SOAL 9 — PERBAIKAN SABOTASE STATIC ROUTING PADA SHIGERU

Pada Soal 9 dilakukan pengujian sabotase dan perbaikan konfigurasi routing pada node Shigeru. Sabotase menyebabkan Lilith tidak dapat berkomunikasi dengan Armisael, meskipun Armisael masih dapat melakukan ping ke gateway-nya sendiri.

#### Menjalankan Script Sabotase

Sesuai instruksi soal, script sabotase `break_routing.sh` dijalankan pada Console Shigeru tanpa membaca isi script terlebih dahulu.

**1. Memberikan izin eksekusi dan menjalankan script sabotase**

```bash
chmod +x /root/break_routing.sh
/root/break_routing.sh
```

Script tersebut dijalankan untuk merusak konfigurasi routing pada Shigeru.

[menjalankan script sabotase pada Shigeru]

<img width="959" height="47" alt="image" src="https://github.com/user-attachments/assets/9790a5a0-c1d6-4b1f-baf2-6dea3c87f99c" />

**2. Memeriksa gejala setelah sabotase**

Pada Console Shigeru:

```bash
ip -br addr
ip route
ip rule show
sysctl net.ipv4.ip_forward
```

[hasil identifikasi kerusakan routing pada Shigeru]

<img width="959" height="272" alt="image" src="https://github.com/user-attachments/assets/c2275929-816b-4c92-8d3a-336ad0db74c1" />

Hasil pemeriksaan menunjukkan beberapa kerusakan, yaitu:
- IP forwarding dalam kondisi nonaktif (`0`).
- Terdapat rute `blackhole` menuju jaringan Lilith `192.225.4.72/29`.
- Terdapat policy routing dengan priority `90` yang mengarahkan paket dari `eth2` ke routing table 100.
- Routing table 100 memiliki rute `unreachable default`.

**3. Menguji konektivitas sebelum perbaikan**

Pada Console Lilith:

```bash
ping -c 4 -W 2 192.225.4.83
```

<img width="959" height="89" alt="image" src="https://github.com/user-attachments/assets/79bce721-bd73-4a6e-82fc-55ad8b0b8592" />

Hasil pengujian menunjukkan koneksi gagal dengan 100% packet loss. Hal ini membuktikan bahwa komunikasi dari Lilith menuju Armisael terputus akibat kerusakan routing pada Shigeru.

#### Perbaikan Routing Secara Manual

Perbaikan dilakukan melalui Console Shigeru dengan menghapus konfigurasi yang bermasalah dan mengembalikan jalur routing.

**1. Menghapus rute blackhole**

```bash
ip route del blackhole 192.225.4.72/29
```

Perintah ini menghapus rute yang menyebabkan paket menuju jaringan Lilith dibuang.

**2. Menghapus policy routing yang bermasalah**

```bash
ip rule del priority 90
```

Perintah ini menghapus aturan policy routing yang mengarahkan paket dari `eth2` ke routing table 100.

**3. Membersihkan routing table 100**

```bash
ip route flush table 100
```

Perintah ini menghapus rute `unreachable default` pada routing table 100.

**4. Menambahkan rute menuju jaringan Lilith**

```bash
ip route replace 192.225.4.72/29 via 192.225.4.157 dev eth0
```

Rute tersebut mengarahkan komunikasi menuju jaringan Lilith melalui gateway `192.225.4.157` pada interface `eth0`.

**5. Mengaktifkan IP forwarding**

```bash
echo 1 > /proc/sys/net/ipv4/ip_forward
```

IP forwarding diaktifkan agar Shigeru dapat meneruskan paket antarjaringan.

<img width="960" height="516" alt="image" src="https://github.com/user-attachments/assets/9c01835b-6c4a-47c4-b2ae-7cc75712d127" />

<img width="959" height="157" alt="image" src="https://github.com/user-attachments/assets/8dc80ff3-c409-4587-b566-10ad3b8d044b" />

#### Perbaikan Routing Menggunakan Script

Setelah perbaikan manual, dibuat script `perbaikan_shigeru.sh` untuk menjalankan seluruh proses perbaikan secara otomatis pada node Shigeru.

**1. Membuat script perbaikan**

Pada Console Shigeru:

```bash
cat > /root/perbaikan_shigeru.sh <<'EOF'
#!/bin/sh

echo "======================================"
echo " PERBAIKAN ROUTING SHIGERU - SOAL 9"
echo "======================================"

if [ "$(id -u)" != 0 ]; then
    echo "ERROR: Script harus dijalankan sebagai root."
    exit 1
fi

case "$(hostname)" in
    *[Ss]higeru*) ;;
    *)
        echo "ERROR: Script ini hanya untuk Shigeru."
        exit 1
        ;;
esac

echo "[1] Menghapus rute blackhole..."
ip route del blackhole 192.225.4.72/29 2>/dev/null

echo "[2] Menghapus policy routing priority 90..."
ip rule del priority 90 2>/dev/null

echo "[3] Membersihkan routing table 100..."
ip route flush table 100

echo "[4] Memperbaiki rute menuju jaringan Lilith..."
ip route replace 192.225.4.72/29 via 192.225.4.157 dev eth0

echo "[5] Mengaktifkan IP forwarding..."
sysctl -w net.ipv4.ip_forward=1

echo ""
echo "=== HASIL ROUTING ==="
ip route

echo ""
echo "=== HASIL POLICY ROUTING ==="
ip rule show

echo ""
echo "=== STATUS IP FORWARDING ==="
sysctl net.ipv4.ip_forward

echo ""
echo "=== PERBAIKAN SHIGERU SELESAI ==="
EOF
```

**2. Memberikan izin eksekusi dan menjalankan script**

```bash
chmod +x /root/perbaikan_shigeru.sh
/root/perbaikan_shigeru.sh
```

Script tersebut menghapus rute dan aturan yang bermasalah, memperbaiki rute menuju jaringan Lilith, serta mengaktifkan IP forwarding.


**3. Memeriksa hasil perbaikan**

```bash
ip route
ip rule show
ip route show table 100
sysctl net.ipv4.ip_forward
```

<img width="960" height="516" alt="image" src="https://github.com/user-attachments/assets/dc020909-a242-4616-b1b2-b759cc83a765" />

Hasil yang diharapkan:
- Rute menuju `192.225.4.72/29` menggunakan gateway `192.225.4.157` melalui `eth0`.
- Rute `blackhole` sudah tidak ada.
- Policy routing priority 90 sudah tidak ada.
- Routing table 100 sudah kosong.
- IP forwarding bernilai `1`.

#### Pengujian Konektivitas Lilith ke Armisael

Pengujian dilakukan untuk memastikan komunikasi antarjaringan kembali berjalan setelah perbaikan.

**1. Menguji koneksi dari Lilith ke Armisael**

Pada Console Lilith:

```bash
ping -c 4 -W 2 192.225.4.83
```

<img width="960" height="516" alt="image" src="https://github.com/user-attachments/assets/55389e8f-7fbb-42a2-adbe-af4002e00521" />

Hasil pengujian menunjukkan:

```text
4 packets transmitted, 4 received, 0% packet loss
```

Artinya, Lilith berhasil berkomunikasi kembali dengan Armisael setelah konfigurasi routing pada Shigeru diperbaiki.

#### Kesimpulan

Sabotase pada Soal 9 menyebabkan komunikasi antara Lilith dan Armisael terputus akibat IP forwarding yang dinonaktifkan, rute blackhole menuju jaringan Lilith, serta policy routing yang mengarahkan paket ke routing table 100 dengan rute unreachable. Perbaikan dilakukan secara manual dan menggunakan script perbaikan_shigeru.sh pada Shigeru. Setelah rute diperbaiki dan IP forwarding diaktifkan, pengujian menunjukkan Lilith berhasil melakukan ping ke Armisael dengan 4 paket diterima dan 0% packet loss. Dengan demikian, konektivitas antarjaringan berhasil dipulihkan.

### SOAL 10 — PERBAIKAN SABOTASE NAT PADA MISATO DAN GENDO

Pada Soal 10 dilakukan pengujian dan perbaikan konfigurasi Network Address Translation (NAT) pada router Misato dan Gendo. Sabotase menyebabkan Unit-01, Unit-02, dan Unit-00 pada jaringan Cage tidak dapat melakukan ping ke internet (`8.8.8.8`), sedangkan Spy pada jaringan Intel tetap dapat mengakses internet. Koneksi dari Cage menuju Lilith tetap normal.

#### Pengerjaan Secara Manual

Pengerjaan manual dilakukan dengan menjalankan script sabotase pada kedua router, memeriksa kerusakan konfigurasi NAT, kemudian memperbaikinya secara langsung melalui Console masing-masing node.

**1. Menjalankan script sabotase pada Misato**

File `break_nat.sh` dimasukkan ke Console Misato menggunakan perintah:

```bash
cat > /root/break_nat.sh <<'EOF'
```

Kemudian seluruh isi script sabotase yang diberikan pada soal dimasukkan hingga penutup `EOF`.

Setelah file dibuat, jalankan:

```bash
chmod +x /root/break_nat.sh
/root/break_nat.sh
```

**2. Menjalankan script sabotase pada Gendo**

File `break_nat.sh` yang sama juga dimasukkan ke Console Gendo. Setelah selesai, jalankan:

```bash
chmod +x /root/break_nat.sh
/root/break_nat.sh
```

**3. Memeriksa konfigurasi NAT pada Misato**

Pada Console Misato:

```bash
ip -br addr
ip route
sysctl net.ipv4.ip_forward
iptables -t nat -L POSTROUTING -n -v --line-numbers
```

Pemeriksaan menunjukkan adanya aturan SNAT yang mengubah alamat sumber jaringan Cage menjadi `172.31.99.1`.

**4. Memeriksa konfigurasi NAT pada Gendo**

Pada Console Gendo:

```bash
ip -br addr
ip route
sysctl net.ipv4.ip_forward
iptables -t nat -L POSTROUTING -n -v --line-numbers
```

Pemeriksaan dilakukan untuk menemukan aturan `RETURN` yang menghalangi proses NAT bagi paket dari jaringan Cage.

**5. Menguji kondisi sebelum perbaikan**

Pada Console Unit-01:

```bash
ping -c 4 -W 2 8.8.8.8
```

Kemudian menguji koneksi menuju Lilith:

```bash
ping -c 4 -W 2 192.225.4.74
```

Kondisi setelah sabotase yang diharapkan adalah ping internet gagal, tetapi koneksi dari Cage ke Lilith tetap berhasil.

**6. Memperbaiki NAT pada Misato**

Pada Console Misato, hapus aturan SNAT yang salah:

```bash
iptables -t nat -D POSTROUTING -s 192.225.4.64/29 ! -d 192.225.0.0/16 -o eth0 -j SNAT --to-source 172.31.99.1
```

Interface `eth0` disesuaikan dengan interface menuju Gendo.

**7. Memperbaiki NAT pada Gendo**

Pada Console Gendo, hapus aturan RETURN yang dibuat oleh sabotase:

```bash
iptables -t nat -D POSTROUTING -s 192.225.4.64/29 -o eth0 -j RETURN
```

Interface `eth0` disesuaikan dengan interface WAN menuju NAT1.

**8. Memastikan aturan MASQUERADE pada Gendo**

```bash
iptables -t nat -C POSTROUTING -s 192.225.0.0/16 ! -d 192.225.0.0/16 -o eth0 -j MASQUERADE 2>/dev/null || iptables -t nat -A POSTROUTING -s 192.225.0.0/16 ! -d 192.225.0.0/16 -o eth0 -j MASQUERADE
```

**9. Mengaktifkan IP forwarding pada Gendo**

```bash
sysctl -w net.ipv4.ip_forward=1
```

**10. Menguji hasil perbaikan dari Unit-01**

```bash
ping -c 4 192.225.4.65
ping -c 4 192.225.4.74
ping -c 4 -W 2 8.8.8.8
```

Pengujian ini memastikan koneksi ke gateway, Lilith, dan internet kembali berjalan.

**Bukti pengerjaan manual:**

[Tempel screenshot menjalankan sabotase pada Misato dan Gendo]

[Tempel screenshot pemeriksaan aturan NAT pada Misato dan Gendo]

[Tempel screenshot perbaikan aturan NAT secara manual]

[Tempel screenshot pengujian Unit-01 sebelum dan setelah perbaikan]

#### Pengerjaan Menggunakan Script

Setelah pengerjaan manual, dibuat script terpisah untuk pemeriksaan dan perbaikan NAT agar proses dapat dijalankan kembali dengan lebih mudah.

**1. Membuat script pemeriksaan NAT**

Script `cek_nat_soal10.sh` dibuat pada Misato dan Gendo.

```bash
cat > /root/cek_nat_soal10.sh <<'EOF'
#!/bin/sh

echo "===================================="
echo " PEMERIKSAAN NAT SOAL 10"
echo "===================================="

echo ""
echo "=== NAMA NODE ==="
hostname

echo ""
echo "=== IP ADDRESS ==="
ip -br addr

echo ""
echo "=== ROUTING ==="
ip route

echo ""
echo "=== IP FORWARDING ==="
sysctl net.ipv4.ip_forward

echo ""
echo "=== NAT POSTROUTING ==="
iptables -t nat -L POSTROUTING -n -v --line-numbers

echo ""
echo "=== FILTER FORWARD ==="
iptables -L FORWARD -n -v --line-numbers

echo ""
echo "=== PEMERIKSAAN SELESAI ==="
EOF
```

Jalankan pada masing-masing router:

```bash
chmod +x /root/cek_nat_soal10.sh
/root/cek_nat_soal10.sh
```

**2. Membuat script perbaikan Misato**

Pada Console Misato:

```bash
cat > /root/perbaikan_misato.sh <<'EOF'
#!/bin/sh

echo "=== PERBAIKAN NAT MISATO ==="

if [ "$(id -u)" != 0 ]; then
    echo "Jalankan sebagai root."
    exit 1
fi

case "$(hostname)" in
    *[Mm]isato*) ;;
    *) echo "Script hanya untuk Misato."; exit 1 ;;
esac

CAGE="192.225.4.64/29"
INTERNAL="192.225.0.0/16"

UPIF=$(ip route show default | awk 'NR==1 {
    for (i=1; i<=NF; i++)
        if ($i=="dev") print $(i+1)
}')

if [ -z "$UPIF" ]; then
    echo "Interface menuju Gendo tidak ditemukan."
    exit 1
fi

while iptables -t nat -D POSTROUTING \
    -s "$CAGE" ! -d "$INTERNAL" \
    -o "$UPIF" -j SNAT --to-source 172.31.99.1 2>/dev/null
do
    :
done

echo "=== HASIL NAT MISATO ==="
iptables -t nat -L POSTROUTING -n -v --line-numbers

echo "Perbaikan Misato selesai."
EOF
```

Jalankan:

```bash
chmod +x /root/perbaikan_misato.sh
/root/perbaikan_misato.sh
```

**3. Membuat script perbaikan Gendo**

Pada Console Gendo:

```bash
cat > /root/perbaikan_gendo.sh <<'EOF'
#!/bin/sh

echo "=== PERBAIKAN NAT GENDO ==="

if [ "$(id -u)" != 0 ]; then
    echo "Jalankan sebagai root."
    exit 1
fi

case "$(hostname)" in
    *[Gg]endo*) ;;
    *) echo "Script hanya untuk Gendo."; exit 1 ;;
esac

CAGE="192.225.4.64/29"
INTERNAL="192.225.0.0/16"

WAN=$(ip route show default | awk 'NR==1 {
    for (i=1; i<=NF; i++)
        if ($i=="dev") print $(i+1)
}')

if [ -z "$WAN" ]; then
    echo "Interface WAN tidak ditemukan."
    exit 1
fi

while iptables -t nat -D POSTROUTING \
    -s "$CAGE" -o "$WAN" -j RETURN 2>/dev/null
do
    :
done

iptables -t nat -C POSTROUTING \
    -s "$INTERNAL" ! -d "$INTERNAL" \
    -o "$WAN" -j MASQUERADE 2>/dev/null || \
iptables -t nat -A POSTROUTING \
    -s "$INTERNAL" ! -d "$INTERNAL" \
    -o "$WAN" -j MASQUERADE

sysctl -w net.ipv4.ip_forward=1

echo "=== HASIL NAT GENDO ==="
iptables -t nat -L POSTROUTING -n -v --line-numbers

echo "=== IP FORWARDING ==="
sysctl net.ipv4.ip_forward

echo "Perbaikan Gendo selesai."
EOF
```

Jalankan:

```bash
chmod +x /root/perbaikan_gendo.sh
/root/perbaikan_gendo.sh
```

**4. Membuat script pengujian Unit-01**

Pada Console Unit-01:

```bash
cat > /root/test_soal10.sh <<'EOF'
#!/bin/sh

echo "===================================="
echo " PENGUJIAN SOAL 10 - UNIT-01"
echo "===================================="

echo ""
echo "=== IP ADDRESS ==="
ip -br addr

echo ""
echo "=== ROUTING ==="
ip route

echo ""
echo "=== PING GATEWAY CAGE ==="
ping -c 4 -W 2 192.225.4.65

echo ""
echo "=== PING LILITH ==="
ping -c 4 -W 2 192.225.4.74

echo ""
echo "=== PING INTERNET ==="
ping -c 4 -W 2 8.8.8.8

echo ""
echo "=== PENGUJIAN SELESAI ==="
EOF
```

Jalankan:

```bash
chmod +x /root/test_soal10.sh
/root/test_soal10.sh
```

**5. Memeriksa hasil akhir**

Pada Misato dan Gendo:

```bash
/root/cek_nat_soal10.sh
```

Pada Gendo, pastikan aturan MASQUERADE untuk jaringan internal terlihat pada POSTROUTING. Alamat sumber paket diterjemahkan pada Gendo ketika paket keluar melalui interface WAN menuju NAT1.

**Bukti pengerjaan menggunakan script:**

[Tempel screenshot script cek_nat_soal10.sh pada Misato]

[Tempel screenshot script cek_nat_soal10.sh pada Gendo]

[Tempel screenshot script perbaikan_misato.sh]

[Tempel screenshot script perbaikan_gendo.sh]

[Tempel screenshot script test_soal10.sh dan hasil ping Unit-01]

#### Kesimpulan

Sabotase pada Soal 10 menyebabkan jaringan Cage tidak dapat mengakses internet akibat aturan SNAT yang salah pada Misato dan aturan RETURN pada Gendo. Jaringan Intel tidak terdampak karena aturan sabotase secara khusus menggunakan sumber jaringan Cage. Perbaikan dilakukan secara manual dan menggunakan script terpisah pada Misato dan Gendo. NAT untuk jaringan internal dilakukan pada Gendo menggunakan MASQUERADE ketika paket keluar menuju NAT1. Keberhasilan perbaikan dibuktikan dengan ping Unit-01 ke `8.8.8.8`, serta pemeriksaan aturan NAT pada kedua router.

# Soal 11 — Casper Harus Jadi Hantu

## A. Permasalahan & Analisis

Casper merupakan salah satu MAGI paling rahasia di Geofront. Untuk mencegah deteksi keberadaannya oleh pihak luar (SEELE) maupun node internal lainnya, diperlukan konfigurasi firewall dengan ketentuan sebagai berikut:

1. Tidak ada node atau perangkat lain yang boleh melakukan **ping (ICMP Echo Request)** ke Casper, termasuk perangkat yang berada dalam satu switch (Switch-Terminal).
2. Casper tetap diperbolehkan melakukan ping keluar ke node mana pun.
3. Layanan TCP port `5000` pada Casper harus tetap aktif dan dapat menerima permintaan koneksi.

Untuk memenuhi kebutuhan tersebut, digunakan mekanisme firewall `iptables` dengan aturan:

- Mengizinkan koneksi loopback lokal.
- Mengizinkan paket balasan dari koneksi yang telah terbentuk menggunakan `conntrack` dengan state `ESTABLISHED,RELATED`.
- Mengizinkan koneksi TCP menuju port `5000`.
- Memblokir seluruh paket ICMP bertipe `echo-request` yang masuk ke Casper.

Dengan konfigurasi ini, Casper tidak dapat di-ping oleh node lain, tetapi tetap dapat melakukan ping keluar dan menerima Echo Reply sebagai balasannya.

## B. Langkah Konfigurasi

### 1. Konfigurasi Firewall pada Magi-Casper

Konfigurasi firewall diterapkan pada node berikut:

| Keterangan | Nilai |
|---|---|
| Nama Node | Magi-Casper |
| IP Address | `192.225.4.58` |
| Firewall | `iptables` |
| Port yang Diizinkan | TCP `5000` |

Jalankan perintah berikut pada terminal Magi-Casper:

```bash
# Membersihkan chain INPUT
iptables -F INPUT

# Mengizinkan traffic loopback lokal
iptables -A INPUT -i lo -j ACCEPT

# Mengizinkan paket balasan (ESTABLISHED dan RELATED)
iptables -A INPUT -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT

# Mengizinkan akses masuk TCP port 5000
iptables -A INPUT -p tcp --dport 5000 -j ACCEPT

# Memblokir ICMP Echo Request yang masuk
iptables -A INPUT -p icmp --icmp-type echo-request -j DROP
```

### 2. Pengecekan Rule Firewall

Untuk memastikan seluruh aturan firewall telah diterapkan, jalankan:

```bash
iptables -S
```

**Bukti Konfigurasi:**

<img width="577" height="183" alt="Screenshot 2026-11-26 015331" src="https://github.com/user-attachments/assets/a33dfbbf-8d72-4478-a06b-f4608ed058c6" />


> Ganti gambar di atas dengan screenshot aktual output `iptables -S` dari Magi-Casper.

## C. Pengujian & Bukti Hasil

### 1. Pengujian Ping dari Node Lain ke Magi-Casper

Pengujian dilakukan untuk memastikan bahwa Casper tidak dapat menerima ping dari node lain, baik yang berada dalam satu switch maupun dari luar subnet.

#### a. Pengujian dari Magi-Balthasar (Satu Switch)

Jalankan perintah berikut pada node Magi-Balthasar:

```bash
ping -c 2 -W 2 192.225.4.58
```

**Hasil yang Diharapkan:**

- Ping gagal.
- Packet loss sebesar 100%.
- Tidak ada Echo Reply yang diterima dari Magi-Casper.

**Bukti Pengujian:**

<img width="575" height="224" alt="Screenshot 2026-11-26 015401" src="https://github.com/user-attachments/assets/31c9a24a-9922-4b27-a6ec-5b6b9ee7e954" />


#### b. Pengujian dari Lilith (Luar Subnet / Switch-Dogma)

Jalankan perintah berikut pada node Lilith:

```bash
ping -c 2 -W 2 192.225.4.58
```

**Hasil yang Diharapkan:**

- Ping gagal.
- Packet loss sebesar 100%.
- Tidak ada Echo Reply yang diterima dari Magi-Casper.

**Bukti Pengujian:**
<img width="647" height="171" alt="Screenshot 2026-11-26 015432" src="https://github.com/user-attachments/assets/54ed1e39-d537-46f7-8823-4a90f52ee05e" />


### 2. Pengujian Ping dari Magi-Casper ke Node Lain

Pengujian selanjutnya dilakukan untuk memastikan bahwa Casper tetap dapat melakukan koneksi keluar ke node lain.

Jalankan perintah berikut pada terminal Magi-Casper:

**Ping ke Magi-Balthasar:**

```bash
ping -c 2 192.225.4.59
```

**Ping ke Lilith:**

```bash
ping -c 2 192.225.4.74
```

**Hasil yang Diharapkan:**

- Kedua pengujian ping berhasil.
- Packet loss sebesar 0%.
- Magi-Casper berhasil menerima ICMP Echo Reply dari kedua node.

**Bukti Pengujian:**

<img width="574" height="317" alt="Screenshot 2026-11-26 015451" src="https://github.com/user-attachments/assets/30ffc760-356c-4bb6-9546-ad58cc373b1f" />


## D. Skrip Otomasi (Restart-Safe)

Untuk mempermudah penerapan konfigurasi firewall, dibuat sebuah skrip otomatis bernama `casper_fw.sh`.

Skrip ini disimpan pada direktori `/root/` di node Magi-Casper.

### 1. Membuat File Script

Jalankan perintah berikut:

```bash
at > /root/casper_fw.sh << 'EOF'
#!/bin/sh
# Firewall Soal 11 - Casper Hantu
iptables -F INPUT
iptables -A INPUT -i lo -j ACCEPT
iptables -A INPUT -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT
iptables -A INPUT -p tcp --dport 5000 -j ACCEPT
iptables -A INPUT -p icmp --icmp-type echo-request -j DROP
echo "== Firewall Soal 11 Terpasang =="
iptables -S
EOF
chmod +x /root/casper_fw.sh
```

### 2. Memberikan Hak Akses Eksekusi

```bash
chmod +x /root/casper_fw.sh
```

### 3. Menjalankan Script

```bash
/root/casper_fw.sh
```

Apabila berhasil, terminal akan menampilkan pesan:

```text
== Firewall Soal 11 Terpasang ==
```

Kemudian aturan firewall aktif akan ditampilkan melalui output `iptables -S`.

> **Catatan:** Skrip ini dapat dijalankan kembali untuk menerapkan ulang aturan firewall. Namun, agar konfigurasi benar-benar bertahan setelah reboot, skrip perlu dipanggil melalui mekanisme startup sistem seperti systemd atau layanan startup lainnya.

## E. Kesimpulan

Berdasarkan konfigurasi dan pengujian yang dilakukan, firewall pada Magi-Casper dirancang untuk memenuhi seluruh kebutuhan keamanan berikut:

| No. | Skenario Pengujian | Hasil yang Diharapkan |
|---|---|---|
| 1 | Ping dari Magi-Balthasar ke Casper | Gagal |
| 2 | Ping dari Lilith ke Casper | Gagal |
| 3 | Ping dari Casper ke Magi-Balthasar | Berhasil |
| 4 | Ping dari Casper ke Lilith | Berhasil |
| 5 | Akses TCP port 5000 | Diizinkan |

Dengan menerapkan aturan `iptables` dan mekanisme `conntrack`, Magi-Casper menjadi tidak dapat dideteksi melalui ICMP Echo Request dari node lain, tetapi tetap dapat melakukan komunikasi keluar secara normal.

Layanan MAGI pada TCP port `5000` juga tetap diizinkan untuk menerima koneksi masuk.

**Casper berhasil menjadi hantu di dalam jaringan Geofront!**

# Soal 12: Teknisi yang Kelewat Semangat

## 1. Kondisi Awal dan Gejala Kerusakan

Setelah script hardening dari teknisi (`break_fw.sh`) dijalankan pada node Magi-Casper, muncul beberapa kegagalan sistem.

### 1.1 Gejala 1 — Casper Gagal Ping ke Internet

**Lokasi:** Magi-Casper

Perintah:

```bash
ping -c 3 8.8.8.8
```

**Hasil:** Gagal dengan 100% packet loss.

Paket ICMP echo-request berhasil dikirim, tetapi balasan ICMP echo-reply dari internet ditolak oleh chain INPUT.

<img width="761" height="727" alt="Screenshot 2026-11-26 170204" src="https://github.com/user-attachments/assets/5891f0f7-05f7-4b87-99ff-8eedf3c0d0e2" />


> Tempatkan screenshot hasil ping 8.8.8.8 dari Magi-Casper yang menunjukkan koneksi gagal.

### 1.2 Gejala 2 — Casper Gagal Menjalankan apt-get update

**Lokasi:** Magi-Casper

Perintah:

```bash
apt-get update
```

**Hasil:** Muncul pesan kesalahan:

```text
Temporary failure resolving 'deb.debian.org'
```

Repositori Debian gagal diunduh karena terjadi kegagalan resolusi nama domain.

<img width="761" height="727" alt="Screenshot 2026-11-26 170204" src="https://github.com/user-attachments/assets/e0b0592b-8048-4a8d-9ace-4e8f104aa45a" />


> Tempatkan screenshot output apt-get update di Magi-Casper yang menunjukkan error DNS.

### 1.3 Gejala 3 — Unit-00 Gagal Terhubung ke TCP Port 5000

**Lokasi:** Unit-00

Perintah:

```bash
nc -w 3 192.225.4.58 5000 < /dev/null && echo "KONEKSI BERHASIL" || echo "KONEKSI GAGAL"
```

**Hasil:** KONEKSI GAGAL atau connection timed out.

Penyebabnya adalah port TCP 5000 belum diizinkan pada chain INPUT Magi-Casper.

<img width="740" height="517" alt="Screenshot 2026-11-26 170149" src="https://github.com/user-attachments/assets/92b0f4ba-afda-4a2f-8090-c03cc4ef4729" />


> Tempatkan screenshot hasil pengujian nc dari Unit-00 ke Magi-Casper pada port 5000.

---

## 2. Analisis Penyebab Masalah

Berdasarkan pemeriksaan aturan firewall menggunakan perintah `iptables -S`, ditemukan tiga penyebab utama.

| No. | Penyebab | Dampak |
|---|---|---|
| 1 | Policy default chain INPUT diset ke DROP tanpa rule ESTABLISHED,RELATED. | Paket balasan dari koneksi yang diinisiasi Casper ikut dibuang. |
| 2 | Terdapat rule sabotase pada chain OUTPUT yang memblokir DNS. | Casper gagal melakukan resolusi nama domain server Debian. |
| 3 | Tidak ada rule yang mengizinkan TCP port 5000 pada chain INPUT. | Unit-00 tidak dapat terhubung ke layanan TCP port 5000. |

### 2.1 Rule Sabotase DNS

Rule yang ditemukan pada chain OUTPUT:

```bash
-A OUTPUT -p udp -m udp --dport 53 -j DROP
```

Rule tersebut membuang seluruh paket DNS keluar melalui UDP port 53 sehingga proses resolusi nama domain tidak dapat berjalan normal.

### 2.2 Tujuan Perbaikan

Perbaikan dilakukan dengan tetap mempertahankan tujuan hardening, yaitu:

- Default policy chain INPUT tetap DROP.
- Ping masuk dari Unit-00 ke Magi-Casper tetap ditolak.
- Koneksi keluar dari Magi-Casper dapat berjalan normal.
- Resolusi DNS dan pembaruan paket dapat dilakukan kembali.
- Layanan TCP port 5000 dapat diakses dari Unit-00.

---

## 3. Langkah Perbaikan pada Magi-Casper

Seluruh perintah berikut dijalankan pada terminal Magi-Casper dengan hak akses root.

### 3.1 Mengatur Default Policy

Pastikan default policy INPUT tetap DROP sesuai requirement.

```bash
iptables -P INPUT DROP
iptables -P FORWARD ACCEPT
iptables -P OUTPUT ACCEPT
```

### 3.2 Membersihkan Rule Lama

Bersihkan rule pada chain INPUT dan OUTPUT.

```bash
iptables -F INPUT
iptables -F OUTPUT
```

### 3.3 Mengizinkan Interface Loopback

```bash
iptables -A INPUT -i lo -j ACCEPT
```

### 3.4 Mengizinkan Paket Balasan

Izinkan paket yang merupakan bagian dari koneksi yang sudah terbentuk atau berkaitan dengan koneksi tersebut.

```bash
iptables -A INPUT -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT
```

### 3.5 Membuka Akses TCP Port 5000

```bash
iptables -A INPUT -p tcp --dport 5000 -j ACCEPT
```

### 3.6 Memastikan Nameserver DNS Terpasang

```bash
echo "nameserver 8.8.8.8" > /etc/resolv.conf
```

### 3.7 Verifikasi Rule Hasil Perbaikan

Jalankan perintah berikut untuk memeriksa konfigurasi firewall.

```bash
iptables -S
```

<img width="601" height="183" alt="image" src="https://github.com/user-attachments/assets/fba5e978-3d2d-48db-b0fe-4de8bbdeb5b1" />


---

## 4. Pengujian dan Validasi Hasil

Setelah perbaikan dilakukan, jalankan pengujian berikut untuk memastikan seluruh fungsi jaringan telah kembali normal.

### 4.1 Pengujian Ping ke Internet

**Lokasi:** Magi-Casper

Perintah:

```bash
ping -c 3 8.8.8.8
```

**Hasil yang diharapkan:** Ping berhasil dengan 0% packet loss.

<img width="570" height="217" alt="Screenshot 2026-11-26 171310" src="https://github.com/user-attachments/assets/f2b01a77-386e-4bd4-a01e-aae4df76982d" />

### 4.2 Pengujian apt-get update

**Lokasi:** Magi-Casper

Perintah:

```bash
apt-get update
```

**Hasil yang diharapkan:** Metadata paket dari repositori Debian berhasil diunduh tanpa error resolusi DNS.

<img width="726" height="383" alt="Screenshot 2026-11-26 171238" src="https://github.com/user-attachments/assets/74c22ba5-d9c4-437e-a482-8589f68aa1c8" />


### 4.3 Pengujian Koneksi TCP Port 5000

**Lokasi:** Unit-00

Perintah:

```bash
nc -w 3 192.225.4.58 5000 < /dev/null && echo "KONEKSI BERHASIL" || echo "KONEKSI GAGAL"
```

**Hasil yang diharapkan:**

```text
KONEKSI BERHASIL
```

<img width="730" height="115" alt="Screenshot 2026-11-26 171405" src="https://github.com/user-attachments/assets/3e7fc77d-e609-412b-be03-711d1b54c0b4" />


### 4.4 Pengujian Ping dari Unit-00 ke Magi-Casper

**Lokasi:** Unit-00

Perintah:

```bash
ping -c 2 -W 2 192.225.4.58
```

**Hasil yang diharapkan:** Ping tetap gagal dengan 100% packet loss atau Request Timed Out (RTO).

Kegagalan ini menunjukkan bahwa akses ICMP echo-request dari Unit-00 tetap ditolak sesuai aturan hardening.

<img width="592" height="205" alt="Screenshot 2026-11-26 171430" src="https://github.com/user-attachments/assets/7e9f261c-ec9c-492e-a61d-2c6767e97a0b" />

---

## 5. Skrip Otomasi Perbaikan

Untuk mempermudah pemulihan konfigurasi, dibuat skrip otomasi yang disimpan pada node Magi-Casper.

**Lokasi skrip:**

```text
/root/perbaikan_casper.sh
```

### 5.1 Isi Skrip

```bash
#!/bin/sh

# Perbaikan Soal 12 di Magi-Casper

# 1. Mengatur policy default
iptables -P INPUT DROP
iptables -P FORWARD ACCEPT
iptables -P OUTPUT ACCEPT

# 2. Membersihkan rule lama
iptables -F INPUT
iptables -F OUTPUT

# 3. Mengizinkan interface loopback
iptables -A INPUT -i lo -j ACCEPT

# 4. Mengizinkan paket balasan
iptables -A INPUT -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT

# 5. Membuka akses TCP port 5000
iptables -A INPUT -p tcp --dport 5000 -j ACCEPT

# 6. Mengatur nameserver DNS
echo "nameserver 8.8.8.8" > /etc/resolv.conf

# 7. Menampilkan hasil konfigurasi
echo "== Perbaikan Soal 12 Selesai =="

iptables -S
```

### 5.2 Memberikan Izin Eksekusi

```bash
chmod +x /root/perbaikan_casper.sh
```

### 5.3 Menjalankan Skrip

```bash
/root/perbaikan_casper.sh
```

### 5.4 Verifikasi Hasil Skrip

Setelah skrip dijalankan, periksa kembali konfigurasi firewall.

```bash
iptables -S
```

Pastikan policy INPUT tetap DROP dan seluruh rule perbaikan telah diterapkan.

<img width="582" height="185" alt="image" src="https://github.com/user-attachments/assets/e8c1c429-02e2-4235-9561-8a2e2f755abe" />

---

## 6. Kesimpulan

Perbaikan konfigurasi firewall pada Magi-Casper dilakukan untuk memulihkan fungsi jaringan yang terganggu akibat script hardening `break_fw.sh`.

Hasil akhir yang diharapkan:

1. Magi-Casper berhasil melakukan ping ke internet.
2. Perintah apt-get update berhasil dijalankan tanpa masalah resolusi DNS.
3. Unit-00 berhasil terhubung ke layanan TCP port 5000.
4. Ping dari Unit-00 ke Magi-Casper tetap ditolak.
5. Default policy chain INPUT tetap DROP sehingga tujuan hardening tetap dipertahankan.

Dengan demikian, konfigurasi firewall telah diperbaiki tanpa menghilangkan tujuan utama hardening sistem.

---
# Soal 13 — Brankas Balthasar

## 1. Analisis dan Identifikasi Masalah

### 1.1 Kondisi Awal

Magi-Balthasar menyimpan seluruh data rahasia Geofront melalui layanan TCP port 5000 dan 5001.

Namun, terlalu banyak pihak yang dapat mengakses port sensitif tersebut, termasuk node lain yang berada dalam satu switch.

Kondisi ini menimbulkan risiko keamanan karena akses terhadap layanan sensitif belum dibatasi berdasarkan alamat IP sumber.

### 1.2 Kebutuhan Keamanan

Konfigurasi firewall harus memenuhi ketentuan berikut:

1. Hanya Magi-Casper (`192.225.4.58`) dan seluruh anggota kategori Pilot yang diizinkan mengakses TCP port 5000 dan 5001.
2. Anggota kategori Pilot terdiri dari:
   - Unit-01
   - Unit-02
   - Unit-00
   - Sachiel (`192.225.3.130`)
3. Seluruh node selain yang diizinkan, seperti Lilith dan Magi-Melchior, harus ditolak seketika menggunakan TCP Reset.
4. Lalu lintas selain TCP port 5000 dan 5001 tidak boleh terganggu.
5. Magi-Balthasar harus tetap dapat melakukan ping ke internet (`8.8.8.8`) dan menerima balasan secara normal.

### 1.3 Informasi Jaringan

| Node | Alamat IP / Subnet | Keterangan |
|---|---|---|
| Magi-Casper | `192.225.4.58` | Diizinkan |
| Unit-00 | `192.225.4.64/29` | Anggota Pilot |
| Unit-01 | Termasuk subnet Pilot | Anggota Pilot |
| Unit-02 | Termasuk subnet Pilot | Anggota Pilot |
| Sachiel | `192.225.3.130` | Anggota Pilot |
| Magi-Balthasar | `192.225.4.59` | Server tujuan |
| Lilith | Sesuai konfigurasi jaringan | Tidak diizinkan |
| Magi-Melchior | Sesuai konfigurasi jaringan | Tidak diizinkan |

---

## 2. Langkah Konfigurasi Firewall

Konfigurasi firewall diterapkan pada node Magi-Balthasar dengan hak akses root.

### 2.1 Membersihkan Chain INPUT

Hapus seluruh rule lama pada chain INPUT.

```bash
iptables -F INPUT
```

### 2.2 Mengizinkan Interface Loopback

Izinkan komunikasi internal melalui interface loopback.

```bash
iptables -A INPUT -i lo -j ACCEPT
```

### 2.3 Mengizinkan Paket Balasan

Izinkan paket yang merupakan bagian dari koneksi yang sudah terbentuk atau berkaitan dengan koneksi tersebut.

```bash
iptables -A INPUT -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT
```

Rule ini diperlukan agar koneksi yang diinisiasi oleh Magi-Balthasar, seperti ping ke internet, tetap dapat menerima balasan.

### 2.4 Membuat Whitelist Magi-Casper

Izinkan Magi-Casper mengakses TCP port 5000 dan 5001.

```bash
iptables -A INPUT -p tcp -s 192.225.4.58 -m multiport --dports 5000,5001 -j ACCEPT
```

### 2.5 Membuat Whitelist Subnet Pilot

Izinkan seluruh anggota subnet Pilot `192.225.4.64/29` mengakses TCP port 5000 dan 5001.

```bash
iptables -A INPUT -p tcp -s 192.225.4.64/29 -m multiport --dports 5000,5001 -j ACCEPT
```

### 2.6 Membuat Whitelist Sachiel

Izinkan Sachiel dengan alamat IP `192.225.3.130` mengakses TCP port 5000 dan 5001.

```bash
iptables -A INPUT -p tcp -s 192.225.3.130 -m multiport --dports 5000,5001 -j ACCEPT
```

### 2.7 Menolak Akses Selain Whitelist

Tolak seluruh koneksi TCP menuju port 5000 dan 5001 yang tidak cocok dengan rule whitelist sebelumnya.

```bash
iptables -A INPUT -p tcp -m multiport --dports 5000,5001 -j REJECT --reject-with tcp-reset
```

Target `REJECT --reject-with tcp-reset` menyebabkan koneksi ditolak secara langsung menggunakan paket TCP Reset, bukan dibiarkan menunggu timeout.

### 2.8 Mempertahankan Lalu Lintas Lain

Atur default policy chain INPUT menjadi ACCEPT agar lalu lintas lain di luar port sensitif tidak terganggu.

```bash
iptables -P INPUT ACCEPT
```

### 2.9 Verifikasi Rule Firewall

Periksa seluruh rule firewall yang aktif.

```bash
iptables -S
```

<img width="735" height="242" alt="Screenshot 2026-11-26 174820" src="https://github.com/user-attachments/assets/297d7c6d-fc55-467b-a027-67946f340da6" />

---

## 3. Pengujian dan Validasi Hasil

Pengujian dilakukan untuk memastikan hanya node yang diizinkan dapat mengakses TCP port 5000 dan 5001, sedangkan node lain ditolak seketika.

### 3.1 Pengujian dari Unit-01 (Kategori Pilot)

**Lokasi:** Unit-01

Pengujian port 5000:

```bash
nc -zv -w 2 192.225.4.59 5000
```

Pengujian port 5001:

```bash
nc -zv -w 2 192.225.4.59 5001
```

**Hasil yang diharapkan:**

Kedua port berhasil tersambung dengan status open atau success.

<img width="542" height="147" alt="Screenshot 2026-11-26 174834" src="https://github.com/user-attachments/assets/ec999365-be73-41ae-858a-3e28bdf8fff6" />


### 3.2 Pengujian dari Lilith (Ditolak Seketika)

**Lokasi:** Lilith

Pengujian port 5000:

```bash
nc -zv -w 2 192.225.4.59 5000
```

Pengujian port 5001:

```bash
nc -zv -w 2 192.225.4.59 5001
```

**Hasil yang diharapkan:**

Koneksi langsung ditolak dengan pesan `Connection refused` tanpa mengalami timeout.

<img width="657" height="112" alt="Screenshot 2026-11-26 174843" src="https://github.com/user-attachments/assets/805103aa-b937-4603-bea8-f69ae954e986" />


### 3.3 Pengujian dari Magi-Melchior (Satu Switch)

**Lokasi:** Magi-Melchior

Pengujian port 5000:

```bash
nc -zv -w 2 192.225.4.59 5000
```

Pengujian port 5001:

```bash
nc -zv -w 2 192.225.4.59 5001
```

**Hasil yang diharapkan:**

Kedua koneksi langsung ditolak dengan pesan `Connection refused`.

<img width="632" height="112" alt="Screenshot 2026-11-26 174857" src="https://github.com/user-attachments/assets/520e5dbe-6eea-460f-84ab-2ba4ca0cdbf3" />

### 3.4 Pengujian Ping Internet dari Magi-Balthasar

**Lokasi:** Magi-Balthasar

Perintah:

```bash
ping -c 3 8.8.8.8
```

**Hasil yang diharapkan:**

Ping berhasil dengan 0% packet loss.

<img width="568" height="207" alt="Screenshot 2026-11-26 174917" src="https://github.com/user-attachments/assets/e28f0e67-db88-4342-8d26-c2acffd77ae5" />

---

## 4. Skrip Otomasi Firewall

Untuk mempermudah penerapan konfigurasi firewall, dibuat skrip otomasi yang disimpan pada node Magi-Balthasar.

**Lokasi skrip:**

```text
/root/balthasar_rules.sh
```

### 4.1 Isi Skrip

```bash
#!/bin/sh

# Rules Soal 13 - Brankas Balthasar

# 1. Membersihkan chain INPUT
iptables -F INPUT

# 2. Mengizinkan interface loopback
iptables -A INPUT -i lo -j ACCEPT

# 3. Mengizinkan paket balasan
iptables -A INPUT -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT

# 4. Whitelist Magi-Casper
iptables -A INPUT -p tcp -s 192.225.4.58 -m multiport --dports 5000,5001 -j ACCEPT

# 5. Whitelist subnet Pilot
iptables -A INPUT -p tcp -s 192.225.4.64/29 -m multiport --dports 5000,5001 -j ACCEPT

# 6. Whitelist Sachiel
iptables -A INPUT -p tcp -s 192.225.3.130 -m multiport --dports 5000,5001 -j ACCEPT

# 7. Menolak akses selain whitelist dengan TCP Reset
iptables -A INPUT -p tcp -m multiport --dports 5000,5001 -j REJECT --reject-with tcp-reset

# 8. Mempertahankan lalu lintas lainnya
iptables -P INPUT ACCEPT

# 9. Menampilkan hasil konfigurasi
echo "== Rules Soal 13 Aktif =="

iptables -S
```

### 4.2 Memberikan Izin Eksekusi

```bash
chmod +x /root/balthasar_rules.sh
```

### 4.3 Menjalankan Skrip

```bash
/root/balthasar_rules.sh
```

### 4.4 Verifikasi Hasil Skrip

Periksa kembali konfigurasi firewall setelah skrip dijalankan.

```bash
iptables -S
```

Pastikan rule whitelist, rule REJECT TCP Reset, dan policy INPUT ACCEPT telah diterapkan.

**Screenshot 6 — Eksekusi skrip otomasi**

<img width="735" height="242" alt="Screenshot 2026-11-26 174820" src="https://github.com/user-attachments/assets/7e860709-d8c7-4a74-9067-c91b9f5a2f51" />

---

## 5. Kesimpulan

Konfigurasi firewall pada Magi-Balthasar berhasil diterapkan untuk membatasi akses terhadap layanan TCP port 5000 dan 5001.

Hasil akhir yang diharapkan:

1. Magi-Casper dan seluruh anggota kategori Pilot dapat mengakses TCP port 5000 dan 5001.
2. Lilith dan Magi-Melchior ditolak secara langsung menggunakan TCP Reset.
3. Lalu lintas lain di luar port sensitif tetap dapat berjalan normal.
4. Magi-Balthasar tetap dapat melakukan ping ke internet dan menerima balasan.
5. Konfigurasi firewall dapat diterapkan kembali menggunakan skrip otomasi.

Dengan demikian, akses terhadap layanan sensitif telah dibatasi sesuai kebutuhan keamanan tanpa mengganggu lalu lintas jaringan lainnya.

---
# Soal 14 — Jam Kunjungan Sang Pinguin

## 1. Analisis dan Identifikasi Masalah

### 1.1 Kondisi Awal

Node Pen-Pen (`192.225.3.195`) menerapkan pembatasan akses terhadap ICMP echo-request (ping) dan TCP port 80 berdasarkan kategori node dan jadwal waktu tertentu.

Pembatasan ini diterapkan menggunakan firewall `iptables` dengan modul `time`.

### 1.2 Kebutuhan Keamanan

Konfigurasi firewall harus memenuhi ketentuan berikut:

| Kategori | Anggota | Jadwal Akses | Ketentuan |
|---|---|---|---|
| Pilot | Unit-01, Unit-02, Unit-00, Sachiel | Senin–Jumat, 08.00–16.00 WIB | Diizinkan |
| Staf Geofront | Lilith dan Adam | Setiap hari, 17.00–23.00 WIB | Diizinkan |
| Terduga Dummy System | Dummy-Plug, Entry-Plug, Spy | Setiap waktu | Selalu ditolak |
| Lainnya | Node di luar kategori tersebut | Setiap waktu | Bebas tanpa batasan |

Pembatasan berlaku untuk ICMP echo-request dan TCP port 80.

### 1.3 Konversi Jadwal WIB ke UTC

Modul `time` pada iptables membaca waktu sistem dalam format UTC. Oleh karena itu, jadwal WIB harus dikonversi dengan mengurangi 7 jam.

| Kategori | Jadwal WIB | Jadwal UTC | Hari |
|---|---|---|---|
| Pilot | 08.00–16.00 | 01:00–09:00 | Senin–Jumat |
| Staf Geofront | 17.00–23.00 | 10:00–16:00 | Setiap hari |

### 1.4 Metode Pengujian

Jam komputer tidak boleh diubah. Pengujian dilakukan dengan menyesuaikan variabel jadwal pada skrip firewall.

Terdapat tiga tahap pengujian:

1. **Kondisi 1 — Jadwal Cocok:** Jadwal disesuaikan dengan waktu sistem saat pengujian agar akses diizinkan.
2. **Kondisi 2 — Jadwal Tidak Cocok:** Jadwal diubah ke rentang waktu di luar waktu pengujian untuk membuktikan bahwa akses ditolak.
3. **Pemulihan:** Jadwal dikembalikan ke ketentuan resmi soal.

---

## 2. Konfigurasi Awal (Kondisi 1 — Jadwal Cocok)

### 2.1 Kondisi Waktu Sistem

Pada saat pengujian, jam sistem container menunjukkan pukul 10:xx UTC pada hari Kamis.

Agar pengujian dapat dilakukan tanpa mengubah jam komputer, variabel jadwal Pilot dan Staf Geofront disesuaikan dengan waktu sistem saat itu.

### 2.2 Lokasi Skrip

Skrip firewall disimpan pada node Pen-Pen dengan lokasi:

```text
/root/penpen_rules.sh
```

### 2.3 Isi Skrip Firewall

```bash
#!/bin/sh

# Variabel jadwal pengujian disesuaikan dengan jam sistem (UTC)

PILOT_START="10:00"
PILOT_STOP="12:00"
PILOT_DAYS="Mon,Tue,Wed,Thu,Fri"

STAF_START="10:00"
STAF_STOP="12:00"

# 1. Membersihkan rule lama
iptables -F INPUT

# 2. Mengizinkan loopback dan koneksi yang sudah terbentuk
iptables -A INPUT -i lo -j ACCEPT
iptables -A INPUT -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT

# 3. Terduga Dummy System: Selalu ditolak

DUMMY_IPS="192.225.4.50 192.225.4.51 192.225.4.102"

for ip in $DUMMY_IPS; do
    iptables -A INPUT -s "$ip" -p icmp --icmp-type echo-request -j DROP
    iptables -A INPUT -s "$ip" -p tcp --dport 80 -j DROP
done

# 4. Kategori Pilot: Akses sesuai jadwal

# Pilot - Subnet Switch-Cage
iptables -A INPUT -s 192.225.4.64/29 \
    -m time --timestart "$PILOT_START" --timestop "$PILOT_STOP" \
    --weekdays "$PILOT_DAYS" \
    -p icmp --icmp-type echo-request -j ACCEPT

iptables -A INPUT -s 192.225.4.64/29 \
    -m time --timestart "$PILOT_START" --timestop "$PILOT_STOP" \
    --weekdays "$PILOT_DAYS" \
    -p tcp --dport 80 -j ACCEPT

# Pilot - Sachiel
iptables -A INPUT -s 192.225.3.130 \
    -m time --timestart "$PILOT_START" --timestop "$PILOT_STOP" \
    --weekdays "$PILOT_DAYS" \
    -p icmp --icmp-type echo-request -j ACCEPT

iptables -A INPUT -s 192.225.3.130 \
    -m time --timestart "$PILOT_START" --timestop "$PILOT_STOP" \
    --weekdays "$PILOT_DAYS" \
    -p tcp --dport 80 -j ACCEPT

# Pilot - Tolak akses di luar jadwal
iptables -A INPUT -s 192.225.4.64/29 \
    -p icmp --icmp-type echo-request -j DROP

iptables -A INPUT -s 192.225.4.64/29 \
    -p tcp --dport 80 -j DROP

iptables -A INPUT -s 192.225.3.130 \
    -p icmp --icmp-type echo-request -j DROP

iptables -A INPUT -s 192.225.3.130 \
    -p tcp --dport 80 -j DROP

# 5. Kategori Staf Geofront: Akses sesuai jadwal

iptables -A INPUT -s 192.225.4.72/29 \
    -m time --timestart "$STAF_START" --timestop "$STAF_STOP" \
    -p icmp --icmp-type echo-request -j ACCEPT

iptables -A INPUT -s 192.225.4.72/29 \
    -m time --timestart "$STAF_START" --timestop "$STAF_STOP" \
    -p tcp --dport 80 -j ACCEPT

# Staf - Tolak akses di luar jadwal
iptables -A INPUT -s 192.225.4.72/29 \
    -p icmp --icmp-type echo-request -j DROP

iptables -A INPUT -s 192.225.4.72/29 \
    -p tcp --dport 80 -j DROP

# 6. Mempertahankan lalu lintas lainnya
iptables -P INPUT ACCEPT
```

### 2.4 Menjalankan Skrip

Berikan izin eksekusi:

```bash
chmod +x /root/penpen_rules.sh
```

Jalankan skrip:

```bash
/root/penpen_rules.sh
```

Periksa rule yang aktif:

```bash
iptables -S
```
---

## 3. Pengujian Kondisi 1 — Jadwal Cocok dengan Jam Sistem

Pada kondisi ini, jadwal Pilot dan Staf Geofront mencakup pukul 10:xx UTC pada hari Kamis.

### 3.1 Pengujian dari Unit-01 (Pilot)

**Lokasi:** Unit-01

Perintah:

```bash
ping -c 2 -W 2 192.225.3.195
```

**Hasil yang diharapkan:** Ping berhasil dengan 0% packet loss.

<img width="585" height="185" alt="Screenshot 2026-11-26 175848" src="https://github.com/user-attachments/assets/49f2987a-54d8-4416-af12-aaa08b6e5922" />


### 3.2 Pengujian dari Lilith (Staf Geofront)

**Lokasi:** Lilith

Perintah:

```bash
ping -c 2 -W 2 192.225.3.195
```

**Hasil yang diharapkan:** Ping berhasil dengan 0% packet loss.

<img width="568" height="180" alt="Screenshot 2026-11-26 175857" src="https://github.com/user-attachments/assets/4b90e537-10d3-4f56-9c27-025eeb68a494" />


### 3.3 Pengujian dari Spy (Terduga Dummy System)

**Lokasi:** Spy

Perintah:

```bash
ping -c 2 -W 2 192.225.3.195
```

<img width="607" height="177" alt="Screenshot 2026-11-26 175930" src="https://github.com/user-attachments/assets/dc437f0b-e0e0-4369-9e4f-969325307921" />

---

## 4. Pengujian Kondisi 2 — Jadwal Tidak Cocok

### 4.1 Mengubah Variabel Jadwal

Jadwal pada skrip `/root/penpen_rules.sh` diubah menjadi pukul 01:00–02:00 UTC.

Rentang waktu tersebut berada di luar waktu pengujian sistem saat ini, yaitu pukul 10:xx UTC.

Jalankan perintah berikut pada Pen-Pen:

```bash
sed -i 's/PILOT_START="10:00"/PILOT_START="01:00"/' /root/penpen_rules.sh

sed -i 's/PILOT_STOP="12:00"/PILOT_STOP="02:00"/' /root/penpen_rules.sh

sed -i 's/STAF_START="10:00"/STAF_START="01:00"/' /root/penpen_rules.sh

sed -i 's/STAF_STOP="12:00"/STAF_STOP="02:00"/' /root/penpen_rules.sh
```

### 4.2 Menerapkan Perubahan

Jalankan kembali skrip:

```bash
/root/penpen_rules.sh
```

Verifikasi rule aktif:

```bash
iptables -S
```
### 4.3 Pengujian dari Unit-01 (Pilot — Di Luar Jadwal)

**Lokasi:** Unit-01

Perintah:

```bash
ping -c 2 -W 2 192.225.3.195
```

**Hasil yang diharapkan:** Ping ditolak dengan 100% packet loss atau RTO.

<img width="577" height="140" alt="Screenshot 2026-11-26 180037" src="https://github.com/user-attachments/assets/eafffa81-e8cf-4e73-8165-3ead3f229f12" />


### 4.4 Pengujian dari Lilith (Staf — Di Luar Jadwal)

**Lokasi:** Lilith

Perintah:

```bash
ping -c 2 -W 2 192.225.3.195
```

**Hasil yang diharapkan:** Ping ditolak dengan 100% packet loss atau RTO.

<img width="597" height="142" alt="Screenshot 2026-11-26 180053" src="https://github.com/user-attachments/assets/bc1d7508-3bef-40af-8e7c-78e87f8f0e00" />


### 4.5 Pengujian dari Spy (Terduga Dummy System)

**Lokasi:** Spy

Perintah:

```bash
ping -c 2 -W 2 192.225.3.195
```

**Hasil yang diharapkan:** Ping tetap ditolak dengan 100% packet loss atau RTO.

<img width="597" height="146" alt="Screenshot 2026-11-26 180111" src="https://github.com/user-attachments/assets/6e843424-789b-4734-b0af-e0697899c2c9" />


---

## 5. Pemulihan ke Jadwal Resmi Soal

Setelah pengujian Kondisi 1 dan Kondisi 2 selesai, jadwal pada skrip `/root/penpen_rules.sh` harus dikembalikan ke ketentuan resmi soal.

### 5.1 Jadwal Resmi

| Kategori | Jadwal WIB | Jadwal UTC | Hari |
|---|---|---|---|
| Pilot | 08.00–16.00 | 01:00–09:00 | Senin–Jumat |
| Staf Geofront | 17.00–23.00 | 10:00–16:00 | Setiap hari |

### 5.2 Mengembalikan Variabel Jadwal

Jalankan perintah berikut pada Pen-Pen:

```bash
sed -i 's/PILOT_START="01:00"/PILOT_START="01:00"/' /root/penpen_rules.sh

sed -i 's/PILOT_STOP="02:00"/PILOT_STOP="09:00"/' /root/penpen_rules.sh

sed -i 's/STAF_START="01:00"/STAF_START="10:00"/' /root/penpen_rules.sh

sed -i 's/STAF_STOP="02:00"/STAF_STOP="16:00"/' /root/penpen_rules.sh
```

### 5.3 Menerapkan Jadwal Resmi

Jalankan kembali skrip:

```bash
/root/penpen_rules.sh
```

Periksa konfigurasi firewall:

```bash
iptables -S
```

Pastikan jadwal resmi telah dikembalikan dan rule firewall aktif.

---

## 6. Kesimpulan

Konfigurasi firewall pada node Pen-Pen berhasil diterapkan untuk membatasi akses berdasarkan kategori node dan jadwal waktu tertentu.

Hasil akhir yang diharapkan:

1. Unit-01 sebagai anggota Pilot dapat melakukan ping ke Pen-Pen selama jadwal akses berlaku.
2. Lilith sebagai Staf Geofront dapat melakukan ping ke Pen-Pen selama jadwal akses berlaku.
3. Spy sebagai Terduga Dummy System selalu ditolak, baik pada Kondisi 1 maupun Kondisi 2.
4. Unit-01 dan Lilith ditolak ketika berada di luar jadwal akses.
5. Jadwal resmi dapat dipulihkan setelah pengujian selesai.
6. Lalu lintas lain di luar pembatasan ICMP echo-request dan TCP port 80 tetap diizinkan.

Dengan demikian, pembatasan akses berdasarkan kategori dan waktu telah berhasil diuji tanpa mengubah jam sistem komputer.

---

# Soal 15: Banjir Ping di Pusat Komando

## 1. Analisis dan Masalah

Node **Tokyo3-Core** (`192.225.4.106`) merupakan pusat komando yang berisiko mengalami gangguan akibat serangan banjir ping (*ICMP flood*).

Kebutuhan pembatasan:

1. Tokyo3-Core hanya menjawab maksimal **5 ping per detik**, menggunakan `-m limit --limit 5/sec --limit-burst 5`.
2. Paket ping yang melebihi batas harus dibuang (*DROP*).
3. Ping normal dengan laju di bawah batas harus tetap diterima.
4. Pembatasan tidak boleh mengganggu ping yang diinisiasi keluar oleh Tokyo3-Core.

**Solusi:** Terapkan *rate limit* pada paket ICMP `echo-request` di chain `INPUT`, lalu buang paket yang melampaui batas. Aturan loopback dan paket balasan untuk koneksi keluar juga tetap diizinkan.

## 2. Langkah Konfigurasi

Aturan firewall diterapkan pada node **Tokyo3-Core**.

```bash
# Bersihkan chain INPUT
iptables -F INPUT

# 1. Izinkan interface loopback
iptables -A INPUT -i lo -j ACCEPT

# 2. Rate limit ICMP echo-request maksimal 5 per detik
iptables -A INPUT -p icmp --icmp-type echo-request \
  -m limit --limit 5/sec --limit-burst 5 -j ACCEPT

# 3. Buang paket ping yang melebihi kuota limit
iptables -A INPUT -p icmp --icmp-type echo-request -j DROP

# 4. Izinkan paket balasan untuk koneksi keluar
iptables -A INPUT -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT

# 5. Izinkan layanan HTTP pada port 80 dan 8080
iptables -A INPUT -p tcp -m multiport --dports 80,8080 -j ACCEPT

# 6. Policy default tetap ACCEPT
iptables -P INPUT ACCEPT
```

### Verifikasi Counter

```bash
iptables -L INPUT -v -n
```
## 3. Pengujian dan Validasi Hasil

### Pengujian 1: Ping Banjir dari Lilith

Jalankan perintah berikut pada node **Lilith**:

```bash
ping -f -c 50 192.225.4.106
```

**Hasil yang diharapkan:** Dari 50 paket yang dikirimkan secara rapat, sebagian besar paket dibuang sehingga terjadi *packet loss* yang signifikan.

<img width="720" height="142" alt="Screenshot 2026-11-26 181517" src="https://github.com/user-attachments/assets/c1f0f756-64c4-4c68-a394-82bfa2c45623" />


### Pengujian 2: Memeriksa Counter Rule DROP

Setelah pengujian ping banjir, jalankan perintah berikut pada **Tokyo3-Core**:

```bash
iptables -L INPUT -v -n
```

**Hasil yang diharapkan:** Counter paket pada rule `DROP` untuk protokol ICMP meningkat. Contoh hasil pengamatan: **43 paket** dan **3612 bytes** dibuang karena melebihi batas.

<img width="940" height="252" alt="Screenshot 2026-11-26 181604" src="https://github.com/user-attachments/assets/b4c71f07-9d95-4e11-9a4f-f6d585c36e3e" />


### Pengujian 3: Ping Normal dengan Jeda 3 Detik

Jalankan perintah berikut pada node **Lilith**:

```bash
ping -i 3 -c 4 192.225.4.106
```

**Hasil yang diharapkan:** Ping berhasil **100%** tanpa *packet loss* (`0% loss`), karena laju paket tidak melampaui batas 5 ping per detik.

<img width="572" height="217" alt="Screenshot 2026-11-26 181652" src="https://github.com/user-attachments/assets/2577aab4-6441-416c-8aa7-57c7e4268083" />

## 4. Skrip Otomasi

Simpan skrip berikut sebagai `/root/tokyo3_limit.sh` pada node **Tokyo3-Core**.

```bash
#!/bin/sh

# Rate Limit Ping Tokyo3-Core (Soal 15)
iptables -F INPUT

# 1. Loopback
iptables -A INPUT -i lo -j ACCEPT

# 2. Rate limit maksimal 5 ping per detik
iptables -A INPUT -p icmp --icmp-type echo-request \
  -m limit --limit 5/sec --limit-burst 5 -j ACCEPT
iptables -A INPUT -p icmp --icmp-type echo-request -j DROP

# 3. Established dan service port
iptables -A INPUT -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT
iptables -A INPUT -p tcp -m multiport --dports 80,8080 -j ACCEPT

iptables -P INPUT ACCEPT

echo "== Rate Limit Tokyo3-Core Aktif =="

iptables -L INPUT -v -n
```

Jalankan skrip:

```bash
chmod +x /root/tokyo3_limit.sh
/root/tokyo3_limit.sh
```

## 5. Catatan

- Rule `DROP` untuk `echo-request` harus berada setelah rule `ACCEPT` yang menggunakan modul `limit`.
- Rule pembatasan hanya mencocokkan paket ICMP `echo-request`; paket ICMP lainnya tidak terkena rule tersebut.
- Paket `echo-reply` untuk ping yang diinisiasi keluar tidak dicocokkan oleh rule `echo-request` dan dapat diterima melalui rule `ESTABLISHED,RELATED`.
- Counter dan hasil pengujian dapat berbeda sesuai kondisi jaringan dan waktu pengujian.


# Soal 16: Pencuri yang Mencoba Setiap Pintu

## 1. Analisis dan Masalah

Node **Dummy-Plug** (`192.225.4.51`) mencoba memindai port sensitif pada pusat komando **Tokyo3-Core** (`192.225.4.106`), yaitu port TCP **22, 23, dan 3306**.

Kebutuhan keamanan:

1. Setiap percobaan koneksi TCP dari Dummy-Plug ke port 22, 23, dan 3306 harus dicatat dalam log sistem menggunakan awalan `SCAN-NERV:`.
2. Koneksi ke port tersebut harus langsung ditolak menggunakan TCP Reset (`REJECT --reject-with tcp-reset`).
3. Layanan normal pada port 80 dan 8080 harus tetap dapat diakses oleh Dummy-Plug maupun klien lainnya.
4. Counter pada rule `LOG` digunakan sebagai bukti bahwa paket percobaan akses telah terdeteksi dan diproses, meskipun log kernel container tidak selalu ditampilkan pada konsol syslog.

**Solusi:** Tambahkan rule `LOG` dan `REJECT` khusus untuk alamat IP Dummy-Plug dan port TCP yang dibatasi. Rule tersebut ditempatkan sebelum rule penerimaan layanan normal.

## 2. Langkah Konfigurasi

Konfigurasi dilakukan pada node **Tokyo3-Core** dengan tetap mempertahankan aturan pembatasan ping dari Soal 15.

```bash
# 1. Bersihkan chain INPUT
iptables -F INPUT

# 2. Izinkan interface loopback
iptables -A INPUT -i lo -j ACCEPT

# 3. Rate limit ping (Soal 15)
iptables -A INPUT -p icmp --icmp-type echo-request \
  -m limit --limit 5/sec --limit-burst 5 -j ACCEPT

iptables -A INPUT -p icmp --icmp-type echo-request -j DROP

# 4. Izinkan paket balasan (ESTABLISHED, RELATED)
iptables -A INPUT -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT

# 5. Catat percobaan akses Dummy-Plug ke port sensitif
iptables -A INPUT -p tcp -s 192.225.4.51 \
  -m multiport --dports 22,23,3306 \
  -j LOG --log-prefix "SCAN-NERV: "

# 6. Tolak koneksi menggunakan TCP Reset
iptables -A INPUT -p tcp -s 192.225.4.51 \
  -m multiport --dports 22,23,3306 \
  -j REJECT --reject-with tcp-reset

# 7. Izinkan akses normal ke port 80 dan 8080
iptables -A INPUT -p tcp -m multiport --dports 80,8080 -j ACCEPT

# 8. Policy default tetap ACCEPT
iptables -P INPUT ACCEPT
```

### Verifikasi Aturan Firewall

```bash
iptables -L INPUT -v -n
```
## 3. Pengujian dan Validasi Hasil

### Pengujian 1: Akses Port Terlarang dari Dummy-Plug

Jalankan perintah berikut pada node **Dummy-Plug**:

```bash
nc -zv -w 2 192.225.4.106 22
nc -zv -w 2 192.225.4.106 23
nc -zv -w 2 192.225.4.106 3306
```

**Hasil yang diharapkan:** Seluruh percobaan koneksi ke port 22, 23, dan 3306 langsung ditolak (*Connection refused*) tanpa menunggu hingga timeout.

<img width="660" height="128" alt="Screenshot 2026-11-26 182321" src="https://github.com/user-attachments/assets/47d05dcb-dab6-4779-8b96-63ca4a936557" />

### Pengujian 2: Akses Port Layanan Normal

Jalankan perintah berikut pada node **Dummy-Plug**:

```bash
echo "Tes 80" | nc -w 2 192.225.4.106 80
echo "Tes 8080" | nc -w 2 192.225.4.106 8080
```

**Hasil yang diharapkan:**

- Port 80 berhasil diakses dan memberikan respons `Welcome to Tokyo3-Core`.
- Port 8080 berhasil diakses dan memberikan respons `syifa imutz`.

Dengan demikian, pembatasan port sensitif tidak mengganggu layanan normal.

<img width="558" height="95" alt="Screenshot 2026-11-26 182328" src="https://github.com/user-attachments/assets/e8c68610-e759-44f9-9cc7-ff68d44c3ca9" />

### Pengujian 3: Memeriksa Counter Rule LOG dan REJECT

Setelah percobaan koneksi dilakukan, jalankan perintah berikut pada **Tokyo3-Core**:

```bash
iptables -L INPUT -v -n
```

**Hasil yang diharapkan:** Counter pada rule `LOG` dan `REJECT` untuk TCP port 22, 23, dan 3306 bertambah. Contoh hasil pengamatan adalah **3 paket** dan **180 bytes** pada masing-masing rule.

Hal ini membuktikan bahwa percobaan koneksi dari Dummy-Plug telah terdeteksi oleh rule `LOG`, kemudian ditolak oleh rule `REJECT`.

<img width="956" height="331" alt="Screenshot 2026-11-26 182404" src="https://github.com/user-attachments/assets/c868de68-0ad5-4d71-b877-7686150b8d3e" />


## 4. Skrip Otomasi

Simpan skrip berikut sebagai `/root/tokyo3_rules.sh` pada node **Tokyo3-Core**.

```bash
#!/bin/sh

# Aturan Tokyo3-Core (Soal 15 & Soal 16)

# Bersihkan chain INPUT
iptables -F INPUT

# 1. Loopback
iptables -A INPUT -i lo -j ACCEPT

# 2. Rate Limit Ping (Soal 15)
iptables -A INPUT -p icmp --icmp-type echo-request \
  -m limit --limit 5/sec --limit-burst 5 -j ACCEPT

iptables -A INPUT -p icmp --icmp-type echo-request -j DROP

# 3. Established dan Related
iptables -A INPUT -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT

# 4. Pencatatan Log Dummy-Plug (Soal 16)
iptables -A INPUT -p tcp -s 192.225.4.51 \
  -m multiport --dports 22,23,3306 \
  -j LOG --log-prefix "SCAN-NERV: "

# 5. Penolakan koneksi menggunakan TCP Reset
iptables -A INPUT -p tcp -s 192.225.4.51 \
  -m multiport --dports 22,23,3306 \
  -j REJECT --reject-with tcp-reset

# 6. Izinkan layanan port 80 dan 8080
iptables -A INPUT -p tcp -m multiport --dports 80,8080 -j ACCEPT

# 7. Policy default
iptables -P INPUT ACCEPT

echo "== Aturan Tokyo3-Core Soal 15 & 16 Aktif =="

# Tampilkan aturan dan counter
iptables -L INPUT -v -n
```

### Menjalankan Skrip

```bash
chmod +x /root/tokyo3_rules.sh
/root/tokyo3_rules.sh
```

## 5. Catatan Teknis

- Rule `LOG` harus ditempatkan sebelum rule `REJECT` agar paket tercatat sebelum koneksinya ditolak.
- Target `LOG` tidak menghentikan pemrosesan paket. Paket akan melanjutkan pemeriksaan ke rule berikutnya.
- Target `REJECT --reject-with tcp-reset` mengirimkan TCP Reset sehingga koneksi ditolak secara langsung.
- Rule pembatasan hanya berlaku untuk sumber `192.225.4.51` dan port TCP 22, 23, serta 3306.
- Port 80 dan 8080 tetap diizinkan untuk seluruh alamat sumber karena rule penerimaannya tidak memiliki pembatasan alamat IP.
- Counter `LOG` dan `REJECT` dapat digunakan sebagai bukti pengujian apabila log kernel tidak terlihat pada konsol container.


# Soal 17: Sihir Hitam di Jalur Paket

## 1. Analisis dan Masalah

Router **Fuyutsuki**, yang berperan sebagai gateway Switch-Terminal, harus mengalihkan koneksi TCP dari **Magi-Casper** (`192.225.4.58`) yang ditujukan ke **Zeruel** (`192.225.4.82`) agar sampai ke **Pen-Pen** (`192.225.3.195`).

Kebutuhan konfigurasi:

1. Pengalihan dilakukan secara transparan menggunakan **Destination NAT (DNAT)** pada chain `PREROUTING` tabel `nat` di router Fuyutsuki.
2. Magi-Casper tidak boleh menyadari adanya pengalihan. Paket balasan akan ditranslasikan kembali oleh connection tracking (*conntrack*) sehingga tetap tampak berasal dari Zeruel.
3. Protokol ICMP tidak boleh dialihkan. Ping dari Magi-Casper ke Zeruel harus tetap menuju alamat Zeruel yang asli.

**Solusi:** Terapkan rule DNAT yang hanya mencocokkan koneksi TCP dari IP Magi-Casper menuju IP Zeruel. Paket yang cocok akan diarahkan ke IP Pen-Pen, sedangkan paket ICMP tidak terpengaruh.

### Informasi Node

| Node | Alamat IP | Peran |
|---|---|---|
| Fuyutsuki | Router Switch-Terminal | Gateway dan pelaksana DNAT |
| Magi-Casper | `192.225.4.58` | Sumber koneksi |
| Zeruel | `192.225.4.82` | Tujuan awal koneksi |
| Pen-Pen | `192.225.3.195` | Tujuan pengalihan |

## 2. Langkah Konfigurasi

Konfigurasi DNAT dilakukan pada router **Fuyutsuki**.

### Memasang Rule DNAT

```bash
# Alihkan koneksi TCP dari Magi-Casper menuju Zeruel ke Pen-Pen
iptables -t nat -A PREROUTING \
  -p tcp \
  -s 192.225.4.58 \
  -d 192.225.4.82 \
  -j DNAT --to-destination 192.225.3.195
```

Rule tersebut hanya berlaku untuk paket TCP dengan alamat sumber dan tujuan yang sesuai. Tidak ada rule untuk ICMP, sehingga paket ping tetap menuju Zeruel.

### Verifikasi Rule NAT

```bash
iptables -t nat -S
```

## 3. Pengujian dan Validasi Hasil

### Persiapan: Menyalakan Listener TCP

Jalankan listener pada port 9000 di kedua node tujuan.

**Pada Pen-Pen (`192.225.3.195`):**

```bash
nc -l -v -n -p 9000
```

**Pada Zeruel (`192.225.4.82`):**

```bash
nc -l -v -n -p 9000
```

Kedua listener digunakan untuk membuktikan bahwa koneksi dari Magi-Casper benar-benar diterima oleh Pen-Pen, bukan Zeruel.

### Pengujian 1: Mengirim Pesan TCP dari Magi-Casper ke IP Zeruel

Jalankan perintah berikut pada node **Magi-Casper**:

```bash
echo "Halo Zeruel dari Casper (Sihir Hitam Soal 17)" | nc -w 3 192.225.4.82 9000
```

**Hasil yang diharapkan:**

1. **Pen-Pen:** Pesan berhasil diterima dan tampil secara utuh pada terminal listener.
2. **Zeruel:** Tidak menerima koneksi atau data apa pun. Terminal listener tetap kosong.

Hal ini membuktikan bahwa koneksi TCP yang ditujukan ke IP Zeruel telah dialihkan oleh Fuyutsuki ke Pen-Pen.

<img width="410" height="127" alt="image" src="https://github.com/user-attachments/assets/997d9a2b-85d2-4c7c-b6ff-fa562deb131a" />
<img width="348" height="92" alt="image" src="https://github.com/user-attachments/assets/4035bc62-52b8-4762-9c5d-39839fa71daf" />

### Pengujian 2: Memeriksa Counter Rule DNAT

Setelah pengiriman pesan TCP, jalankan perintah berikut pada router **Fuyutsuki**:

```bash
iptables -t nat -L PREROUTING -v -n
```

**Hasil yang diharapkan:** Counter pada rule target `DNAT`, khususnya kolom `pkts` dan `bytes`, mengalami peningkatan.

Kenaikan counter membuktikan bahwa paket TCP dari Magi-Casper menuju Zeruel berhasil dicocokkan dan diproses oleh rule DNAT.

<img width="750" height="138" alt="image" src="https://github.com/user-attachments/assets/07696ad9-311e-409c-b62a-b22ef52b9c91" />

### Pengujian 3: Memastikan Ping ke Zeruel Tidak Dialihkan

Jalankan perintah berikut pada node **Magi-Casper**:

```bash
ping -c 2 192.225.4.82
```

**Hasil yang diharapkan:** Ping berhasil menuju Zeruel asli dengan `0% packet loss`.

Paket ICMP tidak dialihkan karena rule DNAT hanya mencocokkan protokol TCP (`-p tcp`).

<img width="581" height="196" alt="image" src="https://github.com/user-attachments/assets/1d280086-3944-4457-9a5a-6a6201e08002" />


## 4. Skrip Otomasi

Simpan skrip berikut sebagai `/root/fuyutsuki_dnat.sh` pada router **Fuyutsuki**.

Skrip menggunakan pemeriksaan `iptables -C` agar rule tidak ditambahkan berulang kali apabila skrip dijalankan lebih dari satu kali.

```bash
#!/bin/sh

# Soal 17 - Sihir Hitam DNAT Casper ke Zeruel dialihkan ke Pen-Pen

# Periksa apakah rule DNAT sudah tersedia.
# Jika belum tersedia, tambahkan rule.
iptables -t nat -C PREROUTING \
  -p tcp \
  -s 192.225.4.58 \
  -d 192.225.4.82 \
  -j DNAT --to-destination 192.225.3.195 2>/dev/null || \
iptables -t nat -A PREROUTING \
  -p tcp \
  -s 192.225.4.58 \
  -d 192.225.4.82 \
  -j DNAT --to-destination 192.225.3.195

echo "== DNAT Fuyutsuki Aktif =="

# Tampilkan aturan NAT
iptables -t nat -S
```

### Menjalankan Skrip

```bash
chmod +x /root/fuyutsuki_dnat.sh
/root/fuyutsuki_dnat.sh
```

## 5. Catatan Teknis

- DNAT dilakukan pada chain `PREROUTING` tabel `nat` agar alamat tujuan paket diubah sebelum proses routing menentukan jalur berikutnya.
- Rule hanya mencocokkan protokol TCP, sumber `192.225.4.58`, dan tujuan `192.225.4.82`.
- Paket ICMP tidak cocok dengan rule tersebut sehingga ping ke Zeruel tetap berjalan normal.
- Conntrack menyimpan informasi translasi koneksi. Untuk koneksi yang berhasil melalui jalur routing dan NAT, paket balasan akan mengalami translasi balik secara otomatis.
- Counter pada tabel `nat` umumnya dihitung berdasarkan paket pertama dari setiap koneksi baru, bukan seluruh paket dalam koneksi tersebut. Karena itu, gunakan koneksi baru saat menguji kenaikan counter.
- Pastikan router Fuyutsuki memiliki jalur routing menuju jaringan Pen-Pen dan kebijakan forwarding mengizinkan paket yang telah ditranslasikan melewati router.
- Jika koneksi TCP tidak sampai ke Pen-Pen, periksa konfigurasi IP forwarding, tabel routing, dan aturan firewall chain `FORWARD` pada Fuyutsuki.

# Soal 18: Gerbang Monolith dan Radar

## 1. Analisis dan Masalah

Area **Monolith** (Switch-Monolith: Zeruel dan Armisael) serta **Radar** (Switch-Radar: Radar-Array) merupakan zona sensitif NERV yang dijaga oleh router **Shigeru**.

Kebutuhan keamanan:

1. Seluruh node di dalam zona sensitif diizinkan untuk memulai koneksi ke luar.
2. Paket balasan dari koneksi yang dimulai oleh node dalam zona harus dapat diterima kembali menggunakan conntrack (`ESTABLISHED,RELATED`).
3. Seluruh node dari luar zona tidak boleh memulai koneksi baru ke dalam zona.
4. Terdapat satu pengecualian: paket ICMP `echo-request` dari subnet Terminal (`192.225.4.56/29`) diizinkan masuk.
5. Pemblokiran harus didasarkan pada interface yang menghadap router pusat Gendo, yaitu `eth0`, bukan dengan mendaftarkan subnet luar satu per satu.

**Solusi:** Terapkan aturan firewall pada chain `FORWARD` di router Shigeru. Izinkan koneksi balasan dan lalu lintas yang berasal dari zona sensitif melalui `eth1` dan `eth2`. Setelah itu, berikan pengecualian ping dari subnet Terminal, lalu blokir lalu lintas lainnya yang masuk melalui `eth0`.

### Informasi Interface

| Interface | Arah / Fungsi |
|---|---|
| `eth0` | Menghadap router pusat Gendo |
| `eth1` | Mengarah ke salah satu zona sensitif |
| `eth2` | Mengarah ke zona sensitif lainnya |

## 2. Langkah Konfigurasi

Konfigurasi firewall diterapkan pada router **Shigeru**, tepatnya di chain `FORWARD`.

### Memasang Aturan Firewall

```bash
# 1. Bersihkan chain FORWARD
iptables -F FORWARD

# 2. Izinkan koneksi balasan
iptables -A FORWARD -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT

# 3. Izinkan traffic yang berasal dari zona sensitif
iptables -A FORWARD -i eth1 -j ACCEPT
iptables -A FORWARD -i eth2 -j ACCEPT

# 4. Pengecualian: Izinkan ping dari subnet Terminal
iptables -A FORWARD -i eth0 \
  -s 192.225.4.56/29 \
  -p icmp --icmp-type echo-request -j ACCEPT

# 5. Blokir seluruh traffic lainnya dari arah Gendo
iptables -A FORWARD -i eth0 -j DROP

# 6. Policy default tetap ACCEPT
iptables -P FORWARD ACCEPT
```

### Verifikasi Aturan Firewall

```bash
iptables -L FORWARD -v -n
```
## 3. Pengujian dan Validasi Hasil

### Pengujian 1: Ping dari Magi-Casper ke Zeruel

Pengujian ini membuktikan bahwa subnet Terminal (`192.225.4.56/29`) mendapatkan pengecualian untuk mengirim ping ke zona sensitif.

Jalankan perintah berikut pada node **Magi-Casper**:

```bash
ping -c 3 192.225.4.82
```

**Hasil yang diharapkan:** Ping berhasil dengan `0% packet loss` karena Magi-Casper berada di subnet Terminal yang diizinkan oleh rule firewall.

<img width="577" height="217" alt="Screenshot 2026-11-26 183753" src="https://github.com/user-attachments/assets/9e98fada-7e51-48ac-acdd-8161240bddd6" />



### Pengujian 2: Ping dari Lilith ke Zeruel

Pengujian ini membuktikan bahwa node dari luar zona sensitif tidak dapat memulai koneksi menuju zona Monolith.

Jalankan perintah berikut pada node **Lilith**:

```bash
ping -c 3 -W 2 192.225.4.82
```

**Hasil yang diharapkan:** Ping gagal dengan `100% packet loss` karena paket berasal dari arah Gendo melalui interface `eth0` dan bukan berasal dari subnet Terminal yang mendapatkan pengecualian.

<img width="613" height="160" alt="Screenshot 2026-11-26 183809" src="https://github.com/user-attachments/assets/fa9dfa0d-b7a5-4e9f-b798-dab8be1ff53a" />


### Pengujian 3: Memeriksa Counter Rule FORWARD

Setelah kedua pengujian selesai, jalankan perintah berikut pada router **Shigeru**:

```bash
iptables -L FORWARD -v -n
```

**Hasil yang diharapkan:**

- Counter pada rule `ACCEPT` untuk ICMP dari subnet Terminal bertambah ketika Magi-Casper melakukan ping ke Zeruel.
- Counter pada rule `DROP` dengan interface masuk `eth0` bertambah ketika Lilith mencoba melakukan ping ke Zeruel.

Kenaikan kedua counter tersebut membuktikan bahwa aturan pengecualian dan pemblokiran telah bekerja sesuai kebutuhan.

<img width="712" height="292" alt="Screenshot 2026-11-26 183828" src="https://github.com/user-attachments/assets/e6dd3001-a0ed-4eaf-a8de-bca4a6459a9b" />


## 4. Skrip Otomasi

Simpan skrip berikut sebagai `/root/shigeru_gate.sh` pada router **Shigeru**.

```bash
#!/bin/sh

# Aturan Gerbang Monolith & Radar (Soal 18)

# Bersihkan chain FORWARD
iptables -F FORWARD

# 1. Izinkan koneksi balasan
iptables -A FORWARD -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT

# 2. Izinkan traffic keluar dari zona sensitif
iptables -A FORWARD -i eth1 -j ACCEPT
iptables -A FORWARD -i eth2 -j ACCEPT

# 3. Pengecualian: Ping dari subnet Terminal
iptables -A FORWARD -i eth0 \
  -s 192.225.4.56/29 \
  -p icmp --icmp-type echo-request -j ACCEPT

# 4. Blokir traffic lainnya dari arah Gendo
iptables -A FORWARD -i eth0 -j DROP

# 5. Policy default tetap ACCEPT
iptables -P FORWARD ACCEPT

echo "== Gerbang Shigeru Aktif =="

# Tampilkan aturan dan counter
iptables -L FORWARD -v -n
```

### Menjalankan Skrip

```bash
chmod +x /root/shigeru_gate.sh
/root/shigeru_gate.sh
```

## 5. Catatan Teknis

- Chain `FORWARD` digunakan karena router Shigeru memproses paket yang melewati router menuju jaringan lain.
- Rule `ESTABLISHED,RELATED` memungkinkan paket balasan dari koneksi yang dimulai oleh node di zona sensitif diterima kembali.
- Rule `-i eth1` dan `-i eth2` mengizinkan koneksi yang berasal dari interface zona sensitif untuk diteruskan keluar.
- Rule pengecualian ICMP harus diletakkan sebelum rule `DROP` agar ping dari subnet Terminal tidak ikut diblokir.
- Rule `-i eth0 -j DROP` memblokir seluruh paket lain yang masuk dari arah Gendo, tanpa perlu mengetahui atau mendaftarkan subnet sumber satu per satu.
- Policy default `ACCEPT` dipertahankan sesuai konfigurasi soal. Perlindungan terhadap traffic dari luar zona dilakukan secara khusus melalui rule `DROP` pada `eth0`.

# Soal 19: Hukuman untuk Sang Pengkhianat

## 1. Analisis dan Masalah

Node Armisael (`192.225.4.83`) pada Switch-Monolith teridentifikasi sebagai penyusup yang harus diisolasi sepenuhnya dari seluruh jaringan Geofront.

### Ketentuan dan Batasan

1. Seluruh lalu lintas masuk dan keluar Armisael harus diblokir, mencakup:
   - Akses ke gateway (router Shigeru).
   - Komunikasi dengan tetangga satu switch, yaitu Zeruel (`192.225.4.82`).
   - Akses ke jaringan lain dan internet.
2. **Larangan mutlak:** Isolasi tidak boleh dilakukan di dalam node Armisael karena node pengkhianat tidak dapat dipercaya.
3. Node Zeruel yang berada pada switch yang sama tidak boleh ikut terisolasi dan harus tetap dapat berkomunikasi secara normal.

### Catatan Teknis Arsitektur Isolasi (Layer 2 vs Layer 3)

#### A. Isolasi Layer 2 (Intra-Switch)

Switch-Monolith hanya menampung dua host, yaitu Zeruel dan Armisael. Karena switch beroperasi pada Layer 2 tanpa dukungan ACL internal, isolasi komunikasi antara kedua host tidak dapat ditangani oleh router.

Oleh karena itu, proteksi dipasang langsung pada host Zeruel menggunakan chain `INPUT` dan `OUTPUT` untuk menolak seluruh komunikasi dengan alamat IP Armisael.

#### B. Isolasi Layer 3 (Inter-Subnet dan Internet)

Seluruh lalu lintas dari Armisael yang ditujukan ke luar switch, seperti menuju Seele (`8.8.8.8`) di internet atau Lilith di Switch-Dogma, secara fisik dan logika harus melewati router Shigeru sebagai default gateway.

Rule `DROP` pada chain `INPUT` dan `FORWARD` di router Shigeru digunakan untuk menjamin isolasi sehingga paket dari dan menuju Armisael dibuang pada hop pertama.

---

## 2. Langkah Konfigurasi

### A. Konfigurasi pada Router Shigeru (Isolasi Gateway dan Lalu Lintas Luar)

Jalankan perintah berikut pada router Shigeru:

```bash
# Blokir akses Armisael ke router gateway Shigeru sendiri
iptables -I INPUT 1 -s 192.225.4.83 -j DROP

# Blokir seluruh lalu lintas Armisael yang melintasi router
# (ke internet dan subnet lain)
iptables -I FORWARD 1 -s 192.225.4.83 -j DROP
iptables -I FORWARD 2 -d 192.225.4.83 -j DROP

# Verifikasi rule aktif
iptables -L FORWARD -v -n
```

<img width="838" height="468" alt="Screenshot 2026-11-26 185044" src="https://github.com/user-attachments/assets/954ff779-0ca2-4a36-9633-3e76a89e51aa" />


### B. Konfigurasi pada Node Zeruel (Proteksi Host Satu Switch)

Jalankan perintah berikut pada Zeruel:

```bash
# Blokir paket masuk dari Armisael
iptables -I INPUT 1 -s 192.225.4.83 -j DROP

# Blokir paket keluar menuju Armisael
iptables -I OUTPUT 1 -d 192.225.4.83 -j DROP

# Verifikasi rule aktif
iptables -S
```

<img width="687" height="258" alt="Screenshot 2026-11-26 185029" src="https://github.com/user-attachments/assets/2f12f50b-f725-435b-8786-d41a92e17937" />

---

## 3. Pengujian dan Validasi Hasil

### Persiapan Listener Pengujian

Sebelum melakukan pengujian konektivitas, jalankan listener Netcat pada masing-masing node berikut.

**Pada Armisael:**

```bash
nc -l -p 9000 &
```

**Pada Zeruel:**

```bash
nc -l -p 9000 &
```

**Pada Lilith:**

```bash
nc -l -p 9000 &
```

### Pengujian 1: Seluruh Akses Masuk dan Keluar Armisael Harus Gagal

Jalankan perintah pengujian berikut dari Armisael.

```bash
# 1. Uji koneksi ke Seele (8.8.8.8)
ping -c 2 -W 2 8.8.8.8
nc -zv -w 2 8.8.8.8 53

# 2. Uji koneksi ke tetangga satu switch (Zeruel)
ping -c 2 -W 2 192.225.4.82
nc -zv -w 2 192.225.4.82 9000

# 3. Uji koneksi ke Lilith (192.225.4.74)
ping -c 2 -W 2 192.225.4.74
nc -zv -w 2 192.225.4.74 9000
```

**Hasil Pengujian:**

Seluruh pengujian menunjukkan bahwa Armisael tidak dapat berkomunikasi dengan node tujuan.

- Seluruh pengujian `ping` menghasilkan 100% packet loss.
- Seluruh koneksi Netcat (`nc`) gagal tersambung.
- Armisael berhasil diisolasi dari jaringan luar maupun tetangga satu switch.
- Proses isolasi dilakukan tanpa mengubah konfigurasi internal Armisael.

<img width="772" height="762" alt="Screenshot 2026-11-26 185206" src="https://github.com/user-attachments/assets/674db15e-e610-4b67-b6ae-3e085a39a4c6" />

### Pengujian 2: Akses dari Zeruel Tetap Berjalan Normal

Selanjutnya, lakukan pengujian konektivitas dari Zeruel untuk memastikan bahwa isolasi Armisael tidak memengaruhi host lain dalam switch yang sama.

Jalankan perintah berikut pada Zeruel:

```bash
# 1. Uji koneksi ke Seele (8.8.8.8)
ping -c 2 8.8.8.8
nc -zv -w 2 8.8.8.8 53

# 2. Uji koneksi ke Lilith (192.225.4.74)
ping -c 2 192.225.4.74
nc -zv -w 2 192.225.4.74 9000
```

**Hasil Pengujian:**

Seluruh pengujian konektivitas dari Zeruel berhasil berjalan normal.

- Seluruh pengujian `ping` berhasil dengan 0% packet loss.
- Koneksi Netcat (`nc`) berhasil tersambung ke port tujuan.
- Zeruel tetap dapat berkomunikasi dengan jaringan internet maupun subnet lain.
- Isolasi Armisael tidak memberikan dampak terhadap konektivitas Zeruel.

<img width="563" height="492" alt="Screenshot 2026-11-26 185222" src="https://github.com/user-attachments/assets/6be07ffe-fa42-4820-9ee7-1de1db1575ce" />

---

## 4. Skrip Otomasi

Untuk mempermudah penerapan aturan isolasi, konfigurasi dapat dijalankan secara otomatis menggunakan skrip shell pada masing-masing node.

### A. Skrip pada Router Shigeru

Buat file `/root/shigeru_isolasi.sh` dengan isi berikut:

```bash
#!/bin/sh

# Isolasi Armisael di Shigeru (Soal 19)

# Blokir akses menuju router Shigeru
iptables -C INPUT -s 192.225.4.83 -j DROP 2>/dev/null || \
iptables -I INPUT 1 -s 192.225.4.83 -j DROP

# Blokir lalu lintas dari Armisael yang melewati router
iptables -C FORWARD -s 192.225.4.83 -j DROP 2>/dev/null || \
iptables -I FORWARD 1 -s 192.225.4.83 -j DROP

# Blokir lalu lintas menuju Armisael yang melewati router
iptables -C FORWARD -d 192.225.4.83 -j DROP 2>/dev/null || \
iptables -I FORWARD 2 -d 192.225.4.83 -j DROP

echo "== Isolasi Armisael di Shigeru Aktif =="
```

### B. Skrip pada Node Zeruel

Buat file `/root/zeruel_protect.sh` dengan isi berikut:

```bash
#!/bin/sh

# Isolasi Armisael di Zeruel (Soal 19)

# Blokir paket masuk dari Armisael
iptables -C INPUT -s 192.225.4.83 -j DROP 2>/dev/null || \
iptables -I INPUT 1 -s 192.225.4.83 -j DROP

# Blokir paket keluar menuju Armisael
iptables -C OUTPUT -d 192.225.4.83 -j DROP 2>/dev/null || \
iptables -I OUTPUT 1 -d 192.225.4.83 -j DROP

echo "== Proteksi Armisael di Zeruel Aktif =="
```

### C. Menjalankan Skrip

Berikan izin eksekusi pada masing-masing skrip.

**Pada Shigeru:**

```bash
chmod +x /root/shigeru_isolasi.sh
/root/shigeru_isolasi.sh
```

**Pada Zeruel:**

```bash
chmod +x /root/zeruel_protect.sh
/root/zeruel_protect.sh
```

---

## 5. Kesimpulan

Berdasarkan konfigurasi dan pengujian yang dilakukan, isolasi terhadap node Armisael (`192.225.4.83`) berhasil diterapkan dengan memanfaatkan kombinasi firewall Layer 2 dan Layer 3.

Penerapan aturan firewall pada router Shigeru menggunakan chain `INPUT` dan `FORWARD` berhasil membatasi akses Armisael menuju gateway, internet, serta jaringan lain. Sementara itu, aturan firewall pada Zeruel menggunakan chain `INPUT` dan `OUTPUT` untuk memblokir komunikasi langsung antara kedua host yang berada dalam satu switch.

Hasil pengujian juga menunjukkan bahwa Zeruel tetap dapat berkomunikasi secara normal dengan jaringan internet maupun node lain.

Dengan demikian, tujuan isolasi Armisael berhasil dicapai tanpa perlu melakukan perubahan konfigurasi pada node yang dicurigai dan tanpa mengganggu konektivitas host lain.

**Status akhir: Armisael terisolasi, Zeruel tetap beroperasi normal.**

# Soal 20: Uji Kebakaran Geofront (Siap Dihancurkan, Siap Dibangun Lagi)

## 1. Analisis dan Masalah

Infrastruktur NERV harus memiliki ketahanan tinggi (*high availability* dan *disaster recovery*) serta mampu dibangun ulang secara cepat ketika terjadi insiden darurat atau bencana, yang dalam pengujian ini disimulasikan sebagai "kebakaran".

### Kebutuhan dan Batasan Pengujian

1. Memilih tiga node mandiri dengan minimal satu node router. Node yang dipilih adalah:
   - **Router Shigeru**: Mewakili router utama zona sensitif.
   - **Host Magi-Casper**: Mewakili host layanan MAGI.
   - **Host Tokyo3-Core**: Mewakili host pusat komando.
2. Pada setiap node, seluruh konfigurasi firewall disimpan menggunakan `iptables-save` ke file `/root/<nama>.rules`.
3. Dilakukan simulasi kehancuran total dengan menghapus seluruh rule iptables pada tabel `filter` dan `nat`, serta menghapus rute yang ditambahkan secara manual.
4. Konfigurasi dipulihkan menggunakan `iptables-restore` dan skrip `/root/<nama>.sh`.
5. Proses pemulihan dijalankan **dua kali berturut-turut** untuk membuktikan prinsip **idempotensi**.

   Indikator keberhasilan:
   - Jumlah baris rule dari `iptables -S` harus sama antara pemulihan pertama dan kedua.
   - Jumlah baris rule dari `iptables -t nat -S` harus sama antara pemulihan pertama dan kedua.
   - Tidak terjadi duplikasi aturan maupun rute.
   - Seluruh node kembali berfungsi normal seperti sebelum simulasi kehancuran.

---

## 2. Langkah Pengujian Node 1: Router Shigeru

### A. Pencadangan Konfigurasi Awal

Sebelum melakukan simulasi kehancuran, simpan seluruh konfigurasi firewall Router Shigeru ke dalam file backup.

```bash
iptables-save > /root/shigeru.rules
```

File `/root/shigeru.rules` digunakan sebagai sumber konfigurasi untuk proses pemulihan.

### B. Simulasi Kehancuran (Flush Total Rule dan Rute)

Lakukan penghapusan seluruh aturan firewall dan rute default yang digunakan oleh Router Shigeru.

```bash
# Hapus seluruh rule pada tabel filter
iptables -F
iptables -X

# Hapus seluruh rule pada tabel nat
iptables -t nat -F
iptables -t nat -X

# Kembalikan default policy menjadi ACCEPT
iptables -P INPUT ACCEPT
iptables -P FORWARD ACCEPT
iptables -P OUTPUT ACCEPT

# Hapus default route
ip route del default 2>/dev/null

# Verifikasi kondisi firewall setelah dihancurkan
iptables -S
iptables -t nat -S

# Verifikasi tabel routing
ip route
```

**Hasil Pengujian:**

Seluruh rule firewall pada tabel `filter` dan `nat` berhasil dihapus. Rute default juga dihapus sehingga Router Shigeru berada dalam kondisi bersih atau kosong sesuai skenario simulasi kehancuran.

<img width="657" height="557" alt="Screenshot 2026-11-26 190846" src="https://github.com/user-attachments/assets/eecd2fa2-e2ad-4583-942c-d787d285fb9d" />

### C. Pemulihan Pertama dan Kedua (Uji Idempotensi)

Lakukan pemulihan konfigurasi sebanyak dua kali berturut-turut untuk memastikan tidak terjadi duplikasi aturan.

```bash
# ==============================
# PEMULIHAN PERTAMA
# ==============================

iptables-restore < /root/shigeru.rules

sh /root/shigeru.sh 2>/dev/null || sh /root/shigeru_route.sh 2>/dev/null

echo "=== PEMULIHAN 1 SHIGERU ==="
echo "filter: $(iptables -S | wc -l)"
echo "nat   : $(iptables -t nat -S | wc -l)"

# ==============================
# PEMULIHAN KEDUA
# ==============================

iptables-restore < /root/shigeru.rules

sh /root/shigeru.sh 2>/dev/null || sh /root/shigeru_route.sh 2>/dev/null

echo "=== PEMULIHAN 2 SHIGERU ==="
echo "filter: $(iptables -S | wc -l)"
echo "nat   : $(iptables -t nat -S | wc -l)"
```

**Hasil Pengujian:**

Jumlah baris rule pada tabel `filter` dan `nat` antara pemulihan pertama dan kedua bernilai **sama persis**.

Hal ini membuktikan bahwa konfigurasi firewall berhasil dipulihkan tanpa menghasilkan duplikasi aturan.

<img width="680" height="387" alt="Screenshot 2026-11-26 190905" src="https://github.com/user-attachments/assets/19542ec7-43e7-4ba4-9f1f-575c3b1b4225" />
<img width="680" height="385" alt="Screenshot 2026-11-26 190920" src="https://github.com/user-attachments/assets/c0633c8e-99c8-4898-96ff-87fe8bb150aa" />

### D. Bukti Fungsionalitas Router Shigeru Pulih

Setelah konfigurasi berhasil dipulihkan, lakukan pengujian konektivitas ke router tetangga Gendo.

```bash
ping -c 2 192.225.4.157
```

**Hasil Pengujian:**

Router Shigeru berhasil melakukan ping ke router tetangga Gendo dengan hasil 0% packet loss.

Hal ini membuktikan bahwa konektivitas jaringan Router Shigeru telah kembali normal setelah proses pemulihan.

<img width="573" height="177" alt="Screenshot 2026-11-26 190935" src="https://github.com/user-attachments/assets/4d7bae21-4a34-4f10-8f6f-5edc80ce0e44" />

---

## 3. Langkah Pengujian Node 2: Host Magi-Casper

### A. Pencadangan Konfigurasi Awal

Simpan seluruh konfigurasi firewall pada Host Magi-Casper menggunakan perintah berikut.

```bash
iptables-save > /root/casper.rules
```

File `/root/casper.rules` akan digunakan sebagai sumber konfigurasi firewall saat proses pemulihan.

### B. Simulasi Kehancuran (Flush Total)

Hapus seluruh aturan firewall dan rute default pada Host Magi-Casper.

```bash
# Hapus seluruh rule pada tabel filter
iptables -F
iptables -X

# Hapus seluruh rule pada tabel nat
iptables -t nat -F
iptables -t nat -X

# Kembalikan default policy menjadi ACCEPT
iptables -P INPUT ACCEPT
iptables -P FORWARD ACCEPT
iptables -P OUTPUT ACCEPT

# Hapus default route
ip route del default 2>/dev/null

# Verifikasi kondisi firewall
iptables -S
iptables -t nat -S

# Verifikasi tabel routing
ip route
```

**Hasil Pengujian:**

Seluruh aturan hardening firewall dan rute default pada Magi-Casper berhasil dihapus sehingga host berada dalam kondisi bersih sesuai skenario simulasi kehancuran.

<img width="602" height="487" alt="Screenshot 2026-11-26 190955" src="https://github.com/user-attachments/assets/bb5e1b11-cfc1-496b-b11c-200d3ba4bc44" />

### C. Pemulihan Pertama dan Kedua (Uji Idempotensi)

Pulihkan konfigurasi firewall menggunakan file backup dan skrip konfigurasi Magi-Casper.

```bash
# ==============================
# PEMULIHAN PERTAMA
# ==============================

iptables-restore < /root/casper.rules

sh /root/magi-casper.sh 2>/dev/null

echo "=== PEMULIHAN 1 CASPER ==="
echo "filter: $(iptables -S | wc -l)"
echo "nat   : $(iptables -t nat -S | wc -l)"

# ==============================
# PEMULIHAN KEDUA
# ==============================

iptables-restore < /root/casper.rules

sh /root/magi-casper.sh 2>/dev/null

echo "=== PEMULIHAN 2 CASPER ==="
echo "filter: $(iptables -S | wc -l)"
echo "nat   : $(iptables -t nat -S | wc -l)"
```

**Hasil Pengujian:**

Jumlah baris rule iptables pada tabel `filter` dan `nat` menunjukkan nilai yang identik antara pemulihan pertama dan kedua.

Dengan demikian, proses pemulihan konfigurasi firewall pada Magi-Casper terbukti tidak menghasilkan duplikasi aturan.

<img width="615" height="457" alt="Screenshot 2026-11-26 191006" src="https://github.com/user-attachments/assets/02ad4bfb-a163-49b2-afe7-0ff7a766faf9" />
<img width="612" height="467" alt="Screenshot 2026-11-26 191024" src="https://github.com/user-attachments/assets/bd6fdb71-6bea-4c34-8eae-416a20360a9a" />

### D. Bukti Fungsionalitas Host Magi-Casper Pulih

Lakukan pengujian konektivitas dari Magi-Casper menuju Balthasar dan internet.

```bash
# Uji koneksi ke Balthasar
ping -c 2 192.225.4.59

# Uji koneksi ke internet
ping -c 2 8.8.8.8
```

**Hasil Pengujian:**

Magi-Casper berhasil melakukan ping ke tetangga satu switch, yaitu Balthasar (`192.225.4.59`), serta ke internet melalui alamat `8.8.8.8`.

Kedua pengujian menunjukkan bahwa konektivitas jaringan Magi-Casper telah kembali normal setelah proses pemulihan.

<img width="572" height="347" alt="Screenshot 2026-11-26 191035" src="https://github.com/user-attachments/assets/a6fcf9fd-efeb-4149-a01c-e8f71a97e383" />


---

## 4. Langkah Pengujian Node 3: Host Tokyo3-Core

### A. Pencadangan Konfigurasi Awal

Simpan seluruh konfigurasi firewall pada Host Tokyo3-Core menggunakan perintah berikut.

```bash
iptables-save > /root/tokyo3.rules
```

File `/root/tokyo3.rules` digunakan sebagai sumber konfigurasi untuk proses pemulihan.

### B. Simulasi Kehancuran (Flush Total)

Hapus seluruh aturan firewall dan rute default pada Tokyo3-Core.

```bash
# Hapus seluruh rule pada tabel filter
iptables -F
iptables -X

# Hapus seluruh rule pada tabel nat
iptables -t nat -F
iptables -t nat -X

# Kembalikan default policy menjadi ACCEPT
iptables -P INPUT ACCEPT
iptables -P FORWARD ACCEPT
iptables -P OUTPUT ACCEPT

# Hapus default route
ip route del default 2>/dev/null

# Verifikasi kondisi firewall
iptables -S
iptables -t nat -S

# Verifikasi tabel routing
ip route
```

**Hasil Pengujian:**

Seluruh aturan rate-limiting dan pencatatan aktivitas scan pada Tokyo3-Core berhasil dihapus. Rute default juga dihapus sehingga host berada dalam kondisi bersih sesuai simulasi kehancuran.

<img width="622" height="466" alt="Screenshot 2026-11-26 191054" src="https://github.com/user-attachments/assets/1bbd5ce3-9572-44dc-99ad-bc29b0311508" />

### C. Pemulihan Pertama dan Kedua (Uji Idempotensi)

Lakukan pemulihan konfigurasi menggunakan file backup dan skrip Tokyo3-Core sebanyak dua kali berturut-turut.

```bash
# ==============================
# PEMULIHAN PERTAMA
# ==============================

iptables-restore < /root/tokyo3.rules

sh /root/tokyo3-core.sh 2>/dev/null

echo "=== PEMULIHAN 1 TOKYO3-CORE ==="
echo "filter: $(iptables -S | wc -l)"
echo "nat   : $(iptables -t nat -S | wc -l)"

# ==============================
# PEMULIHAN KEDUA
# ==============================

iptables-restore < /root/tokyo3.rules

sh /root/tokyo3-core.sh 2>/dev/null

echo "=== PEMULIHAN 2 TOKYO3-CORE ==="
echo "filter: $(iptables -S | wc -l)"
echo "nat   : $(iptables -t nat -S | wc -l)"
```

**Hasil Pengujian:**

Jumlah baris rule iptables pada tabel `filter` dan `nat` tetap konsisten antara pemulihan pertama dan kedua.

Tidak ditemukan penambahan aturan secara berulang sehingga konfigurasi firewall Tokyo3-Core terbukti dapat dipulihkan tanpa duplikasi.

<img width="621" height="417" alt="Screenshot 2026-11-26 191123" src="https://github.com/user-attachments/assets/1720f2bc-edb8-4093-9915-a495017e5b8c" />
<img width="623" height="422" alt="Screenshot 2026-11-26 191137" src="https://github.com/user-attachments/assets/e5b37a3d-7674-4f2c-bc8f-f5f9ed20c275" />

> Tempatkan screenshot hasil perbandingan jumlah baris rule pada pemulihan pertama dan kedua di Host Tokyo3-Core.

### D. Bukti Fungsionalitas Host Tokyo3-Core Pulih

Setelah konfigurasi berhasil dipulihkan, lakukan pengujian konektivitas menuju router gateway Gendo.

```bash
ping -c 2 192.225.4.105
```

**Hasil Pengujian:**

Tokyo3-Core berhasil terhubung kembali ke router gateway Gendo dengan hasil 0% packet loss.

Hal ini membuktikan bahwa konektivitas jaringan Tokyo3-Core telah pulih setelah proses pemulihan konfigurasi.

<img width="572" height="186" alt="Screenshot 2026-11-26 191148" src="https://github.com/user-attachments/assets/e1ffff6a-0057-42a6-9c64-8918f0739380" />


---

## 5. Kesimpulan Babak Final

Pengujian pada ketiga node, yaitu Router Shigeru, Host Magi-Casper, dan Host Tokyo3-Core, membuktikan bahwa prosedur pencadangan (*backup*) dan pemulihan (*restore*) konfigurasi firewall dapat diterapkan untuk mendukung ketahanan infrastruktur NERV.

Melalui proses pencadangan menggunakan `iptables-save`, simulasi kehancuran menggunakan perintah `iptables -F` dan `iptables -t nat -F`, serta pemulihan menggunakan `iptables-restore` dan skrip konfigurasi masing-masing node, sistem berhasil dikembalikan ke kondisi operasional.

Pengujian pemulihan sebanyak dua kali berturut-turut juga digunakan untuk membuktikan prinsip **idempotensi**. Jumlah baris rule pada tabel `filter` dan `nat` tetap sama antara pemulihan pertama dan kedua sehingga tidak terjadi penambahan aturan firewall secara berulang.

Selain itu, pengujian konektivitas menunjukkan bahwa masing-masing node dapat kembali berkomunikasi dengan jaringan dan gateway sebagaimana mestinya.

Dengan demikian, mekanisme pencadangan dan pemulihan konfigurasi menjadi bagian penting dalam strategi *disaster recovery* untuk memastikan infrastruktur NERV mampu menghadapi skenario kegagalan dan dibangun kembali dengan cepat.

**Status Akhir: Backup berhasil, konfigurasi berhasil dipulihkan, idempotensi teruji, dan konektivitas jaringan kembali normal.**
