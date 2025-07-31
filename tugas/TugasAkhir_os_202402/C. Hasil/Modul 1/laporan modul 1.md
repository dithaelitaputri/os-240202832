# 📝 Laporan Tugas Akhir

**Mata Kuliah**: Sistem Operasi
**Semester**: Genap / Tahun Ajaran 2024–2025
**Nama**: `<Ditha Elita Putri>`
**NIM**: `<240202832>`
**Modul yang Dikerjakan**:
`(Contoh: Modul 1 – System Call dan Instrumentasi Kernel)`

---

## 📌 Deskripsi Singkat Tugas

* **Modul 1 – System Call dan Instrumentasi Kernel**:
Pada modul ini, dilakukan penambahan dua system call baru ke dalam kernel xv6.
getpinfo(), berfungsi untuk menampilkan informasi proses-proses yang sedang aktif di sistem.
getReadCount(), digunakan untuk menghitung berapa kali fungsi read() dipanggil sejak sistem

## 🛠️ Rincian Implementasi

-Menambahkan system call baru
Tambahkan sys_getpinfo() dan sys_getReadCount() di sysproc.c untuk mengambil info proses dan jumlah pemanggilan read().
-Mendaftarkan nomor syscall
Tambahkan nomor unik untuk kedua syscall di syscall.h.
-Mendaftarkan syscall ke user space
Tambahkan entri di usys.S dan deklarasi fungsi di user.h agar bisa digunakan oleh program user.
-Membuat struktur data proses
Buat struct pinfo di proc.h untuk menyimpan PID dan nama proses.
-Menambahkan variabel penghitung read
Tambahkan variabel global readcount di kernel.
-Menambah logika di sys_read()
Tambahkan readcount++ di sys_read() agar jumlah pemanggilan read() tercatat.
-Membuat program uji coba
ptest.c: memanggil getpinfo() dan mencetak PID dan nama proses.
rtest.c: mencetak nilai getReadCount() sebelum dan sesudah read() untuk memastikan nilai bertambah.

### Modul 1 System Call dan Instrumentasi Kernel:

* Menambahkan dua system call baru di file `sysproc.c` dan `syscall.c`
* Mengedit `user.h`, `usys.S`, dan `syscall.h` untuk mendaftarkan syscall
* Menambahkan struktur `struct pinfo` di `proc.h`
* Menambahkan counter `readcount` di kernel
* Membuat dua program uji: `ptest.c` dan `rtest.c`
---


## ✅ Uji Fungsionalitas

ptest:
Program ini memanggil fungsi getpinfo() untuk menampilkan semua proses yang sedang aktif, lalu mencetak informasi seperti PID (Process ID) dan nama proses masing-masing.**

rtest:
Program ini menggunakan getReadCount() untuk mendapatkan jumlah pemanggilan read() sebelum dan sesudah melakukan operasi read(), guna memastikan bahwa penghitung (counter) benar-benar bertambah setelah fungsi read() dipanggil.******


## 📷 Hasil Uji


### 📍 Output `ptest`:

```
$ ptest
PID    MEM     NAME
1      12288   init
2      16384   sh
3      12288   ptest
```

### 📍 Output `rtest`:

```
Read Count Sebelum: 14
hello
Read Count Setelah: 15
```

### 📸 screenshot:
<img width="1000" height="679" alt="modul 1" src="https://github.com/user-attachments/assets/8899cd59-30a3-4ac4-b8c1-11d5a778d17c" />

![hasil ptest dan rtest](./screenshots/modul1.png)


---

## ⚠️ Kendala yang Dihadapi

Struktur data tidak terbaca antara kernel dan user space.
Variabel global tidak dikenali di file lain (kurang extern).

---

## 📚 Referensi

Tuliskan sumber referensi yang Anda gunakan, misalnya:

* Buku xv6 MIT: [https://pdos.csail.mit.edu/6.828/2018/xv6/book-rev11.pdf](https://pdos.csail.mit.edu/6.828/2018/xv6/book-rev11.pdf)
* Repositori xv6-public: [https://github.com/mit-pdos/xv6-public](https://github.com/mit-pdos/xv6-public)
* Stack Overflow, GitHub Issues, diskusi praktikum

---
