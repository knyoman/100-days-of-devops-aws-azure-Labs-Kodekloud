# Day 13: SSH into an Azure Virtual Machine

## 🖥️ TAHAP 1: Dapatkan IP Publik VM via Azure Portal (GUI)

- Buka browser, pergi ke https://portal.azure.com
- Login dengan kredensial:
  - Username: `kk_lab_user_main-8a160e98972a42dc@azurefreekmlprod.onmicrosoft.com`
  - Password: `vBP+$#$&`
- Di search bar atas, ketik "Virtual machines" → klik hasilnya
- Cari VM bernama **nautilus-vm** → klik namanya
- Di halaman Overview, lihat bagian "Public IP address" → catat IP-nya (contoh: 20.x.x.x)

![images](/imgs_azure/day13.png)

---

## 🔒 TAHAP 2: Pastikan Port 22 Terbuka (GUI - Azure Portal)

- Masih di halaman **nautilus-vm**
- Di menu kiri, klik **Networking** → **Network settings**
- Lihat **Inbound port rules** — pastikan ada rule untuk Port 22 (SSH)
- Jika belum ada, klik **Add inbound port rule**:
  - Source: Any
  - Destination port ranges: 22
  - Protocol: TCP
  - Action: Allow
  - Priority: 300
  - Name: Allow-SSH
  - Klik **Add**

  ![images](/imgs_azure/day13_1.png)

---

## 💻 TAHAP 3: Ambil Public Key dari Azure Client Host (Terminal)

- Buka terminal di Azure client host (landing host), lalu jalankan:

```bash
# Lihat isi public key root user
cat /root/.ssh/id_rsa.pub
```
- Salin seluruh output (dimulai dari `ssh-rsa AAAA...` hingga akhir baris).

![images](/imgs_azure/day13_2.png)

---

## 🔧 TAHAP 4: Copy Key + Fix Semua Konfigurasi Sekaligus

```bash
VM_IP="20.225.61.166"
PUB_KEY=$(cat /root/.ssh/id_rsa.pub)

ssh -o StrictHostKeyChecking=no azureuser@$VM_IP "sudo bash -c '
mkdir -p /root/.ssh
chmod 700 /root/.ssh
echo \"$PUB_KEY\" > /root/.ssh/authorized_keys
chmod 600 /root/.ssh/authorized_keys
chown -R root:root /root/.ssh
echo \"PermitRootLogin yes\" >> /etc/ssh/sshd_config
systemctl restart sshd
cat /root/.ssh/authorized_keys
'"
```

![images](/imgs_azure/day13_3.png)

---

## ✅ TAHAP 5: Test Koneksi Root

```bash
ssh -o StrictHostKeyChecking=no -i /root/.ssh/id_rsa root@20.225.61.166 "whoami"
```

![images](/imgs_azure/day13_4.png)

---