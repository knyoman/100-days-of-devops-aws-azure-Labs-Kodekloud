# Day 19: Install and Configure Web Application 


## Langkah 1: Copy File Website dari Jump Host ke App Server 3

```bash
scp -r /home/thor/news banner@stapp03:/tmp/
scp -r /home/thor/games banner@stapp03:/tmp/
```
![images](/imgs_DevOps/day19.png)

> Menyalin folder `news` dan `games` dari jump host ke server `stapp03`, lalu menyimpannya di direktori sementara `/tmp`.
---

## Langkah 2: SSH ke App Server 3

```bash
ssh banner@stapp03
```

![images](/imgs_DevOps/day19_1.png)
> Masuk ke server `stapp03` menggunakan user `banner`.
---

## Langkah 3: Install Apache (`httpd`)

```bash
sudo yum install -y httpd
```

![images](/imgs_DevOps/day19_2.png)
> Menginstal web server Apache agar server dapat melayani website.
---

## Langkah 4: Ubah Port Apache ke 8083

```bash
sudo vi /etc/httpd/conf/httpd.conf
```

Ubah:

```apache
Listen 80
```

Menjadi:

```apache
Listen 8083
```

![images](/imgs_DevOps/day19_3.png)
> Mengubah port default Apache dari 80 ke 8083 sesuai kebutuhan task.
---

## Langkah 5: Buat Direktori Website

```bash
sudo mkdir -p /var/www/html/news
sudo mkdir -p /var/www/html/games
```

![images](/imgs_DevOps/day19_4.png)
> Membuat folder tujuan untuk menyimpan file website `news` dan `games`.
---

## Langkah 6: Copy File Website ke Direktori Apache

```bash
sudo cp -r /tmp/news/* /var/www/html/news/
sudo cp -r /tmp/games/* /var/www/html/games/
```

![images](/imgs_DevOps/day19_5.png)
> Memindahkan file website dari `/tmp` ke folder yang akan dibaca oleh Apache.
---

## Langkah 7: Set Permission dan Ownership

```bash
sudo chown -R apache:apache /var/www/html/news
sudo chown -R apache:apache /var/www/html/games
sudo chmod -R 755 /var/www/html/news
sudo chmod -R 755 /var/www/html/games
```

![images](/imgs_DevOps/day19_6.png)
> Memberikan hak kepemilikan kepada user Apache dan memastikan file dapat dibaca oleh web server.
---

## Langkah 8: Buat Konfigurasi Alias Website

```bash
sudo vi /etc/httpd/conf.d/websites.conf
```

Isi file:

```apache
<VirtualHost *:8083>
    DocumentRoot /var/www/html
    ServerName localhost

    Alias /news /var/www/html/news
    Alias /games /var/www/html/games

    <Directory /var/www/html/news>
        Options Indexes FollowSymLinks
        AllowOverride None
        Require all granted
    </Directory>

    <Directory /var/www/html/games>
        Options Indexes FollowSymLinks
        AllowOverride None
        Require all granted
    </Directory>
</VirtualHost>
```

![images](/imgs_DevOps/day19_7.png)
> Membuat URL `/news` dan `/games` mengarah ke folder website masing-masing.
---

## Langkah 9: Test Konfigurasi Apache

```bash
sudo apachectl configtest
```


> Memastikan konfigurasi Apache tidak mengandung kesalahan sintaks.
---

## Langkah 10: Start dan Enable Apache

```bash
sudo systemctl start httpd
sudo systemctl enable httpd
sudo systemctl status httpd
```

![images](/imgs_DevOps/day19_8.png)
> Menjalankan Apache, mengaktifkannya saat boot, dan memeriksa status layanan.
---

## Langkah 11: Verifikasi Website

```bash
curl http://localhost:8083/news/
curl http://localhost:8083/games/
```
![images](/imgs_DevOps/day19_9.png)
![images](/imgs_DevOps/day19_10.png)
> Menguji apakah kedua website dapat diakses melalui port 8083.
---

# Troubleshooting

## Melihat Error Log Apache

```bash
sudo tail -f /var/log/httpd/error_log
```

![images](/imgs_DevOps/day19_11.png)
> Menampilkan log error Apache secara real-time.
---

## Memeriksa Port 8083

```bash
sudo lsof -i :8083
```

![images](/imgs_DevOps/day19_12.png)
> Memastikan Apache sedang mendengarkan pada port 8083.
---

## Memeriksa seluruh file konfigurasi Apache

```bash
sudo apachectl configtest
```

![images](/imgs_DevOps/day19_13.png)
> Syntax OK, Apache berjalan dengan sempurna tanpa kendala teknis pada konfigurasi
---

