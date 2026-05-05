# Day 11: Attach Elastic Network Interface to EC2 Instance
> **Task:** Attach Network Interface ke EC2 Instance | Region: `us-east-1`

---

## 01 · LOGIN

```
URL      → https://538701479232.signin.aws.amazon.com/console?region=us-east-1
User     → kk_labs_user_899236
Password → Hg6Ul5!fO!Er
```

---

## 02 · CEK INSTANCE

```
Search Bar → EC2 → Instances → Instances (running)
           → cari: datacenter-ec2
           → catat Instance ID (i-0abc1234...)
           → tunggu status: ✅ Running + ✅ 2/2 checks passed
```
![images](/imgs_aws/day11.png)

> ⚠️ Jangan lanjut sebelum **Status Check = 2/2 passed**

---

## 03 · TEMUKAN ENI

```
EC2 Dashboard → Network & Security → Network Interfaces
              → cari: datacenter-eni
              → catat Network Interface ID (eni-0abc1234...)
              → pastikan status: Available ✓
```
![images](/imgs_aws/day11_1.png)

---

## 04 · ATTACH ENI

```
Network Interfaces → centang: datacenter-eni
                  → klik [Actions]
                  → pilih: Attach
```
![images](/imgs_aws/day11_2.png)

Pada dialog **Attach Network Interface:**

```
Instance ID → pilih: datacenter-ec2
            → klik [Attach] ✓
```
![images](/imgs_aws/day11_3.png)

---

## 05 · VERIFIKASI

Cek dari **EC2 Instance:**

```
Instances → datacenter-ec2
          → tab: Networking
          → Network Interfaces → datacenter-eni muncul ✅
```
![images](/imgs_aws/day11_4.png)
