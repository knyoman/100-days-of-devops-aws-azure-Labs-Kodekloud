# Day 13: IPtables Installation And Configuration
 
> **Tujuan:** Mengamankan Apache port `3003` di semua App Server agar hanya dapat diakses oleh Load Balancer (stlb01).
 
---
 
## 📋 Topologi Infrastruktur
 
| Host | Hostname | IP Statis | User Login |
|------|----------|-----------|------------|
| App Server 1 | stapp01 | 172.16.238.10 | tony |
| App Server 2 | stapp02 | 172.16.238.11 | steve |
| App Server 3 | stapp03 | 172.16.238.12 | banner |
| Load Balancer | stlb01 | 172.16.238.14 | loki |
| Jump Host | thor | — | thor |
 
---
 
## ⚠️ Persiapan: Verifikasi IP Asli LBR
 
> **Pelajaran penting:** IP yang digunakan stlb01 saat menghubungi app server bisa berbeda dari IP statis. Selalu verifikasi terlebih dahulu!
 
```bash
# SSH ke LBR dari jump host
ssh loki@stlb01
 
# Cek IP asli yang aktif
hostname -I
 
# Cek interface dan IP yang digunakan untuk menghubungi app server
ip route get <IP_appserver>
```
 
📝 Catat IP hasil `hostname -I` — IP inilah yang digunakan pada rule iptables di setiap app server.
 
---
 
## 🛠️ Konfigurasi App Server
 
Lakukan langkah berikut secara berurutan di **masing-masing app server**.
 
### Masuk ke Server
 
```bash
# App Server 1
ssh tony@stapp01
 
# App Server 2
ssh steve@stapp02
 
# App Server 3
ssh banner@stapp03
```
 
### Masuk sebagai Root
 
```bash
sudo su -
```
 
> ❗ Semua perintah iptables memerlukan akses root. Tanpa `sudo su -` akan muncul error `Permission denied`.
 
---
 
### Step 1 — Install IPTables dan Dependensinya
 
```bash
yum install -y iptables iptables-services
```
 
---
 
### Step 2 — Enable dan Start Service IPTables
 
```bash
# Aktifkan agar berjalan otomatis saat reboot
systemctl enable iptables
 
# Jalankan service
systemctl start iptables
 
# Verifikasi status
systemctl status iptables
```
 
Output yang diharapkan:
```
Active: active (exited) ...
iptables: Applying firewall rules: [  OK  ]
```
 
---
 
### Step 3 — Hapus Rule Lama (Jika Ada yang Salah)
 
```bash
# Lihat semua rule yang ada
iptables -L INPUT --line-numbers -v -n
 
# Hapus rule ACCEPT lama jika menggunakan IP yang salah
# Ganti angka sesuai nomor baris rule tersebut
iptables -D INPUT 1
```
 
---
 
### Step 4 — Tambahkan Rule Baru
 
```bash
# Blokir SEMUA incoming traffic ke port 3003
iptables -A INPUT -p tcp --dport 3003 -j DROP
 
# Izinkan HANYA LBR mengakses port 3003
# Ganti <IP_ASLI_stlb01> dengan hasil hostname -I dari stlb01
iptables -I INPUT 1 -p tcp --dport 3003 -s <IP_ASLI_stlb01> -j ACCEPT
```
 
> 💡 **Mengapa `-I` bukan `-A`?**
> - `-I` = **Insert** → menyisipkan rule di posisi tertentu (atas)
> - `-A` = **Append** → menambahkan rule di paling bawah
>
> Rule ACCEPT **harus berada di atas** rule DROP karena iptables membaca dari atas ke bawah — rule pertama yang cocok langsung dieksekusi.
 
---
 
### Step 5 — Verifikasi Urutan Rules
 
```bash
iptables -L INPUT --line-numbers -v -n
```
 
Output yang benar:
 
```
Chain INPUT (policy ACCEPT)
num   pkts  target   prot  source              destination
1        0  ACCEPT   tcp   <IP_stlb01>         anywhere     tcp dpt:3003
2      ...  ACCEPT   all   0.0.0.0/0           0.0.0.0/0    state RELATED,ESTABLISHED
3        0  ACCEPT   icmp  0.0.0.0/0           0.0.0.0/0
4        0  ACCEPT   all   lo                  0.0.0.0/0
5        0  ACCEPT   tcp   0.0.0.0/0           0.0.0.0/0    state NEW tcp dpt:22
6        0  REJECT   all   0.0.0.0/0           0.0.0.0/0    reject-with icmp-host-prohibited
7        0  DROP     tcp   0.0.0.0/0           0.0.0.0/0    tcp dpt:3003
```
 
✅ Rule ACCEPT (LBR) → **nomor 1, paling atas**
✅ Rule DROP → **di bawah REJECT/ACCEPT**
 
---
 
### Step 6 — Simpan Rules agar Permanen (Survive Reboot)
 
```bash
# Simpan rules ke file konfigurasi
service iptables save
 
# Verifikasi file tersimpan
cat /etc/sysconfig/iptables
```
 
Output `/etc/sysconfig/iptables` yang benar:
 
```
*filter
:INPUT ACCEPT [0:0]
:FORWARD ACCEPT [0:0]
:OUTPUT ACCEPT [0:0]
-A INPUT -s <IP_stlb01>/32 -p tcp -m tcp --dport 3003 -j ACCEPT
-A INPUT -m state --state RELATED,ESTABLISHED -j ACCEPT
-A INPUT -p icmp -j ACCEPT
-A INPUT -i lo -j ACCEPT
-A INPUT -p tcp -m state --state NEW -m tcp --dport 22 -j ACCEPT
-A INPUT -j REJECT --reject-with icmp-host-prohibited
-A INPUT -p tcp -m tcp --dport 3003 -j DROP
COMMIT
```
 
---
 
## ✅ Verifikasi Akhir
 
### Dari stlb01 — Harus BERHASIL ✅
 
```bash
ssh loki@stlb01
 
curl -v http://stapp01:3003
curl -v http://stapp02:3003
curl -v http://stapp03:3003
```
 
Respons yang diharapkan: koneksi berhasil / data Apache diterima.
 
---
 
### Dari Jump Host — Harus GAGAL ❌
 
```bash
curl -v http://stapp01:3003
curl -v http://stapp02:3003
curl -v http://stapp03:3003
```
 
Respons yang diharapkan:
```
curl: (7) Failed to connect to stappXX port 3003: No route to host
```
 
## 📊 Diagram Alur Akses Akhir
 
```
                    ┌─────────────────┐
                    │  Jump Host      │
                    │  (thor)         │
                    └────────┬────────┘
                             │
              ┌──────────────┴──────────────┐
              │                             │
              ▼                             ▼
   ┌──────────────────┐         ┌────────────────────┐
   │  stlb01 (LBR)   │         │  Direct Access     │
   │  <IP_asli>       │         │  dari luar LBR     │
   └────────┬─────────┘         └──────────┬─────────┘
            │                              │
            ▼                              ▼
   Port 3003 → ✅ ACCEPT         Port 3003 → ❌ DROP/REJECT
            │
            ├──► stapp01:3003  ✅
            ├──► stapp02:3003  ✅
            └──► stapp03:3003  ✅
```
 
---