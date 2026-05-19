# Day 22: Configuring Secure SSH Access to an EC2 Instancea

---

## Bagian 1 — Buat Kunci SSH di Terminal aws-client

```bash
# Buat key pair RSA
ssh-keygen -t rsa -f /root/.ssh/id_rsa -N ""

# Tampilkan public key
cat /root/.ssh/id_rsa.pub
```
![images](/imgs_aws/day22.png)
![images](/imgs_aws/day22_1.png)

> Salin seluruh teks yang muncul (diawali `ssh-rsa`, diakhiri `root@aws-client`).

---

## Bagian 2 — Launch EC2 Instance

Buka **EC2** → **Launch instances**, isi konfigurasi berikut:

| Field           | Value                        |
|-----------------|------------------------------|
| Name            | `devops-ec2`                 |
| AMI             | Amazon Linux 2023 / 2        |
| Instance type   | `t2.micro`                   |
| Key pair        | Buat dummy key (misal `temp-key`) |
| Network / SSH   | Allow SSH traffic from **Anywhere** |

Klik **Launch instance** → tunggu status **Running**.

![images](/imgs_aws/day22_3.png)
---

## Bagian 3 — Masukkan Kunci ke Root EC2

**Connect ke instance:**
Centang `devops-ec2` → **Connect** → tab **EC2 Instance Connect** → **Connect**.

**Di terminal browser, jalankan:**

```bash
# Masuk sebagai root
sudo su -

# Masukkan public key (ganti teks di dalam tanda kutip)
echo "<PASTE_KUNCI_DI_SINI>" > /root/.ssh/authorized_keys

# Izinkan root login via SSH
sed -i 's/.*PermitRootLogin.*/PermitRootLogin yes/g' /etc/ssh/sshd_config

# Restart SSH service
systemctl restart sshd
```

![images](/imgs_aws/day22_4.png)
---

## Bagian 4 — Pengujian dari aws-client

Ambil **Private/Public IP** EC2 dari AWS Console, lalu SSH dari terminal lab:

```bash
ssh root@<IP_ADDRESS_EC2>
```

![images](/imgs_aws/day22_5.png)
> Jika muncul konfirmasi fingerprint, ketik `yes` lalu **Enter**.

> ✅ Jika berhasil masuk tanpa password, konfigurasi berhasil.