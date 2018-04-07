---
layout:     post
title:      "Brackets di Python"
subtitle:   "menggunakan kurung kurawal di python"
date:       2018-04-07
author:     "am k"
header-img: "img/post-bg-unix-linux.jpg"
tags:
    - python
---

Dari pada menggunakan brackets/curly brackets atau di kenal juga kurung kurawal python memilih menerapkan indentasi berupa spasi atau bisa juga tab untuk block script, yang kadang membuat tidak nyaman terutama bagi mereka yang terbiasa ngoding di bahasa pemrograman C family kemudian migrasi ke python

> Python with braces. Because python is awesome, but whitespace is awful.

sebenarnya ada cara supaya tetap bisa menggunakan brackets di python yaitu dengan [bython](https://github.com/mathialo/bython) sebuah python preprosessor yang membantu menerjemahkan brackets menjadi standard python indentasi

 **installasi bython** 

untuk menginstall bython hanya perlu beberapa langkah, berikut perintahnya :
```
$ git clone https://github.com/mathialo/bython.git
$ cd bython
$ sudo make install
```
setelah installasi selesai, kita bisa menjalankan `bython` : main bython preprosessor dan  `py2by` yang bisa di pergunakan untuk mengconvert normal python script/file menjadi bython

> gunakan perintah  `bython -h`  dan  `py2by -h`  untuk melihat semua command yang tersedia

<script src="https://asciinema.org/a/PRrvhuFAJkiKFbZetWsV6t42E.js" id="asciicast-PRrvhuFAJkiKFbZetWsV6t42E" async></script>

 **contoh code bython** 

dengan menggunakan bython hanya mempengaruhi syntax indentasi yang lainnya tidak ada yang berubah, berikut ini contohnya :

``` python

def print_message(num_of_times) {
    for i in range(num_of_times) {
        print("bython is awesome!");
    }
}

if __name__ == "__main__" {
    print_message(10);
}
```
untuk menjalankan script diatas, simpan dengan nama file  `test.by` kemudian jalankan perintah

```
$ bython test.by
```
kita juga bisa mengcompile file bython menjadi normal python dengan option  `-c` :
```
$ bython -c test.by
```
setelah menjalankan perintah diatas akan ada file test.py di folder yang sama dengan test.by

<script src="https://asciinema.org/a/XI77Qjv63VSuHNWvEPu7xv5Df.js" id="asciicast-XI77Qjv63VSuHNWvEPu7xv5Df" async></script>



