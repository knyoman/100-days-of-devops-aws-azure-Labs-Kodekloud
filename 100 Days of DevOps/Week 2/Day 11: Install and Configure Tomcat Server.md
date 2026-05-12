# 🚀 Panduan Deploy Tomcat - App Server 2 (Port 8088)

> **Task:** Install Tomcat di App Server 2, konfigurasi port `8088`, dan deploy `ROOT.war`

---

## Prasyarat

| Item | Detail |
|------|--------|
| **Server** | App Server 2 (`stapp02`) |
| **User** | `steve` / Password: `Am3ric@` |
| **Port** | `8088` |
| **File WAR** | `/tmp/ROOT.war` (di Jump Host) |

---

## Step 1: Copy ROOT.war ke App Server 2

Di **Jump Host**, jalankan perintah berikut:

```bash
scp /tmp/ROOT.war steve@stapp02:/tmp/
```
![images](/imgs_DevOps/day11.png)

> 🔑 Password: `Am3ric@`

---

## Step 2: SSH ke App Server 2

```bash
ssh steve@stapp02
```
![images](/imgs_DevOps/day11_1.png)

Masuk ke root:

```bash
sudo su -
```
![images](/imgs_DevOps/day11_2.png)

---

## Step 3: Install Java

```bash
yum install -y java-11-openjdk java-11-openjdk-devel
```
![images](/imgs_DevOps/day11_3.png)

Verifikasi instalasi:

```bash
java -version
```
![images](/imgs_DevOps/day11_4.png)

---

## Step 4: Download & Install Tomcat

```bash
# Pergi ke direktori /opt
cd /opt

# Download Tomcat versi 9.x
wget https://archive.apache.org/dist/tomcat/tomcat-9/v9.0.65/bin/apache-tomcat-9.0.65.tar.gz

# Extract file
tar -xvzf apache-tomcat-9.0.65.tar.gz

# Rename direktori
mv apache-tomcat-9.0.65 tomcat
```
![images](/imgs_DevOps/day11_5.png)

---

## Step 5: Ubah Port ke 8088

Edit file konfigurasi `server.xml`:

```bash
vi /opt/tomcat/conf/server.xml
```

Cari baris berikut:

```xml
<Connector port="8080" protocol="HTTP/1.1"
```

Ubah menjadi:

```xml
<Connector port="8088" protocol="HTTP/1.1"
```
![images](/imgs_DevOps/day11_6.png)

> 💾 Simpan file: tekan `ESC` → ketik `:wq` → Enter

---

## Step 6: Deploy ROOT.war

```bash
# Hapus ROOT lama jika ada
rm -rf /opt/tomcat/webapps/ROOT
rm -f /opt/tomcat/webapps/ROOT.war

# Copy ROOT.war ke direktori webapps
cp /tmp/ROOT.war /opt/tomcat/webapps/ROOT.war
```
![images](/imgs_DevOps/day11_7.png)

> ⚠️ Nama file harus **`ROOT.war`** (huruf kapital) agar aplikasi tersedia di base URL `/`

---

## Step 7: Buat Tomcat sebagai Service (systemd)

```bash
vi /etc/systemd/system/tomcat.service
```


Isi dengan konfigurasi berikut:

```ini
[Unit]
Description=Apache Tomcat
After=network.target

[Service]
Type=forking
ExecStart=/opt/tomcat/bin/startup.sh
ExecStop=/opt/tomcat/bin/shutdown.sh
Restart=always

[Install]
WantedBy=multi-user.target
```

Aktifkan dan jalankan service:

```bash
systemctl daemon-reload
systemctl enable tomcat
systemctl start tomcat
```

---

## Step 8: Buka Port Firewall (jika diperlukan)

```bash
firewall-cmd --permanent --add-port=8088/tcp
firewall-cmd --reload
```

> ℹ️ Jika `firewall-cmd: command not found`, lewati langkah ini — tidak ada firewall yang aktif.

---

## Step 9: Verifikasi Deployment

Tunggu 15-20 detik, lalu jalankan:

```bash
curl http://stapp02:8088
```

![images](/imgs_DevOps/day11_13.png)
