# Day 2: Temporary User Setup with Expiry

---

### Tahap 1: Login ke App Server 2
Melakukan remote login dari jump-host ke App Server 2 menggunakan protokol SSH.

```bash
ssh steve@stapp02
```
![images](/imgs_DevOps/day2.png)

---

### Tahap 2: Buat User dengan Expiry Date
Membuat user baru bernama `james` dengan tanggal expired akun.

```bash
sudo useradd -e 2027-02-17 james
```
![images](/imgs_DevOps/day2_1.png)

---

### Tahap 3: Verifikasi Hasil
Memverifikasi detail masa berlaku akun yang telah dibuat.

```bash
sudo chage -l james
```
![images](/imgs_DevOps/day2_2.png)

---