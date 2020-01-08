# yunbuye/thinkphp-model-factory
## thinkphp 的模型工厂
方便的批量生成模型的模拟数据

## 说明
此为[laravel的模型工厂](https://learnku.com/docs/laravel/6.x/database-testing/5185#writing-factories)的thinkphp的适配版，大部分功能都可用（需要手动创建工厂文件，定义数据库连接不可用）

## 使用
1. 安装  
```bash
composer require yunbuye/thinkphp-model-factory 
```

1. 建立目录  
在根目录建立 "./database/factories" 工厂目录

1. 使用  
    1. 定义工厂，在工厂目录 新建和编写工厂
        ```php
        use Faker\Generator as Faker;
        
        $factory->define(App\User::class, function (Faker $faker) {
            return [
                'name' => $faker->name,
                'email' => $faker->unique()->safeEmail,
                'email_verified_at' => now(),
                'password' => '$2y$10$TKh8H1.PfQx37YgCzwiKb.KjNyWgaHb9cbcoQgdIVFlYg7B77UdFm', // secret
                'remember_token' => Str::random(10),
            ];
        });
        ```
   1. 在模型中使用工厂
        ```php
        public function testDatabase()
        {
            $user = factory(App\User::class)->make();
            
            // 在测试中使用模型...
        }
        ```
    
1. 语言  
默认中文zh_CN    
可以添加配置 app.faker_locale 到配置文件进行定义
