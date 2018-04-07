---
layout:     post
title:      "Panduan menulis style code Python"
subtitle:   "menerapkan standard coding style pep8"
date:       2018-03-20
author:     "am k"
header-img: "img/post-bg-unix-linux.jpg"
tags:
    - python
---

Membiasakan menulis code dengan rapi membuat code yang dibuat lebih readability dan memudahkan dalam hal maintenance seperti menambah atau mengurangi baris/block script

mungkin setiap orang mempunyai style coding masing2, akan tetapi sangat di anjurkan untuk mengikuti standard coding style yang ditetapkan  [PEP8](https://www.python.org/dev/peps/pep-0008/) karena style sendiri belum tentu sesuai dengan best practice daripada menulis code yang rapi sekaligus agar tidak terjadi bentrok saat mengerjakan project bersama tim

untuk menyesuaikan code kita dengan standard  `pep8`  tidaklah susah

pertama-tama kita cukup ngoding seperti biasa, setelah selesai kita bisa memastikan standard  `pep8`  dengan  `pycodestyle` 

install  `pycodestyle`  jika sebelumnya belum terinstall

```
pip install pycodestyle
```
menggunakan   `pycodestyle` 
```
pycodestyle --first <file-kamu>
```
> jalankan perintah  `pycodestyle -h ` untuk melihat semua command yang tersedia

jika hasilnya banyak error yang ditemukan oleh  `pycodestyle`  itu wajar, nanti setelah terus-menerus mengikuti arahan  `pycodestyle`  kita akan terbiasa menulis code style sesuai standard  `pep8` 

selain cara manual ada juga cara memformat code secara otomatis dengan  `autopep8` 

install  `autopep8`  jika sebelumnya belum terinstall

```
pip install autopep8
```
menggunakan `autopep8` 

```
autopep8 --in-place --aggressive --aggressive <file-kamu>
```
> jalankan perintah  `autopep8 -h`  untuk melihat semua command yang tersedia

setelah memformat dengan `autopep8` gunakan  `pycodestyle` untuk memverifikasi, kemudian perbaiki secara manual jika masih ada error.