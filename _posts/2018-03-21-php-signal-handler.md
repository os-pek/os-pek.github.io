---
layout:     post
title:      "PHP signal Handler"
subtitle:   "menghandle signal pada php cli"
date:       2018-03-21
author:     "am k"
header-img: "img/post-bg-unix-linux.jpg"
tags:
    - php
    - php-cli
---

Bagi programer php yang hanya menggunakan php sebagai backend website mungkin asing dengan signal handler, karena signal tempatnya di terminal

contohnya saat menjalankan program CLI, kemudian menginput  `CTRL+C` maka program tersebut akan terhenti, karena kita mengirimkan signal  `SIGINT` , agar program tidak berhenti saat menerima signal maka di perlukan signal handler

selain  `sigint` ada berbagai signal diataranya :

| no | signal |
|:----------:|:----------:|
|      1      |     SIGHUP       |
|      2    |    SIGINT        |
|      3      |      SIGQUIT      |
|      4   |       SIGILL     |
|      5      |     SIGTRAP       |

dan seterusnya ...

 **PHP Signal Handler** 

setiap bahasa pemrograman memiliki fungsi untuk menghandle signal termasuk php, di php untuk menghandle signal kita menggunakan fungsi  `pcntl_signal()` 

berikut ini contoh implementasinya, pertama-tama buat infinite loop tanpa signal handler

 `loop.php` 

``` php
<?php
$i = 0;
while (true):
    ++$i;
    echo $i."\n";
    sleep(3);
endwhile;
```
jalankan program diatas pada terminal dengan perintah  `php loop.php`  , dan biarkan berjalan beberapa saat kemudian baru kita hentikan dengan  `CTRL+C` 

sekarang kita terapkan singnal handler pada script diatas

``` php
<?php
declare(ticks=1);
function konfirm() 
{
    while (true):
        echo"yakin keluar? [y/n] : ";
        $handle = fopen("php://stdin", "r");
        $answer = trim(fgets($handle));
        if ($answer=="y") {
            echo "ok, selamat tinggal!\n";
            exit(0);
        } elseif ($answer=="n") {
            fclose($handle);
            echo "ok, lanjut bro ... \n";
            break;
        } else {
            echo "pilih y atau n! \n";
        }
    endwhile;
}
pcntl_signal(SIGINT, "konfirm");
$i = 0;
while (true):
      ++$i;
    echo $i."\n";
    sleep(2);
endwhile;
```
setelah menerapkan signal handle diatas maka saat meneima signal SIGINT atau  `CTRL+C` akan trigger ke fungsi callback  `konfirm()`  lihat asciicast di bawah untuk demo nya

<script src="https://asciinema.org/a/n6c7qI5pTgW0KyzZkUI4y6lYD.js" id="asciicast-n6c7qI5pTgW0KyzZkUI4y6lYD" async></script>

selain menghandle dengan fungsi callback kita juga dapat mengabaikan signal yang masuk dengan  `SIG_IGN`.
