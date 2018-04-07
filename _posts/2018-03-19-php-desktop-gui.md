---
layout:     post
title:      "PHP Desktop GUI"
subtitle:   "remember php desktop gui? it still alive!"
date:       2018-03-19
author:     "am k"
header-img: "img/post-bg-unix-linux.jpg"
tags:
    - php
    - php-gui
    - gui
    - desktop
    - english
lang: en_US
---

PHP was popular in web environment by power up 80% website in the world, anyway it always possible to build desktop application with php language

before start building desktop application you need one of extension/library below

 **[PHP GTK](https://github.com/php/php-gtk-src)** 

![image](http://gtk.php.net/images/gtkaboutdialog.png)


PHP-GTK is an extension for the PHP programming language that implements language bindings for GTK+. It provides an object-oriented interface to GTK+ classes and functions and greatly simplifies writing client-side cross-platform GUI applications.

site: [gtk.php.net](http://gtk.php.net)

 **[WXPHP](https://github.com/wxphp/wxphp)** 

wxPHP stands for "wxWidgets for PHP" and it is a binding/wrapper for the cross-platform library wxWidgets, which gives you the ability to develop desktop applications using the PHP programming language.

site: [wxphp.org](https://wxphp.org)

  **[PHPQt](https://github.com/wxmaper/PQEngine)** 

Creating GUI applications in PHP using the Qt toolkit.

site: [phpqt.ru](http://phpqt.ru)

 **[UI](https://github.com/krakjoe/ui)** 

This extension wraps the very excellent [libui](https://github.com/andlabs/libui) to provide PHP 7 with an API for the creation of cross platform native look-and-feel interfaces.

site: [php.net/ui](http://php.net/ui)


### create single executable

using library/extension above make your desktop application only access able in terminal by typing  `php file.php` 

for ready distribution you need to create a single executable with [phc-win](https://github.com/jaredallard/phc-win)

### bonus

its also possible to packaging web based php into desktop application with [phpdesktop](https://github.com/cztomczak/phpdesktop).