# Laravel-Modules

## Why This Fork?
- Prefix module name when creating table for the module
- Added `--api` option when generating controller

The main branch is an excellent work of art! But sometimes when you are building a Module, you need the migration table to have the module's name prefix so as to avoid collision with other tables, and/or keep modules clean. It's arguably easier to view all tables used by the module at a glance, and also avoid collisions with other modules which would potentially use the same table (e.g. Role, Department, Category models)
This package will generate a migration table prefixed with the module's name.
```bash
# artisan command. Syntax: model name, module name, -m (migration flag) -p (prefix flag)
php artisan module:make-model Person Hr -pm

# API Controllers generation
php artisan module:make-controller Postcontroller --api
```
## Output
#### Model:

```php

<?php

namespace $NAMESPACE$; // namespace will be autofilled

use Illuminate\Database\Eloquent\Model;

class Person extends Model
{
    /**
     * The attributes that are mass assignable.
     *
     * @var array
     */
    protected $fillable = $FILLABLE$; // fillable properties will be inserted here if specified

    /**
     * The table associated with the model.
     *
     * @var string
     */
    protected $table = "hr_persons"; // auto-generates this in model

    //

}
```

#### Migration

```php
// 2018_03_25_210616_create_hr_persons_table.php

<?php

use Illuminate\Support\Facades\Schema;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Database\Migrations\Migration;

class CreateHrPersonsTable extends Migration
{
    /**
     * Run the migrations.
     *
     * @return void
     */
    public function up()
    {
        Schema::create('hr_persons', function (Blueprint $table) {
            $table->increments('id');

            $table->timestamps();
        });
    }

    /**
     * Reverse the migrations.
     *
     * @return void
     */
    public function down()
    {
        Schema::dropIfExists('hr_persons');
    }
}

```
The automatic appending of module-name in table name is done **Only** when making a model with the migration switch. It **Does Not** affect the *php artisan module:make-migration* just in case you need to generate other migrations to do other stuffs without appending the module name.


## Install

To install through Composer, by run the following command:

``` bash
composer require lexxyungcarter/laravel-modules
```

The package will automatically register a service provider and alias.

Optionally, publish the package's configuration file by running:

``` bash
php artisan vendor:publish --provider="Nwidart\Modules\LaravelModulesServiceProvider"
```

> NB: Namespacing has been preserved to the parent's repo for easier migration between the packages.
However, if coming from the parent repo, you should uninstall the package before requiring this package
to avoid collisions.

### Updates
This package will always be kept in sync with the parent repo. No need to worry about obsoleteness.

### Future
- Add [laracasts/Laravel-5-Generators-Extended](https://github.com/laracasts/Laravel-5-Generators-Extended) features into the package to extend migration command features. (Maybe you'll fork it and push it here? That would be GREAT!)

## Credits
- [Lexx YungCarter](https://github.com/lexxyungcarter)
- [Nicolas Widart](https://github.com/nwidart)

# Readme From Forked Project
[![Latest Version on Packagist](https://img.shields.io/packagist/v/nwidart/laravel-modules.svg?style=flat-square)](https://packagist.org/packages/nwidart/laravel-modules)
[![Software License](https://img.shields.io/badge/license-MIT-brightgreen.svg?style=flat-square)](LICENSE.md)
[![Build Status](https://img.shields.io/travis/nWidart/laravel-modules/master.svg?style=flat-square)](https://travis-ci.org/nWidart/laravel-modules)
[![Scrutinizer Coverage](https://img.shields.io/scrutinizer/coverage/g/nWidart/laravel-modules.svg?maxAge=86400&style=flat-square)](https://scrutinizer-ci.com/g/nWidart/laravel-modules/?branch=master)
[![SensioLabsInsight](https://img.shields.io/sensiolabs/i/25320a08-8af4-475e-a23e-3321f55bf8d2.svg?style=flat-square)](https://insight.sensiolabs.com/projects/25320a08-8af4-475e-a23e-3321f55bf8d2)
[![Quality Score](https://img.shields.io/scrutinizer/g/nWidart/laravel-modules.svg?style=flat-square)](https://scrutinizer-ci.com/g/nWidart/laravel-modules)
[![Total Downloads](https://img.shields.io/packagist/dt/nwidart/laravel-modules.svg?style=flat-square)](https://packagist.org/packages/nwidart/laravel-modules)

| **Laravel**  |  **laravel-modules** |
|---|---|
| 5.4  | ^1.0  |
| 5.5  | ^2.0  |
| 5.6  | ^3.0  |
| 5.7  | ^4.0  |

`nwidart/laravel-modules` is a Laravel package which created to manage your large Laravel app using modules. Module is like a Laravel package, it has some views, controllers or models. This package is supported and tested in Laravel 5.

This package is a re-published, re-organised and maintained version of [pingpong/modules](https://github.com/pingpong-labs/modules), which isn't maintained anymore. This package is used in [AsgardCMS](https://asgardcms.com/).

With one big added bonus that the original package didn't have: **tests**.

Find out why you should use this package in the article: [Writing modular applications with laravel-modules](https://nicolaswidart.com/blog/writing-modular-applications-with-laravel-modules).


The package will automatically register a service provider and alias.

Optionally, publish the package's configuration file by running:

``` bash
php artisan vendor:publish --provider="Nwidart\Modules\LaravelModulesServiceProvider"
```

### Autoloading

By default the module classes are not loaded automatically. You can autoload your modules using `psr-4`. For example:

``` json
{
  "autoload": {
    "psr-4": {
      "App\\": "app/",
      "Modules\\": "Modules/"
    }
  }
}
```

**Tip: don't forget to run `composer dump-autoload` afterwards.**

## Documentation

You'll find installation instructions and full documentation on [https://nwidart.com/laravel-modules/](https://nwidart.com/laravel-modules/).

## Credits

- [Nicolas Widart](https://github.com/nwidart)
- [gravitano](https://github.com/gravitano)
- [All Contributors](../../contributors)

## About Nicolas Widart

Nicolas Widart is a freelance web developer specialising on the Laravel framework. View all my packages [on my website](https://nwidart.com/), or visit [my website](https://nicolaswidart.com).


## License

The MIT License (MIT). Please see [License File](LICENSE.md) for more information.
