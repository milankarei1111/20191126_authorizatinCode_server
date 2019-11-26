# OAuth 2.0 passport(授權碼模式) 
----
## 影片教學
 [laravel6 授权码 1 配置]
(https://www.bilibili.com/video/av74879198?p=7)

[laravel6 授权码 2 ]
(https://www.bilibili.com/video/av74879198?p=8)

----
### 實作:服務器端(微信 ex:lisan.com) 

時間 01:22 

http://localhost:9988

----
## 準備工作
1. 建立專案
2. .env 資料庫配置 *如果你在同一台機器上,請在config文件夾配置你的項目,避免環境變量衝突

3. 修改資料庫默認字串長度,因應後面套件包產生的表名長度會過長 AppServiceProvider 的 boot() 加入 Schema::defaultStringLength(191);

4. composer require laravel/passport
5. Laravel\Passport\HasApiTokens Trait	將此特徵引入App\Usr模型中

----
## 安裝前端必備(腳手架)

** 事前須先下載node

* 建立專案
* composer require laravel/ui
* php artisan ui vue --auth
* npm install cnpm -g --registry=https://registry.npm.taobao.org	
* cnpm install
* cnpm run prod

----
## 安裝Guzzle套件包發送http請求 
* composer require guzzlehttp/guzzle

----
## 配置passport認證
* config/auth.php 

   'api' => ['driver' => 'passport']

----
## 遷移資料庫

* php artisan migrate // 創建表來儲存客戶端和 access_token
* php artisan passport:keys // 加密生成的access_token

----
## 註冊路由 (AuthServiceProvider文件夾)
    Passport::routes();

>加入過期時間

    Passport::tokensExpireIn(now()->addDays(15));
    Passport::refreshTokensExpireIn(now()->addDays(60));

----
## 創建客戶端(嗶哩嗶哩)
    php artisan passport:client

        Which user ID should the client be assigned to?: 自動設置

        What should we name the client?: bili

        Where should we redirect the request after authorization?:
	    http://localhost:9987/auth/callback
