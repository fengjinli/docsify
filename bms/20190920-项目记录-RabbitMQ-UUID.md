## 0920

### RabbitMQ

- 删除队列操作

~~~java
访问 http://{rabbitmq 安装 IP}:15672，帐号 guest，密码 guest（也可以使用自己创建的帐号）。

登录后访问 http://{rabbitmq 安装 IP}:15672/#/queues，这里可以看到你创建的所有的 Queue，

选中某一个 Queue，下方有个 Delete/Purge，展开，选择 purge 即可。

注意：Delete 表示 delete 这个 Queue，而 purge 表示清除所有暂存在 Queue 里面的消息。
~~~

**参考：**[链接](https://blog.csdn.net/wangnan9279/article/details/54694991)

### 项目启动时 RabbitMQ 报错

- 描述：报错信息如下

<div align=center><img src="https://mortre-picgo.oss-cn-beijing.aliyuncs.com/bms-rabbitmq1.png"/></div>
<div align=center><img src="https://mortre-picgo.oss-cn-beijing.aliyuncs.com/bms-rabbitmq2.png"/></div>
- 完整信息如下：

~~~java
2019-09-20 09:44:27.526  INFO 14864 --- [cTaskExecutor-1] o.s.a.r.c.CachingConnectionFactory       : Attempting to connect to: [127.0.0.1:15672]
2019-09-20 09:44:32.539 ERROR 14864 --- [cTaskExecutor-1] o.s.a.r.l.SimpleMessageListenerContainer : Failed to check/redeclare auto-delete queue(s).

org.springframework.amqp.AmqpIOException: java.io.IOException
	at org.springframework.amqp.rabbit.support.RabbitExceptionTranslator.convertRabbitAccessException(RabbitExceptionTranslator.java:71) ~[spring-rabbit-2.0.8.RELEASE.jar:2.0.8.RELEASE]
	at org.springframework.amqp.rabbit.connection.AbstractConnectionFactory.createBareConnection(AbstractConnectionFactory.java:504) ~[spring-rabbit-2.0.8.RELEASE.jar:2.0.8.RELEASE]
	at org.springframework.amqp.rabbit.connection.CachingConnectionFactory.createConnection(CachingConnectionFactory.java:628) ~[spring-rabbit-2.0.8.RELEASE.jar:2.0.8.RELEASE]
	at org.springframework.amqp.rabbit.connection.ConnectionFactoryUtils.createConnection(ConnectionFactoryUtils.java:240) ~[spring-rabbit-2.0.8.RELEASE.jar:2.0.8.RELEASE]
	at org.springframework.amqp.rabbit.core.RabbitTemplate.doExecute(RabbitTemplate.java:1816) ~[spring-rabbit-2.0.8.RELEASE.jar:2.0.8.RELEASE]
	at org.springframework.amqp.rabbit.core.RabbitTemplate.execute(RabbitTemplate.java:1790) ~[spring-rabbit-2.0.8.RELEASE.jar:2.0.8.RELEASE]
	at org.springframework.amqp.rabbit.core.RabbitTemplate.execute(RabbitTemplate.java:1771) ~[spring-rabbit-2.0.8.RELEASE.jar:2.0.8.RELEASE]
	at org.springframework.amqp.rabbit.core.RabbitAdmin.getQueueProperties(RabbitAdmin.java:345) ~[spring-rabbit-2.0.8.RELEASE.jar:2.0.8.RELEASE]
	at org.springframework.amqp.rabbit.listener.AbstractMessageListenerContainer.redeclareElementsIfNecessary(AbstractMessageListenerContainer.java:1604) ~[spring-rabbit-2.0.8.RELEASE.jar:2.0.8.RELEASE]
	at org.springframework.amqp.rabbit.listener.SimpleMessageListenerContainer$AsyncMessageProcessingConsumer.run(SimpleMessageListenerContainer.java:995) [spring-rabbit-2.0.8.RELEASE.jar:2.0.8.RELEASE]
	at java.lang.Thread.run(Thread.java:748) [na:1.8.0_191]
Caused by: java.io.IOException: null
	at com.rabbitmq.client.impl.AMQChannel.wrap(AMQChannel.java:126) ~[amqp-client-5.4.3.jar:5.4.3]
	at com.rabbitmq.client.impl.AMQChannel.wrap(AMQChannel.java:122) ~[amqp-client-5.4.3.jar:5.4.3]
	at com.rabbitmq.client.impl.AMQConnection.start(AMQConnection.java:373) ~[amqp-client-5.4.3.jar:5.4.3]
	at com.rabbitmq.client.ConnectionFactory.newConnection(ConnectionFactory.java:1104) ~[amqp-client-5.4.3.jar:5.4.3]
	at com.rabbitmq.client.ConnectionFactory.newConnection(ConnectionFactory.java:1054) ~[amqp-client-5.4.3.jar:5.4.3]
	at com.rabbitmq.client.ConnectionFactory.newConnection(ConnectionFactory.java:994) ~[amqp-client-5.4.3.jar:5.4.3]
	at org.springframework.amqp.rabbit.connection.AbstractConnectionFactory.createBareConnection(AbstractConnectionFactory.java:457) ~[spring-rabbit-2.0.8.RELEASE.jar:2.0.8.RELEASE]
	... 9 common frames omitted
Caused by: com.rabbitmq.client.ShutdownSignalException: connection error
	at com.rabbitmq.utility.ValueOrException.getValue(ValueOrException.java:66) ~[amqp-client-5.4.3.jar:5.4.3]
	at com.rabbitmq.utility.BlockingValueOrException.uninterruptibleGetValue(BlockingValueOrException.java:36) ~[amqp-client-5.4.3.jar:5.4.3]
	at com.rabbitmq.client.impl.AMQChannel$BlockingRpcContinuation.getReply(AMQChannel.java:494) ~[amqp-client-5.4.3.jar:5.4.3]
	at com.rabbitmq.client.impl.AMQConnection.start(AMQConnection.java:315) ~[amqp-client-5.4.3.jar:5.4.3]
	... 13 common frames omitted
Caused by: java.io.EOFException: null
	at java.io.DataInputStream.readUnsignedByte(DataInputStream.java:290) ~[na:1.8.0_191]
	at com.rabbitmq.client.impl.Frame.readFrom(Frame.java:91) ~[amqp-client-5.4.3.jar:5.4.3]
	at com.rabbitmq.client.impl.SocketFrameHandler.readFrame(SocketFrameHandler.java:164) ~[amqp-client-5.4.3.jar:5.4.3]
	at com.rabbitmq.client.impl.AMQConnection$MainLoop.run(AMQConnection.java:596) ~[amqp-client-5.4.3.jar:5.4.3]
	... 1 common frames omitted

2019-09-20 09:44:32.542  INFO 14864 --- [cTaskExecutor-1] o.s.a.r.c.CachingConnectionFactory       : Attempting to connect to: [127.0.0.1:15672]
2019-09-20 09:44:37.543 ERROR 14864 --- [127.0.0.1:15672] c.r.c.impl.ForgivingExceptionHandler     : An unexpected connection driver error occured

java.net.SocketException: Socket Closed
	at java.net.SocketInputStream.socketRead0(Native Method) ~[na:1.8.0_191]
	at java.net.SocketInputStream.socketRead(SocketInputStream.java:116) ~[na:1.8.0_191]
	at java.net.SocketInputStream.read(SocketInputStream.java:171) ~[na:1.8.0_191]
	at java.net.SocketInputStream.read(SocketInputStream.java:141) ~[na:1.8.0_191]
	at java.io.BufferedInputStream.fill(BufferedInputStream.java:246) ~[na:1.8.0_191]
	at java.io.BufferedInputStream.read(BufferedInputStream.java:265) ~[na:1.8.0_191]
	at java.io.DataInputStream.readUnsignedByte(DataInputStream.java:288) ~[na:1.8.0_191]
	at com.rabbitmq.client.impl.Frame.readFrom(Frame.java:91) ~[amqp-client-5.4.3.jar:5.4.3]
	at com.rabbitmq.client.impl.SocketFrameHandler.readFrame(SocketFrameHandler.java:164) ~[amqp-client-5.4.3.jar:5.4.3]
	at com.rabbitmq.client.impl.AMQConnection$MainLoop.run(AMQConnection.java:596) ~[amqp-client-5.4.3.jar:5.4.3]
	at java.lang.Thread.run(Thread.java:748) [na:1.8.0_191]

2019-09-20 09:44:37.588  INFO 14864 --- [           main] o.s.b.w.e.u.UndertowServletWebServer     : Undertow started on port(s) 8020 (http) with context path '/oauth'
2019-09-20 09:44:37.590  INFO 14864 --- [           main] i.c.oauth.OauthServerApplication         : Started OauthServerApplication in 23.168 seconds (JVM running for 24.113)
2019-09-20 09:44:37.595  INFO 14864 --- [           main] i.c.o.a.s.impl.RequestMappingHandler     : 自动加载permission注解开始----------------------------------------------
2019-09-20 09:44:37.595  INFO 14864 --- [           main] i.c.o.a.s.impl.RequestMappingHandler     : 自动加载permission注解结束----------------------------------------------
2019-09-20 09:44:37.595  INFO 14864 --- [           main] i.c.o.a.s.impl.RequestMappingHandler     : 发送rabbit消息给oauth-server进行数据插入处理开始----------------------------------------------
2019-09-20 09:44:37.604  INFO 14864 --- [           main] o.s.a.r.c.CachingConnectionFactory       : Attempting to connect to: [127.0.0.1:15672]
2019-09-20 09:44:42.560  INFO 14864 --- [cTaskExecutor-1] o.s.a.r.l.SimpleMessageListenerContainer : Restarting Consumer@3e0eb917: tags=[{}], channel=null, acknowledgeMode=AUTO local queue size=0
2019-09-20 09:44:42.605  INFO 14864 --- [cTaskExecutor-2] o.s.a.r.c.CachingConnectionFactory       : Attempting to connect to: [127.0.0.1:15672]
2019-09-20 09:44:42.605 ERROR 14864 --- [127.0.0.1:15672] c.r.c.impl.ForgivingExceptionHandler     : An unexpected connection driver error occured

java.net.SocketException: Socket Closed
	at java.net.SocketInputStream.socketRead0(Native Method) ~[na:1.8.0_191]
	at java.net.SocketInputStream.socketRead(SocketInputStream.java:116) ~[na:1.8.0_191]
	at java.net.SocketInputStream.read(SocketInputStream.java:171) ~[na:1.8.0_191]
	at java.net.SocketInputStream.read(SocketInputStream.java:141) ~[na:1.8.0_191]
	at java.io.BufferedInputStream.fill(BufferedInputStream.java:246) ~[na:1.8.0_191]
	at java.io.BufferedInputStream.read(BufferedInputStream.java:265) ~[na:1.8.0_191]
	at java.io.DataInputStream.readUnsignedByte(DataInputStream.java:288) ~[na:1.8.0_191]
	at com.rabbitmq.client.impl.Frame.readFrom(Frame.java:91) ~[amqp-client-5.4.3.jar:5.4.3]
	at com.rabbitmq.client.impl.SocketFrameHandler.readFrame(SocketFrameHandler.java:164) ~[amqp-client-5.4.3.jar:5.4.3]
	at com.rabbitmq.client.impl.AMQConnection$MainLoop.run(AMQConnection.java:596) ~[amqp-client-5.4.3.jar:5.4.3]
	at java.lang.Thread.run(Thread.java:748) [na:1.8.0_191]

2019-09-20 09:44:42.609  INFO 14864 --- [           main] ConditionEvaluationReportLoggingListener : 

Error starting ApplicationContext. To display the conditions report re-run your application with 'debug' enabled.
2019-09-20 09:44:42.609  INFO 14864 --- [           main] ConfigServletWebServerApplicationContext : Closing org.springframework.boot.web.servlet.context.AnnotationConfigServletWebServerApplicationContext@3f4fd0dc: startup date [Fri Sep 20 09:44:26 GMT+08:00 2019]; parent: org.springframework.boot.web.servlet.context.AnnotationConfigServletWebServerApplicationContext@27e32fe4
2019-09-20 09:44:42.622 ERROR 14864 --- [           main] o.s.boot.SpringApplication               : Application run failed

java.lang.IllegalStateException: Failed to execute CommandLineRunner
	at org.springframework.boot.SpringApplication.callRunner(SpringApplication.java:795) [spring-boot-2.0.6.RELEASE.jar:2.0.6.RELEASE]
	at org.springframework.boot.SpringApplication.callRunners(SpringApplication.java:776) [spring-boot-2.0.6.RELEASE.jar:2.0.6.RELEASE]
	at org.springframework.boot.SpringApplication.run(SpringApplication.java:315) [spring-boot-2.0.6.RELEASE.jar:2.0.6.RELEASE]
	at org.springframework.boot.SpringApplication.run(SpringApplication.java:1242) [spring-boot-2.0.6.RELEASE.jar:2.0.6.RELEASE]
	at org.springframework.boot.SpringApplication.run(SpringApplication.java:1230) [spring-boot-2.0.6.RELEASE.jar:2.0.6.RELEASE]
	at io.choerodon.oauth.OauthServerApplication.main(OauthServerApplication.java:29) [classes/:na]
Caused by: org.springframework.amqp.AmqpTimeoutException: java.util.concurrent.TimeoutException
	at org.springframework.amqp.rabbit.support.RabbitExceptionTranslator.convertRabbitAccessException(RabbitExceptionTranslator.java:74) ~[spring-rabbit-2.0.8.RELEASE.jar:2.0.8.RELEASE]
	at org.springframework.amqp.rabbit.connection.AbstractConnectionFactory.createBareConnection(AbstractConnectionFactory.java:504) ~[spring-rabbit-2.0.8.RELEASE.jar:2.0.8.RELEASE]
	at org.springframework.amqp.rabbit.connection.CachingConnectionFactory.createConnection(CachingConnectionFactory.java:628) ~[spring-rabbit-2.0.8.RELEASE.jar:2.0.8.RELEASE]
	at org.springframework.amqp.rabbit.connection.ConnectionFactoryUtils.createConnection(ConnectionFactoryUtils.java:240) ~[spring-rabbit-2.0.8.RELEASE.jar:2.0.8.RELEASE]
	at org.springframework.amqp.rabbit.core.RabbitTemplate.doExecute(RabbitTemplate.java:1816) ~[spring-rabbit-2.0.8.RELEASE.jar:2.0.8.RELEASE]
	at org.springframework.amqp.rabbit.core.RabbitTemplate.execute(RabbitTemplate.java:1790) ~[spring-rabbit-2.0.8.RELEASE.jar:2.0.8.RELEASE]
	at org.springframework.amqp.rabbit.core.RabbitTemplate.send(RabbitTemplate.java:861) ~[spring-rabbit-2.0.8.RELEASE.jar:2.0.8.RELEASE]
	at org.springframework.amqp.rabbit.core.RabbitTemplate.convertAndSend(RabbitTemplate.java:924) ~[spring-rabbit-2.0.8.RELEASE.jar:2.0.8.RELEASE]
	at org.springframework.amqp.rabbit.core.RabbitTemplate.convertAndSend(RabbitTemplate.java:907) ~[spring-rabbit-2.0.8.RELEASE.jar:2.0.8.RELEASE]
	at io.choerodon.oauth.api.service.impl.RequestMappingHandler.run(RequestMappingHandler.java:134) ~[classes/:na]
	at org.springframework.boot.SpringApplication.callRunner(SpringApplication.java:792) [spring-boot-2.0.6.RELEASE.jar:2.0.6.RELEASE]
	... 5 common frames omitted
Caused by: java.util.concurrent.TimeoutException: null
	at com.rabbitmq.utility.BlockingCell.get(BlockingCell.java:77) ~[amqp-client-5.4.3.jar:5.4.3]
	at com.rabbitmq.utility.BlockingCell.uninterruptibleGet(BlockingCell.java:120) ~[amqp-client-5.4.3.jar:5.4.3]
	at com.rabbitmq.utility.BlockingValueOrException.uninterruptibleGetValue(BlockingValueOrException.java:36) ~[amqp-client-5.4.3.jar:5.4.3]
	at com.rabbitmq.client.impl.AMQChannel$BlockingRpcContinuation.getReply(AMQChannel.java:494) ~[amqp-client-5.4.3.jar:5.4.3]
	at com.rabbitmq.client.impl.AMQConnection.start(AMQConnection.java:315) ~[amqp-client-5.4.3.jar:5.4.3]
	at com.rabbitmq.client.ConnectionFactory.newConnection(ConnectionFactory.java:1104) ~[amqp-client-5.4.3.jar:5.4.3]
	at com.rabbitmq.client.ConnectionFactory.newConnection(ConnectionFactory.java:1054) ~[amqp-client-5.4.3.jar:5.4.3]
	at com.rabbitmq.client.ConnectionFactory.newConnection(ConnectionFactory.java:994) ~[amqp-client-5.4.3.jar:5.4.3]
	at org.springframework.amqp.rabbit.connection.AbstractConnectionFactory.createBareConnection(AbstractConnectionFactory.java:457) ~[spring-rabbit-2.0.8.RELEASE.jar:2.0.8.RELEASE]
	... 14 common frames omitted

2019-09-20 09:44:42.623  INFO 14864 --- [           main] ConfigServletWebServerApplicationContext : Closing org.springframework.boot.web.servlet.context.AnnotationConfigServletWebServerApplicationContext@27e32fe4: startup date [Fri Sep 20 09:44:16 GMT+08:00 2019]; parent: org.springframework.context.annotation.AnnotationConfigApplicationContext@59252cb6
2019-09-20 09:44:42.623  INFO 14864 --- [           main] o.s.c.n.e.s.EurekaServiceRegistry        : Unregistering application OAUTH-SERVER with eureka with status DOWN
2019-09-20 09:44:42.625  INFO 14864 --- [           main] o.s.c.support.DefaultLifecycleProcessor  : Stopping beans in phase 2147483647
2019-09-20 09:44:42.630  INFO 14864 --- [           main] o.s.a.r.l.SimpleMessageListenerContainer : Waiting for workers to finish.
2019-09-20 09:44:42.631  INFO 14864 --- [           main] o.s.a.r.l.SimpleMessageListenerContainer : Successfully waited for workers to finish.
2019-09-20 09:44:42.631  INFO 14864 --- [           main] o.s.c.support.DefaultLifecycleProcessor  : Stopping beans in phase 0
2019-09-20 09:44:42.633  INFO 14864 --- [           main] o.s.i.endpoint.EventDrivenConsumer       : Removing {logging-channel-adapter:_org.springframework.integration.errorLogger} as a subscriber to the 'errorChannel' channel
2019-09-20 09:44:42.633  INFO 14864 --- [           main] o.s.i.channel.PublishSubscribeChannel    : Channel 'oauth-server-1.errorChannel' has 0 subscriber(s).
2019-09-20 09:44:42.633  INFO 14864 --- [           main] o.s.i.endpoint.EventDrivenConsumer       : stopped _org.springframework.integration.errorLogger
2019-09-20 09:44:42.633  INFO 14864 --- [           main] o.s.s.c.ThreadPoolTaskScheduler          : Shutting down ExecutorService 'taskScheduler'
2019-09-20 09:44:42.634  INFO 14864 --- [           main] o.s.i.monitor.IntegrationMBeanExporter   : Unregistering JMX-exposed beans on shutdown
2019-09-20 09:44:42.634  INFO 14864 --- [           main] o.s.i.monitor.IntegrationMBeanExporter   : Unregistering JMX-exposed beans
2019-09-20 09:44:42.634  INFO 14864 --- [           main] o.s.i.monitor.IntegrationMBeanExporter   : Summary on shutdown: nullChannel
2019-09-20 09:44:42.634  INFO 14864 --- [           main] o.s.i.monitor.IntegrationMBeanExporter   : Summary on shutdown: errorChannel
2019-09-20 09:44:42.634  INFO 14864 --- [           main] o.s.i.monitor.IntegrationMBeanExporter   : Summary on shutdown: _org.springframework.integration.errorLogger.handler
2019-09-20 09:44:42.635  INFO 14864 --- [           main] o.s.j.e.a.AnnotationMBeanExporter        : Unregistering JMX-exposed beans on shutdown
2019-09-20 09:44:42.635  INFO 14864 --- [           main] o.s.j.e.a.AnnotationMBeanExporter        : Unregistering JMX-exposed beans
2019-09-20 09:44:47.607 ERROR 14864 --- [127.0.0.1:15672] c.r.c.impl.ForgivingExceptionHandler     : An unexpected connection driver error occured

java.net.SocketException: Socket Closed
	at java.net.SocketInputStream.socketRead0(Native Method) ~[na:1.8.0_191]
	at java.net.SocketInputStream.socketRead(SocketInputStream.java:116) ~[na:1.8.0_191]
	at java.net.SocketInputStream.read(SocketInputStream.java:171) ~[na:1.8.0_191]
	at java.net.SocketInputStream.read(SocketInputStream.java:141) ~[na:1.8.0_191]
	at java.io.BufferedInputStream.fill(BufferedInputStream.java:246) ~[na:1.8.0_191]
	at java.io.BufferedInputStream.read(BufferedInputStream.java:265) ~[na:1.8.0_191]
	at java.io.DataInputStream.readUnsignedByte(DataInputStream.java:288) ~[na:1.8.0_191]
	at com.rabbitmq.client.impl.Frame.readFrom(Frame.java:91) ~[amqp-client-5.4.3.jar:5.4.3]
	at com.rabbitmq.client.impl.SocketFrameHandler.readFrame(SocketFrameHandler.java:164) ~[amqp-client-5.4.3.jar:5.4.3]
	at com.rabbitmq.client.impl.AMQConnection$MainLoop.run(AMQConnection.java:596) ~[amqp-client-5.4.3.jar:5.4.3]
	at java.lang.Thread.run(Thread.java:748) [na:1.8.0_191]

2019-09-20 09:44:47.608 ERROR 14864 --- [cTaskExecutor-2] o.s.a.r.l.SimpleMessageListenerContainer : Failed to check/redeclare auto-delete queue(s).

org.springframework.amqp.AmqpTimeoutException: java.util.concurrent.TimeoutException
	at org.springframework.amqp.rabbit.support.RabbitExceptionTranslator.convertRabbitAccessException(RabbitExceptionTranslator.java:74) ~[spring-rabbit-2.0.8.RELEASE.jar:2.0.8.RELEASE]
	at org.springframework.amqp.rabbit.connection.AbstractConnectionFactory.createBareConnection(AbstractConnectionFactory.java:504) ~[spring-rabbit-2.0.8.RELEASE.jar:2.0.8.RELEASE]
	at org.springframework.amqp.rabbit.connection.CachingConnectionFactory.createConnection(CachingConnectionFactory.java:628) ~[spring-rabbit-2.0.8.RELEASE.jar:2.0.8.RELEASE]
	at org.springframework.amqp.rabbit.connection.ConnectionFactoryUtils.createConnection(ConnectionFactoryUtils.java:240) ~[spring-rabbit-2.0.8.RELEASE.jar:2.0.8.RELEASE]
	at org.springframework.amqp.rabbit.core.RabbitTemplate.doExecute(RabbitTemplate.java:1816) ~[spring-rabbit-2.0.8.RELEASE.jar:2.0.8.RELEASE]
	at org.springframework.amqp.rabbit.core.RabbitTemplate.execute(RabbitTemplate.java:1790) ~[spring-rabbit-2.0.8.RELEASE.jar:2.0.8.RELEASE]
	at org.springframework.amqp.rabbit.core.RabbitTemplate.execute(RabbitTemplate.java:1771) ~[spring-rabbit-2.0.8.RELEASE.jar:2.0.8.RELEASE]
	at org.springframework.amqp.rabbit.core.RabbitAdmin.getQueueProperties(RabbitAdmin.java:345) ~[spring-rabbit-2.0.8.RELEASE.jar:2.0.8.RELEASE]
	at org.springframework.amqp.rabbit.listener.AbstractMessageListenerContainer.redeclareElementsIfNecessary(AbstractMessageListenerContainer.java:1604) ~[spring-rabbit-2.0.8.RELEASE.jar:2.0.8.RELEASE]
	at org.springframework.amqp.rabbit.listener.SimpleMessageListenerContainer$AsyncMessageProcessingConsumer.run(SimpleMessageListenerContainer.java:995) [spring-rabbit-2.0.8.RELEASE.jar:2.0.8.RELEASE]
	at java.lang.Thread.run(Thread.java:748) [na:1.8.0_191]
Caused by: java.util.concurrent.TimeoutException: null
	at com.rabbitmq.utility.BlockingCell.get(BlockingCell.java:77) ~[amqp-client-5.4.3.jar:5.4.3]
	at com.rabbitmq.utility.BlockingCell.uninterruptibleGet(BlockingCell.java:120) ~[amqp-client-5.4.3.jar:5.4.3]
	at com.rabbitmq.utility.BlockingValueOrException.uninterruptibleGetValue(BlockingValueOrException.java:36) ~[amqp-client-5.4.3.jar:5.4.3]
	at com.rabbitmq.client.impl.AMQChannel$BlockingRpcContinuation.getReply(AMQChannel.java:494) ~[amqp-client-5.4.3.jar:5.4.3]
	at com.rabbitmq.client.impl.AMQConnection.start(AMQConnection.java:315) ~[amqp-client-5.4.3.jar:5.4.3]
	at com.rabbitmq.client.ConnectionFactory.newConnection(ConnectionFactory.java:1104) ~[amqp-client-5.4.3.jar:5.4.3]
	at com.rabbitmq.client.ConnectionFactory.newConnection(ConnectionFactory.java:1054) ~[amqp-client-5.4.3.jar:5.4.3]
	at com.rabbitmq.client.ConnectionFactory.newConnection(ConnectionFactory.java:994) ~[amqp-client-5.4.3.jar:5.4.3]
	at org.springframework.amqp.rabbit.connection.AbstractConnectionFactory.createBareConnection(AbstractConnectionFactory.java:457) ~[spring-rabbit-2.0.8.RELEASE.jar:2.0.8.RELEASE]
	... 9 common frames omitted

2019-09-20 09:44:47.609  INFO 14864 --- [           main] o.s.a.r.l.SimpleMessageListenerContainer : Shutdown ignored - container is not active already
2019-09-20 09:44:47.610  INFO 14864 --- [           main] s.c.a.AnnotationConfigApplicationContext : Closing FeignContext-notify-service: startup date [Fri Sep 20 09:44:20 GMT+08:00 2019]; parent: org.springframework.boot.web.servlet.context.AnnotationConfigServletWebServerApplicationContext@27e32fe4
2019-09-20 09:44:47.611  WARN 14864 --- [           main] s.c.a.AnnotationConfigApplicationContext : Exception thrown from ApplicationListener handling ContextClosedEvent

org.springframework.beans.factory.BeanCreationNotAllowedException: Error creating bean with name 'eurekaAutoServiceRegistration': Singleton bean creation not allowed while singletons of this factory are in destruction (Do not request a bean from a BeanFactory in a destroy method implementation!)
	at org.springframework.beans.factory.support.DefaultSingletonBeanRegistry.getSingleton(DefaultSingletonBeanRegistry.java:208) [spring-beans-5.0.10.RELEASE.jar:5.0.10.RELEASE]
	at org.springframework.beans.factory.support.AbstractBeanFactory.doGetBean(AbstractBeanFactory.java:315) ~[spring-beans-5.0.10.RELEASE.jar:5.0.10.RELEASE]
	at org.springframework.beans.factory.support.AbstractBeanFactory.getBean(AbstractBeanFactory.java:199) ~[spring-beans-5.0.10.RELEASE.jar:5.0.10.RELEASE]
	at org.springframework.context.support.AbstractApplicationContext.getBean(AbstractApplicationContext.java:1087) [spring-context-5.0.10.RELEASE.jar:5.0.10.RELEASE]
	at org.springframework.context.event.ApplicationListenerMethodAdapter.getTargetBean(ApplicationListenerMethodAdapter.java:288) ~[spring-context-5.0.10.RELEASE.jar:5.0.10.RELEASE]
	at org.springframework.context.event.ApplicationListenerMethodAdapter.doInvoke(ApplicationListenerMethodAdapter.java:258) ~[spring-context-5.0.10.RELEASE.jar:5.0.10.RELEASE]
	at org.springframework.context.event.ApplicationListenerMethodAdapter.processEvent(ApplicationListenerMethodAdapter.java:180) ~[spring-context-5.0.10.RELEASE.jar:5.0.10.RELEASE]
	at org.springframework.context.event.ApplicationListenerMethodAdapter.onApplicationEvent(ApplicationListenerMethodAdapter.java:142) ~[spring-context-5.0.10.RELEASE.jar:5.0.10.RELEASE]
	at org.springframework.context.event.SimpleApplicationEventMulticaster.doInvokeListener(SimpleApplicationEventMulticaster.java:172) ~[spring-context-5.0.10.RELEASE.jar:5.0.10.RELEASE]
	at org.springframework.context.event.SimpleApplicationEventMulticaster.invokeListener(SimpleApplicationEventMulticaster.java:165) ~[spring-context-5.0.10.RELEASE.jar:5.0.10.RELEASE]
	at org.springframework.context.event.SimpleApplicationEventMulticaster.multicastEvent(SimpleApplicationEventMulticaster.java:139) ~[spring-context-5.0.10.RELEASE.jar:5.0.10.RELEASE]
	at org.springframework.context.support.AbstractApplicationContext.publishEvent(AbstractApplicationContext.java:400) [spring-context-5.0.10.RELEASE.jar:5.0.10.RELEASE]
	at org.springframework.context.support.AbstractApplicationContext.publishEvent(AbstractApplicationContext.java:406) [spring-context-5.0.10.RELEASE.jar:5.0.10.RELEASE]
	at org.springframework.context.support.AbstractApplicationContext.publishEvent(AbstractApplicationContext.java:354) [spring-context-5.0.10.RELEASE.jar:5.0.10.RELEASE]
	at org.springframework.context.support.AbstractApplicationContext.doClose(AbstractApplicationContext.java:998) [spring-context-5.0.10.RELEASE.jar:5.0.10.RELEASE]
	at org.springframework.context.support.AbstractApplicationContext.close(AbstractApplicationContext.java:965) [spring-context-5.0.10.RELEASE.jar:5.0.10.RELEASE]
	at org.springframework.cloud.context.named.NamedContextFactory.destroy(NamedContextFactory.java:76) [spring-cloud-context-2.0.2.RELEASE.jar:2.0.2.RELEASE]
	at org.springframework.beans.factory.support.DisposableBeanAdapter.destroy(DisposableBeanAdapter.java:256) [spring-beans-5.0.10.RELEASE.jar:5.0.10.RELEASE]
	at org.springframework.beans.factory.support.DefaultSingletonBeanRegistry.destroyBean(DefaultSingletonBeanRegistry.java:571) [spring-beans-5.0.10.RELEASE.jar:5.0.10.RELEASE]
	at org.springframework.beans.factory.support.DefaultSingletonBeanRegistry.destroySingleton(DefaultSingletonBeanRegistry.java:543) [spring-beans-5.0.10.RELEASE.jar:5.0.10.RELEASE]
	at org.springframework.beans.factory.support.DefaultListableBeanFactory.destroySingleton(DefaultListableBeanFactory.java:954) [spring-beans-5.0.10.RELEASE.jar:5.0.10.RELEASE]
	at org.springframework.beans.factory.support.DefaultSingletonBeanRegistry.destroySingletons(DefaultSingletonBeanRegistry.java:504) [spring-beans-5.0.10.RELEASE.jar:5.0.10.RELEASE]
	at org.springframework.beans.factory.support.DefaultListableBeanFactory.destroySingletons(DefaultListableBeanFactory.java:961) [spring-beans-5.0.10.RELEASE.jar:5.0.10.RELEASE]
	at org.springframework.context.support.AbstractApplicationContext.destroyBeans(AbstractApplicationContext.java:1039) [spring-context-5.0.10.RELEASE.jar:5.0.10.RELEASE]
	at org.springframework.context.support.AbstractApplicationContext.doClose(AbstractApplicationContext.java:1015) [spring-context-5.0.10.RELEASE.jar:5.0.10.RELEASE]
	at org.springframework.context.support.AbstractApplicationContext.close(AbstractApplicationContext.java:965) [spring-context-5.0.10.RELEASE.jar:5.0.10.RELEASE]
	at org.springframework.boot.SpringApplication.handleRunFailure(SpringApplication.java:813) [spring-boot-2.0.6.RELEASE.jar:2.0.6.RELEASE]
	at org.springframework.boot.SpringApplication.run(SpringApplication.java:318) [spring-boot-2.0.6.RELEASE.jar:2.0.6.RELEASE]
	at org.springframework.boot.SpringApplication.run(SpringApplication.java:1242) [spring-boot-2.0.6.RELEASE.jar:2.0.6.RELEASE]
	at org.springframework.boot.SpringApplication.run(SpringApplication.java:1230) [spring-boot-2.0.6.RELEASE.jar:2.0.6.RELEASE]
	at io.choerodon.oauth.OauthServerApplication.main(OauthServerApplication.java:29) [classes/:na]

2019-09-20 09:44:48.727  INFO 14864 --- [           main] com.netflix.discovery.DiscoveryClient    : Shutting down DiscoveryClient ...
2019-09-20 09:44:48.727  INFO 14864 --- [           main] com.netflix.discovery.DiscoveryClient    : Completed shut down of DiscoveryClient
2019-09-20 09:44:48.727  INFO 14864 --- [           main] com.zaxxer.hikari.HikariDataSource       : HikariPool-1 - Shutdown initiated...
2019-09-20 09:44:48.731  INFO 14864 --- [           main] com.zaxxer.hikari.HikariDataSource       : HikariPool-1 - Shutdown completed.
Disconnected from the target VM, address: '127.0.0.1:5076', transport: 'socket'

Process finished with exit code 1

~~~



- 服务的 rabbit 配置：

~~~
  rabbitmq:
    host: 127.0.0.1
    port: 15672
    username: guest
    password: guest
~~~



- 原因：

  **5672：应用访问端口；15672：控制台Web端口号**

端口号错误：配置信息改为下面这个，参考文章见下面的参考链接，详细区分 **5672：应用访问端口；15672：控制台Web端口号**

~~~java
  rabbitmq:
    host: 127.0.0.1
    port: 5672
    username: guest
    password: guest
~~~



- 参考链接：[参考链接](https://blog.csdn.net/shanchahua123456/article/details/84312144)

### 路由服务页面报错如下

~~~java
Forwarding gateway helper error
~~~



### 客户端注册不到注册中心

~~~java
#是否向服务注册中心注册自己（true 为注册， false 为不向注册中心注册，下同）
register-with-eureka: false

#是否检索服务
fetch-registry: false
    
    
如果不写的话，默认都是开启的。即不写的话，默认会向注册中心注册
~~~

- [参考链接](https://blog.csdn.net/feiz3020/article/details/80171839)

~~~java
启动 Eureka 客户端 时报的错，要么就是 Eureka 服务端 没有启动 要么连接 Eureka 服务端 URL 不对（我就是属于后者，大意导致的）解决办法是：检查 Eureka 服务端是否启动。访问 Eureka 服务端是否正常。

如果访问地址是：http://127.0.0.1:9999/eureka/

则在 Eureka 客户端 应该配置的是 eureka.client.serviceUrl.defaultZone=http://localhost:9999/eureka/eureka/

第一个 eureka 是项目名，配置中配置了 server.context-path= /eureka

如果配置成 server.context-path= /eurekaServer

则 Eureka 服务端 访问地址是 http://localhost:9999/eurekaServer/

Eureka 客户端 链接地址是 eureka.client.serviceUrl.defaultZone=http://localhost:9999/eurekaServer/eureka/
~~~



- [参考链接](https://www.cnblogs.com/hfultrastrong/p/8549590.html)

~~~
1、fetch-registry：表示是否从 eureka server 获取注册信息，如果是单一节点，不需要同步其他 eureka server 节点，则可以设置为 false，但此处为集群，应该设置为 true，默认为 true，可不设置。

2、register-with-eureka：表示是否将自己注册到 eureka server，因为要构建集群环境，需要将自己注册到及群众，所以应该开启。默认为 true，可不显式设置。
~~~



- 问题描述：

~~~java
当换一个注册中心，就可以注册上去，其配置文件为：
server:
  port: 8001
spring:
  application:
    name:  eureka-server
eureka:
  client:
    register-with-eureka: false
    fetch-registry: false
    service-url:
      defaultZone: http://127.0.0.1:8001/eureka
~~~

- 如图所示，已经注册上去了：

<div align=center><img src="https://mortre-picgo.oss-cn-beijing.aliyuncs.com/20190920160341.png"/></div>
- //TODO

  - 201909231617更新：

    注册不上去的原因是：配置中心开启了安全认证，代码和截图如下：

    ~~~java
    security:
      user:
        name: admin
        password: admin
    ~~~

    <div align=center><img src="https://mortre-picgo.oss-cn-beijing.aliyuncs.com/20190923161803.png"/></div>

- 修改方法：
  - 第一种：关闭安全认证，即把对应的安全认证配置注释掉，注册地址使用：`http://localhost:8001/eureka/`
  - 第二种：较为安全，依旧使用安全认证，只需要改一下各个服务对应的注册地址，改为：`http://admin:admin@localhost:8001/eureka/`

### Swagger 页面加载失败

失败描述：Failed to load API definition.

<div align=center><img src="https://mortre-picgo.oss-cn-beijing.aliyuncs.com/20190920161954.png"/></div>

- 解决：//TODO


  - 201909231621更新：

    是因为各个服务无法注册到注册中心，原因见上（已完成），此处需要注意：

    在启动服务的过程中，控制台可能会显示：`Fetching config from server at : http://localhost:8888`，但是你的端口并不是 8888；这是因为配置文件的优先级不同，根据优先级在加载过程中产生的问题，bootstrap.yml 和 application.yml 的优先级是不同的；具体查看源码。

- 此问题可以参考：[参考]([https://www.baidu.com/s?ie=utf-8&f=8&rsv_bp=1&rsv_idx=1&tn=baidu&wd=Fetching%20config%20from%20server%20at%20%3A%20http%3A%2F%2Flocalhost%3A8888&rsv_pq=f789745c0002d845&rsv_t=5bb0VUFgAhO0yxg5Y3axL2%2BDKuJCu%2FuEdWt1poz0kvLLWq0pC3VQbwIUmSM&rqlang=cn&rsv_enter=1&rsv_dl=tb&rsv_n=2&rsv_sug3=1&rsv_sug2=0&inputT=346&rsv_sug4=345](https://www.baidu.com/s?ie=utf-8&f=8&rsv_bp=1&rsv_idx=1&tn=baidu&wd=Fetching config from server at %3A http%3A%2F%2Flocalhost%3A8888&rsv_pq=f789745c0002d845&rsv_t=5bb0VUFgAhO0yxg5Y3axL2%2BDKuJCu%2FuEdWt1poz0kvLLWq0pC3VQbwIUmSM&rqlang=cn&rsv_enter=1&rsv_dl=tb&rsv_n=2&rsv_sug3=1&rsv_sug2=0&inputT=346&rsv_sug4=345)) ,[优先级问题概述链接1](https://blog.csdn.net/hubo_88/article/details/80726901) ，[优先级问题概述链接2](https://blog.csdn.net/qq_17394183/article/details/89886389)



- 参考： [链接](http://www.mamicode.com/info-detail-2235108.html)



### 所有的请求都是通过路由来访问，不允许直接访问服务，也访问不了

~~~
现阶段只能通过路由访问各个服务，没有办法直接访问服务，除非关闭 api 权限校验
~~~





### 用户 QX 表的 ID 是 UUID 随机生成的

- 如下为对应的实体类，从注解可看出是用户权限表

~~~java
@Table(name = "au_user_role")
public class AuUserRole {
    /**
     * ID
     */
    @Id
    @Column(name = "ID")
    private String id;
    
    xxx;
}
~~~

- 对应的方法，如图：

~~~java
AuUserRole auUserRole1 = new AuUserRole();
auUserRole1.setId(UUID.randomUUID().toString().replace("-", ""));
~~~

<div align=center><img src="https://mortre-picgo.oss-cn-beijing.aliyuncs.com/20190920165650.png"/></div>
