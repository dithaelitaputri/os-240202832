# 📝 Laporan Tugas Akhir

**Mata Kuliah**: Sistem Operasi  
**Semester**: Genap / Tahun Ajaran 2024–2025  
**Nama**: `<Ditha Elita Putri>`  
**NIM**: `<240202832>`  
**Modul yang Dikerjakan**:
`(Modul 5 – Audit dan Keamanan Sistem (xv6-public)

---

## 📌 Deskripsi Singkat Tugas

* **Modul 5 – Audit dan Sistem Keamanan (xv6-public)**:
- Modul ini menambahkan fitur audit log pada xv6, yang mencatat setiap pemanggilan system call secara otomatis. Log hanya dapat diakses oleh proses dengan PID 1 melalui syscall get_audit_log(), sehingga terjamin keamanannya dari proses lain.  

---

## 🛠️ Rincian Implementasi

1. syscall.c  
Menambahkan:  
- Struktur audit_entry  
- Array log audit_log[MAX_AUDIT]  
- Variabel indeks audit_index : Memodifikasi fungsi syscall() untuk mencatat setiap pemanggilan syscall ke dalam log secara otomatis.  
2. sysproc.c  
- Menambahkan definisi struct audit_entry serta deklarasi eksternal audit_log dan audit_index.  
- Mengimplementasikan syscall baru sys_get_audit_log() yang hanya dapat diakses oleh proses dengan PID 1.  
3. defs.h  
- Menambahkan makro #define MAX_AUDIT 128.  
- Menambahkan deklarasi fungsi get_audit_log(struct audit_entry*, int) sebagai antarmuka ke syscall audit  
4. user.h  
- Menambahkan definisi struct audit_entry untuk digunakan di user space.  
- Menambahkan deklarasi int get_audit_log(void *buf, int max) agar program pengguna dapat memanggil syscall audit.    
5. usys.S  
- Menambahkan entri syscall SYSCALL(get_audit_log) untuk menjembatani syscall ke kode user.  
6. syscall.h  
- Menambahkan #define SYS_get_audit_log 22 untuk mendefinisikan nomor syscall audit log.  
7. audit.c  
- Membuat program user space untuk menguji syscall get_audit_log().  
8. Makefile  
  - Menambahkan audit.c ke daftar program user agar disertakan dalam build xv6.  

---


## ✅ Uji Fungsionalitas

- audit:  
- untuk melihat isi log system call (jika dijalankan oleh PID 1)  
---

## 📷 Hasil Uji

### 📍 Output `audit dengan PID bukan 1`:

```
$ audit  
Access denied or error.  
```
### 📍 Output audit PID = 1 :

=== Audit Log ===  
[0] PID=1 SYSCALL=7 TICK=10  
[1] PID=1 SYSCALL=15 TICK=15  
[2] PID=1 SYSCALL=17 TICK=15  
[3] PID=1 SYSCALL=15 TICK=20  

### 📸 screenshot:
<img width="644" height="437" alt="modull 5" src="https://github.com/user-attachments/assets/fc2f070f-ae28-4219-aaa1-24dd6708f008" />  


---

## ⚠️ Kendala yang Dihadapi

- Lupa mendefinisikan ulang struct audit_entry di user.h, sehingga program user tidak bisa mengenali data log dari syscall.  
- Menggunakan sizeof(struct audit_entry) tanpa definisi lengkap di sysproc.c menyebabkan error kompilasi.  
- Forward declaration di defs.h tidak cukup untuk operasi seperti copyout atau sizeof, karena tidak menyertakan isi struct.  
- Tanpa definisi lengkap struct di sysproc.c, fungsi sys_get_audit_log() gagal mengakses dan menyalin log dengan benar.  

---

## 📚 Referensi

Tuliskan sumber referensi yang Anda gunakan, misalnya:

* Buku xv6 MIT: [https://pdos.csail.mit.edu/6.828/2018/xv6/book-rev11.pdf](https://pdos.csail.mit.edu/6.828/2018/xv6/book-rev11.pdf)
* Repositori xv6-public: [https://github.com/mit-pdos/xv6-public](https://github.com/mit-pdos/xv6-public)
* Stack Overflow, GitHub Issues, diskusi praktikum

---
