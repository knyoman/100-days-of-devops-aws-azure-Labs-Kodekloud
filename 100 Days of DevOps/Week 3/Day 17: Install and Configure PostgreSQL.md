# Day 17: Install and Configure PostgreSQL

---

## Tahap 1 SSH ke Database Server

```bash
ssh peter@stdb01
```
![images](/imgs_DevOps/day18.png)

---

## Tahap 2 Switch ke User PostgreSQL

```bash
sudo su - postgres
```
![images](/imgs_DevOps/day18_1.png)

---

## Tahap 3 Masuk ke psql

```bash
psql
```
![images](/imgs_DevOps/day18_2.png)

---

## Tahap 4 Buat User

```sql
CREATE USER kodekloud_top WITH PASSWORD 'GyQkFRVNr3';
```
![images](/imgs_DevOps/day18_3.png)
> Output: `CREATE ROLE`

---

## Tahap 5 Buat Database

```sql
CREATE DATABASE kodekloud_db7;
```
![images](/imgs_DevOps/day18_4.png)
> Output: `CREATE DATABASE`

---

## Tahap 6 Berikan Full Permissions

```sql
GRANT ALL PRIVILEGES ON DATABASE kodekloud_db7 TO kodekloud_top;
```
![images](/imgs_DevOps/day18_5.png)
> Output: `GRANT`

---

## Tahap 7 Verifikasi

```sql
-- Cek user
\du

-- Cek database
\l
```
![images](/imgs_DevOps/day18_6.png)
![images](/imgs_DevOps/day18_7.png)

> Pastikan `kodekloud_top` dan `kodekloud_db7` muncul di daftar.

---

## Tahap 8 Keluar dari psql

```sql
\q
```
> ✅ Setup selesai.