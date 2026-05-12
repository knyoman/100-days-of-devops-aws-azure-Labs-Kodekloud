# Day 16: Install and Configure Nginx as an LBR

**Tujuan:** Konfigurasi `stlb01` sebagai Load Balancer untuk mendistribusikan traffic ke 3 App Server (`stapp01`, `stapp02`, `stapp03`) yang menjalankan Apache.

---

## Step 1 — Cek Port Apache di App Server

```bash
ssh tony@stapp01 "grep -i 'Listen' /etc/httpd/conf/httpd.conf"
ssh steve@stapp02 "grep -i 'Listen' /etc/httpd/conf/httpd.conf"
ssh banner@stapp03 "grep -i 'Listen' /etc/httpd/conf/httpd.conf"
```

![images](/imgs_DevOps/day16.png)

> Salin  port contoh  **3003**.

---

## Step 2 — Pastikan Apache Aktif

```bash
ssh tony@stapp01
ssh steve@stapp02
ssh banner@stapp03
```

```bash
ssh tony@stapp01 "sudo systemctl status httpd"
ssh steve@stapp02 "sudo systemctl status httpd"
ssh banner@stapp03 "sudo systemctl status httpd"
```
![images](/imgs_DevOps/day16_1.png)

---

## Step 3 — Login ke LBR & Install Nginx

```bash
ssh loki@stlb01
sudo yum install nginx -y
```
![images](/imgs_DevOps/day16_2.png)

---

## Step 4 — Tulis Konfigurasi Nginx

```bash
sudo tee /etc/nginx/nginx.conf > /dev/null << 'EOF'
user nginx;
worker_processes auto;
error_log /var/log/nginx/error.log;
pid /run/nginx.pid;

include /usr/share/nginx/modules/*.conf;

events {
    worker_connections 1024;
}

http {
    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';

    access_log  /var/log/nginx/access.log  main;

    sendfile            on;
    tcp_nopush          on;
    tcp_nodelay         on;
    keepalive_timeout   65;
    types_hash_max_size 2048;

    include             /etc/nginx/mime.types;
    default_type        application/octet-stream;

    upstream nautilusapp {
        server stapp01:8080;
        server stapp02:8080;
        server stapp03:8080;
    }

    server {
        listen       80;
        server_name  stlb01;

        location / {
            proxy_pass http://nautilusapp;
        }
    }
}
EOF
```
![images](/imgs_DevOps/day16_3.png)

---

## Step 5 — Validasi & Jalankan Nginx

```bash
sudo nginx -t                  
sudo systemctl enable nginx
sudo systemctl start nginx
sudo systemctl status nginx
```
![images](/imgs_DevOps/day16_4.png)

---

## Step 6 — Test Load Balancer

```bash
curl http://stlb01:80
```

![images](/imgs_DevOps/day16_5.png)

> ✅ Jika muncul respons dari salah satu App Server, Load Balancer berhasil.