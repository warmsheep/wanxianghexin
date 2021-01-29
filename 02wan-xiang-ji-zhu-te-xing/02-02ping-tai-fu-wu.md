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

