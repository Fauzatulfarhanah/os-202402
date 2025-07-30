# 📝 Laporan Tugas Akhir

**Mata Kuliah**: Sistem Operasi
**Semester**: Genap / Tahun Ajaran 2024–2025
**Nama**: `<Fauzatul Farhanah>`
**NIM**: `<240202834>`
**Modul yang Dikerjakan**:`(Modul 3 – Manajemen Memori Tingkat Lanjut (xv6-public x86))`

---

## 📌 Deskripsi Singkat Tugas

* **Modul 3 – Manajemen Memori Tingkat Lanjut (xv6-public x86)**:
 Modul ini berfokus pada optimalisasi manajemen memori di sistem operasi xv6, dengan mengimplementasikan dua fitur penting:
1. Copy-on-Write (CoW) Fork
   Meningkatkan efisiensi fork() dengan menunda penyalinan halaman memori hingga proses melakukan penulisan. Halaman memori awalnya dibagikan dalam mode read-only, dan        hanya disalin saat terjadi page fault akibat operasi tulis. Manajemen memori fisik dikendalikan melalui sistem reference counting.
2. Shared Memory ala System V
   Menyediakan mekanisme berbagi memori antar proses menggunakan sistem panggilan:
   - `void* shmget(int key)` untuk mengambil atau membuat shared memory berdasarkan key tertentu.
   - `int shmrelease(int key)` untuk melepaskan shared memory. Implementasi ini memungkinkan beberapa proses mengakses satu halaman memori bersama dengan pengelolaan akses       melalui reference count.
     
---

## 🛠️ Rincian Implementasi

* Menambahkan dua system call baru di file `sysproc.c` dan `syscall.c`
* Mengedit `user.h`, `usys.S`, dan `syscall.h` untuk mendaftarkan syscall
* Menambahkan struktur `struct pinfo` di `proc.h`
* Menambahkan counter `readcount` di kernel
* Membuat dua program uji: `ptest.c` dan `rtest.c`
  
---

## ✅ Uji Fungsionalitas

Tuliskan program uji apa saja yang Anda gunakan, misalnya:

* `ptest`: untuk menguji `getpinfo()`
* `rtest`: untuk menguji `getReadCount()`
* `cowtest`: untuk menguji fork dengan Copy-on-Write
* `shmtest`: untuk menguji `shmget()` dan `shmrelease()`
* `chmodtest`: untuk memastikan file `read-only` tidak bisa ditulis
* `audit`: untuk melihat isi log system call (jika dijalankan oleh PID 1)

---

## 📷 Hasil Uji

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
---
📷 Screenshot:

A. Cowtest
---  
![screenshot modul 3A ](https://github.com/user-attachments/assets/d07d1623-9a7d-4aee-b971-92368a95126e)

---
B. shmtest
---
![screenshot modul 3B ](https://github.com/user-attachments/assets/03e043b0-3e3b-4ae1-a570-4f65e2d61d4d)

---

## ⚠️ Kendala yang Dihadapi
- jj
  

---

## 📚 Referensi

Tuliskan sumber referensi yang Anda gunakan, misalnya:

* Buku xv6 MIT: [https://pdos.csail.mit.edu/6.828/2018/xv6/book-rev11.pdf](https://pdos.csail.mit.edu/6.828/2018/xv6/book-rev11.pdf)
* Repositori xv6-public: [https://github.com/mit-pdos/xv6-public](https://github.com/mit-pdos/xv6-public)
* Stack Overflow, GitHub Issues, diskusi praktikum

---

