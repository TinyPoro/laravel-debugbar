## Laravel Debugbar
[![Packagist License](https://poser.pugx.org/barryvdh/laravel-debugbar/license.png)](http://choosealicense.com/licenses/mit/)
[![Latest Stable Version](https://poser.pugx.org/barryvdh/laravel-debugbar/version.png)](https://packagist.org/packages/barryvdh/laravel-debugbar)
[![Total Downloads](https://poser.pugx.org/barryvdh/laravel-debugbar/d/total.png)](https://packagist.org/packages/barryvdh/laravel-debugbar)

### Ghi chú cho phiên bản 3: Hiện bạn đã có thể require (yêu cầu) gói Debugbar  nhưng vẫn cần để APP_DEBUG = true như mặc định!

### Hãy sử dụng [nhánh 2.4](https://github.com/barryvdh/laravel-debugbar/tree/2.4) cho các phiên bản laravel 5.5 đổ xuống!

Đây là gói để tích hợp [PHP Debug Bar](http://phpdebugbar.com/)(1 cái để tích hợp vào các project php, có thể thể hiện thông tin dữ liệu bất kỳ phần nào của ứng dụng của mình, kiểu kiểu vardump), vào Laravel. Nó báo gồm 1 service provider để đăng ký và gắn với đầu ra. Bạn có thể publish assets(Package có thể có assets như là JavaScript, CSS, và images. Publish assets là đẩy nó vào thư mục public bằng publisher) cúng như cấu hình nó qua laravel.
Nó khởi động vài Collector để làm việc với Laravel cũng như thực hiện 1 cặp DataCollectors tùy chỉnh, riêng cho Laravel.
 Nó được cấu hình để thể hiện điều hướng và jquery ajax request.
Đọc [tài liệu](http://phpdebugbar.com/docs/) để biết thêm chi tiết các lựa chọn cấu hình. 

![Screenshot](https://cloud.githubusercontent.com/assets/973269/4270452/740c8c8c-3ccb-11e4-8d9a-5a9e64f19351.png)

Note: Lưu ý: chỉ sử dụng debugbar trong phát triển. Nó phải thu thập dữ liệu nên sẽ làm chậm ứng dụng. Vì vậy khi thấy ứng dụng có dấu hiệu chậm, tắt 1 số collector thử xem. 

Gói này nó bao gồm 1 vài collectors tùy chỉnh: 
 - QueryCollector: hiện tất cả query bao gồm cả ràng buộc và thowfig ian. 
 - RouteCollector: hiện thông tin về route hiện tại. 
 - ViewCollector: hiện view được load hiện tại(có thể hiện thêm dữ liệu được chia sẻ)
 - EventsCollector: hiện tất cả event 
 - LaravelCollector: hiện phiên bản laravel và loại môi trường(mặc đinh sẽ được tắt) 
 - SymfonyRequestCollector: thay thế RequestCollector với nhiều thông tin hơn về request/response. 
 - LogsCollector: hiện thị log mới nhất trong thư mục storage(mặc định tắt) 
 - FilesCollector: hiện các file được include/require bởi php(mặc định tắt) 
 - ConfigCollector: hiện các giá trị trong các file config(mặc định tắt) 
 - CacheCollector: hiện tất cả các sự kiên cache (mặc định tắt) 

Khởi động các collectors sau cho Laravel: 
 - LogCollector: hiện tất cả các thông báo Log. 
 - SwiftMailCollector và SwiftLogCollector cho Mail. 

Và các collector mặc định: 
 - PhpInfoCollector 
 - MessagesCollector 
 - TimeDataCollector (bao gồm thời gian khởi động và ứng dụng) 
 - MemoryCollector 
 - ExceptionsCollector 

Nó cũng cung cấp một giao diện Facade để dễ dàng log ra thông báo, ngoại lệ cũng như thời gian. 

## Cài đặt: 

Require gói này với composer. Như đã nói bên trên, require cho môi trường dev thôi 

```shell
composer require barryvdh/laravel-debugbar --dev
```

Laravel 5.5 sử dụng gói Auto-Discovery, vì vậy bạn không cần phải thêm service provider thủ công.

Debugbar sẽ được bật khi `APP_DEBUG` là `true`. 

> Nếu bạn sử dụng catch_all /fallback route thì phải load debugbar service provider trước app service provider. 

### Laravel 5.5+:

Nếu không xài auto-discovery, thì thêm service provider vào mảng providers trong config/app.php dòng như sau

```php
Barryvdh\Debugbar\ServiceProvider::class,
```

Nếu bạn muốn sử dụng facade để in thông báo, thêm dòng sau vào facade cũng trong app.php luôn 

```php
'Debugbar' => Barryvdh\Debugbar\Facade::class,
```

Nó sẽ được bật mặc định khi App_debug = true(cái này nhắc nhiều voãi). Bạn có thể ghi đè lại trong config(`debugbar.enabled`) hoặc bằng cài đặt `debugbar_enabled` trong file `env`. Xem thêm các lựa chọn trong `config/debuggar.php`.
Bạn cũng có thể cài trong cấu hình config của bạn nếu bạn muốn thêm/bỏ các file vendor(FontAwesome, HighlightJs, Jquery). Nếu bạn đã sử dụng chúng cho trang của mình, đặt nó về false.
Bạn cũng có thể chỉ hiện js hoặc css vendor, bằng cách cài nó thành 'js' hoặc 'css'. Highlight.js yêu cầu cả css và js, vì vậy hãy đặt nó thành true để làm nổi bật cú pháp. 

Sao chép gói cấu hình đến cấu hình trên local bằng lệnh publish: 

```shell
php artisan vendor:publish --provider="Barryvdh\Debugbar\ServiceProvider"
```

### Lumen:

Đối với Lumen, đăng ký 1 provider khác ở trong file `bootstrap/app.php`:

```php
if (env('APP_DEBUG')) {
 $app->register(Barryvdh\Debugbar\LumenServiceProvider::class);
}
```

Để thay đổi cấu hình, sao chép tệp đến thư mục cấu hình của bạn và khởi động nó: 

```php
$app->configure('debugbar');
```

## Sử dụng: 

Ngay lúc này, bạn có thể thêm các thông báo bằng cách sử dụng Facade(khi nó được thêm vào), sử dụng mức prs-3(sửa lỗi, thông tin, chú ý, thông báo, lỗi, quan trọng, cảnh báo, khẩn cấp): 

```php
Debugbar::info($object);
Debugbar::error('Error!');
Debugbar::warning('Watch out…');
Debugbar::addMessage('Another message', 'mylabel');
```

Và bạn cũng có thể bắt đầu/ dừng tính giờ: 

```php
Debugbar::startMeasure('render','Time for rendering');
Debugbar::stopMeasure('render');
Debugbar::addMeasure('now', LARAVEL_START, microtime(true));
Debugbar::measure('My long operation', function() {
    // Do something…
});
```

Hoặc bạn cũng có thể đưa ra những ngoại lệ: 

```php
try {
    throw new Exception('foobar');
} catch (Exception $e) {
    Debugbar::addThrowable($e);
}
```

Ngoài ra, có những hàm hỗ trợ mà hay được sử dụng như: 

```php
// All arguments will be dumped as a debug message
debug($var1, $someString, $intValue, $object);

start_measure('render','Time for rendering');
stop_measure('render');
add_measure('now', LARAVEL_START, microtime(true));
measure('My long operation', function() {
    // Do something…
});
```

Nếu bạn muốn bạn có thể tự thêm DataCollectors của riêng bạn, thống qua Container hoặc Facade: 

```php
Debugbar::addCollector(new DebugBar\DataCollector\MessagesCollector('my_messages'));
//Or via the App container:
$debugbar = App::make('debugbar');
$debugbar->addCollector(new DebugBar\DataCollector\MessagesCollector('my_messages'));
```

Mặc định, debugbar được đưa vào ngay trước thẻ `</body>`. Tuy nhiên nếu bạn muốn tự thêm debugbar, đặt lựa chọn cài đặt inject thành false và tử sử dụng renderer theo hướng dẫn từ http://phpdebugbar.com/docs/rendering.html

```php
$renderer = Debugbar::getJavascriptRenderer();
```

Lưu ý: không sử dụng cái auto-inject, nó sẽ tắt cái thông tin request, bởi vì nó sẽ được thêm vào sau khi có response. 
Thay vào đó bạn có thể thêm datacollector default_request vào cấu hình, 

## Bật/ tắt trong lúc chạy
Bạn có thể bật tắt debugbar trong lúc chạy như sau

```php
\Debugbar::enable();
\Debugbar::disable();
```

Lưu ý: ngay khi được bật, các collectors sẽ được thêm vào(có thể gây tốn thêm chi phí tài nguyên), do vậy nếu muốn sử dụng debugbar trong môi trướng phát triển, tắt chúng trong cấu hình và chỉ bật lên khi cần thiết.


## Tích hợp nhánh

Laravel debugbar gồm 2 nhánh mở rộng.Chúng đã được kiểm tra với [rcrowe/TwigBridge](https://github.com/rcrowe/TwigBridge) 0.6.x

Thêm những mở rộng sau vào file config/extensions.php trong twigbridge của bạn( hoặc đăng ký mở rộng thủ công bằng tay) 

```php
'Barryvdh\Debugbar\Twig\Extension\Debug',
'Barryvdh\Debugbar\Twig\Extension\Dump',
'Barryvdh\Debugbar\Twig\Extension\Stopwatch',
```

Mở rộng dump sẽ thay thế các [hàm dump](http://twig.sensiolabs.org/doc/functions/dump.html) để đưa ra các biến sử dụng dataformatter. Mở rộng debug thêm hàm `debug()` có tác dụng truyển biến tới các Message Collector, thay vì hiển thị trực tiếp trong mẫu template. Nó sẽ xuất ra tất cả các đối số, hoặc cũng có khi rỗng, tất cả các biế.n

```twig
{{ debug() }}
{{ debug(user, categories) }}
```

Mở rộng Stopwatch thêm một [stopwatch tag](http://symfony.com/blog/new-in-symfony-2-4-a-stopwatch-tag-for-twig)  tương tự như Symfony/Silex Twigbridge.

```twig
{% stopwatch "foo" %}
    …some things that gets timed
{% endstopwatch %}
```
