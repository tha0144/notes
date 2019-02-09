# LaravelでのURL・HTMLリンクの生成


参照：[Laravel公式ドキュメント　4.2 ヘルパ関数](https://readouble.com/laravel/4.2/ja/helpers.html)


### route：名前付きルートへのURL生成  
```php
$url = route('routeName', $parameters = array());
```
使用例：
```php
<a href="{{ route('users.show', ['id' => $user->id]) }}">
```


### asset：アセットへのURL生成
```php
$url = asset('img/photo.jpg');
```


### link_to：URLへのHTMLリンク生成
```php
echo link_to('foo/bar', $title, $attributes = array());
```
使用例：
```php
echo link_to('foo/bar.html', 'リンクだよ！', ['class' => 'link']);
// <a href="foo/bar.html" class="link">リンクだよ！</a>
```


### link_to_route：ルートへのHTMLリンク生成
```php
echo link_to_route('route.name', $title, $parameters = array(), $attributes = array());
```
これは
```php
<a href="{{ route('route.name', $parameters) }}" $attributes>$title</a>
```
と等価。


### link_to_asset：asset版link_to_route