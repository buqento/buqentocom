---
title: rest api menggunakan lumen
date: 2019-03-06 14:45:12
tags:
---


## Installing Lumen

Lumen utilizes Composer to manage its dependencies. So, before using Lumen, make sure you have Composer installed on your machine.

### Via Composer Create-Project

You may also install Lumen by issuing the Composer create-project command in your terminal:

$ composer create-project --prefer-dist laravel/lumen blog


### Serving Your Application

To serve your project locally, you may use the Laravel Homestead virtual machine, Laravel Valet, or the built-in PHP development server:

$ php -S localhost:8000 -t public
<!-- more -->

### Setting Database Connection

edit .env file

DB_DATABASE=pdpasar
DB_USERNAME=root
DB_PASSWORD=



### Create Controller
Add new file app\Http\Controllers\ProdukController.php

namespace App\Http\Controllers;
use App\Produk;

class ProdukController extends Controller
{

    public function index()
    {
        $data = Produk::all();
        return response($data);
    }

}


### Create Model
Add new file app\Http\Produk.php

namespace App;
use Illuminate\Database\Eloquent\Model;

class Produk extends Model
{
    protected $table = 'produk';
}


### Create route

routes\app.php

$router->get('/produk', 'ProdukController@index');


### Uncomment

bootstrap/app.php

$app->withFacades();
$app->withEloquent();
$app->register(App\Providers\AppServiceProvider::class);
$app->register(App\Providers\AuthServiceProvider::class);
$app->register(App\Providers\EventServiceProvider::class);