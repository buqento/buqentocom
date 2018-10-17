---
title: web client yii 2.0
date: 2018-10-17 13:31:43
tags: [web]
categories: [Yii Framework]
---

## Instal yii basic

{% codeblock %}
composer create-project --prefer-dist yiisoft/yii2-app-basic basic
{% endcodeblock %}

## Create model

Buat tabel dengan menggunakan struktur tabel berikut. Contoh berikut dengan nama tabel "alarm".

{% codeblock %}
CREATE TABLE "public"."alarm" (
  "id" int2 NOT NULL DEFAULT nextval('alarm_id_seq'::regclass),
  "waktu" varchar(255) COLLATE "pg_catalog"."default",
  "kamera" varchar(255) COLLATE "pg_catalog"."default",
  "snapshot" varchar(255) COLLATE "pg_catalog"."default"
)
{% endcodeblock %}

Gunakan GII untuk menggenerate model dari tabel "alarm" yang telah dibuat.

{% asset_img "Capture1.PNG" "Generate model alarm" %}


## Instal HTTP Client Extension for Yii 2

{% codeblock %}
php composer.phar require --prefer-dist yiisoft/yii2-httpclient
{% endcodeblock %}

## Controller

controllers\AlarmController.php

{% codeblock AlarmController.php lang:php %}
<?php
...
use yii\data\ArrayDataProvider;
use yii\httpclient\Client;
use yii\helpers\Json;
...

public function actionIndex()
{
    $client = new Client();
    $response = $client->createRequest()
        ->setUrl('http://localhost/yiiapi/web/index.php/absensis')
        ->addHeaders(['content-type' => 'application/json'])
        ->send();
    $data = Json::decode($response->content);
    $dataProvider = new ArrayDataProvider([
        'allModels' => $data,
        'pagination' => [
            'pageSize' => 10,
        ],
    ]);
    return $this->render('index', [
        'dataProvider' => $dataProvider,
    ]);
}
...

{% endcodeblock %}
<!-- more -->

## View

views\alarm\index.php

{% codeblock index.php lang:php %}
...
<?= GridView::widget([
    'dataProvider' => $dataProvider,
    // 'filterModel' => $searchModel,
    'columns' => [
        ['class' => 'yii\grid\SerialColumn'],
        'waktu',
        'kamera',
        'snapshot',
    ],
]); ?>
...
{% endcodeblock %}