# Day 14: Linux Process Troubleshooting - Apache Port Conflict

## Langkah 1: Login & Identifikasi Awal

- Login ke App Server 1 dari Jump Host:

```bash
ssh tony@stapp01
```

- Cek status layanan Apache:

```bash
sudo systemctl status httpd
```

- Analisis Log: Status menunjukkan `failed` dengan pesan error:
  ```
  (98) Address already in use: could not bind to address 0.0.0.0:8087
  ```
  Ini artinya port `8087` sudah diduduki proses lain.

![images](/imgs_DevOps/day14.png)

---

## Langkah 2: Investigasi Konflik Port

- Cari tahu proses yang menduduki port `8087`:

```bash
sudo ss -tlnp | grep 8087
```
![images](/imgs_DevOps/day14_2.png)

- Hasil: Ditemukan bahwa port `8087` sedang digunakan oleh layanan **sendmail** (PID 12655).

---

## Langkah 3: Konfigurasi Ulang Layanan Pengganggu (Sendmail)

- Agar port `8087` bisa digunakan oleh Apache, harus memindahkan port sendmail:

```bash
sudo nano /etc/mail/sendmail.mc
```

- Ubah port sendmail dari `8087` ke port alternatif agar tidak bentrok.

- Terapkan perubahan:

```bash
sudo systemctl restart sendmail
```
![images](/imgs_DevOps/day14_3.png)

---

## Langkah 4: Konfigurasi & Aktivasi Apache (httpd)

- Pastikan Apache dikonfigurasi di port `8087`:

```bash
sudo nano /etc/httpd/conf/httpd.conf
```

- Memastikan baris `Listen 8087` sudah benar.

- Jalankan layanan Apache:

```bash
sudo systemctl start httpd
```

- Aktifkan Apache agar otomatis jalan saat reboot:

```bash
sudo systemctl enable httpd
```
![images](/imgs_DevOps/day14_4.png)

---

## Langkah 5: Verifikasi Akhir

- Cek kembali port `8087`:

```bash
sudo ss -tlnp | grep 8087
```
![images](/imgs_DevOps/day14_5.png)

- Hasil: Sekarang yang muncul adalah proses **httpd** (Apache), bukan lagi sendmail.

- Cek status layanan:

```bash
sudo systemctl status httpd
```
![images](/imgs_DevOps/day14_6.png)

- Hasil: Status sudah `active (running)`.