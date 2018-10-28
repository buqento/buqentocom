---
title: dependent dropdown yii 2.0
date: 2018-10-04 17:33:48
tags: [web]
categories: [Yii Framework]
---

Dependent dropdown yang dimaksudkan adalah metode untuk merelasikan (saling bergantung) beberapa dropdown. Asumsi bahwa terdapat tiga tabel, yaitu: jemaat, sektor dan unit. Struktur masing-masing tabel dapat dilihat pada blok kode berikut.

{% codeblock %}
CREATE TABLE `jemaat`  (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `nama_jemaat` varchar(100) CHARACTER SET latin1 COLLATE latin1_swedish_ci NOT NULL,
  PRIMARY KEY (`id`) USING BTREE
)

CREATE TABLE `sektor`  (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `name` varchar(50) CHARACTER SET latin1 COLLATE latin1_swedish_ci NOT NULL,
  `jemaat_id` smallint(6) NOT NULL,
  PRIMARY KEY (`id`) USING BTREE
)

CREATE TABLE `unit`  (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `name` varchar(50) CHARACTER SET latin1 COLLATE latin1_swedish_ci NULL DEFAULT NULL,
  `jemaat_id` smallint(6) NULL DEFAULT NULL,
  `sektor_id` smallint(6) NULL DEFAULT NULL,
  PRIMARY KEY (`id`) USING BTREE
)
{% endcodeblock %}

### instal widget depdrop

Gunakan composer untuk menginstal widger depdrop.
{% codeblock %}
php composer.phar require kartik-v/yii2-widget-depdrop "@dev"
{% endcodeblock %}

### controller

Tambahkan kode berikut pada controller form (UnitController.php)

{% codeblock lang:php UnitController.php %}
...
use app\models\Sektor;
...
//menampilkan list sektor pada dropdown sektor
public function actionSektor() {
    $out = [];
    if (isset($_POST['depdrop_parents'])) {
        $parents = $_POST['depdrop_parents'];
        if ($parents != null) {
            $jemaat_id = $parents[0];
            $out = Sektor::getSektorList($jemaat_id); 
            return json_encode(['output'=>$out, 'selected'=>'']);
        }
    }
    return json_encode(['output'=>'', 'selected'=>'']);
}
...
{% endcodeblock %}

### model

Tambahkan fungsi getSektorList() dan parameter jemaat_id pada model Sektor. 

{% codeblock lang:php Sektor.php %}
public static function getSektorList($jemaat_id)
{
    $sektors = self::find()
        ->select(['id', 'name'])
        ->where(['jemaat_id' => $jemaat_id])
        ->asArray()
        ->all();
    return $sektors;
}
{% endcodeblock %}

### view

Kemudian pada view _form tambahkan baris kode berikut.

{% codeblock lang:php _form.php %}
...
use kartik\depdrop\DepDrop;
use yii\helpers\Url;
...

$jemaats = Jemaat::find()->select('nama_jemaat')->indexBy('id')->column();
echo $form->field($model, 'jemaat_id')->widget(Select2::classname(), [
    'data' => $jemaats,
    'options' => ['id' => 'jemaat-id', 'prompt' => 'Pilih Jemaat'],
]);?>

echo $form->field($model, 'sektor_id')->widget(DepDrop::classname(), [
    'type'=>DepDrop::TYPE_SELECT2,
    'options'=>['prompt' => 'Pilih Sektor'],
    'pluginOptions'=>[
        'depends'=>['jemaat-id'],
        'placeholder'=>'Pilih Sektor',
        'url'=>Url::to(['/unit/sektor']),
        'loadingText'=>'Loading...',
    ],

]);
...

{% endcodeblock %}