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
