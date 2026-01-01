
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

### Model factories
#### What Are Factories?

Factories allow you to scaffold or generate fake data for your models. For example, you might want to create 10 users for testing or populate your local environment with many job listings without manually entering each record.

Laravel includes a default `UserFactory` that defines fake data for user attributes like `name`, `email`, and timestamps. You can also define additional states, such as an unverified user, by tweaking attributes.

#### Using Factories with Tinker

You can use factories anywhere in your Laravel code, but a great place to experiment is with **Artisan Tinker**, an interactive REPL for Laravel:

```bash
php artisan tinker
```

Example of creating a user with a factory:

```php
User::factory()->create();
```

If you encounter errors, such as missing columns, check that your database schema matches the factory attributes. For example, if you renamed `name` to `firstName` and `lastName` in your users table, update the factory accordingly using Faker's methods:

```php
'firstName' => $this->faker->firstName(),
'lastName' => $this->faker->lastName(),
```

Remember to restart Tinker after making changes to your code.
#### Creating Multiple Records

To create multiple records at once:

```php
User::factory()->count(100)->create();
```

This quickly generates 100 fake users.
#### Creating a Factory for Job Listings

Instead of duplicating the user factory, generate a new factory for your `Job` model:

```bash
php artisan make:factory JobFactory --model=Job
```

In the `JobFactory`, define attributes like `title` and `salary`. Use Faker methods such as `jobTitle` for realistic data. You can hardcode values if variability isn't needed.

Example:

```php
public function definition()
{
    return [
        'title' => $this->faker->jobTitle(),
        'salary' => $this->faker->numberBetween(30000, 100000),
    ];
}
```
#### Using Factories with Relationships

If your `Job` model belongs to an `Employer`, you can define this relationship in your factory by creating an `EmployerFactory` and referencing it:

```php
'employer_id' => Employer::factory(),
```

This tells Laravel to create a new employer record when generating a job and associate it accordingly.

If you get errors like "Employer factory not found," ensure you have generated the factory and added the `HasFactory` trait to your model.
### Factory States

Factories can define **states** to represent different variations of a model. For example, the `UserFactory` has an `unverified` state that sets `emailVerifiedAt` to `null`:

```php
public function unverified()
{
    return $this->state(fn (array $attributes) => [
        'email_verified_at' => null,
    ]);
}
```

You can create a user in this state like so:

```php
User::factory()->unverified()->create();
```

You can define your own states, such as an `admin` state for users with administrative privileges.
# Sources
[[PHP-Laravel Sources]]

