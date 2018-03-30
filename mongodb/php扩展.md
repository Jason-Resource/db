- [相关扩展文件，密码：uug2](https://pan.baidu.com/s/1ejj1-uXKEsGiNcgeKPsDGg)
  
```
http://php.net/manual/zh/mongodb.installation.php

http://pecl.php.net/package/mongodb

tar zxvf mongodb-1.2.3.tgz
cd mongodb-1.2.3
/usr/local/php/bin/phpize
./configure --enable-mongodb --with-php-config=/usr/local/php/bin/php-config --prefix=/usr/local/phpmongodb
make && make install


打开 php.ini 文件，在最后面添加：
extension=mongodb.so				##### 也可以指定完整路径：extension=/usr/local/php/lib/php/extensions/no-debug-non-zts-20131226/mongodb.so  


然后重启php-fpm

phpinfo()检查是否加载成功


```

- 写个文件测试一下
```php
try {

	//服务器状态
	echo '<hr>';
	$mng = new MongoDB\Driver\Manager("mongodb://localhost:27017");

    $stats = new MongoDB\Driver\Command(["dbstats" => 1]);
    $res = $mng->executeCommand("test", $stats);
    
    $stats = current($res->toArray());
    print_r($stats);

	//查询数据---前提要在数据库创建了test库，user表
	echo '<hr>';

    $query = new MongoDB\Driver\Query([]); 
     
    $rows = $mng->executeQuery("test.user", $query);
    
    foreach ($rows as $row) {
    
        echo "用户名：$row->name<br>";
    }

} catch (MongoDB\Driver\Exception\Exception $e) {

    $filename = basename(__FILE__);
    
    echo "The $filename script has experienced an error.\n"; 
    echo "It failed with the following exception:\n";
    
    echo "Exception:", $e->getMessage(), "\n";
    echo "In file:", $e->getFile(), "\n";
    echo "On line:", $e->getLine(), "\n";       
}
```
