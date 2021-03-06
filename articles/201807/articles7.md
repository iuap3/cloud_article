# 用友云开放平台之API网关

作者：（云平台-混合云服务[**iPaaS**]-API产品）**程序设计专家**

导读：本文介绍选择API网关应考虑的几方面内容，API网关在微服务框架中的作用，API网关如何选型，用友云开放平台的API网关可以做什么。文章内容详实，深入浅出。

随着互联网的快速发展，当前已步入移动互联、物联网时代。企业内部系统，企业与客户，企业供应链上下游之间，甚至于社会化公共数据的共享都对系统架构提出了新的需求。

微服务框架的强势崛起，使更多企业迅速的完成了企业内部的API化，但在企业供应链和社会化开放数据和能力的强烈需求下，安全，隔离，共享成为刚性需求，所以API网关就成为了企业开放的必备产品。

很多互联网平台已基于网关的设计思路，构建自身平台的API网关，国内主要有京东、携程、唯品会等，国外主要有Netflix、Amazon等。
    
**如何选择自己的API网关?**

不管用已有还是自研的API网关  我们都需要从以下几个方面去考虑。

1、安全与防护

大型企业都把网络安全看成信息化的重中之重，作为企业数据和服务的对外出口，API网关要自带基本的安全防护功能，能够防注入，防重放，防篡改，防一定规模的DDOS攻击，自定义规则对非	法流量进行过滤。

2、性能与稳定性

API网关就会作为企业应用核心，性能和可用性是最基本的需求要求。
（1）从性能上来说，需要让网关增加的时间消耗越短越好，个人觉得需要10ms以下。 系统需要采用非阻塞的IO，如epoll，NIO等。网关和各种依赖的交互也需要是非阻塞的，这样才能保证整体系统的高性能。
（2）网关必须支持集群部署和高可用，能够横行扩展，支撑高并发和大流量，同时任何一个节点down掉都不能影响整体的可用性。
（3）尽可能多套网关应该支持同一管理平台和同一监控中心。 如： 一个企业的OpenAPI网关和内部应用的多个系统群的不同的微服务网关可以在同一监控中心进行监控。

3、可扩展性、可维护性

企业的需求是多样化的而且不断变化，作为基础平台的核心组件，要提供二次开发能力，方便扩展以及和其他基础平台之间流程打通

4、需求匹配度

需要评估各API网关在需求上是否能满足，如： 如果是OpenAPI平台需要使用API网关，那么需要看API网关在合作伙伴应用接入、合作伙伴门户集成、访问次数限额等OpenAPI核心需求上去思考产品是否能满足要求。 如果是微服务网关，那么要从微服务的运维、监控、管理等方面去思考产品是否足够强大。

**API网关在微服务框架中的作用？**

![](/articles/201807/images/articles7/images7.1.png)

1.企业安全隔离

企业内部系统在对公有云或者外部系统集成时，需要一个明显的边界去保证自己企业的业务数据安全及权限的统一控制与管理，API网关在对外开放数据和提供能力时需要提供各种通用的安全认证标准。

2.统一管理，全局入口

在微服务架构之下，服务被拆的非常零散，降低了耦合度的同时也给服务的统一管理增加了难度，
缺乏对外开放能力的全局视图管理及监控能力，API网关要完成全局开放流量入口的分析与管理。

3.跨平台，跨语言，易集成，方便扩展

用友云平台是基于JAVA语言开发的微服务治理平台，在JAVA语言调用时很方便，但是PHP，C系列等其它语言调用微服务时需要开发SideCar ，这就造成集成的复杂度，API网关提供标准的restful接口给产品在集成时提供很大便利。

**API网关如何选型？ 为什么是Nginx+Lua+c?**

现在开源的API网关主要基于Nginx、ZUUL、Spring Cloud  Gateway、Linkerd等开源项目，但是各有特点：

Linkerd也是一个非常有前途的项目，是基于Scala实现的、目前市面上仅有的生产级别的Service Mesh，但是资料少，学习成本高，二次开发和功能扩展困难， 整体开发生态还没建立起来。

Spring Cloud  Gateway 是Spring Cloud创建了一个嵌入式Zuul代理，所以两者实质上都是Netflix Zuul， Zuul的性能不错，Zuul 2.0 本身采用了Netty 的NIO，复杂度提高了，但性能更加强悍，Zuul1.0和Spring 框架也原生集成，基于JAVA开发语言,可以和Eureka,Ribbon,Hystrix等配件组合:很容易实现 身份认证,监 控,动态路由,压力测试,负载分配,静态响应等功能,Zuul 1.0已开源6年多，很易用，在实战中也得到了检验，zuul 2.0 在超大型互联应用中还有坑要趟，但整体来说，在强大的java生态中zuul是一个很不错的技术选型方向。

Nginx生态的Nginx+Lua+c,主要代表产品有kong等开源产品。kong 自2015年在github开源以后，已有1.69万+的star，其核心价值在于稳定，高性能，易扩展；基于nginx+c的Tengine在阿里巴巴集团内还在大量使用，尚在壮年；  京东更是用nginx+lua这套技术框架证实了亿万流量的最佳实践。虽然开发效率比较低，好在网关的逻辑足够简单，稳定，所以这个技术组合对这样一个业务场景尤其合适。用友云API网关核心部分就是基于这套框架开发的。
   
**用友云开放平台的API网关可以做什么？ **

API网关（API Gateway）提供了API的全生命周期管理。辅助用户简单、快速、低成本、低风险的将数据、业务逻辑或功能安全可靠的开放出来，用以实现自身系统集成、以及与合作伙伴的业务连接。目前已成功应用于用友云开放平台，APILink，

![](/articles/201807/images/articles7/images7.2.png)


产品特性：

1.安全防护

支持安全认证，自定义流量过滤，黑白名单，服务降级，流量限制，熔断等基本功能。

2.API 生命周期管理

提供 API 创建、维护、发布、运行、下线等操作的全生命周期管理。覆盖API定义、测试、发布用以部署API。同时提供便捷的日常管理、版本管理、支持在先版本升级和快速回滚。节约因 API 管理而造成的工作量与人力。

3.请求管理，链路追踪

请求经过 API 网关，可根据您的配置进行参数类型、参数值的校验，减少后端对非法请求、无效请求的资源消耗和处理成本。同时，您可以在 API 网关定义参数映射规则，网关通过映射规则将后端服务通过映射翻译成任何形式，以满足不同用户的不同需求，从而避免功能重复开发。请求过程全链路追踪机制，方便快捷定位问题。

4.监控告警，统计分析
	
提供实时、可视化的 API 监控，包括：调用量、调用方式、响应时间、错误率，让您能够清楚的了解 API 的详细信息和分析用户的行为习惯。方便用户的运维管理，以便 API 的后期迭代与维护，提高效率。支持自定义报警规则，来针对异常情况进行报警，缩短故障处理时间。
