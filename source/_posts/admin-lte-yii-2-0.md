---
title: admin lte yii 2.0
date: 2018-10-25 10:27:24
tags: [web]
categories: [Yii Framework]
---

### instal admin lte

composer require dmstr/yii2-adminlte-asset "^2.1"

### konfigurasi

Tambahkan konfigurasi berikut pada file web.php pada direktori \config.

{% codeblock web.php lang:php %}
'components' => [
    'view' => [
         'theme' => [
             'pathMap' => [
                '@app/views' => '@vendor/dmstr/yii2-adminlte-asset/example-views/yiisoft/yii2-app'
             ],
         ],
    ],
],
{% endcodeblock %}
<!-- more -->
### mengatur skin
Untuk mengatur warna skin, dapat mengubah parameter class body pada file main.php pada direktori vendor\dmstr\yii2-adminlte-asset\exmple-views\yiisoft\yii2-app\layouts\

{% codeblock main.php lang:php %}
<body class="hold-transition skin-yellow sidebar-mini">
{% endcodeblock %}