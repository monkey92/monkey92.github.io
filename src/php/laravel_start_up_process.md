### laravel5的启动流程

#### 总体流程

1. 加载composer的依赖  

    ```php
    #bootstrap/autoload.php
    require __DIR__.'/../vendor/autoload.php';
    ```
2. 初始化容器对象  

    ```php
    #bootstrap/app.php
    $app = new Illuminate\Foundation\Application(realpath(__DIR__.'/../'));
    ```
3. 绑定重要的接口实现类 

    ```php
    #bootstrap/app.php
    $app->singleton(Illuminate\Contracts\Http\Kernel::class,App\Http\Kernel::class);
    $app->singleton(Illuminate\Contracts\Console\Kernel::class,App\Console\Kernel::class);
    $app->singleton(Illuminate\Contracts\Debug\ExceptionHandler::class,App\Exceptions\Handler::class);
    ```
4. 处理请求，返回响应  

    ```php
    #public/index.php
    $kernel = $app->make(Illuminate\Contracts\Http\Kernel::class);
    $response = $kernel->handle($request = Illuminate\Http\Request::capture());
    $response->send();
    $kernel->terminate($request, $response);
    ```

#### 具体细节

##### composer加载依赖的原理

[composer\_加载原理](composer_load_principle.md)

##### 容器核心方法

* public function bind\($abstract,$concrete = null,$shared = false\); //向容器里面注册所需对象的解析器\(Closure\)
* public function make\($abstract,array $parameters = \[\]\); //实例化所需要的对象
* public function build\($concrete,array $parameters = \[\]\);//make的辅助方法，真正创建对象的地方
* public function register\($provider, $options = \[\], $force = false\); //注册serviceprovider

##### 初始化容器对象

* constructor 
 
    ```php
    #vendor/laravel/framework/src/Illuminate/Foundation/Application.php
    public function __construct($basePath = null){
        $this->registerBaseBindings();
        $this->registerBaseServiceProviders();
        $this->registerCoreContainerAliases(); 
        if($basePath){
            $this->setBasePath($basePath);
        }
    }
    ```
* registerBaseBidings  
    注册基本的对象解析器，单列化了容器对象,保存到$instances数组里面。

* registerBaseServiceProviders  
    注册基本的ServiceProvider，[个人理解的ServiceProvider](laravel_service_provider.md)  
    核心的两个ServiceProvider: EventServiceProvider,RoutingServiceProvider  

* registerCoreContainerAliases  
    注册容器核心的别名map

* setBasePath
    保存应用程序所需要的常用路径字符串  
    ```php
    foreach (['base', 'config', 'database', 'lang', 'public', 'storage'] as $path){
        $this->instance('path.'.$path, $this->{$path.'Path'}());
    }
    ```

##### 处理请求返回响应

* [laravel请求处理](laravel_process_request.md)  
* [laravel响应处理](laravel_process_response.md)


