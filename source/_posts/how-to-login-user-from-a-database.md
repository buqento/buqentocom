---
title: How to login user from a database
date: 2018-09-03 16:09:59
tags:
categories: [Yii Framework]
---

This tutorial explains how to make login functionality with users coming from database. Login functionality is one of the most important parts of every application. 

## Create table

{% codeblock %}
CREATE TABLE `user_admin` (
  `id` int(10) UNSIGNED NOT NULL,
  `first_name` varchar(15) DEFAULT NULL,
  `last_name` varchar(20) DEFAULT NULL,
  `username` varchar(30) DEFAULT NULL,
  `password` varchar(30) DEFAULT NULL,
  `auth_key` char(50) DEFAULT NULL
) 
{% endcodeblock %}


## Generate Model

Next step is generate model with GII

{% asset_img "model.png" "Generate UserAdmin Model" %}

## Add function 
Update UserAdmin class in \models\UserAdmin.php

{% codeblock lang:php UserAdmin.php %}
class UserAdmin extends \yii\db\ActiveRecord implements \yii\web\IdentityInterface
{
...
    public function getAuthKey()
    {
        return $this->authKey;
    }

    public function getId()
    {
        return $this->id;
    }

    public function validateAuthKey($authKey)
    {
        return $this->authKey === $authKey;
    }

    public static function findIdentity($id)
    {
        return self::findOne($id);
    }

    public static function findIdentityByAccessToken($token, $type = null)
    {
        throw new \yii\base\NotSupportedException();
    }

    public static function findByUsername($username)
    {
        return self::findOne(['username' => $username]);
    }

    public function validatePassword($password)
    {
        return $this->password === $password;
    }
}
{% endcodeblock %}


Update LoginForm Class in \models\LoginForm.php

{% codeblock lang:php LoginForm.php %}
...
public function getUser()
{

    if ($this->_user === false) {
        $this->_user = UserAdmin::findByUsername($this->username);
    }

    return $this->_user;
}

{% endcodeblock %}

## Configure component 
Keep in mind to modify in the config path the \config\web.php file.

{% codeblock lang:php web.php %}
'user' => [
    'identityClass' => 'app\models\UserAdmin',
    'enableAutoLogin' => true,
    'enableSession' => true,
],
{% endcodeblock %}

## Watch
{% youtube O7oEl7TUqtA %}