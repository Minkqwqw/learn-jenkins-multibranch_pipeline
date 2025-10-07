# 🚀 Jenkins Multibranch Pipeline with Discord Notification

Proyek ini merupakan praktik **CI/CD menggunakan Jenkins Multibranch Pipeline** yang terintegrasi dengan **Discord Notification**.  

Tujuannya adalah menguji otomatisasi build dan test untuk setiap branch di GitHub.

---

## 🧱 Struktur Proyek

```
.
├── app.py         
├── test_app.py     
└── Jenkinsfile     
```

---

## ⚙️ Persiapan Jenkins

Pastikan Jenkins sudah terpasang plugin berikut:

- ✅ **Docker Pipeline**  
- ✅ **HTTP Request Plugin**

---

## 🚀 Langkah Praktik

1. Clone repository ini:
   ```bash
   git clone https://github.com/FirmansyahDzakwanArifien/learn-jenkins-multibranch_pipeline.git
   ```

2. Buka Jenkins → Buat **Multibranch Pipeline Project**

3. Masukkan **Repository URL**:
   ```
   https://github.com/FirmansyahDzakwanArifien/learn-jenkins-multibranch_pipeline.git
   ```

4. Jalankan scan repository agar branch `main` dan `feature` terdeteksi otomatis.

5. Pastikan Jenkinsfile sudah berisi pipeline dengan tahapan berikut:
   - Build aplikasi menggunakan Docker (opsional)
   - Jalankan testing (`pytest`)
   - Kirim notifikasi hasil build ke Discord

---

## 🔔 Integrasi Discord Webhook

Notifikasi build dari Jenkins akan dikirim otomatis ke **Discord Channel** menggunakan webhook

---

## 🧪 Testing

Pipeline akan menjalankan langkah berikut:
1. Build image Docker (opsional)
2. Menjalankan `pytest` pada file `test_app.py`
3. Mengirim status hasil build ke Discord

Untuk menjalankan testing secara manual:
```bash
pytest -v
```

---


## 💡 Tips

- Pastikan webhook GitHub sudah diatur agar Jenkins dapat menerima trigger otomatis setiap ada perubahan di repo.
- Gunakan `feature` branch berbeda untuk menguji pipeline multibranch.



