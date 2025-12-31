
# Laravel Base 
- New project : `laravel new projectName`
- Use the MVC pattern.
### Categories later
- `props` anything that is not an attribute.
- write :active="" means that everything inside "" should be treated as an expression.
## Routes and View
Routes are used to load what ressource we need for a particular html action
```php
Route::get('/', function () {
    return view('welcome');
});
```

View are in `Project/ressources/views`
View are used to show what we see.

## Layout files (Master files)
Blade is laravel templating engines.

Example layout

```php
<!DOCTYPE html>
<html lang=fr>
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1">
        <title></title>
        <link href="css/style.css" rel="stylesheet">
    </head>
    <body>
        {{ $slot }}
    </body>
</html>

```

`$slot` is for the  **contenue**

Call a layout

```php
<x-layoutName>
	<h1> Contenue </h1>
</x-layoutName>
```

`$attributes` is an object that refer to the html attributes

```php
// nav-link.blade.php file   
<a {{ $attributes  }}> {{ $slot }} </a>
```
can be used 
```php
<x-nav-link href='/'> Home</x-nav-link>
<x-nav-link href='/about'> About</x-nav-link>
<x-nav-link href='/contact'>Contact </x-nav-link>
```

### Blade Directives 
Blade can have some directive that  are compile to php . The blade directives start with a @.
```php
@props(['active' => false, 'type' => 'a'])
@if ($type === 'a')
    <a class="{{ $active ? "bg-gray-900 text-white": "text-gray-300 hover:bg-white/5 hover:text-white"}} rounded-md  px-3 py-2 text-sm font-medium"
    aria-current="{{ $active ? 'page': 'false'}}"
    {{ $attributes }}
    >{{ $slot}} </a>
@else
    <button class="{{ $active ? "bg-gray-900 text-white": "text-gray-300 hover:bg-white/5 hover:text-white"}} rounded-md  px-3 py-2 text-sm font-medium"
    aria-current="{{ $active ? 'page': 'false'}}"
    {{ $attributes }}
    >{{ $slot}} </button>
@endif
```

### Components
Reusable block 

## Route wildcards
```php
Route::get('/jobs/{id}', function ($id) {
    $jobs = [
        ['id' => 1, 'title' => 'Director', 'salary' => 50000],
        ['id' => 2, 'title' => 'Programmer', 'salary' => 10000],
        ['id' => 3, 'title' => 'Teacher', 'salary' => 40000],
    ];

    $job = Arr::first($jobs, fn($job) => $job['id'] == $id); //Collect () is not used in the video.

    return view('job', ['job' => $job]);
});
```
 
 ### Passing data to views
 ```php
Route::get('/', function () {
    return view('home', [
        'greeting' => 'Hello', //$greeting will be accesible into the view
        'name' => 'Larry Robot',
    ]);
});
```

### Autoloading, Namespaces and models
# Working with database
- `php artisan migrate` runs all pending migrations to create or update database tables.
- `php artisan migrate:refresh` rolls back all migrations and runs them again, useful during development.
- `php artisan migrate:rollback` rolls back the last batch of migrations.

- `up()`: Defines the changes to apply (e.g., creating tables, adding columns).
- `down()`: Defines how to revert those changes (e.g., dropping tables, removing columns).

For example, a migration to create a `job_listings` table might include columns for `id`, `title`, and `salary`. You can add or modify columns by creating new migrations.

## Creating migration  and running a migrate
```bash
php artisan make:migration create_job_listings_table
```

```bash
php artisan migrate
```
## Eloquent
Converting a class to a Eloquent model

```php
use Illuminate\Database\Eloquent\Model;

class Job extends Model
{
    // Your model code here
}
```
By default, Eloquent expects the table name to be the plural snake_case of the model name (`jobs` for `Job`).
If your table has a different name, specify it in the model:
```php
protected $table = 'job_listings';
```
You can retrieve all records with `all()`, or find a specific record by ID with `find()`:

Create a record
```php
Job::create([
    'title' => 'Acme Director',
    'salary' => '1000000',
]);
```
However, Laravel protects against **mass assignment vulnerabilities** by requiring you to specify which attributes are mass assignable in your model:
```php
protected $fillable = ['title', 'salary'];
```

Laravel’s **Tinker** is a REPL (interactive shell) for your application:

```bash
php artisan tinker
```
# Sources
[[PHP-Laravel Sources]]

