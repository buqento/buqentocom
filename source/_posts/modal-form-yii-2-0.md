---
title: modal form yii 2.0
date: 2018-10-30 15:55:39
tags: [web]
categories: [Yii Framework]
---

### view

{% codeblock index.php lang:php %}
...
use yii\bootstrap\Modal;
use yii\helpers\Url;
...
<?= Html::button('Tambah Data', ['value' => Url::to(['create']), 
'class' => 'btn btn-success', 'id' => 'modalButton']) ?>

Modal::begin([
    'header' => '<h4>Tambah Data</h4>',
    'id' => 'modal',
    'size' => 'modal-sm',
]);
echo "<div id='modalContent'></div>";
Modal::end();
...
{% endcodeblock %}

<!-- more -->
### controller

{% codeblock YourController.php lang:php %}
...
public function actionCreate()
{
    ...
    return $this->renderAjax('create', [
        'model' => $model,
    ]);
}
...
{% endcodeblock %}


### assets

{% codeblock AppAsset.php lang:php %}
...
public $js = [
    'js/main.js',
];
...
{% endcodeblock %}

### javascript
{% codeblock main.js lang:javascript %}
$(function(){
	$('#modalButton').click(function(){
		$('#modal').modal('show')
		.find('#modalContent')
		.load($(this).attr('value'));
	});
});
{% endcodeblock %}