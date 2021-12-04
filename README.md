## Laravel Breeze Tutorial 

The following documentation is based on my [Laravel Breeze Tutorial]() tutorial where we will be diving into Laravel Breeze. <br> <br>
•	Author: [Code With Dary](https://github.com/codewithdary) <br>
•	Twitter: [@codewithdary](https://twitter.com/codewithdary) <br>
•	Instagram: [@codewithdary](https://www.instagram.com/codewithdary/) <br>


## Technical Requirements
•	PHP => 7.2.5 <br>
•	Mailtrap <br>

## Prerequisites
•	Basic Laravel knowledge <br>
•	Low level HTML & CSS/TailwindCSS knowledge <br>

## Introduction
Laravel Breeze has replaced the previous Laravel UI command to pull in an authentication scaffolding in Laravel. 

Laravel Breeze is an optional authentication scaffolding that you can pull in through Composer. Why bothering creating your own authentication system when you can simply pull in a package that has been created by the developers?

## Installation
Like I’ve mentioned above, Laravel Breeze can be pulled in through Composer (as a dev dependency)
```
composer require Laravel/breeze –-dev
```

This command does not pull in the authentication scaffolding itself. It has pulled in a new option that you can run with artisan.
```
php artisan breeze:install
```

The frontend part of Laravel Breeze has been built out of Components, that use TailwindCSS for styling. Therefore, it’s asking us to run the ```npm install && npm run dev``` command to build our assets.
```
npm install && npm run dev
```

## Email verification
By default, Laravel Breeze turns off email verification and wants you to add it yourself on the route. Inside the ```routes/web.php``` file, you’ll see the ```/dashboard``` endpoint that is using the ```middleware()``` on the route. It also accepts an array that has only one value. This needs to be modified to the following

```php
Route::get('/dashboard', function () {
    return view('dashboard');
})->middleware(['auth', 'verified'])->name('dashboard');
```

We’re almost done, since the ```MustVerifyEmail``` class needs to be added as an implementation on the User model

```php
class User extends Authenticatable implements MustVerifyEmail
{
…
}
```

There is no need to pull in the ```MustVerifyEmail``` class since Laravel already added it inside the use statement.

```php
use Illuminate\Contracts\Auth\MustVerifyEmail;
```
