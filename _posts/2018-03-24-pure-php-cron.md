---
layout:     post
title:      "Pure PHP Cron Daemon"
subtitle:   "contoh implementasi php daemon"
date:       2018-03-24
author:     "am k"
header-img: "img/post-bg-unix-linux.jpg"
tags:
    - php
    - php-cli
---

PHP cron [scheduler](https://packagist.org/packages/peppeocchi/php-cron-scheduler) merupakan library yang sangat bagus untuk membuat schedule, kita cukup mengatur agar berjalan setiap menit pada cron tab kemudian tidak perlu lagi menyentuh cron, semua perubuhan pada schedule hanya perlu mengedit scheduler.php

pada post ini kita akan mengganti fungsi cron tab dengan pure php daemon, sebelumnya mari kita pahami beberapa benefit daripada mengganti cron dengan php :

- tidak perlu menginstall cron

- meringankan image berbasis docker

- saat hosting tidak memiliki fitur cron dan kita tidak di berikan akses root untuk menginstall cron seperti kebanyakan paas


 **Initialize project:** 

mulai project baru bersama php cron daemon

```
composer create-project ospek/cron:dev-master test-project
```
kemudian  `cd` ke folder  `test-project`, kamu akan melihat file:

- scheduler.php : file yang menjalankan library  `php-cron-schuduler` 
- hello.php : test script yang di jalankan setiap menit pada scheduler.php

mulailah membuat coding pada  `test-project`  atau mengimport script yang sudah ada ke folder ini, jika kamu tidak menggunakan framework, tidak ada salahnya untuk membaca best practice [modern php without a framework](https://kevinsmith.io/modern-php-without-a-framework)


 **Menjalankan Cron Daemon :** 

untuk menjalankan cron daemon gunakan perintah:

```
php cron.php <option>
```

option yang tersedia:

 -  `start`  memulai cron

-  `status` cek status cron 

-  `stop`  menghentikan cron

 **How it's work?** 

untuk memahami cara kerja  `cron.php`  kita bisa melihat dari source code dibawah ini

``` php
<?php

$lock = fopen('cron.pid', 'c+');
if (isset($argv[1])) {
    switch($argv[1]) {
    case "start":
        if (!flock($lock, LOCK_EX | LOCK_NB)) {
            die('cron already running! \n');
        }
 
        switch ($pid = pcntl_fork()) {
        case -1:
            die('unable to fork! \n');
        case 0: // this is the child process
            break;
        default: // otherwise this is the parent process
            fseek($lock, 0);
            ftruncate($lock, 0);
            fwrite($lock, $pid);
            fflush($lock);
            exit;
        }
 
        if (posix_setsid() === -1) {
             die('could not setsid! \n');
        }
 
        fclose(STDIN);
        fclose(STDOUT);
        fclose(STDERR);
 
        $stdIn = fopen('/dev/null', 'r'); // set fd/0
        $stdOut = fopen('/dev/null', 'w'); // set fd/1
        $stdErr = fopen('php://stdout', 'w'); // a hack to duplicate fd/1 to 2
 
        pcntl_signal(SIGTSTP, SIG_IGN);
        pcntl_signal(SIGTTOU, SIG_IGN);
        pcntl_signal(SIGTTIN, SIG_IGN);
        pcntl_signal(SIGHUP, SIG_IGN);
 
        // cron like execute scheduler every minutes
        
        while (true) {
            sleep(60);
            exec('php scheduler.php > /dev/null 2>&1');
        }
        break;
    case "status":
        if (flock($lock, LOCK_EX | LOCK_NB)) :
            echo 'status: stopped \n';
            else:
                echo 'status: running \n';
            endif;
        break;
        
    case "stop":
        if (flock($lock, LOCK_EX | LOCK_NB)) {
            die('cron not running \n');
        }
        $pid = fgets($lock);
 
        posix_kill($pid, SIGTERM);
        echo 'cron stop successful \n';
        break;
    default:
        echo 'only available argument start, status & stop \n';
    } 
} else {
        echo 'no argument provided! \n';
}

```
process daemon berbeda dengan process latar belakang biasa, dengan [signal handler](/2018/03/21/php-signal-handler/) dan lainnya sangat mungkin untuk mendaemonising php, sayangnya ini tidak akan berjalan di windows

> sebagai alternative di windows gunakan php [win32service](https://github.com/InExtenso/win32service) extension untuk mendaemonising script php kamu

 **live demo :** 

<script src="https://asciinema.org/a/1aA49KwLcsgWtmZrBLYBpvnKN.js" id="asciicast-1aA49KwLcsgWtmZrBLYBpvnKN" async></script>

 **Heroku Deploy** 

saat deploy ke heroku, jadikan sebagai worker pada  `Procfile` 

```
worker: php cron.php start
```

