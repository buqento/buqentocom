---
title: lumen installation
date: 2019-01-25 10:53:38
tags:
---


### Via Composer Create-Project
You may also install Lumen by issuing the Composer create-project command in your terminal:

{% codeblock %}
composer create-project --prefer-dist laravel/lumen blog
{% endcodeblock %}

### Serving Your Application
To serve your project locally, you may use the Laravel Homestead virtual machine, Laravel Valet, or the built-in PHP development server:

{% codeblock %}
php -S localhost:8000 -t public
{% endcodeblock %}
<!-- more -->
### Setup Database Connection

root/.env

{% codeblock %}
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=homestead
DB_USERNAME=homestead
DB_PASSWORD=secret
{% endcodeblock %}

### Configure App

Uncomment webroot/bootstrap/app.php

{% codeblock %}
$app->withFacades();
$app->withEloquent();

$app->register(App\Providers\AppServiceProvider::class);
$app->register(App\Providers\AuthServiceProvider::class);
$app->register(App\Providers\EventServiceProvider::class);
{% endcodeblock %}


### Create Controller


Create file VisitedController.php in webroot/app/Http/Controllers/ directory

{% codeblock %}
<?php

namespace App\Http\Controllers;
use App\Visited;
use Illuminate\Http\Request;

class VisitedController extends Controller
{
    /**
     * Create a new controller instance.
     *
     * @return void
     */
    public function __construct()
    {
        //
    }

    //

    public function index(){
        $data = Visited::all();
        return response($data);
    }

    public function show($id){
        return Visited::findOrFail($id);
        // $data = Visited::where('id',$id)->get();
        // return response ($data);
    }

    // public function store (Request $request){
    //     $data = new Todo();
    //     $data->activity = $request->input('activity');
    //     $data->description = $request->input('description');
    //     $data->save();

    //     return response('Berhasil Tambah Data');
    // }

    public function update(Request $request, $id){
        $data = Visited::where('id',$id)->first();
        // $data->status = $request->input('status');
        $data->status = 1;
        $data->save();

        return response('Berhasil Merubah Data');
    }

    // public function destroy($id){
    //     $data = Todo::where('id',$id)->first();
    //     $data->delete();

    //     return response('Berhasil Menghapus Data');
    // }
}


{% endcodeblock %}


### Create New Model

Create file Visited.php in webroot/app/ directory

{% codeblock %}
<?php
namespace App;
use Illuminate\Database\Eloquent\Model;

class Visited extends Model
{
    protected $table = 'visited';
}

{% endcodeblock %}


### Add New Routes

webroot/routes/web.php

{% codeblock %}
$router->get('/visited', 'VisitedController@index');
{% endcodeblock %}