- [扩展下载，密码：5ial](https://pan.baidu.com/s/1jz1mjQ9XSugmDTYPVli89w)

```
扩展包下载
http://pecl.php.net/package/redis


安装PHP的 redis 扩展
tar zxvf redis-3.1.0.tgz
cd redis-3.1.0
/usr/local/php/bin/phpize
./configure --enable-redis --with-php-config=/usr/local/php/bin/php-config --prefix=/usr/local/phpredis
make && make install


打开 php.ini 文件，在最后面添加：
extension=redis.so				##### 也可以指定完整路径：extension=/usr/local/php/lib/php/extensions/no-debug-non-zts-20131226/redis.so  


然后重启php-fpm

phpinfo()检查是否加载成功


-------------------------------------------------------------------------------------------------------------------------------------------------
写个文件测试一下：
<?php
$redis = new Redis();
$redis->connect('127.0.0.1', 6379);

echo "Server is running: " . $redis->ping() . '<br>';

$redis->SET('name', 'jason');

echo $redis->GET('name');
?>

使用文档
https://github.com/phpredis/phpredis/#readme
```
