# Day 12: Linux Network Services
 
> **Masalah:** Apache gagal berjalan karena port `3004` sudah digunakan layanan lain (sendmail).
> **Tujuan:** Menyelesaikan konflik port, menjalankan Apache, dan memastikan firewall dikonfigurasi dengan benar.
 
---
 
## 📋 Ringkasan Masalah
 
| Item | Detail |
|------|--------|
| Server | stapp01 |
| Service bermasalah | Apache (`httpd`) |
| Port konflik | `3004` |
| Penyebab | Sendmail memakai port yang sama |
| Solusi | Pindahkan sendmail ke port `2525` |
 
---
 
## Tahap 1 — Identifikasi Masalah
 
### Masuk ke App Server
 
```bash
ssh tony@stapp01
```
 
### Cek Status Apache
 
```bash
sudo systemctl status httpd
```
 
**Hasil:**
 
```
● httpd.service - The Apache HTTP Server
   Active: failed
   ...
   (98) Address already in use: AH00072: make_sock: could not bind to address 0.0.0.0:3004
```
 
> ❗ Error `(98) Address already in use` menandakan port `3004` sudah dipakai oleh proses lain sehingga Apache tidak bisa bind ke port tersebut.
 
---
 
## Tahap 2 — Menyelesaikan Konflik Port
 
### Cari Layanan yang Memakai Port 3004
 
```bash
sudo ss -tlnp | grep 3004
```
 
**Hasil:**
 
```
LISTEN  0  128  0.0.0.0:3004  0.0.0.0:*  users:(("sendmail", pid=XXXX, fd=X))
```
 
> 🔍 Diketahui: **sendmail** menggunakan port `3004`.
 
---
 
### Edit Konfigurasi Sendmail
 
```bash
sudo vi /etc/mail/sendmail.mc
```
 
Cari baris yang berisi `Port=3004` lalu ubah ke port lain:
 
```text
# Sebelum
Port=3004
 
# Sesudah
Port=2525
```
 
Simpan file: tekan `Esc` → ketik `:wq` → tekan `Enter`
 
---
 
### Terapkan Perubahan Sendmail
 
```bash
sudo systemctl restart sendmail
```
 
### Verifikasi Sendmail Sudah Pindah Port
 
```bash
sudo ss -tlnp | grep 3004
```
 
> ✅ Tidak ada output → port `3004` sudah bebas.
 
```bash
sudo ss -tlnp | grep 2525
```
 
> ✅ Sendmail kini berjalan di port `2525`.
 
---
 
## Tahap 3 — Menjalankan Apache
 
### Start Apache
 
```bash
sudo systemctl start httpd
```
 
### Verifikasi Status Apache
 
```bash
sudo systemctl status httpd
```
 
**Hasil yang diharapkan:**
 
```
● httpd.service - The Apache HTTP Server
   Active: active (running)
   ...
```
 
> ✅ Apache berhasil berjalan di port `3004`.
 
### (Opsional) Enable Apache agar Otomatis Berjalan saat Reboot
 
```bash
sudo systemctl enable httpd
```
 
---
 
## Tahap 4 — Konfigurasi Firewall (IPTables)
 
### Cek Rules Firewall yang Ada
 
```bash
sudo iptables -L INPUT -n --line-numbers
```
 
### Izinkan Port 3004 di Posisi Paling Atas
 
```bash
sudo iptables -I INPUT 1 -p tcp --dport 3004 -j ACCEPT
```
 
> 💡 Menggunakan `-I INPUT 1` agar rule ACCEPT disisipkan di **baris paling atas**, sehingga dibaca pertama kali sebelum rule DROP/REJECT lainnya.
 
### Verifikasi Rule Sudah Masuk
 
```bash
sudo iptables -L INPUT -n --line-numbers
```
 
**Output yang diharapkan:**
 
```
Chain INPUT (policy ACCEPT)
num  target  prot  source     destination
1    ACCEPT  tcp   0.0.0.0/0  0.0.0.0/0   tcp dpt:3004
...
```
 
### Simpan Rule agar Permanen
 
```bash
sudo service iptables save
```
 
---
 
## Tahap 5 — Verifikasi Akhir
 
### Test Lokal di stapp01
 
```bash
curl http://localhost:3004
```
 
**Hasil yang diharapkan:** Halaman HTML dari Apache tampil.
 
---
 
### Test dari Jump Host
 
```bash
# Keluar dari stapp01 terlebih dahulu
exit
 
# Test dari jump host
curl http://stapp01:3004
```
 
**Hasil yang diharapkan:** Koneksi berhasil dan menampilkan halaman Apache.
 
---
 
## 📊 Diagram Alur Troubleshooting
 
```
Apache gagal start
        │
        ▼
systemctl status httpd
        │
        └──► Error: port 3004 "Address already in use"
                        │
                        ▼
              ss -tlnp | grep 3004
                        │
                        └──► Sendmail pakai port 3004
                                        │
                                        ▼
                             Edit /etc/mail/sendmail.mc
                             Ganti Port=3004 → Port=2525
                                        │
                                        ▼
                             systemctl restart sendmail
                                        │
                                        ▼
                             systemctl start httpd
                                        │
                                        ▼
                             iptables -I INPUT 1 (port 3004 ACCEPT)
                                        │
                                        ▼
                             curl localhost:3004 ✅
```
 
---