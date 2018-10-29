---
title: mengubah struktur direktori yii 2.0 basic
date: 2018-10-29 09:59:49
tags: [web]
categories: [Yii Framework]
---

Secara default untuk mengakses aplikasi yii 2.0 basic melalui url: http://localhost/nama_aplikasi_anda/web. Tutorial ini akan menjelaskan cara mengubahnya, agar dapat diakses langsung melalui url: http://localhost/nama_aplikasi_anda.

### struktur direktori & file

1. Tambahkan direktori dengan nama _protected, assets dan themes.
2. Pindahkan semua isi direktori (tidak termasuk direktori web), ke dalam direktori _protected.
3. Pindahkan semua isi direktori web ke luar. Direktori web sudah tidak diperlukan sehingga bisa dihapus.
4. Pindahkan direktori css, js dan images ke dalam direktori themes.
<!-- more -->
### konfigurasi

Ubah konfigurasi file index.php sesuai dengan blok kode berikut:

{% codeblock index.php lang:php %}
// comment out the following two lines when deployed to production
defined('YII_DEBUG') or define('YII_DEBUG', true);
defined('YII_ENV') or define('YII_ENV', 'dev');

require __DIR__ . '/_protected/vendor/autoload.php';
require __DIR__ . '/_protected/vendor/yiisoft/yii2/Yii.php';

$config = require __DIR__ . '/_protected/config/web.php';

(new yii\web\Application($config))->run();
{% endcodeblock %}

Kemudian ubah juga class AppAsset yang ada pada _protected/assets/AppAsset.php

{% codeblock AppAsset.php lang:php %}
...
public $css = [
    'themes/css/site.css',
];
...
{% endcodeblock %}

Tambahkan sebuah file .httaccess yang isinya adalah sebagai berikut.

{% codeblock .httaccess %}
Options +FollowSymLinks
RewriteEngine on
RedirectMatch 404 /_protected
RedirectMatch 404 /\.git
RedirectMatch 404 /composer\.
RedirectMatch 404 /.bowerrc
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule . index.php
{% endcodeblock %}

### ujicoba

Aplikasi sudah bisa diakses melalui url: http://localhost/nama_aplikasi_anda