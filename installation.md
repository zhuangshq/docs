# 安装

- [安装](#installation)
    - [服务器要求](#server-requirements)
    - [开始安装Laravel](#installing-laravel)
    - [配置](#configuration)
- [Web服务器配置](#web-server-configuration)
    - [简化URL](#pretty-urls)

<a name="installation"></a>
## 安装

> {video} 从一个视频入手开始了解Laravel是一个非常好的选择，我们(Laracasts)为初学者提供了一个[免费视频](http://laravelfromscratch.com)，你可以通过视频对Laravel有一个大致的了解。

<a name="server-requirements"></a>
### 服务器要求

Laravel框架对系统有一些要求，如果你选择使用[Laravel Homestead](/docs/5.6/homestead)提供的虚拟机，就可以跳过这些配置内容，所以我们极力推荐你使用Laravel Homestead作为你的本地开发环境。

如果你没有使用Homestead作为开发环境，那么请确保你的服务器满足这些要求：

<div class="content-list" markdown="1">
- PHP >= 7.1.3
- OpenSSL PHP扩展
- PDO PHP扩展
- Mbstring PHP扩展
- Tokenizer PHP扩展
- XML PHP扩展
- Ctype PHP扩展
- JSON PHP扩展
</div>

<a name="installing-laravel"></a>
### 开始安装Laravel

Laravel使用[Composer](https://getcomposer.org)来管理依赖，所以必须安装Composer，才能正常使用Laravel框架。

#### 通过Laravel Installer安装

首先，通过Composer安装Laravel installer：

    composer global require "laravel/installer"

为了能快捷地使用Composer命令，请确保Composer的`vendor/bin`目录已经添加到你的系统中的`$PATH`变量中， 在不同的操作系统中，这个目录所在的位置也不同，如：

<div class="content-list" markdown="1">
- macOS: `$HOME/.composer/vendor/bin`
- GNU / Linux 发行套件: `$HOME/.config/composer/vendor/bin`
</div>

安装完Laravel框架之后，你就可以使用`laravel new`命令在指定位置创建一个Laravel的实例。例如，执行`laravel new blog`命令将会在当前目录下创建一个新的目录`blog`，这个目录将会包含所有在你已经安装的Laravel依赖：

    laravel new blog

#### 通过Composer Create-Project命令安装

你也可以选择通过Composer的`create-project`命令来安装Laravel，具体步骤是在命令行中执行以下指令：

    composer create-project --prefer-dist laravel/laravel blog "5.6.*"

#### Local Development Server

If you have PHP installed locally and you would like to use PHP's built-in development server to serve your application, you may use the `serve` Artisan command. This command will start a development server at `http://localhost:8000`:

    php artisan serve

Of course, more robust local development options are available via [Homestead](/docs/{{version}}/homestead) and [Valet](/docs/{{version}}/valet).

<a name="configuration"></a>
### Configuration

#### Public Directory

After installing Laravel, you should configure your web server's document / web root to be the `public` directory. The `index.php` in this directory serves as the front controller for all HTTP requests entering your application.

#### Configuration Files

All of the configuration files for the Laravel framework are stored in the `config` directory. Each option is documented, so feel free to look through the files and get familiar with the options available to you.

#### Directory Permissions

After installing Laravel, you may need to configure some permissions. Directories within the `storage` and the `bootstrap/cache` directories should be writable by your web server or Laravel will not run. If you are using the [Homestead](/docs/{{version}}/homestead) virtual machine, these permissions should already be set.

#### Application Key

The next thing you should do after installing Laravel is set your application key to a random string. If you installed Laravel via Composer or the Laravel installer, this key has already been set for you by the `php artisan key:generate` command.

Typically, this string should be 32 characters long. The key can be set in the `.env` environment file. If you have not renamed the `.env.example` file to `.env`, you should do that now. **If the application key is not set, your user sessions and other encrypted data will not be secure!**

#### Additional Configuration

Laravel needs almost no other configuration out of the box. You are free to get started developing! However, you may wish to review the `config/app.php` file and its documentation. It contains several options such as `timezone` and `locale` that you may wish to change according to your application.

You may also want to configure a few additional components of Laravel, such as:

<div class="content-list" markdown="1">
- [Cache](/docs/{{version}}/cache#configuration)
- [Database](/docs/{{version}}/database#configuration)
- [Session](/docs/{{version}}/session#configuration)
</div>

<a name="web-server-configuration"></a>
## Web Server Configuration

<a name="pretty-urls"></a>
### Pretty URLs

#### Apache

Laravel includes a `public/.htaccess` file that is used to provide URLs without the `index.php` front controller in the path. Before serving Laravel with Apache, be sure to enable the `mod_rewrite` module so the `.htaccess` file will be honored by the server.

If the `.htaccess` file that ships with Laravel does not work with your Apache installation, try this alternative:

    Options +FollowSymLinks -Indexes
    RewriteEngine On

    RewriteCond %{REQUEST_FILENAME} !-d
    RewriteCond %{REQUEST_FILENAME} !-f
    RewriteRule ^ index.php [L]

#### Nginx

If you are using Nginx, the following directive in your site configuration will direct all requests to the `index.php` front controller:

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

Of course, when using [Homestead](/docs/{{version}}/homestead) or [Valet](/docs/{{version}}/valet), pretty URLs will be automatically configured.
