---
layout: post
title: laravel 启动流程
categories: php laravel
---

# laravel5的启动流程

## 总体流程
    1. 加载composer的依赖

    {% highlight php %}
    <?php
    #bootstrap/autoload.php
    require __DIR__.'/../vendor/autoload.php';
    {% endhighlight %}

    2. 初始化容器对象
    {% highlight php %}
    <?php
    //bootstrap/app.php
    $app = new Illuminate\Foundation\Application(realpath(__DIR__.'/../'));
    {% endhighlight %}

    3. 绑定重要的接口实现类 

    {% highlight php %}
    <?php
    //bootstrap/app.php
    $app->singleton(Illuminate\Contracts\Http\Kernel::class,App\Http\Kernel::class);
    $app->singleton(Illuminate\Contracts\Console\Kernel::class,App\Console\Kernel::class);
    $app->singleton(Illuminate\Contracts\Debug\ExceptionHandler::class,App\Exceptions\Handler::class);
    {% endhighlight %}

    4. 处理请求，返回响应 

    {% highlight php %}
    <?php
    //public/index.php
    $kernel = $app->make(Illuminate\Contracts\Http\Kernel::class);
    $response = $kernel->handle($request = Illuminate\Http\Request::capture());
    $response->send();
    $kernel->terminate($request, $response);
    {% endhighlight %}

## 具体细节

## composer加载依赖的原理

[composer加载原理](composer_load_principle.html)

## 容器核心方法

{% highlight php %}
    <?php
    //向容器里面注册所需对象的解析器(Closure)
    public function bind($abstract,$concrete = null,$shared = false);
    //实例化所需要的对象
    public function make($abstract,array $parameters = []); 
    //make的辅助方法，真正创建对象的地方
    public function build($concrete,array $parameters = []);
    //make的辅助方法，真正创建对象的地方
    public function register($provider, $options = [], $force = false); 
{% endhighlight %}

## 初始化容器对象

{% highlight php %}
<?php
//vendor/laravel/framework/src/Illuminate/Foundation/Application.php
public function __construct($basePath = null){
    $this->registerBaseBindings();
    $this->registerBaseServiceProviders();
    $this->registerCoreContainerAliases(); 
    if($basePath){
        $this->setBasePath($basePath);
    }
}
/*
registerBaseBidings  
注册基本的对象解析器，单列化了容器对象,保存到$instances数组里面。

registerBaseServiceProviders
核心的两个ServiceProvider: EventServiceProvider,RoutingServiceProvider  

registerCoreContainerAliases  
注册容器核心的别名map

setBasePath
保存应用程序所需要的常用路径字符串 
*/
//basePath
foreach (['base', 'config', 'database', 'lang', 'public', 'storage'] as $path){
    $this->instance('path.'.$path, $this->{$path.'Path'}());
}
{% endhighlight %}
