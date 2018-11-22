# yii2-redis-pub-sub
基于yii2通过redis的订阅／发布者模式实现的消息队列

# install
- 安装phpredis扩展
- 安装代码
``` php
composer require --prefer-dist hollisho/yii2-redis-pub-sub
```

# usage
- 配置文件
``` php
'redisPubSub'=>[
    'class' => 'hollisho\redis_pub_sub\RedisPubSub',
    'connect' => [
        'class' => 'yii\redis\Connection',
        'hostname' => '127.0.0.1',
        'port' => 6379,
        'database' => 0,
        'password' => '',
        'connectionTimeout' => 20,
    ]
],
```
- 使用
```php
//　前台发送
/* @var $redisPubSub RedisPubSub */
$redisPubSub = \Yii::$app->redisPubSub;
$redisPubSub->publish('test', 'xxxxxxxxxxxxxxx');

// console里面监听，并且处理，设置监听不超时
/* @var $redisPubSub RedisPubSub */
$redisPubSub = \Yii::$app->redisPubSub;
$redisPubSub->setOptReadTimeout(-1);
$redisPubSub->subscribe('test', function($instance, $channelName, $message) {
    var_dump($message);
});
```
