# laravel-cheatsheet

## Routing

###### Router Methods

```
Route::get($uri, $callback);
Route::post($uri, $callback);
Route::put($uri, $callback);
Route::patch($uri, $callback);
Route::options($uri, $callback);
```

Route that responds to multiple HTTP verbs.

```
 Route::match(['get', 'post'], '/', function(){
    //
 });
```

Route that responds to any HTTP verbs.

```
Route::any('/', function(){
    //
});
```

Forms using methods such as `POST`, `PUT`, `DELETE` should include CSRF Token field.

```
<form method="POST" action="">
{{ csrf_field() }}
</form>
```

###### Redirect Routes

```
Route::redirect('/here', '/there', 301);
```

###### View Routes

```
Route::view('/welcome', 'welcome');
Route::view('/welcome', 'welcome', ['name'=>'test data']);
```

###### Route Parameters

> Required Parameters

```
Route::get('user/{id}', function($id){
    return $id;
});

Route::get('posts/{post}/comments/{comment}, function(){
//
});
```

> Optional Parameters

```
Route::get('user/{name?}', function($name = null){
return $name;
});
```

###### Regular Expression Constraints

```
Route::get('user/{name}', function($name){
    //
})->where('name', '[A-Za-z]+');
Route::get('user/{id}', function($id){
    //
})->where('id', '[0-9]+');
Route::get('user/{id}/{name}', function($id, $name){

})->where(['id'=>'[0-9]+', 'name' => '[a-z]+');
```

###### Global Constraints
> Use `pattern` method for this in `RouteServiceProvider`'s `boot` method.
```
public function boot(){
    Route::pattern('id', '[0-9]+');
    parent::boot();
}
```