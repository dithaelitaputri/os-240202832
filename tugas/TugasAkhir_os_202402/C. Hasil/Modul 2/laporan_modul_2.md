# 📝 Laporan Tugas Akhir

**Mata Kuliah**: Sistem Operasi  
**Semester**: Genap / Tahun Ajaran 2024–2025  
**Nama**: `<Ditha Elita Putri>`  
**NIM**: `<240202832>`  
**Modul yang Dikerjakan**:
`(Modul 2 – Penjadwalan CPU Lanjutan Penjadwalan Prioritas Non-Preemptive)`

---

## 📌 Deskripsi Singkat Tugas

* **Modul 2 – Penjadwalan CPU Lanjutan (Penjadwalan Prioritas Non-Preemptive)**:
- Tugas ini adalah mengubah cara kerja penjadwalan proses di sistem operasi xv6 dari Round Robin menjadi Non-Preemptive Priority Scheduling. Dalam sistem ini, proses dengan prioritas tertinggi akan dijalankan lebih dulu, tanpa diganggu oleh proses lain. Untuk itu, ditambahkan field priority pada setiap proses, lalu dibuat system call set_priority(int) agar user bisa mengatur prioritas proses. Terakhir, bagian scheduler() diubah agar selalu memilih proses RUNNABLE dengan prioritas tertinggi.  

---

## 🛠️ Rincian Implementasi

1. Membuat file ptest.c
Buat program user bernama ptest.c yang akan digunakan untuk menguji pembuatan proses dan pengaturan urutan eksekusi.  
2. Memanggil fork() dua kali
Di dalam program, gunakan fork() sebanyak dua kali untuk membuat dua proses anak dari proses utama (parent).  
3. Mengatur urutan output dengan wait()
Gunakan system call wait() agar proses induk menunggu semua proses anak selesai terlebih dahulu. Ini dilakukan supaya output tidak tercampur dan urutannya rapi.  
4. Menampilkan pesan dari proses anak dan induk
Masing-masing proses anak mencetak pesan bahwa tugasnya sudah selesai. Setelah semua anak selesai, proses induk akan mencetak pesan terakhir sebagai penutup.  
5. Tanpa menambahkan system call baru
Modul ini hanya menggunakan system call yang sudah tersedia di xv6 (seperti fork(), wait(), dan printf), jadi tidak perlu mengubah kode kernel.    

---


## ✅ Uji Fungsionalitas

- ptest:
Digunakan untuk menguji proses pembuatan anak (melalui fork()) dan sinkronisasi antara proses induk dan anak.  
- output:
Output program menunjukkan bahwa proses anak selesai lebih dulu, kemudian diikuti oleh proses induk.  
---

## 📷 Hasil Uji

### 📍 Output `ptest`:

```
Child 2 selesai  
Child 1 selesai  
Parent selesai  
```


### 📸 screenshot:
<img width="389" height="130" alt="modul 2" src="https://github.com/user-attachments/assets/d887d16c-4c68-4b32-a625-cb0ba72a688a" />

---

![hasil ptest dan rtest](./screenshots/modul 2.png)  


---

## ⚠️ Kendala yang Dihadapi

- Output anak dan orang tua tercampur
Kalau wait() tidak dipakai dengan benar, proses anak dan induk bisa mencetak pesan bersamaan, jadi urutannya kacau.  

- Semua proses menjalankan kode yang sama
Setelah fork(), baik parent maupun child menjalankan baris yang sama. Kalau tidak dicek, kita tidak tahu siapa yang harus mencetak apa.  

---

## 📚 Referensi

Tuliskan sumber referensi yang Anda gunakan, misalnya:

* Buku xv6 MIT: [https://pdos.csail.mit.edu/6.828/2018/xv6/book-rev11.pdf](https://pdos.csail.mit.edu/6.828/2018/xv6/book-rev11.pdf)
* Repositori xv6-public: [https://github.com/mit-pdos/xv6-public](https://github.com/mit-pdos/xv6-public)
* Stack Overflow, GitHub Issues, diskusi praktikum

---
