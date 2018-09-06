---
title: langkah cepat menginstal phalcon framework
date: 2018-09-05 17:07:54
tags: [web]
categories: [Phalcon]
---
{% blockquote %}
A full-stack PHP framework delivered as a C-extension.
{% endblockquote %}

Kalimat pertama saat berkunjung ke {% link phalconphp.com https://phalconphp.com/en/ %}. Phalcon merupakan framework PHP yang menggunakan C-extention, membuatnya sangat ringan dan cepat. 
<!-- more -->

## Instal file dll
Langkah pertama yang yang mestinya dilakukan untuk menggunakan phalcon pada windows adalah dengan menginstal phalcon.dll. DLL file tersebut dapat di unduh melalui [phalcon](https://phalconphp.com/en/download/windows)

## Periksa versi dan arsitektur
Selanjutnya anda dapat memeriksa versi dan arsitektur PHP melalui phpinfo() agar tidak mengunduh DLL yang salah. 

{% asset_img "arsitektur.png" "Versi dan arsitektur" %}

Pada gambar di atas, terlihat bahwa komputer yang saya pakai menggunakan PHP versi 7.2.3 dengan arsitektur x86. Oleh karena itu, yang harus saya unduh adalah: 

``` bash
phalcon_x86_vc15_php7.2_3.4.1-1751.zip
```

Setelah diunduh, ekstrak dan salin file dll tersebut ke direktori.

``` bash
C:\xampp\php\ext
```
{% asset_img "ekstrak.png" "Lokasi ekstrak file dll" %}

## Konfigurasi PHP.ini
Lakukan konfigurasi dengan menambahkan statemen pada file PHP.ini (C:\xampp\php).
``` bash
extension=php_phalcon.dll
```
{% asset_img "change.png" "Konfigurasi ekstention PHP.ini" %}

## Restart webserver
Restart server anda untuk memastikan apakah telah berhasil menginstal phalcon pada server. Untuk melihat hasilnya, periksa pada phpinfo().

{% asset_img "berhasil.png" "Tampilan phpinfo" %}