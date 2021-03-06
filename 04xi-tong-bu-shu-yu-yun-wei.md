# 系统部署与运维

---

### 网络部署结构

> 网络部署结构将整个网络分成：DMZ入口、DMZ外联、DMZ互联、AP区、运维管理区，同时将DMZ入口会划分成DMZ核心入口以及普通入口区，AP区划分为AP核心区、AP普通区、AP中间件区、AP数据库区。大的区域之间网络互不打通，需要开通网络策略才可进行访问。

* DMZ入口：接收外部请求，主要部署网关、API应用、代理服务（Nginx/APISIX）
* DMZ外联：发送请求至互联网（部署Gateway应用、代理服务Nginx）
* DMZ互联：和银行、机构的专线连接（部署Gateway应用、渠道应用）
* AP：业务应用、中间件、数据库
* 运维管理区：堡垒机、自动化运维工具、VPN

![](/assets/网络结构示意图.png)

### 自持客户网络部署结构

> 面向UKEY自持客户，通过旁路组网模式，无需改变企业自身网络结构，快速部署组件异地虚拟局域网。免除繁杂企业公网IP配置，机房布放、部署。快速完成企业网络实施交付。

![](/assets/异地组网.png)

> 对所有企业与银企之间的网络可管理，可视化。网络健康，网络管理，全链路可追溯。
>
> 同时自持前置机状态可管理，历史状态可追溯。

![](/assets/VPN网络监控.png)![](/assets/VPN网络管理2.png)![](/assets/VPN上线下记录.png)![](/assets/前置机管理.png)

### 混合云部署

> 通过在托管机房和云服务提供商分别建一整套完整应用，银行前置机和UKEY设备托管放置在机房，通过专线互联。从网络质量区分多线路，应用灾备多地。

![](/assets/混合云部署方案.png)

### 数据库部署

> 数据库采用一主两从一历史库策略，分别做主从高可用切换，读写分离，历史归档用途。

* 高可用：保障数据库主库故障能够迅速切换至从库，达成SLA等级
* 读写分离：将大量查询请求发往第二从库，降低主库的日常负载，提升整体数据库处理能力。
* 历史归档：将半年以上的历史数据迁移至历史库，通过FDW链接。维持主库大小相对恒定，数据库性能不会随着时间线性下降。
* 延迟备库：资源充足情况下考虑做延迟备库，主要应对误操作、误删除、误更新，延迟备库保留有一定时间内未操作数据供恢复，降低数据风险。

### DevOps部署

> 从产品开发到集成测试到生产上线，进行全自动化。通过GitLab管理整体应用版本代码，主要由Jenkins集成其他插件，SonarQube进行代码质量扫描，使用MeterSphere对系统进行测试计划和测试案例的管理，同时做接口测试和性能测试。功能主要以黑盒测试为主。
>
> 上线过程通过Jenkins Pipeline实现自定义流程上线，做到上线前的无故障切换，历史版本备份，自动寻找上线包可用区，生产上线版本可追踪到具体Git提交版本。大大降低上线复杂度。

![](/assets/DevOps流程.png)

### 高可用

* 交易全场景实现生产环境高可用，为高价值客户提供7\*24小时、SLA99.99%的高品质服务。
* 双盾双前置双活

### 安全

* 从主机、网络、软件、应用、数据、管理等全维度，从研发、测试、发布变更等全流程，从资金的操作端、外联接口端、存放端等全节点保证安全无漏点。
* 构建安全态势感知平台，提前发现全网安全攻击。
* 客户密码及软证书通过线上直接提交落库加密存储；
* 用安全中心产品优化银企联业务流程，让用友提供给客户的服务更安全、更可信、更便捷。

### 智能化

* 建设devsecops平台。
* 银企联云系统故障自愈方案落地，自持和托管模式的UKEY、前置机故障自愈方案落地。
* 混沌工程验证。
* RPA的自动化运维工作。

### 监控

* IAAS、PAAS、SAAS监控全覆盖。
  * 主机资源
  * 网络资源
  * 应用健康
  * 中间件健康
  * 数据库健康
  * 全局时间
  * 分布式存储
  * 日志分析
* 每笔交易数据全链路监控。
  * 交易链路
  * 日志链路
  * 性能链路

### 规范化管理

* 等保三级、金融行业系统管理标准等体系化规范

### 一体化应急处理

* 全面应急预案
* 操作层、运营层、管理层实现监、管、控的联动
* 确保98%的事故在十分钟内处置完成

### 



