---
title: virtual host pada xampp di windows
date: 2018-09-23 08:00:10
tags: [web]
---

## Menambahkan domain baru
Buka direktori C:\Windows\System32\drivers\etc, kemudian tambahkan domain baru file "hosts" menggunakan notepad.

{% codeblock host %}
...
127.0.0.1   frontend.vms
...
{% endcodeblock %}

## Menambahkan data virtual host
Buka direktori C:\xampp\apache\conf\extra, kemudian dengan menggunakan notepad tambahkan perintah berikut:

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

## Uji coba
Jalankan apache service melalui XAMPP Control Panel. Kemudian buka web browser dengan mengetikan alamat Virtual Host yang telah dibuat yaitu frontend.vms

{% asset_img "uji.jpg" "Virtual host" %}
