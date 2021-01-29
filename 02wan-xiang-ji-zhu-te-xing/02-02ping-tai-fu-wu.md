# 技术平台

---

## 技术栈

> 从开发、运维、测试采用以下工具链，完成系统开发、DevOps以及自动化测试实践

* JDK 1.8
* Spring Boot 
* Spring Cloud 
* Spring Cloud Config
* Spring Cloud Sleuth
* Netflix Fegin
* Netflix Ribbon
* Hystrix
* RabbitMQ
* Eureka
* Redis
* SkyWalking
* ELK
* GitLab
* Jenkins
* PostgreSQL
* MeterSphere
* APISIX
* Nginx
* Etcd
* Ceph
* NFS
* OpenStack
* Ansible
* Docker
* GreenPlum

![](/assets/技术栈.png)

## 微服务架构

> 微服务架构具备以下特征

* 单一职责
* 轻量级通讯（HTTP）
* 隔离性
* 数据独立性
* 技术多样性

> 服务注册与发现

![](/assets/服务注册与发现.png)

* ### 服务负载均衡

> 可根据轮询、随机、权重、HASH等算法进行负载均衡调用，同时可扩展自定义算法进行流量分割

![](/assets/服务负载均衡.png)

* ### 服务熔断机制

> 没有熔断机制的情况下，底层服务的访问缓慢或者异常，会引起上层服务的崩溃，蝴蝶效应会导致整个系统瘫痪。
>
> 触发熔断机制的情况下，服务会快速响应失败，请求压力不再发往后端服务，使整体服务能保持健康的状态。部分服务不可用，但不至于让整体系统瘫痪

![](/assets/服务熔断机制.png)

* ### 限流规则配置和效果

![](/assets/限流规则.png)

![](/assets/限流效果.png)

* ### 任务调度机制

> 采用Spring线程池实现可管理的任务调度，根据系统配置可定制任务首次执行时间、执行频率，针对任务可配置参数、对应系统、描述以及执行方式：定时触发、依据上次成功后间隔触发。
>
> 对任务执行进度可视化，可控制任务暂停以及手动触发重新执行，存留任务的全部执行记录

![](/assets/添加任务.png)

* 可配置每个任务的执行线程

```java
    @Bean
    public Executor taskRun() {
        ThreadPoolTaskExecutor executor = new ThreadPoolTaskExecutor();
        executor.setCorePoolSize(100);
        executor.setMaxPoolSize(100);
        executor.setQueueCapacity(100);
        executor.setThreadNamePrefix("taskRun");
        executor.initialize();

        return executor;
    }
    @Bean
    public Executor taskRunV2() {
        ThreadPoolTaskExecutor executor = new ThreadPoolTaskExecutor();
        executor.setCorePoolSize(200);
        executor.setMaxPoolSize(200);
        executor.setQueueCapacity(200);
        executor.setThreadNamePrefix("taskRunV2");
        executor.initialize();
        return executor;
    }
```

* 定时任务读取到任务配置信息后进行缓存，同时有另一个新的线程定时刷新缓存，确保任务参数变更能短时间内生效，同时确保任务执行无需频繁查库。
* 批量任务的调度机制采用Java中非阻塞模型，使用Future.isDone\(\)来判断线程状态，不影响主线程的同时，保障子线程执行。

* ### 队列机制

> 系统中大量采用消息队列处理请求，其中包含批量请求、任务调度、日志记录、异步推送等，使用消息队列对系统压力进行削峰填谷，同时保障系统运行过程中消息的可靠性。
>
> 在设计中，我们设计了Sender和Receiver两个角色，分别作为两个微服务存在，他们将消息队列投递以及监听进行的标准化输出，可适配多种类型消息队列中间件，现采用RabbitMQ。业务系统将消息发送给Sender来进行投递，Receiver对队列进行监听，监听到投递的消息后转送给业务系统处理。

![](/assets/消息队列调用机制.png)

> 对于部分需要重发的消息以及需要延迟发送的消息，系统中会采用双队列进行投递和监听。将固定延迟的消息会投递给死信队列，等待时间过期重新取出发送。注：单个死信队列的延迟时间需要一致，队列中消息延迟不一致会导致不同消息消费时间会根据前一条消息的延迟顺延排队。

![](/assets/延迟队列调用.png)



* ### 银行流控机制

> 对于银企直联业务以及很多网银类业务，限流区分两部分，对前端客户的并发控制，需要支撑的尽可能高并发。第二部分是对于后端银行渠道，由于银行前置机、UKEY等性能受限，需要达成尽可能高的交易成功率，此时不适合将大量流量流向前置机和银行渠道。
>
> 万象核心采用漏桶+优先队列机制，将前端大规模流量



