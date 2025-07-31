# 📝 Laporan Tugas Akhir

**Mata Kuliah**: Sistem Operasi  
**Semester**: Genap / Tahun Ajaran 2024–2025  
**Nama**: `<Ditha Elita Putri>`  
**NIM**: `<240202832>`  
**Modul yang Dikerjakan**:
`(Modul 3 – Manajemen Memori Tingkat Lanjut xv6-public x86)`

---

## 📌 Deskripsi Singkat Tugas

* **Modul 3 – Copy-on-Write dan Shared Memory**:
  Modul ini menambahkan dua fitur penting ke dalam kernel XV6:
- Copy-on-Write (CoW): membuat fork() lebih efisien dengan membagi halaman memori secara baca-saja, dan hanya menyalin saat proses menulis.  
- Shared Memory: memungkinkan beberapa proses berbagi satu halaman memori menggunakan shmget() dan shmrelease().

  
---

## 🛠️ Rincian Implementasi

1. Modifikasi mekanisme fork()
Ubah fork() agar tidak langsung menyalin seluruh memori. Proses parent dan child cukup berbagi halaman memori dengan izin baca-saja.  
2. Tangani penulisan dengan Copy-on-Write (CoW)
Tambahkan logika untuk mendeteksi page fault saat proses mencoba menulis. Saat itu, sistem akan menyalin halaman baru khusus untuk proses tersebut.  
3. Gunakan refcount untuk manajemen memori
Tambahkan penghitung referensi (refcount) pada setiap halaman fisik untuk melacak berapa banyak proses yang berbagi halaman tersebut.  
4. Tambahkan fitur Shared Memory
Buat system call shmget(int key) untuk mengakses halaman memori bersama berdasarkan key, dan shmrelease(int key) untuk melepasnya.  
5. Berbagi halaman antar proses
Proses yang memanggil shmget() dengan key yang sama akan mendapatkan alamat ke halaman memori yang sama, dan refcount akan bertambah.     

---


## ✅ Uji Fungsionalitas

- cowtest:
digunakan untuk memastikan bahwa setelah proses fork() dengan Copy-on-Write, parent dan child memiliki salinan data yang berbeda saat salah satu melakukan perubahan.    
- shmtest:
digunakan untuk menguji apakah parent dan child dapat berbagi halaman memori yang sama, namun tetap bisa mengakses dan mengubah data secara mandiri melalui mekanisme shared memory.
    
---

## 📷 Hasil Uji

### 📍 Output `cowtest`:

```
Child sees: Y
Parent sees: X

```
### 📍 Output `shmtest`:

```
Child reads: A
Parent reads: B
```

### 📸 screenshot:
<img width="435" height="183" alt="modul 3" src="https://github.com/user-attachments/assets/c95055c5-4946-44f0-b804-0fe72be54bf1" />

---

## ⚠️ Kendala yang Dihadapi

- Refcount tidak berjalan dengan benar
Awalnya saya lupa menambah dan mengurangi refcount saat halaman dibagi atau dibebaskan. Akibatnya, ada memori yang dibuang padahal masih dipakai, atau malah tidak pernah dibebaskan.

- Dua proses menulis ke halaman yang sama secara bersamaan
Saya mengalami kasus di mana proses parent dan child menulis ke memori bersama hampir bersamaan. Ini membuat data jadi tidak konsisten, dan sulit dilacak karena tanpa proteksi yang jelas.  
---

## 📚 Referensi

Tuliskan sumber referensi yang Anda gunakan, misalnya:

* Buku xv6 MIT: [https://pdos.csail.mit.edu/6.828/2018/xv6/book-rev11.pdf](https://pdos.csail.mit.edu/6.828/2018/xv6/book-rev11.pdf)
* Repositori xv6-public: [https://github.com/mit-pdos/xv6-public](https://github.com/mit-pdos/xv6-public)
* Stack Overflow, GitHub Issues, diskusi praktikum

---
