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

如果你在本地安装了PHP环境，那么你可以使用PHP内置的开发服务器来启动你的web应用。具体操作是使用Artisan的`serve`命令来启动PHP内置服务器，地址为：`http://localhost:8000`，在命令行中执行以下命令：

    php artisan serve

使用[Homestead](/docs/{{version}}/homestead)和[Valet](/docs/{{version}}/valet)支持更多的开发配置。

<a name="configuration"></a>
### 配置

#### Public目录

安装完Laravel后，将`public`配置为web的根目录。 该目录下的`index.php`将会作为所有HTTP请求的入口文件。

#### 配置文件

Laravel框架中的所有配置文件都放置在`config`目录下，所有的配置都在配置文件中，你应该对这些配置文件有所熟悉，并尽可能掌握你所需要的配置文件。

#### 目录权限

安装完Laravel后，为了让Laravel正常运作，你可能需要对文件及目录的读写权限进行配置，比如web服务器应该对`storage`目录下的文件和`bootstrap/cache`具有读写权限。假设你使用了[Homestead](/docs/{{version}}/homestead)虚拟机作为开发环境，那你就可以跳过权限配置的步骤了。

#### 应用程序密钥

接下来配置应用程序密钥，如果你是通过Composer或者Laravel installer安装Laravel的话，你就可以跳过这个步骤了(安装过程中Laravel已经自动地通过`php artisan key:generate`命令完成了这个操作)。

首先将`.env.example`文件重命名为`.env`，想办法生成一个长度为32的随机字符串，将这个字符串配置到`.env`环境配置文件的应用程序密钥中。 **如果没有设置该密钥，你所有的用户会话和加密数据的安全性都无法保障！**

#### 更多配置

除了上面所说的配置以外，其他配置对Laravel来说都不是必须的，你可以直接开始开发项目。但是你可以了解一下`config/app.php`文件及其文档，你可能需要根据你的项目进行一些个性化配置，如`timezone`，`locale`等。

更多配置：

<div class="content-list" markdown="1">
- [Cache](/docs/{{version}}/cache#configuration)
- [Database](/docs/{{version}}/database#configuration)
- [Session](/docs/{{version}}/session#configuration)
</div>

<a name="web-server-configuration"></a>
## Web服务器配置

<a name="pretty-urls"></a>
### 简化URL

#### Apache

Laravel项目中包含了`public/.htaccess`文件，通过修改这个文件的配置，你可以在URL中取出`index.php`。 在Apache环境下，需要修改Apache的配置文件来启用`mod_rewrite`模块，这样的话`.htaccess`文件中的配置才会生效。

如果Laravel自带的`.htaccess`文件配置后不生效，你可以用以下配置替换配置文件中的内容：

    Options +FollowSymLinks -Indexes
    RewriteEngine On

    RewriteCond %{REQUEST_FILENAME} !-d
    RewriteCond %{REQUEST_FILENAME} !-f
    RewriteRule ^ index.php [L]

#### Nginx

如果你使用的是Nginx服务器，那么以下配置将会自动将所有HTTP请求指向你的入口文件`index.php`：

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

还是那句话，如果你使用了[Homestead](/docs/{{version}}/homestead)或者[Valet](/docs/{{version}}/valet)，你可以跳过这个步骤。
