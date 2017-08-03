# Aliyun Oss Service Provider for Laravel 5

[![Build Status](https://travis-ci.org/aliyun/aliyun-oss-php-sdk-laravel.svg?branch=master)](https://travis-ci.org/aliyun/aliyun-oss-php-sdk-laravel)
[![Coverage Status](https://coveralls.io/repos/github/aliyun/aliyun-oss-php-sdk-laravel/badge.svg?branch=master)](https://coveralls.io/github/aliyun/aliyun-oss-php-sdk-laravel?branch=master)

## laravel项目中引用该包
```
1. 安装laravel/lumen并新建laravel/lumen工程
2. 在工程的composer.json中添加
{
    "require": {
        "aliyuncs/aliyun-oss-php-sdk-laravel": "~1.2.0"
    }
}
3. 然后执行
composer update
```

##  laravel工程
```
1. 修改vendor/aliyun-oss/aliyun-oss-php-sdk-laravel/config/config.php
return [
    'id' => 'your id',
    'key' => 'your key',
    'endpoint' => 'your endpoint',
    'bucket' => 'your bucket'
];

2. 修改 config/app.php 并且register aliyunoss Service Provider.

    'providers' => array(
        // ...
        AliyunOss\Laravel\AliyunOssServiceProvider::class,
    )

3. 在config/app.php 增加aliases.

    'aliases' => array(
        // ...
        'OSS' => AliyunOss\Laravel\AliyunOssFacade::class,
    )

4. 修改routes/web.php为

Route::get('/', function()
{
    $client = App::make('aliyun-oss');
    $client->putObject("your bucket", "your object", "content you want to upload");
    $result = $client->getObject("your bucket", "your boject");
    echo $result;
});
```

## lumen工程
```
1. 修改vendor/aliyun-oss/aliyun-oss-php-sdk-laravel/config/config.php
return [
    'id' => 'your id',
    'key' => 'your key',
    'endpoint' => 'your endpoint',
    'bucket' => 'your bucket'
];

2. 在bootstrap/app.php 中注册aliyun-oss Service Providers,
    $app->register(AliyunOss\Laravel\AliyunOssServiceProvider::class);

3. 修改routes/web.php为

$app->get('/', function () use ($app) {
    $client = $app->make('aliyun-oss');
    $client->putObject('your bucket', 'your key',  "content you want to upload");
    $result = $client->getObject("your bucket", "your boject");
    echo $result;
});
```

## 运行test case
```
1. 首先设置环境变量
export OSS_ENDPOINT=''                 
export OSS_ACCESS_KEY_ID=''              
export OSS_ACCESS_KEY_SECRET=''
export OSS_BUCKET=''
2. 进入目录,执行
php vendor/bin/phpunit
```
