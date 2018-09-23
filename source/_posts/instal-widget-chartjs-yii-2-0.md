---
title: instal widget chartjs yii 2.0
date: 2018-09-23 11:16:04
tags: [web]
categories: [Yii Framework]
---

## Instal widget
Ada dua cara menginstal widget chartjs melalui composer. Cara pertama yaitu menjalankan perintah berikut:

{% codeblock %}
composer require 2amigos/yii2-chartjs-widget:~2.0
{% endcodeblock %}

Cara kedua, yaitu menambahkan perintah di bawah ini pada bagian require di file composer.json pada aplikasi. Kemudian melakukan update composer.

{% codeblock composer.json %}
...
"require": {
    ...
    "2amigos/yii2-chartjs-widget": "~2.0",
    ...
},
...
{% endcodeblock %}

## Menampilkan di view
Blok kode di bawah ini adalah contoh untuk menampilkan line chart pada view file index.php menggunakan data dummy.

{% codeblock index.php lang:php %}
use dosamigos\chartjs\ChartJs;

<?= ChartJs::widget([
    'type' => 'line',
    'options' => [
        'height' => 400,
        'width' => 400
    ],
    'data' => [
        'labels' => ["January", "February", "March", "April", "May", "June", "July"],
        'datasets' => [
            [
                'label' => "My First dataset",
                'backgroundColor' => "#ff6384",
                'borderColor' => "rgba(179,181,198,1)",
                'pointBackgroundColor' => "rgba(179,181,198,1)",
                'pointBorderColor' => "#fff",
                'pointHoverBackgroundColor' => "#fff",
                'pointHoverBorderColor' => "rgba(179,181,198,1)",
                'data' => [65, 59, 90, 81, 56, 55, 40]
            ]
        ]
    ]
]);
?>
{% endcodeblock %}

{% asset_img "chart.png" "Bar Chart" %}

## Tipe chart
Ada beberapa tipe chart yang bisa digunakan, yaitu Line, Bar, Radar, Polar, Pie, Doughnut, Bubble, Scatter, Area dan Mixed.