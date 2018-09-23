---
title: virtual host pada xampp di windows
date: 2018-09-23 08:00:10
tags: [web]
---

## Data domain
Sebagai contoh nama domain yang akan dibuat adalah frontend.vms. Untuk menambahkan domain baru tersebut, buka direktori C:\Windows\System32\drivers\etc, kemudian buka file "hosts" menggunakan text editor (notepad atau yang lainnya). Tambahkan perintah seperti pada blok kode berikut.

{% codeblock host %}
...
127.0.0.1   frontend.vms
...
{% endcodeblock %}

<!-- more -->
## Data virtual host
Langkah selanjutnya adalah menambahkan virtual host. Buka direktori C:\xampp\apache\conf\extra. Kemudian buka file httpd-vhosts.conf menggunakan text editor. Tambahkan virtual host baru seperti pada blok kode berikut.

{% codeblock httpd-vhosts.conf %}
...
<VirtualHost *:80>
    ServerName frontend.vms
    DocumentRoot "C:/xampp/htdocs/vms/frontend/web/"
    <Directory "C:/xampp/htdocs/vms/frontend/web/">
        RewriteEngine on
        RewriteCond %{REQUEST_FILENAME} !-f
        RewriteCond %{REQUEST_FILENAME} !-d
        RewriteRule . index.php
        DirectoryIndex index.php
        Require all granted
    </Directory>
</VirtualHost>
...
{% endcodeblock %}

Perhatikan pada bagian ServerName dan DocumentRoot. ServerName bernilai nama domain. DocumentRoot bernilai direct ke direktori web, yaitu C:/xampp/htdocs/vms/frontend/web/.

## Uji coba
Untuk melakukan uji coba, jalankan apache service melalui XAMPP control panel. Kemudian buka web browser (mozila atau google chrome) dengan mengetikan alamat virtual host http://frontend.vms.

{% asset_img "uji.jpg" "Virtual host" %}