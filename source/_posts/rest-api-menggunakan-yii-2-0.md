---
title: rest api menggunakan yii 2.0
date: 2018-10-16 10:38:08
tags: [web]
categories: [Yii Framework]
---

## Create API module
Buat direktori baru dengan nama "modules" pada root app. Kemudian gunakan GII untuk membuat module baru pada aplikasi.

{% asset_img "Capture1.PNG" "create API module" %}

Langkah selanjutnya, yaitu menambahkan baris perintah berikut pada config/web.php

{% codeblock web.php lang:php %}
...
'modules' => [
    'api' => [
        'class' => 'app\modules\api\Api',
    ],
],
...
{% endcodeblock %}
<!-- more -->

## Create model API

Pada contoh ini, kita membuat model baru menggunakan tabel dengan nama "summary". Struktur tabel dapat dilihat pada blok kode berikut:

{% codeblock %}
CREATE TABLE "public"."summary" (
  "id" int2 NOT NULL DEFAULT nextval('summary_id_seq'::regclass),
  "name" varchar(255) COLLATE "pg_catalog"."default",
  "total" int8
)
{% endcodeblock %}

Gunakan struktur tabel di atas, kemudian generate model menggunakan GII.

{% asset_img "Capture2.PNG" "Create model API" %}

Selanjutnya tambahkan baris perintah berikut pada model yang telah digenerate.

{% codeblock Summary.php lang:php %}
<?php
class Summary extends \yii\db\ActiveRecord
{
	...
    const SCENARIO_CREATE = 'create';

    public function scenarios()
    {
        $scenarios = parent::scenarios();
        $scenarios['create'] = ['name', 'total'];
        return $scenarios;
    }
    ...
}
{% endcodeblock %}

## create controller API

Selanjutnya buatlah sebuah controller menggunakan GII.

{% asset_img "Capture3.PNG" "Generate controller" %}

Tambahkan baris perintah berikut pada controller yang telah digenerate.

{% codeblock SummaryController.php lang:php %}
<?php
namespace app\modules\api\controllers;
use app\modules\api\models\Summary;

class SummaryController extends \yii\web\Controller
{
	...
    public $enableCsrfValidation = false;

    public function actionCreateSummary()
    {
        \Yii::$app->response->format = \yii\web\Response::FORMAT_JSON;
        $summary = new Summary();
        $summary->scenario = Summary::SCENARIO_CREATE;
        $summary->attributes = \Yii::$app->request->post();
        // return array('status' => true);

        if($summary->validate()){
            $summary->save();
            return array('status' => true, 'data' => 'Summary created successfully.');
        }else{
            return array('status' => false, 'data' => $summary->getErrors());
        }
    }

    public function actionListSummary()
    {
        \Yii::$app->response->format = \yii\web\Response::FORMAT_JSON;
        $summary = Summary::find()->all();
        if(count($summary) > 0){
            return array('status' => true, 'data' => $summary);
        }else{
            return array('status' => false, 'data' => 'No data summary.');
        }
    }
    ...
}
{% endcodeblock %}

## Uji coba

Anda dapat menggunakan postman untuk menguji coba.

Ujicoba POST data dapat menggunakan url berikut: http://localhost/sdpdashboard/web/index.php/api/summary/create-summary?name=smartcity&total=150
{% asset_img "Capture4.PNG" "Post data" %}


Untuk ujicoba GET data dapat menggunakan url berikut:
http://localhost/sdpdashboard/web/index.php/api/summary/list-summary
{% asset_img "Capture5.PNG" "Get data" %}