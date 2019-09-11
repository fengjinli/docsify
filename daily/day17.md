Hzero

1、这几天的 Hzero 练习让我意识到一个真正的系统的 API 接口竟然这么多。在搭建 demo 的时候，swagger 调试页面的 api 接口看的人头疼。自己原来的小项目里的接口也只有那几个，实现一些简单的增删改查个能而已。

2、继续坚持每天都抽时间看一下 qmq。

3、其他的消息中间件：

|                | ActiveMQ               | Kafka                    | RockeMQ  | RabbitMQ                                 |
| -------------- | ---------------------- | ------------------------ | -------- | ---------------------------------------- |
| 集群           | 支持                   | 支持                     | 支持     | 支持                                     |
| 持久化         | 内存、磁盘文件、数据库 | 磁盘文件                 | 磁盘文件 | 磁盘文件                                 |
| 消费失败重试   | 支持                   | 不支持                   | 支持     | 支持                                     |
| 分布式事务消息 | 支持                   | 不支持                   | 支持     | 不支持（需要单线程发送单线程接收）       |
| 消息顺序消费   | 不支持                 | 支持单分区级别的顺序消费 | 支持     | 不支持                                   |
| 延时/定时消息  | 支持                   | 不支持                   | 支持     | 不支持                                   |
| 消息堆积       | 支持                   | 支持                     | 支持     | 支持，内存堆积达到特定阈值时会影响其性能 |
| 消息回溯       | 不支持                 | 支持                     | 支持     | 不支持                                   |
| 消息查询       | 支持                   | 不支持                   | 支持     | 不支持                                   |
| 消息轨迹       | 不支持                 | 不支持                   | 支持     | 支持                                     |
| 社区活跃度     | 高                     | 高                       | 高       | 高                                       |
| 文档           | 多                     | 多                       | 中       | 多                                       |
| 开发语言       | Java                   | scala                    | Java     | Erlang                                   |