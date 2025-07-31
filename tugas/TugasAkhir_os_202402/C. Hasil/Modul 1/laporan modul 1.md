# 📝 Laporan Tugas Akhir

**Mata Kuliah**: Sistem Operasi
**Semester**: Genap / Tahun Ajaran 2024–2025
**Nama**: `<Ditha Elita Putri>`
**NIM**: `<240202832>`
**Modul yang Dikerjakan**:
`(Contoh: Modul 1 – System Call dan Instrumentasi Kernel)`

---

## 📌 Deskripsi Singkat Tugas

Tuliskan deskripsi singkat dari modul yang Anda kerjakan. Misalnya:

* **Modul 1 – System Call dan Instrumentasi Kernel**:
  Pada modul ini, dilakukan penambahan dua system call baru ke dalam kernel xv6. System call pertama, getpinfo(), berfungsi untuk menampilkan informasi proses-proses yang sedang aktif di sistem. Sedangkan system call kedua, getReadCount(), digunakan untuk menghitung berapa kali fungsi read() dipanggil sejak sistem melakukan booting. Penambahan ini bertujuan untuk memahami cara kerja system call serta bagaimana kernel dapat diinstrumentasi untuk memantau aktivitas internal sistem secara langsung.

## 🛠️ Rincian Implementasi

Tuliskan secara ringkas namun jelas apa yang Anda lakukan:

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
---

## 📷 Hasil Uji

Lampirkan hasil uji berupa screenshot atau output terminal. Contoh:

### 📍 Contoh Output `cowtest`:

```
Child sees: Y
Parent sees: X
```

### 📍 Contoh Output `shmtest`:

```
Child reads: A
Parent reads: B
```

### 📍 Contoh Output `chmodtest`:

```
Write blocked as expected
```

Jika ada screenshot:

```
![hasil cowtest](./screenshots/cowtest_output.png)
```

---

## ⚠️ Kendala yang Dihadapi

Tuliskan kendala (jika ada), misalnya:

* Salah implementasi `page fault` menyebabkan panic
* Salah memetakan alamat shared memory ke USERTOP
* Proses biasa bisa akses audit log (belum ada validasi PID)

---

## 📚 Referensi

Tuliskan sumber referensi yang Anda gunakan, misalnya:

* Buku xv6 MIT: [https://pdos.csail.mit.edu/6.828/2018/xv6/book-rev11.pdf](https://pdos.csail.mit.edu/6.828/2018/xv6/book-rev11.pdf)
* Repositori xv6-public: [https://github.com/mit-pdos/xv6-public](https://github.com/mit-pdos/xv6-public)
* Stack Overflow, GitHub Issues, diskusi praktikum

---
