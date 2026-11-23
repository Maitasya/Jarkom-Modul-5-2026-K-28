# Konfigurasi Soal 4 dan 5 — Cisco Packet Tracer

## Soal 4 — DHCP

### 1. Konfigurasi IP Server & Storage DC

Atur IP statis pada server melalui **Desktop → IP Configuration**.

- IP Address: `10.64.238.2`
- Subnet Mask: `255.255.255.0`
- Default Gateway: `10.64.238.1`
- DNS Server: `8.8.8.8`

### 2. Konfigurasi DHCP Pool

Buka **Server & Storage DC → Services → DHCP**, aktifkan DHCP, lalu atur pool:

- Pool Name: `CCTV-KOTA`
- Default Gateway: `10.64.64.1`
- DNS Server: `8.8.8.8`
- Start IP Address: `10.64.64.10`
- Subnet Mask: `255.255.224.0`
- Maximum Number of Users: sesuaikan kebutuhan

Klik **Add** untuk menyimpan pool.

### 3. Konfigurasi Router R-DC

```text
enable
configure terminal

interface fastEthernet0/0.10
 encapsulation dot1Q 10
 ip address 10.64.64.1 255.255.224.0
 ip helper-address 10.64.238.2
exit

interface fastEthernet0/0.20
 encapsulation dot1Q 20
 ip address 10.64.238.1 255.255.255.0
exit

end
write memory
```

*Catatan: konfigurasi VLAN 10 dan VLAN 20 mengasumsikan VLAN tersebut sesuai dengan topologi.*

### 4. Pengujian DHCP

Pada PC CCTV-KOTA, buka **Desktop → IP Configuration → DHCP**.

Pastikan PC memperoleh alamat IP, subnet mask, gateway, dan DNS yang sesuai.

Uji koneksi melalui Command Prompt:

```text
ping 10.64.64.1
ping 10.64.238.2
```

---

## Soal 5 — NAT/PAT

**Tujuan:** Seluruh host internal dapat mengakses server publik `8.8.8.8` menggunakan satu IP publik milik R-PUSAT. R-ISP tidak boleh memiliki rute ke alamat privat internal.

### 1. Konfigurasi NAT pada R-PUSAT

Interface publik menuju R-ISP adalah `Serial0/1/1`, dengan IP `203.0.113.33`.

```text
enable
configure terminal

interface fastEthernet0/0
 ip nat inside
exit

interface fastEthernet0/1
 ip nat inside
exit

interface serial0/1/0
 ip nat inside
exit

interface serial0/2/0
 ip nat inside
exit

interface serial0/2/1
 ip nat inside
exit

interface serial0/3/0
 ip nat inside
exit

interface serial0/3/1
 ip nat inside
exit

interface serial0/1/1
 ip nat outside
exit

access-list 1 permit 10.64.0.0 0.0.255.255

ip nat inside source list 1 interface serial0/1/1 overload

end
write memory
```

Konfigurasi tersebut menggunakan PAT (*Port Address Translation*) dengan satu IP publik, yaitu IP pada `Serial0/1/1`.

Pastikan rute statis internal dan default route R-PUSAT yang sudah ada tidak dihapus.

Default route R-PUSAT:

```text
ip route 0.0.0.0 0.0.0.0 203.0.113.34
```

### 2. Pengujian NAT

Pada PC CCTV-KOTA, buka Command Prompt:

```text
ping 8.8.8.8
```

Jika muncul `Reply from 8.8.8.8`, koneksi berhasil.

Kemudian, pada CLI R-PUSAT, jalankan:

```text
show ip nat statistics
show ip nat translations
```

Contoh translasi NAT yang berhasil:

```text
Pro  Inside global     Inside local       Outside local  Outside global
icmp 203.0.113.33:24   10.64.64.10:24     8.8.8.8:24     8.8.8.8:24
```

Keterangan:

- **Inside local:** IP privat host internal.
- **Inside global:** IP publik yang digunakan untuk translasi.
- **Outside global:** IP server publik tujuan.

Nomor identifikasi ICMP dapat berbeda. Yang penting, IP privat `10.64.64.10` diterjemahkan menjadi IP publik `203.0.113.33`.

### 3. Verifikasi Routing R-ISP

Pada CLI R-ISP, jalankan:

```text
show ip route
```

Hasil yang telah diperiksa menunjukkan:

- `8.8.8.0/24` terhubung langsung melalui `FastEthernet0/0`.
- `203.0.113.32/30` terhubung langsung melalui `Serial0/3/0`.
- Tidak ada rute menuju jaringan privat internal `10.64.x.x`.

Dengan demikian, R-ISP tidak memiliki rute ke jaringan privat internal.

---

## Checklist Pengujian

- [ ] PC CCTV-KOTA mendapatkan IP melalui DHCP.
- [ ] PC dapat melakukan ping ke `10.64.64.1`.
- [ ] PC dapat melakukan ping ke `10.64.238.2`.
- [ ] PC dapat melakukan ping ke `8.8.8.8`.
- [ ] Translasi NAT menunjukkan `10.64.64.10` menjadi `203.0.113.33`.
- [ ] R-ISP tidak memiliki rute ke jaringan privat internal `10.64.x.x`.
