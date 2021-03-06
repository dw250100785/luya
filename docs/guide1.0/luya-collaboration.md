Help us improve LUYA
==================

If you like to contribute to the LUYA project you can easy follow these few steps:

1. Fork the [luyadev/luya](https://github.com/luyadev/luya) project to your account.
2. Define your working environment
3. Rebase the master
4. Create a new branch
5. Commit, push and create pull-request

Fork
------
To Fork the the [LUYA](https://github.com/luyadev/luya) project click on the FORK Button, this will create a copy of the repository on your account. After forking the repository you have to clone it into your local composer  via `git clone https://github.com/yourusername/luya`. 

![fork-luya](https://raw.githubusercontent.com/luyadev/luya/master/docs/guide1.0/img/start-collaboration-fork.jpg "Fork Luya")

> Tipps with [git clone](https://help.github.com/articles/importing-a-git-repository-using-the-command-line/).

Working environment
---------------

After successfull clone into your webserver or local computer you will find a folder `envs/dev` in your *LUYA* fork project. This is the working environment you can test all functions and modules directly against the *LUYA* source code (even of the modules).

Now the envs/dev environment needs to be configured. To do so, go into the configs folder `envs/dev/configs` and copy the file `server.php.dist` to `server.php` and modify all the components and modules to fit your needs. The most important will be the *Database Component* you have to configure matching your server settings.

```sh
cp  server.php.dist server.php
```
> Make sure your database information and setting are correctly configured in `configs/server.php`.

As we assume you have [installed composer](install.md) already on your computer now you can run `composer install` inside of your `envs/dev` folder, this will install all required depenencies and create the psr4 mappings to the local *LUYA* library files (src, modules, etc.).

After `composer install` simply run this terminal commands in your console:

1.) Navigate into your public_html folder:

```sh
cd public_html
```

2.) Install Database:

```sh
php index.php migrate
```

3.) Import data from env to database

```sh
php index.php import
```

4.) and finally after importer has been run successfully setup the envs instance and configure your user account:

```sh
php index.php setup
```

5.) Open the *public_html* folder of your dev environment in your browser`localhost/luya/envs/dev/public_html`.

> To access the admin area visit `localhost/luya/envs/dev/public_html/admin` 

Rebase your Master
------------------

We have added a little script where you can rebase your master to create new branches from an clean dev-master branch. The rebasemaster script will configure the original `luyadev/luya` repo as upstream, switch into the master branch and update the code.

> When you run the rebasemaster script for the first time, you have to add the init flag, this will configure the upstream.

```sh
./scripts/rebasemaster.sh init
```

When you have configure the upstream with init, then just fo with the following code:

```
./scripts/rebasemaster.sh
```

Create a branch
----------------

To have no conflicts with your Master branch, you should always create a new branch from the current upstream branch, so run the rebmaster master script and after that create a new branch

```sh
git checkout -b your-fix-branch master
```

Commit, Push and Pull Request
-----------------------------

You can now commit all your changes into the new branch you just created, after commiting all the changes you have to push to changes to your repository on GitHub:

```sh
git push origin
```

Visit your *LUYA* Fork on GitHub now and you will see a **PULL REQUEST** Button where you can create a Pull-Request:

![pull-request](https://raw.githubusercontent.com/luyadev/luya/master/docs/guide1.0/img/start-collaboration-pull-request.jpg "Pull request")


Informations about Design and CSS
=================================

Admin Design compile
-------------------------

To compile the styles you have to install the following tools and plugins:

* [Compass](http://compass-style.org/install/) (gem install compass)
* [Autoprefixer-rails](autoprefixer-rails) (gem install autoprefixer-rails)

> If you have not enough rights to run the command use *sudo* to run the commands, or change the permissions in the install directory of ruby.


If you have installed the tools successfull, you can now switch to the `resources` folder and run:

```sh
compass watch
```

or

```
compass compile
```

+ compile: will compile all styles once
+ watch: watching for changes in the file and runs compile automatic


Each module does have its own compass configratuons `config.rb`, so you have to run this process in each sub folder for the specific module.

> All LUYA admin styles are compose in the scss format and have to to be writen corresponding the [cssguidelines](http://cssguidelin.es).

CODING CONVENTIONS
===================

SQL
----------------------
+ Tables are singular
+ Table and column names are seperated by underscore (_)
+ The Primary Key is always ***id***
+ ***ALL*** tables have the module name as prefix. (e.g. admin_*)
+ Always use the FRONTEND-MODULE name as prefix if there are both.

table name examples
```
admin_user
admin_user_setting
admin_group
admin_user_group (ref table between user and group)
news_data
news_category
```

field name examples
```
table: admin_user
id
firstname
password_salt
group_id
```


PHP
---------
PSR2 Naming convention

(http://www.php-fig.org/psr/psr-2/)

### Example

This example encompasses some of the rules below as a quick overview:

```php
<?php
namespace Vendor\Package;

use FooInterface;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

class Foo extends Bar implements FooInterface
{
    public function sampleFunction($a, $b = null)
    {
        if ($a === $b) {
            bar();
        } elseif ($a > $b) {
            $foo->bar($arg1);
        } else {
            BazClass::bar($arg2, $arg3);
        }
    }

    final public static function bar()
    {
        // method body
    }
}
```

CSS
-----

(http://cssguidelin.es/)

JS
-----

(https://github.com/airbnb/javascript)


JSON-SCHEMA:
------------
(http://json-schema.org/latest/json-schema-core.html)
