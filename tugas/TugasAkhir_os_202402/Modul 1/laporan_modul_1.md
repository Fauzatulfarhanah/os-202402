# 📝 Laporan Tugas Akhir Modul 1 – System Call dan Instrumentasi Kernel  
Mata Kuliah: Sistem Operasi Semester: Genap / Tahun Ajaran 2024–2025

Nama  : Fauzatul Farhanah  
NIM   : 240202834  
Kelas : 2IKRA

## 📌 Deskripsi Singkat Tugas  
Modul 1 – System Call dan Instrumentasi Kernel: Menambahkan dua system call baru, yaitu getpinfo() untuk melihat proses yang aktif dan getReadCount() untuk menghitung jumlah pemanggilan read() sejak boot.

## 🛠️ Rincian Implementasi
- Menambahkan dua system call baru di file `sysproc.c` dan `syscall.c`
- Mengedit `user.h` `usys.S` `syscall.h` untuk mendaftarkan syscall
- Menambahkan struktur struct pinfo di `proc.h`
- Menambahkan variabel global int readcount = 0; di `proc.c`
- Menambahkan counter readcount di kernel
- Membuat dua program uji yaitu ptest.c dan rtest.c

## ✅ Uji Fungsionalitas
- `ptest`: untuk menguji `getpinfo()`
- `rtest`: untuk menguji `getReadCount()`
  
## 📷 Hasil Uji  
📍 Output ptest
```
$ ptest  
PID     MEM     NAME  
1       12288   init  
2       16384   sh  
3       12288   ptest
```
📍 Output rtest
```
$ rtest  
Read Count Sebelum: 12  
hello  
Read Count Setelah: 13  
$ $   
```
📷 screenshot 

![Hasil Testing](https://example.com/path/to/screenshot.png)

## ⚠️ Kendala yang Dihadapi 
- `readcount` tidak dikenali yang menyebabkan **error undefined reference**
- Salah menambahkan field `priority` pada `struct proc` sehingga menyebabkan gagal kompilasi
- **Makefile error** karena penggunaan spasi bukan tab
- Output ptest tidak rapi karena proses mencetak secara bersamaan tanpa sinkronisasi

## 📚 Referensi  
Buku xv6 MIT: https://pdos.csail.mit.edu/6.828/2018/xv6/book-rev11.pdf  
Repositori xv6-public: https://github.com/mit-pdos/xv6-public  
MIT xv6-labs (Instruksi menambah system call): https://pdos.csail.mit.edu/6.828/2021/labs/syscall.h





