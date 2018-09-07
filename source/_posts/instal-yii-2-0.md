---
title: instal yii 2.0
date: 2018-09-07 08:33:16
tags: [web]
categories: [Yii 2.0]
---

Anda dapat menginstal Yii dengan dua cara, menggunakan manajer paket Composer atau dengan mengunduh file arsip. Yang pertama adalah cara yang lebih disukai, karena memungkinkan Anda untuk menginstal ekstensi baru atau memperbarui Yii hanya dengan menjalankan satu perintah.

## Instal menggunakan Composer
Untuk server windows anda dapat mengunduh dan menginstal composer melalui {% link getcomposer.org https://getcomposer.org/ %}

Selanjutnya jalankan perintah berikut melalui command prompt:

{% codeblock %}
composer create-project --prefer-dist yiisoft/yii2-app-basic yiibaseapp
{% endcodeblock %}
<!-- more -->
## Jalankan web server
Pastikan anda telah menginstal apache service pada komputer. Saya menggunakan XAMPP yang dapat di unduh di {% link www.apachefriends.org https://www.apachefriends.org/download.html %}

## Buka browser
Jalankan browser dan lihat hasilnya melalui link berikut:

{% codeblock %}
http://localhost/yiibaseapp/web/
{% endcodeblock %}

## Tonton video lengkap
{% youtube SXQ19XYZYkg %}
