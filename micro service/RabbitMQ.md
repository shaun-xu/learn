##  为什么用MessageQueue

* 什么场景下用过MQ(秒杀，发送)
* 什么场景下要用到可靠性投递，什么时候用快速发送
* 可靠性投递用的什么方案

##  AMQP 核心概念

<img src="/Users/xxp/Library/Application Support/typora-user-images/image-20200817154210006.png" alt="image-20200817154210006" style="zoom:30%;" />

### 1） server

> 又称为broker,接受客户端连接，实现amqp实体服务



### 2)  Connection

>  连接，应用程序与broker建立的网络连接



### 3)  Channel

> 网络通道，几乎所有的操作都在channel中进行的，是进行消息帝乡的通道，客户端可以建立多个通道，每一个channel表示一个会话任务



### 4) Message

> 服务器和应用程序之间传递数据的载体，有properties(消息属性，用来修饰消息，比如优先级，延时投递等)和body(消息体)

### 5) Virtual host(虚拟主机)

> 是一个逻辑概念， 最上层的消息路由，一个虚拟主机中可以包含多个exchange和queue，但是一个虚拟主机中不能有名称相同的exchange和queue

### 6） exchange(交换机)

>  消息直接投递在交换机上，然后交换机根据消息的路由key路由到对应绑定的队列(queue)上。

* 直接交换机

  key-队列1

* 主题交换机

  Key.* |# - 队列

