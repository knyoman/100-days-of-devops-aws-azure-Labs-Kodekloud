# Day 21: Assigning Public IP to Virtual Machines

---

## Step 0 — SSH ke Storage Server

```bash
ssh natasha@ststor01.stratos.xfusioncorp.com
```
![images](/imgs_DevOps/day21.png)
> Jika perlu akses root: `sudo su -`

---

## Step 1 — Install Git

```bash
sudo yum install -y git
git --version
```
![images](/imgs_DevOps/day21_1.png)
---

## Step 2 — Buat Bare Repository

```bash
sudo git init --bare /opt/ecommerce.git
ls -la /opt/ecommerce.git/
```
![images](/imgs_DevOps/day21_2.png)
---

## Step 3 — Validasi

```bash
cat /opt/ecommerce.git/config
```
![images](/imgs_DevOps/day21_3.png)

Pastikan output mengandung:

```
[core]
    bare = true
```

> ✅ Repository `/opt/ecommerce.git` siap digunakan sebagai remote repo.