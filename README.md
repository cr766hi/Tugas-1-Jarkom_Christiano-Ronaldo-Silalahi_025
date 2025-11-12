# Tugas-1-Jarkom_Christiano-Ronaldo-Silalahi_025

# 📝 Dokumentasi Tugas 1 Jaringan Komputer: Implementasi VLSM dan CIDR

## 1. Pendahuluan

Dokumen ini berisi perhitungan dan implementasi jaringan komputer untuk Yayasan Pendidikan ARA. Perancangan dilakukan menggunakan metode **VLSM** (Variable Length Subnet Mask) untuk efisiensi alokasi IP dan **CIDR** (Classless Inter-Domain Routing) untuk efisiensi *routing* antar kantor pusat dan kantor cabang.

### Base Network Unik

* **Aturan Perhitungan:** $\text{10.(NRP mod 256).0.0}$
* **Base Network:** $\mathbf{10.65.0.0}$

---

## 2. Topologi Jaringan (Cisco Packet Tracer)

Topologi dirancang menggunakan arsitektur Router Pusat ($\text{Router0}$) yang terhubung langsung ke *Edge Router* ($\text{Router2}$ - $\text{Router6}$) untuk setiap segmen LAN Kantor Pusat, serta terhubung ke $\text{Router1}$ (Kantor Cabang) melalui Link WAN Serial.

* **Bobot Penilaian Kriteria 2 (Desain Topologi):** 15%

### Screenshot Topologi Final

*Pastikan label Network ID, Prefix, dan IP Address Interface terlihat jelas.*

```markdown
![Topologi Jaringan Final](link_gambar_topologi_anda.png)
