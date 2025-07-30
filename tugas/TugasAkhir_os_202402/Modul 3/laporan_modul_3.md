# 📝 Laporan Tugas Akhir

**Mata Kuliah**: Sistem Operasi  
**Semester**: Genap / Tahun Ajaran 2024–2025  
**Nama**: `<Fauzatul Farhanah>`  
**NIM**: `<240202834>`  
**Modul yang Dikerjakan**:`(Modul 3 – Manajemen Memori Tingkat Lanjut (xv6-public x86))`

---

## 📌 Deskripsi Singkat Tugas

**Modul 3 – Manajemen Memori Tingkat Lanjut (xv6-public x86)**:  
Modul ini berfokus pada optimalisasi manajemen memori di sistem operasi xv6, dengan mengimplementasikan dua fitur penting:
1. Copy-on-Write (CoW) Fork
   Meningkatkan efisiensi fork() dengan menunda penyalinan halaman memori hingga proses melakukan penulisan. Halaman memori awalnya dibagikan dalam mode read-only, dan        hanya disalin saat terjadi page fault akibat operasi tulis. Manajemen memori fisik dikendalikan melalui sistem reference counting.
2. Shared Memory ala System V
   Menyediakan mekanisme berbagi memori antar proses menggunakan sistem panggilan:
   - `void* shmget(int key)` untuk mengambil atau membuat shared memory berdasarkan key tertentu.
   - `int shmrelease(int key)` untuk melepaskan shared memory. Implementasi ini memungkinkan beberapa proses mengakses satu halaman memori bersama dengan pengelolaan akses       melalui reference count.
     
---

## 🛠️ Rincian Implementasi
1. Copy-on-Write (CoW) Fork
   * `vm.c` : Menambahkan array `refcount[]`, fungsi `incref()` dan `decref()` untuk mengelola jumlah referensi halaman fisik, dan memodifikasi `copyuvm()` menjadi              `cowuvm()` untuk mendukung mekanisme Copy-on-Write.
   * `proc.c` : Mengubah fungsi `fork()` agar menggunakan `cowuvm()` sebagai pengganti `copyuvm()` saat duplikasi page table proses.
   * `trap.c` : Menambahkan penanganan page fault untuk melakukan salinan halaman (copy) saat proses melakukan penulisan pada halaman bertanda `PTE_COW`.
   * `mmu.h` : Menambahkan definisi flag `PTE_COW` untuk menandai entri page table yang menggunakan mekanisme Copy-on-Write.
   * `defs.h` : Menambahkan deklarasi fungsi `incref()` dan `decref()` untuk manajemen `refcount` pada halaman memori fisik.
   * `cowtest.c` : Membuat program uji `cowtest`.
   * Mendaftarkan program uji `_cowtest` ke `Makefile`.

2. Shared Memory ala System V
   * `sysproc.c` : Menambahkan syscall `sys_shmget()` untuk memperoleh satu halaman shared memory berdasarkan key, dan `sys_shmrelease()` untuk mengurangi `refcount` dan       menghapus halaman jika tidak ada proses yang menggunakannya.
   * `vm.c` : Membuat array `shmtab[]` yang menyimpan informasi key, alamat halaman memori (frame), dan `refcount` untuk mencatat jumlah proses yang mengakses shared           memory.
   * `syscall.h` : Menambahkan nomor syscall `SYS_shmget` dan `SYS_shmrelease` supaya fungsi bisa dikenali sistem.
   * `user.h` : Menambahkan deklarasi fungsi `shmget(int)` dan `shmrelease(int)` supaya bisa digunakan oleh program user.
   * `usys.S` : Menambahkan entri syscall `SYSCALL(shmget)` dan `SYSCALL(shmrelease)` untuk menjembatani pemanggilan dari user space ke kernel.
   * `syscall.c` : Mendaftarkan `sys_shmget` dan `sys_shmrelease` ke dalam tabel syscall untuk menghubungkan nomor syscall dengan fungsi yang dijalankan.
   * `shmtest` : Membuat program uji `shmtest`.
   * Mendaftarkan program uji ke `Makefile` (_`shmtest`).

---

## ✅ Uji Fungsionalitas

* `cowtest`: untuk menguji apakah proses fork berjalan dengan mekanisme Copy-on-Write (CoW) tanpa langsung menggandakan seluruh memori.
* `shmtest`: untuk menguji apakah `shmget()` dapat membagi memori antar proses, dan `shmrelease()` berhasil melepasnya saat tidak digunakan lagi.



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
* 

---

## 📚 Referensi

Tuliskan sumber referensi yang Anda gunakan, misalnya:

* Buku xv6 MIT: [https://pdos.csail.mit.edu/6.828/2018/xv6/book-rev11.pdf](https://pdos.csail.mit.edu/6.828/2018/xv6/book-rev11.pdf)
* Repositori xv6-public: [https://github.com/mit-pdos/xv6-public](https://github.com/mit-pdos/xv6-public)
* Stack Overflow, GitHub Issues, diskusi praktikum

---

