# lumen-cache
路由缓存

## 简介

本组件是为了解决lumen不支持路由缓存的问题

## 使用说明

首先创建文件夹`bootstrap/cache`，然后创建`bootstrap/cache/.gitignore`，输入以下内容

```gitignore
*
!.gitignore
```

接下来修改`bootstrap/app.php` 中加载路由的地方。

框架最开始是这样的：

```php
$app->router->group([
    'namespace' => 'App\Http\Controllers',
], function ($router) {
    require __DIR__.'/../routes/web.php';
});
```

修改后变成这样：

```php
if (file_exists($app->basePath("bootstrap/cache/router.php"))) {
    require_once $app->basePath("bootstrap/cache/router.php");
} else {
    $app->router->group([
        'namespace' => 'App\Http\Controllers',
    ], function ($router) {
        require __DIR__.'/../routes/web.php';
    });
}
```

这样就完成了。

然后我们就可以查看命令：

```bash
$ php artisan
Laravel Framework Lumen (6.3.3) (Laravel Components ^6.0)

Usage:
  command [options] [arguments]

Options:
  -h, --help            Display this help message
  -q, --quiet           Do not output any message
  -V, --version         Display this application version
      --ansi            Force ANSI output
      --no-ansi         Disable ANSI output
  -n, --no-interaction  Do not ask any interactive question
      --env[=ENV]       The environment the command should run under
  -v|vv|vvv, --verbose  Increase the verbosity of messages: 1 for normal output, 2 for more verbose output and 3 for debug

Available commands:
  help                Displays help for a command
  list                Lists commands
  migrate             Run the database migrations
 route
  route:cache         Create a route cache file for faster route registration
  route:clear         Remove the route cache file
  route:list          List all registered routes
```

有什么问题可以来 issus.
