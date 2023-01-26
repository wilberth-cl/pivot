## Simple Example
## Add Extra Fields to Laravel Pivot Table.

## Make sure you have the laravel environment set up.

+ [Laravel](https://github.com/laravel/laravel)
+ [Is required Git](https://git-scm.com/download/win)
+ [Is required Node.js](https://nodejs.org/en/)
+ [Is required Composer](https://getcomposer.org/doc/00-intro.md#installation-windows)

### Php version[^1]:
> [PHP ^8.0.2](https://sourceforge.net/projects/xampp/files/XAMPP%20Windows/)

## Immediately after cloning the repository, you need to run the following commands.
````
npm install[^2]
````
````
composer install[^2]
````

## The project contains two seeders to start with.
> IngredientSeeder & SizeSeeder
* the first time:
````
php artisan migrate --seed
````
* other times:
````
php artisan migrate:fresh --seed
````

## These fields do not replace the id() & timestamps() fields, but are part of them.

* table 'size' (model & migration)
````
$table->string('nombre',60)->unique();
$table->string('descripcion',90)->nullable();
````
* table 'ingredients' (model & migration)
````
$table->string('nombre',60)->unique();
$table->string('descripcion',90)->nullable();
````
* table 'specialties' (model & migration)
````
$table->foreignId('size_id')->constrained('sizes')
            ->onUpdate('cascade')
            ->onDelete('cascade');
$table->string('nombre',60)->unique();
$table->decimal('precio',10,3)->require();
````
* table 'specialty_ingredient' (migration)
````
$table->unsignedBigInteger('specialty_id');
            $table->unsignedBigInteger('ingredient_id');
$table->foreign('specialty_id')->references('id')->on('specialties')
            ->onDelete('cascade')
            ->onUpdate('cascade');
$table->foreign('ingredient_id')->references('id')->on('ingredients')
            ->onDelete('cascade')
            ->onUpdate('cascade');
````
> Extra Fields in 'specialty_ingredient'
~~~
$table->integer('cantidad');
$table->string('thing');
~~~
#
[^1]: The version of php is extremely important.
[^2]: Using npm update or composer update would cause some problems.
