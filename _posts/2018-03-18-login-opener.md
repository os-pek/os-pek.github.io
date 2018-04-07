---
layout:     post
title:      "Login opener"
subtitle:   "metode login dengan membuka tab baru"
date:       2018-03-18
author:     "am k"
header-img: "img/post-bg-js-version.jpg"
tags:
    - php
    - js
    - javascript
---

Pasti sudah sering melihat di web yang membuka tab baru kemudian di kembalikan ke tab awal contohnya pada login akun google

jika belum tau caranya mungkin akan mengalami kesulitan karena search di google pun belum tentu mendapatkan hasil yang di inginkan

tetapi kita bisa dengan mudah membuat yang seperti itu dengan javascript opener

agar lebih mudah lagi saya buatkan library kecil2an yang sekaligus menghandle non opener & browser dengan minim fitur seperti opera mini

 **install dengan bower :** 
```
$ bower install https://github.com/os-pek/redparentjs.git
```
 **contoh implementasi dengan php :** 

 `index.php` 

``` php

<?php
if (!isset($_COOKIE['login'])) {
    echo '<p> <a href="login.php" target="_blank"> klik </a> untuk login! </p>'; 
} else {
     echo '<p> kamu sudah login! </p>';
     setcookie("login", null, -1, "/");
              unset($_COOKIE["login"]);
}

```
 `login.php` 

``` php

<?php
if (!isset($_POST['login'])) {
    echo '<p> ini adalah simulasi login form! </p>';
      echo ' <form action="login.php" method="post">
<input type="submit" name ="login" value="Login Now!"/></form> '; 
} else {
    echo' <p> ini adalah simulasi login berhasil!</p>';
    echo' <p> klik <a href="index.php"> disini </a> jika tidak dialihkan. </p>';
    setcookie("login", "user", time()+(86400*30), "/"); 
    echo '<script src="bower_components/redparentjs/dist/redparent.min.js"></script>';
    echo ' <script> redparent("index.php") </script>';
}
```

dari script diatas saat pertama buka  `index.php` maka akan terlihat link untuk login dan ketika link tersebut di klik membukan  `login.php` di tab baru, setelah menekan tombol login di  `login.php` tab akan otomatis tertutup dan kembali ke  `index.php`  dengan tulisan  `kamu sudah login!`.

