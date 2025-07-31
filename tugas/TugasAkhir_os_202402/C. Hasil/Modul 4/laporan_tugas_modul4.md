# 📝 Laporan Tugas Akhir

**Mata Kuliah**: Sistem Operasi  
**Semester**: Genap / Tahun Ajaran 2024–2025  
**Nama**: `<Ditha Elita Putri>`  
**NIM**: `<240202832>`  
**Modul yang Dikerjakan**:
`(Modul 4 – Alternatif Kernel Subsistem (xv6-public))`

---

## 📌 Deskripsi Singkat Tugas

* **Modul 4 – Alternatif Kernel Subsistem (xv6-public)**:  
Modul ini bertujuan untuk menambahkan dua fitur ke dalam kernel xv6:  
- System call chmod(path, mode) untuk mengatur izin akses file, apakah hanya bisa dibaca (read-only) atau bisa dibaca dan ditulis (read-write).  
- Device /dev/random, yaitu perangkat semu (pseudo-device) yang menghasilkan data acak dan bisa dibaca oleh program user.  

---

## 🛠️ Rincian Implementasi

1. System Call chmod(path, mode)
Untuk menambahkan fitur pengaturan hak akses file, dilakukan beberapa perubahan:  
- sysfile.c: Tambahkan fungsi sys_chmod() untuk mengubah nilai mode pada inode file.  
- fs.c: Ubah fungsi writei() agar menolak penulisan jika file dalam mode hanya-baca.  
- file.c: Integrasikan logika penolakan tulis ke dalam filewrite(), agar berlaku saat proses user menulis.  
- user.h dan usys.S: Tambahkan deklarasi dan entri untuk syscall chmod().  
- syscall.c dan syscall.h: Daftarkan SYS_chmod dengan nomor syscall baru.  
- defs.h: Tambahkan deklarasi sys_chmod() untuk digunakan di bagian kernel lain.  
- fs.h: Tambahkan field mode ke dalam struktur inode untuk menyimpan status akses file.  
- chmodtest.c: Buat program uji untuk membuat file, mengubahnya ke hanya-baca, lalu mencoba menulis ke file tersebut.  
- Makefile: Tambahkan chmodtest ke daftar program yang dikompilasi.  

2. Perangkat /dev/random  
Untuk menambahkan device yang menghasilkan data acak:  
- random.c: Buat fungsi randomread() untuk menghasilkan byte acak saat file dibaca.  
- file.c dan fs.c: Daftarkan device /dev/random dalam array devsw[], agar pembacaan diarahkan ke randomread().  
- sysfile.c: Tambahkan dukungan untuk membuat device dengan mknod().  
- defs.h: Deklarasikan fungsi randomread() agar dikenali oleh kernel.  
- init.c: Tambahkan baris mknod("/dev/random", 1, 3); agar device otomatis dibuat saat sistem booting.  
- randomtest.c: Buat program uji yang membaca byte dari /dev/random dan menampilkannya.  
- Makefile: Tambahkan randomtest ke daftar program uji.  

---


## ✅ Uji Fungsionalitas

- chmodtest:
 Berhasil memblokir penulisan pada file yang sudah diubah menjadi read-only.    
- randomtest:
Berhasil menghasilkan dan menampilkan byte acak dari `/dev/random`.    
---

## 📷 Hasil Uji

### 📍 Output `randomtest`:

```
$ randomtest
186 195 152 73 166 100 37 
```


### 📸 screenshot:
<img width="371" height="134" alt="modul 4" src="https://github.com/user-attachments/assets/ca19278e-9dce-4cf3-b71a-01c371eaad5d" />


---

## ⚠️ Kendala yang Dihadapi

- Proteksi tulis awalnya gagal karena logika di writei() belum tepat.  
- Lupa mendaftarkan syscall chmod, jadi tidak dikenali oleh kernel.  
- /dev/random tidak muncul saat boot karena mknod() belum ditambahkan di init.c.  
- randomread() belum terhubung ke devsw[], sehingga pembacaan gagal.  

---

## 📚 Referensi

Tuliskan sumber referensi yang Anda gunakan, misalnya:

* Buku xv6 MIT: [https://pdos.csail.mit.edu/6.828/2018/xv6/book-rev11.pdf](https://pdos.csail.mit.edu/6.828/2018/xv6/book-rev11.pdf)
* Repositori xv6-public: [https://github.com/mit-pdos/xv6-public](https://github.com/mit-pdos/xv6-public)
* Stack Overflow, GitHub Issues, diskusi praktikum

---
