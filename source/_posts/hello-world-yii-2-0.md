title: hello world yii 2.0
tags:
  - web
categories:
  - Yii Framework
date: 2018-09-07 23:09:29
---
Langkah pertama adalah dengan membuat sebuah file dengan nama HelloController.php pada direktori controllers. File ini berisi class HelloController (nama kelas harus sama dengan nama file). Berikut blok kode lengkap file HelloController.php

{% codeblock HelloController.php lang:php %}
<?php
namespace app\controllers;
use yii\web\Controller;

class HelloController extends Controller{
    public function actionIndex()
    {
        return $this->render("welcome");
    }
}
{% endcodeblock %}
<!-- more -->
## Membuat view
Buatlah sebuah direktori dengan nama "hello" pada direktori views. Kemudian tambahkan sebuah file dengan nama welcome.php pada direktori hello. Perhatikan bahwa nama file harus sama dengan nilai kembalian pada fungsi actionIndex.

{% codeblock welcome.php lang:php %}
<?php
echo("Hello World!");
{% endcodeblock %}

## Melihat hasil
Jalankan browser, kemudian isi url dengan alamat:
{% codeblock %}
http://localhost/yiibaseapp/web/?r=hello
{% endcodeblock %}

## Tonton video lengkap
{% youtube t70OWtQRYwg %}