# Day 15: Setup SSL for Nginx

---

## Tahap 1  Instalasi Nginx

Masuk ke App Server 1, lalu instal Nginx.

```bash
ssh tony@stapp01
sudo yum install nginx -y
```
![images](/imgs_DevOps/day15.png)
![images](/imgs_DevOps/day15_1.png)

---

## Tahap 2  Siapkan Sertifikat & Document Root

Pindahkan sertifikat ke direktori standar PKI, lalu buat halaman default.

```bash
# Pindahkan sertifikat
sudo mv /tmp/nautilus.crt /etc/pki/tls/certs/
sudo mv /tmp/nautilus.key /etc/pki/tls/private/

# Buat index.html
echo "Welcome!" | sudo tee /usr/share/nginx/html/index.html
```
![images](/imgs_DevOps/day15_2.png)
![images](/imgs_DevOps/day15_3.png)

---

## Tahap 3  Konfigurasi SSL Nginx

Edit file konfigurasi utama Nginx.

```bash
sudo vi /etc/nginx/nginx.conf
```

Tambahkan atau sesuaikan blok `server` berikut:

```nginx
server {
    listen       443 ssl;
    listen       [::]:443 ssl;
    server_name  stapp01;

    ssl_certificate     "/etc/pki/tls/certs/nautilus.crt";
    ssl_certificate_key "/etc/pki/tls/private/nautilus.key";

    root /usr/share/nginx/html;

    location / {
    }
}
```

> ⚠️ Pastikan tidak ada blok `server` lain yang bentrok di port 443.

---

## Tahap 4  Jalankan Layanan

Test konfigurasi, lalu aktifkan Nginx.

```bash
sudo nginx -t
sudo systemctl enable nginx
sudo systemctl start nginx
```
![images](/imgs_DevOps/day15_4.png)
![images](/imgs_DevOps/day15_5.png)

---

## Tahap 5  Verifikasi dari Jump Host

Keluar dari App Server 1, lalu jalankan curl untuk memverifikasi.

```bash
exit
curl -Ik https://stapp01/
```
![images](/imgs_DevOps/day15_6.png)

> ✅ Jika muncul respons header HTTPS dengan status `200`, konfigurasi berhasil.