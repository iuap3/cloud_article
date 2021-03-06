# 浅谈bPaaS模式下的数据隔离
---2018年6月
作者：（云平台-企业业务中台[bPaaS]-能力中心）部门经理

导读：本文定位于大型的企业互联网平台，介绍在企业互联网服务领域内，租户和如何实现租户业务的数据隔离方案的统一方案，文章图文并茂，逻辑性强，值得一读。

随着互联网技术的发展，越来越多的企业开始发展SaaS服务，或期望将自己的业务系统能发展为公有云服务进行创收。很多企业与科技公司合作开发领域内的SaaS化产品。很多项目也在追求多租户的业务模式。但从目前的实践来看，在企业互联网服务这一领域内，对于租户和如何实现租户业务的数据隔离方案，还没有形成统一的方案。不同的领域内选择的方案都所不同，在业务领域内只按租户进行隔离、有个PaaS层应用会存在主子租户的定义。本文主要就大型的企业互联网平台如何进行数据隔离，以支持不同层次的业务产品实现进行讨论。
## 一、业务模型分析
在多租户的云服务模式下，我们对企业业务中的数据对象进行分类。总体来说，在一个SaaS产品下，数据分为三种:

社会级：用户、企业、币种、银行、开户行、国家地区等，在不同的租户下使用的数据是一致的。数据一般由平台的运营人员负责管理。

租户级：组织、员工、客户、供应商、物料等，这部分数据一般是按租户隔离，不同租户的数据是一般是相互不可见的。

应用级数据：一般是作为预置数据或配置级数据存在，例如一些全局配置参数，初始化的预置数据模版等。内置的消息通道、后台任务等。
## 二、用户、租户、应用服务模型关系
首先，第一个要说明是用户，在一个统一的云服务下，用户体系是全局唯一的，即一个云一个账号。一个自然人在整个体系内不会按企业、租户、组织等建立不同的账号。目前的主流产品都是按此实现的。用户是可以跨产品和租户使用的。例如淘宝账号可以作为淘宝、天猫、1688、阿里云等一些列产品的登录账号。

其次，第二个主要对象是租户，一般指实现如何于多用户的环境下共用相同的系统或程序组件，并且仍可确保各用户间数据的隔离性。目前租户在不同的系统中实现方式有一定区别。先以现有的实现举例：

第一种场景，以用户作为租户，对于ToC的产品会将用户作为租户进行服务的开通，每个用户购买不同的应用能力。在部分ToB的产品也会将第一个注册的用户作为租户，用户可以补充企业信息，其他的用户加入当前的用户创建的企业下，这种情况下其实隐含了租户的概念，在开通团队或企业产品时，默认后台相当于使用当前用户作为数据隔离的维度。这里会存在一些问题，例如当前的管理员（创建企业的用户）从企业离职或工作切换时，账号不能直接切换，只能将原有账号修改手机、邮箱，交给一下个用户使用。

![](/articles/201806/images/article4/images4.1.png)

第二场景，以企业为租户，用户登录后创建企业，作为当前的企业管理员。数据按企业进行隔离，企业的管理员可以转移给其他人。这个方案基本可以支撑目前的多租户的场景使用。但这里存在一个概念的问题，企业和企业购买的服务载体，这两者一般情况下可能不一致。很多情况下企业可能会以内部组织、团队来购买开通产品。一个企业可能会产生多个不同租户的购买记录。因此不建议直接将租户作为企业信息进行沉淀。

![](/articles/201806/images/article4/images4.2.png)

目前方案，租户（目前命名为“企业账号”）、用户、企业三者分离，用户与租户建立关系，可以指定用户为租户的管理员。企业信息为经过单纯的企业信息，租户与企业之间为松耦合关系，即租户可以绑定企业、也可以不绑定企业。在绑定企业时，可根据企业和租户的关系查询到企业下的用户，以及企业下其他数据（组织、员工、业务数据等）的关系。

![](/articles/201806/images/article4/images4.3.png)

最后，还有应用服务，这里的应用服务是指在平台上进行开发并对外提供完整统一的功能，可以在销售系统（云市场、云商务、商务）上购买的的SaaS类应用产品。例如，友云采、友空间、云表单都为应用服务。但一些不能独立使用，做为其他产品的支撑服务的应用服务，例如基础数据、编码规则、元数据等PaaS类应用不作为对外的应用服务，一般与支撑的应用服务一起购买和使用。用友云作为bPaaS平台，同时支持多个独立的应用服务统一在平台上运行使用。

![](/articles/201806/images/article4/images4.4.png)

## 三、bPaaS平台的数据维度
从应用的场景分析，会存在两种类型的应用：
独立应用：与其他应用没有关系，独立的开通使用。
融合版本应用：多个应用融合在一起对客户提供服务。

对于上述两种应用，bPaaS平台提供都会提供服务支持，但数据隔离的方案会存在区别。

第一类应用在使用平台提供的数据服务时，与其他应用数据隔离。目前的应用大部分都是独立的应用，有自己的官网和首页，平台提供的功能也都是在个应用下的独立的入口进行维护和使用。例如友云采和友人才，都在使用平台提供的权限服务，但在云采中不会也不能授权友人才的权限。

融合版本的应用，一般会是存在统一的维护入口，或者存在一个公共的管理入口。对于平台同的服务是以统一的方式使用的。例如目前的三云融合项目，融合了友空间、友人才、玩事等多个产品，对于权限、组织、员工等公共数据的维护，都统一在web端的工作台入口中进行。业务产品使用数据时，也都会按照统一的应用的编码进行访问。

因此对于bPaaS平台提供的服务来说，数据应该是按应用进行隔离，业务服务访问数据时，要指定对应的应用编码。总体上的数据隔离可以参考下图。

![](/articles/201806/images/article4/images4.5.png)

## 四、数据访问方式
上面我们讨论了应用的场景和针对不同应用如何隔离数据。那么接下来就是如何使用这些服务。一般一个服务对外提供的能力分为以下几种：
1. 界面
2. 接口服务
3. 事件

对于平台提供的界面，在业务系统使用时，一般会在打开界面时，通过参数指定对应的租户ID和应用编码来控制界面的显示和维护数据的范围。

对于事件来说，在事件的内容中要保护租户和应用的信息，业务系统在接收时，可以根据这两者进行过滤，判断是否要处理。

下面主要讨论一下提供的接口服务如何控制。首先从提供方来说，对于社会级数据，提供的接口是不需要按租户或应用进行隔离的。这部分接口会根据使用场景判断如何控制接口的使用或返回的数据范围。例如:

1. 根据用户ID查询用户的接口：所以的服务都可以调用，但返回的数据只是可公开的数据，不保护用户的私有数据，例如用户的手机号或邮箱会加密处理。在特定领域需要是，需要根据单独的访问授权才可以获取。
2. 应用服务中心的租户查询接口，一般会根据查询的开通过当前应用的范围对数据进行过滤，为开通过应用的租户的相关信息无法访问。
对于其他的bPaaS层的基础数据服务，对数据访问时都应该携带租户、应用参数。访问时根据参数进行过滤查询。

其次针对目前的使用者，存在公有云服务、私有部署服务、软件产品和外部伙伴的服务几种类型的使用者。
	
![](/articles/201806/images/article4/images4.6.png)
	
1. 体系内的公有云服务：基本上按应用控制可使用数据范围。
2. 私有部署服务：一般按应用+租户控制可使用数据范围。
3. 软件产品：与私有部署相同，一般使用的云上的数据是通过定时同步下发的方式，不直接访问云服务界面或服务。基本同私有部署的服务。
4. 外部伙伴服务：同公有云服务，只是使用接口范围受限制。

目前通过通过Rest 服务提供访问的接口，为了保证安全，一般会提供加签校验的逻辑，即需要在统一的服务管理中心申请Accesskey，业务系统根据Accesskey对请求进行签名、将标志和签名结果放入请求参数中，服务方接收请求时会根据强求参数调用服务管理中心查询对应的accesskey进行验签，通过后才允许访问。
在上述的控制基础上，对应用的访问，需要在增加对访问数据范围的控制。基本实现方案如下：

![](/articles/201806/images/article4/images4.7.png)

基本过程如下

1. 申请accesskey时，在accesskey的扩展信息中指定使用的应用和租户（可以为全部应用或租户）。
2. 公有云通过人工申请和分配方式，私有部署的通过租户中心在开通应用时进行开通时直接下载。
3. 在业务服务调用时，通过验签的拦截器时，通过后从accesskey中获取到扩展信息验证，业务可以通过独立的拦截器校验是否满足租户、应用的范围条件。


