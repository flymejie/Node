# PHP $mysql 语句

```php
db.php   公用数据
<?php
//链接数据库
$mysql = new mysqli('localhost', 'root', '', 'tide', 3306);
//判断是否链接成功
if ($mysql->connect_errno) {
    echo '数据库链接失败,失败原因是:' . $mysql->connect_errno;
    exit();
}
//设置查询字符集
$mysql->query('set names utf8');
```

##select

```php
  $mysql -> query("select from tablename where aid=$aid");
```

## insert into

```php
$mysql -> query("insert into tablename() values ()");
```

## update

```php
$mysql -> query("update tablename set aid = '{$aid}' where aid=$aid");
```

## delete

```php
$mysql -> query("delete from tablename where aid=$aid");

批量删除
    
```







