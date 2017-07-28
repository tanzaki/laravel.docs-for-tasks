# Installation

- [Installation](#installation)
    - [Server Requirements](#server-requirements)
    - [Installing Laravel](#installing-laravel)

<a name="installation"></a>
## Installation

> {video} Are you a visual learner? Laracasts provides a [free, thorough introduction to Laravel](http://laravelfromscratch.com) for newcomers to the framework. It's a great place to start your journey.

<a name="server-requirements"></a>
### Server Requirements
 
The Laravel framework has a few system requirements. Of course, all of these requirements are satisfied by the

### XAMPP Web Server

https://bitnami.com/redirect/to/153273/bitnami-wampstack-5.6.31-0-windows-x64-installer.exe

[![XAMPP](http://i.imgur.com/KuCYijn.png)](https://bitnami.com/redirect/to/153273/bitnami-wampstack-5.6.31-0-windows-x64-installer.exe)

so it's highly recommended that you use XAMPP as your local Laravel development environment.

However, if you are not using XAMPP, you will need to make sure your server meets the following requirements:

- PHP >= 5.6.4
- OpenSSL PHP Extension
- PDO PHP Extension
- Mbstring PHP Extension
- Tokenizer PHP Extension
- XML PHP Extension

<a name="installing-laravel"></a>
### Installing Laravel

Laravel utilizes [Composer](https://getcomposer.org) to manage its dependencies. So, before using Laravel, make sure you have Composer installed on your machine.

You may install Laravel by issuing the Composer `create-project` command in your terminal:

    composer create-project --prefer-dist laravel/laravel blog

#### Local Development Server

If you have PHP installed locally and you would like to use PHP's built-in development server to serve your application, you may use the `serve` Artisan command. This command will start a development server at `http://localhost:8000`:

    cd blog
    php artisan serve
