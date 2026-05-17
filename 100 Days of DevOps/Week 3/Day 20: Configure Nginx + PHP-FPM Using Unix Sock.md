# Day 20: Configure Nginx + PHP-FPM Using Unix Sock

---

## Step 1: Login ke App Server 1

```bash
ssh tony@stapp01
```

![images](/imgs_DevOps/day20.png)
---

## Step 2: Install Nginx

```bash
sudo dnf install -y nginx
```
![images](/imgs_DevOps/day20_1.png)
---

## Step 3: Install Repository Remi

```bash
sudo dnf install -y epel-release
sudo dnf install -y https://rpms.remirepo.net/enterprise/remi-release-9.rpm
```

![images](/imgs_DevOps/day20_2.png)
---

## Step 4: Enable PHP 8.3

```bash
sudo dnf module reset php -y
sudo dnf module enable php:remi-8.3 -y
```

![images](/imgs_DevOps/day20_3.png)
---

## Step 5: Install PHP 8.3 & PHP-FPM

```bash
sudo dnf install -y php php-fpm php-cli
```

![images](/imgs_DevOps/day20_4.png)
---

## Step 6: Buat Direktori Socket

```bash
sudo mkdir -p /var/run/php-fpm
```

![images](/imgs_DevOps/day20_5.png)
---

## Step 7: Konfigurasi PHP-FPM

```bash
sudo vi /etc/php-fpm.d/www.conf
```

Ubah baris berikut:

```ini
listen = /var/run/php-fpm/default.sock
listen.owner = nginx
listen.group = nginx
listen.mode = 0660
```

![images](/imgs_DevOps/day20_6.png)
---

## Step 8: Konfigurasi Nginx

```bash
sudo vi /etc/nginx/nginx.conf
```

Ubah blok `server` menjadi:

```nginx
server {
    listen       8096;
    listen       [::]:8096;
    server_name  stapp01;
    root         /var/www/html;
    index        index.php index.html;

    location / {
        try_files $uri $uri/ =404;
    }

    location ~ \.php$ {
        include fastcgi_params;
        fastcgi_intercept_errors on;
        fastcgi_pass unix:/var/run/php-fpm/default.sock;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
    }
}
```

![images](/imgs_DevOps/day20_7.png)
---

## Step 9: Atur Permission

```bash
sudo chown -R nginx:nginx /var/www/html
sudo chmod -R 755 /var/www/html
```

![images](/imgs_DevOps/day20_8.png)
---

## Step 10: Test Konfigurasi Nginx

```bash
sudo nginx -t
```

![images](/imgs_DevOps/day20_9.png)
---

## Step 11: Start & Enable Service

```bash
sudo systemctl enable --now php-fpm
sudo systemctl enable --now nginx
```

![images](/imgs_DevOps/day20_10.png)
---

## Step 12: Verifikasi Versi PHP-FPM

```bash
php-fpm -v
```

![images](/imgs_DevOps/day20_11.png)
> Pastikan output menunjukkan `PHP 8.3.x`.

---

## Step 14: Test dari Jump Host

```bash
curl http://stapp01:8096/index.php
```

![images](/imgs_DevOps/day20_12.png)
> ✅ Jika muncul output dari `index.php`, konfigurasi berhasil.