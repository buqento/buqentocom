---
title: Instal Phalcon di Windows
date: 2018-09-01 08:22:32
tags: 
categories: [Phalcon]
---

## Instal file dll
Untuk menggunakan phalcon pada windows, perlu menginstal phalcon.dll. DLL file dapat di unduh pada link berikut: [phalcon](https://phalconphp.com/en/download/windows)

## Periksa versi dan arsitektur
Anda dapat memeriksa versi dan arsitektur PHP melalui phpinfo() agar tidak mengunduh DLL yang salah. Saya menggunakan PHP versi 7.2.3 dengan arsitektur x86, maka yang harus saya unduh adalah ekstrak dan salin file dll tersebut ke direktori.

``` bash
C:\xampp\php\ext
```
<!-- more -->

## Konfigurasi PHP.ini
Lakukan konfigurasi dengan menambahkan statemen pada file PHP.ini (C:\xampp\php).
``` bash
extension=php_phalcon.dll
```

## Restart webserver
Restart server untuk memastikan apakah telah berhasil. Kemudian periksa phpinfo() apakah phalcon telah berhasil. terinstal.

{% youtube 75W-emM4wNQ %}