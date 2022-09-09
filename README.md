# Laravel Multi Level Authentication

In this tutorial I will explain how create separate user and admin panel authentication.

#

## Installation

#

Create a laravel project

    composer create-project laravel/laravel=9.1 example-app

Install laravel `breeze` package

    composer require laravel/breeze=1.9 --dev
    php artisan breeze:install
    npm install
    npm run dev

Create a database and update `.env` file with your database credentials and then run migration

    php artisan migrate

Create a `modal` for admin

    php artisan make:model Admin -m

-   Copy users columns to admin migration file
-   Copy all text from User model to Admin model and set the class name Admin

Create all necessary routes for admin authentication

    /*
    |--------------------------------------------------------------------------
    | Admin Routes
    |--------------------------------------------------------------------------
    */

    Route::get('/admin/login', [AuthenticatedSessionController::class, 'create'])->name('admin.login')->middleware('guest:admin');

    Route::post('/admin/login/store', [AuthenticatedSessionController::class, 'store'])->name('admin.login.store');

    Route::group(['middleware' => 'admin'], function() {

    Route::get('/admin', [HomeController::class, 'index'])->name('admin.dashboard');

    Route::post('/admin/logout', [AuthenticatedSessionController::class, 'destroy'])->name('admin.logout');
    });
