---
title: login user dengan database
date: 2018-09-07 09:21:41
tags: [web]
categories: [Yii Framework]
---

Fungsi login secara umum adalah salah satu bagian terpenting pada setiap aplikasi. Tutorial ini akan menjelaskan langkah-langkah membuat fungsi login dengan menggunakan model user basic yang ada pada yii framework.

### Membuat tabel
Buatlah sebuah tabel dengan nama user_admin. Saran saya agar tidak memberi nama tabel (user), karena nanti akan terbentur dengan user model bawaan yii. Struktur tabel user_admin dapat mengikuti blok kode di bawah:

{% codeblock %}
CREATE TABLE `user_admin`  (
  `id` int(11) UNSIGNED NOT NULL AUTO_INCREMENT,
  `username` varchar(15) CHARACTER SET latin1 COLLATE latin1_swedish_ci NOT NULL,
  `password` varchar(100) CHARACTER SET latin1 COLLATE latin1_swedish_ci NOT NULL,
  `authKey` char(64) CHARACTER SET latin1 COLLATE latin1_swedish_ci NOT NULL,
  `created` timestamp(0) NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP(0),
  PRIMARY KEY (`id`) USING BTREE
)
{% endcodeblock %}

<!-- more -->
### Generate model
Langkah selanjutnya adalah membuat model. Anda dapat menggunakan generator GII untuk membuat model. Atau dengan cara menambahkan sebuah file dengan nama UserAdmin.php pada direktori /models

{% asset_img "model.png" "Generate UserAdmin model menggunakan GII" %}

### Menambahkan fungsi
Tambahkan implements \yii\web\IdentityInterface pada class UserAdmin. Tambahkan juga beberapa fungsi pada model tersebut seperti kode blok di bawah:

{% codeblock lang:php UserAdmin.php %}
class UserAdmin extends \yii\db\ActiveRecord implements \yii\web\IdentityInterface
{
    ...
    public function getAuthKey(){
        return $this->authKey;
    }

    public function getId(){
        return $this->id;
    }

    public function validateAuthKey($authKey){
        return $this->authKey === $authKey;
    }

    public static function findIdentity($id){
        return self::findOne($id);
    }

    public static function findIdentityByAccessToken($token, $type = null){
        throw new \yii\base\NotSupportedException();
    }

    public static function findByUsername($username){
        return self::findOne(['username' => $username]);
    }

    public function validatePassword($password)
    {
        return Yii::$app->security->validatePassword($password, $this->password);
    }

    public function setPassword($password)
    {
        return Yii::$app->security->generatePasswordHash($password);
    }

    public function generateAuthKey()
    {
        return Yii::$app->security->generateRandomString();
    }
    ...
}
{% endcodeblock %}

Ubah baris kode pada model LoginForm yang ada pada direktori \models\LoginForm.php seperti pada kode blok di bawah:

{% codeblock lang:php LoginForm.php %}
    ...
    public function getUser(){
        if ($this->_user === false) {
            $this->_user = UserAdmin::findByUsername($this->username);
        }
        return $this->_user;
    }
    ...
{% endcodeblock %}

### Konfigurasi Component 

Langkah selanjutnya adalah mengubah parameter user component pada file \config\web.php.

{% codeblock lang:php web.php %}
'user' => [
    'identityClass' => 'app\models\UserAdmin',
    'enableAutoLogin' => true,
    'enableSession' => true,
],
{% endcodeblock %}

Tambahkan parameter dibawah ini untuk memfilter user sesi login saat aplikasi dijalankan.
{% codeblock lang:php web.php %}
'as beforeRequest' => [
    'class' => 'yii\filters\AccessControl',
    'rules' => [
        [
            'allow' => true,
            'actions' => ['login'],
        ],
        [
            'allow' => true,
            'roles' => ['@'],
        ],
    ],
    'denyCallback' => function () {
        return Yii::$app->response->redirect(['site/login']);
    },
],
{% endcodeblock %}

### Referensi
{% youtube O7oEl7TUqtA %}