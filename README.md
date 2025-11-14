# Tugas-1-Jarkom_Christiano-Ronaldo-Silalahi_025

Dokumentasi Tugas 1 Jaringan Komputer: Implementasi VLSM dan CIDR

## 1. Pendahuluan dan Deskripsi Tugas

Dokumen ini berisi perhitungan dan implementasi jaringan komputer untuk Yayasan Pendidikan ARA. Perancangan dilakukan menggunakan metode **VLSM** (Variable Length Subnet Mask) untuk efisiensi alokasi IP dan **CIDR** (Classless Inter-Domain Routing) untuk efisiensi *routing* antar kantor pusat dan kantor cabang.

### Deskripsi Tugas Singkat

Tugas ini mengharuskan perancangan jaringan dengan kriteria:
1.  **Topologi:** Menggunakan Cisco Packet Tracer untuk merancang topologi yang menghubungkan Kantor Pusat dan Kantor Cabang.
2.  **Base Network:** Menggunakan Base Network unik berdasarkan NRP: $\mathbf{10.65.0.0}$.
3.  **Perhitungan:** Melakukan perhitungan **VLSM** dan **CIDR** untuk seluruh jaringan LAN dan *link* antar-router.
4.  **Implementasi:** Mengkonfigurasi alamat IP dan *routing* di CPT sesuai hasil perhitungan.

### Kebutuhan Host (Kantor Pusat dan Kantor Cabang)

Berikut adalah daftar kebutuhan host yang menjadi dasar perhitungan VLSM:

| Ruang | Jumlah Host Aktif |
| :--- | :--- |
| **Sekretariat** | 380 host |
| **Bidang Kurikulum** | 220 host |
| **Bidang Guru & Tendik** | 95 host |
| **Bidang Sarana Prasarana** | 45 host |
| **Bidang Pengawas Sekolah (Cabang)** | 18 host |
| **Server & Admin** | 6 host |

### Base Network Unik

* **Aturan Perhitungan:** $\text{10.(NRP mod 256).0.0}$
* **Base Network:** $\mathbf{10.65.0.0}$

---

## 2. Topologi Jaringan (Cisco Packet Tracer)

Topologi dirancang menggunakan arsitektur Router Pusat ($\text{Router0}$) yang terhubung langsung ke *Edge Router* ($\text{Router2}$ - $\text{Router6}$) untuk setiap segmen LAN Kantor Pusat, serta terhubung ke $\text{Router1}$ (Kantor Cabang) melalui Link WAN Serial.


### Screenshot Topologi Final


![WhatsApp Image 2025-11-12 at 22 15 35_3d400769](https://github.com/user-attachments/assets/ae043d28-ba34-468d-91a2-7b6998149d35)

## 3. Hasil Perhitungan VLSM Lengkap

![VLSM](https://github.com/user-attachments/assets/eb5f378d-8531-4c68-a36a-8811a5f6fd92)


Tabel ini mencakup semua jaringan LAN dan Link WAN, serta detail IP Address lengkap yang diperlukan untuk konfigurasi di Cisco Packet Tracer.

| Ruang | Kebutuhan Host | Network Address | Prefix | Subnet Mask | Range Host | Broadcast Address | Gateway (First Host) |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **Sekretariat** | 380 | `10.65.0.0` | `/23` | `255.255.254.0` | `10.65.0.1 - 10.65.1.254` | `10.65.1.255` | `10.65.0.1` |
| **Bidang Kurikulum** | 220 | `10.65.2.0` | `/24` | `255.255.255.0` | `10.65.2.1 - 10.65.2.254` | `10.65.2.255` | `10.65.2.1` |
| **Bidang Guru & Tendik** | 95 | `10.65.3.0` | `/25` | `255.255.255.128` | `10.65.3.1 - 10.65.3.126` | `10.65.3.127` | `10.65.3.1` |
| **Bidang Sarana Prasarana** | 45 | `10.65.3.128` | `/26` | `255.255.255.192` | `10.65.3.129 - 10.65.3.190` | `10.65.3.191` | `10.65.3.129` |
| **B. Pengawas Sek. (Cabang)** | 18 | `10.65.3.192` | `/27` | `255.255.255.224` | `10.65.3.193 - 10.65.3.222` | `10.65.3.223` | `10.65.3.193` |
| **Server & Admin** | 6 | `10.65.3.224` | `/29` | `255.255.255.248` | `10.65.3.225 - 10.65.3.230` | `10.65.3.231` | `10.65.3.225` |
| **Link WAN 1** | 2 | `10.65.3.232` | `/30` | `255.255.255.252` | `10.65.3.233 - 10.65.3.234` | `10.65.3.235` | `10.65.3.233` |

---

## 4. Hasil Perhitungan CIDR Lengkap

![Agregrasi](https://github.com/user-attachments/assets/dfa92381-c1a8-4c2f-8521-27d007fcd827)


### 4.1 Tabel Hasil CIDR Lengkap

Tabel ini menyajikan ringkasan final dari hasil agregasi rute (**Supernetting**) untuk seluruh jaringan Kantor Pusat, menggunakan prefix terpendek **`/22`**.

| Kriteria | Network Address | Prefix | Subnet Mask | Range Host | Broadcast Address | Gateway |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **CIDR (Agregasi Kantor Pusat)** | `10.65.0.0` | `/22` | `255.255.252.0` | `10.65.0.1 - 10.65.3.254` | `10.65.3.255` | N/A (Rute Agregat) |

### 4.2 Visualisasi Supernetting (Agregasi)

Tabel ini menunjukkan proses bertahap bagaimana subnet-subnet VLSM digabungkan menjadi rute CIDR final `/22`.

#### Tahap 1: Agregasi Parsial (Blok `10.65.3.x`)

| Nama Blok (Anggota) | NID (Network Address) | Broadcast Address | Prefix |
| :--- | :--- | :--- | :--- |
| **Bidang Guru & Tendik** | `10.65.3.0` | `10.65.3.127` | `/25` |
| **Bidang Sarana Prasarana** | `10.65.3.128` | `10.65.3.191` | `/26` |
| **Server & Admin** | `10.65.3.224` | `10.65.3.231` | `/29` |
| **Agregasi 1 (Blok 3)** | $\mathbf{10.65.3.0}$ | $\mathbf{10.65.3.255}$ | $\mathbf{/24}$ |

#### Tahap 2: Agregasi Total (Kantor Pusat)

| Nama Blok (Anggota) | NID (Network Address) | Broadcast Address | Prefix |
| :--- | :--- | :--- | :--- |
| **Sekretariat** | `10.65.0.0` | `10.65.1.255` | `/23` |
| **Bidang Kurikulum** | `10.65.2.0` | `10.65.2.255` | `/24` |
| **Agregasi 1 (Blok 3)** | `10.65.3.0` | `10.65.3.255` | `/24` |
| **Hasil Agregasi Total (CIDR)** | $\mathbf{10.65.0.0}$ | $\mathbf{10.65.3.255}$ | $\mathbf{/22}$ |

#### Tahap 3: Agregasi Jaringan Total (Pusat & Cabang)

| Anggota Jaringan | NID (Network Address) | Broadcast Address | Prefix | Keterangan |
| :--- | :--- | :--- | :--- | :--- |
| **Blok 1 (Sekretariat)** | `10.65.0.0` | `10.65.1.255` | `/23` | Rangkuman Jaringan Sekretariat |
| **Blok 2 (Kurikulum)** | `10.65.2.0` | `10.65.2.255` | `/24` | Jaringan Kurikulum |
| **Blok 3 (Lainnya/Agregasi)** | `10.65.3.0` | `10.65.3.255` | `/24` | Mencakup semua sub-jaringan .3.x (Termasuk Cabang) |
| **Hasil Agregasi Total (CIDR)** | **`10.65.0.0`** | **`10.65.3.255`** | **`/22`** | Rute Ringkasan (Summary Route) |

## 5. Visualisasi Struktur Jaringan VLSM dan CIDR

Visualisasi ini menunjukkan hierarki subnetting (VLSM) dan penggabungan (CIDR) di bawah alokasi total **10.65.0.0/22**.

```text
10.65.0.0/22 (Total Alokasi Kantor Pusat)
├── 10.65.0.0/23 (Sekretariat)
│   ├── Network: 10.65.0.0
│   └── Broadcast: 10.65.1.255
│
├── 10.65.2.0/24 (Bidang Kurikulum)
│   ├── Network: 10.65.2.0
│   └── Broadcast: 10.65.2.255
│
└── 10.65.3.0/24 (Agregasi Subnet Blok 3)
    ├── Network: 10.65.3.0
    └── Broadcast: 10.65.3.255
        │
        ├── 10.65.3.0/25     (Bidang Guru & Tendik)
        ├── 10.65.3.128/26  (Bidang Sarana Prasarana)
        ├── 10.65.3.192/27  (B. Pengawas Sekolah - Cabang)
        ├── 10.65.3.224/29  (Server & Admin)
        ├── 10.65.3.232/30  (Link WAN 1)
