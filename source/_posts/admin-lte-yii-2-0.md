---
title: admin lte yii 2.0
date: 2018-10-25 10:27:24
tags: [web]
categories: [Yii Framework]
---

C:\xampp\htdocs\klasisambon>composer require dmstr/yii2-adminlte-asset "^2.1"

'components' => [
    'view' => [
         'theme' => [
             'pathMap' => [
                '@app/views' => '@vendor/dmstr/yii2-adminlte-asset/example-views/yiisoft/yii2-app'
             ],
         ],
    ],
],

vendor\dmstr\yii2-adminlte-asset\exmple-views\yiisoft\yii2-app\layouts\main.php

<body class="hold-transition skin-yellow sidebar-mini">