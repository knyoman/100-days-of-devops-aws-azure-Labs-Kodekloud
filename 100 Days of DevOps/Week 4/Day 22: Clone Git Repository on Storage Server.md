# Day 22: Clone Git Repository on Storage Server

> Meng-clone bare repository dari source lokal ke direktori target tanpa mengubah permission.

---

## Analisis Tugas

| Parameter | Detail |
|---|---|
| Source Repository | `/opt/apps.git` (bare repository) |
| Target Directory | `/usr/src/kodekloudrepos` |
| Username | `natasha` |
| Server | Storage Server (Stratos DC) |
| Constraint | ⚠️ Tidak boleh mengubah permission atau modifikasi tidak sah |

---

## Langkah Eksekusi

### Step 1 — SSH ke Storage Server

```bash
ssh natasha@ststor01.stratos.xfusioncorp.com
```

![images](/imgs_DevOps/day22.png)

---

### Step 2 — Verifikasi repository source

```bash
ls -la /opt/apps.git
```
![images](/imgs_DevOps/day22_1.png)

> Pastikan ini adalah bare git repository (berisi folder `HEAD`, `branches`, `config`, dll).

---

### Step 3 — Cek direktori target

```bash
ls -la /usr/src/kodekloudrepos
```

![images](/imgs_DevOps/day22_2.png)

> ⚠️ Direktori ini harus sudah ada — **jangan buat ulang atau ubah permission**.

---

### Step 4 — Clone repository

```bash
git clone /opt/apps.git /usr/src/kodekloudrepos/apps
```
![images](/imgs_DevOps/day22_3.png)

---

### Step 5 — Verifikasi hasil clone

```bash
ls -la /usr/src/kodekloudrepos/

cd /usr/src/kodekloudrepos/apps
git log --oneline      # Pastikan commit history terbaca
git status             # Pastikan working tree bersih
git remote -v          # Pastikan remote mengarah ke /opt/apps.git
```

![images](/imgs_DevOps/day22_4.png)

---

## Referensi Perintah

| Perintah | Fungsi |
|---|---|
| `git clone <src> <dest>` | Clone repository ke direktori tujuan |
| `git log --oneline` | Tampilkan riwayat commit secara ringkas |
| `git status` | Cek kondisi working tree |
| `git remote -v` | Tampilkan URL remote repository |

---

> 💡 **Tips:** Gunakan `git clone` dengan path lokal (bukan URL) untuk clone antar direktori di server yang sama — lebih cepat dan tidak memerlukan koneksi jaringan.