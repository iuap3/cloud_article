#  4A，夯实企业数字化转型中的身份安全管理（一）

作者：（云平台-专属云服务-应用平台）**产品经理**

导读：什么事4A，既身份认证、账号、授权和审计定义为网络安全的四大组成部分。

随着信息化的迅猛发展，政府、企事业单位的业务系统一直在不断增加中，这些业务系统里记录的都是企业核心的数字资产，因此这些业务系统都要求实现用户账号管理、用户身份认证、访问的授权等必要的跟身份安全相关的保障措施。


## 一、什么是4A

那什么是4A呢？这里的4A，不是国家4A级旅游景区，也不是斗地主里的王炸，而是认证Authentication、账号Account、授权Authorization、审计Audit，简称4A, 认证Authentication、账号Account、授权Authorization、审计Audit，中文名称为统一安全管理平台解决方案。即将身份认证、账号、授权和审计定义为网络安全的四大组成部分，从而确立了身份认证在整个网络安全系统中的地位与作用。

另外身份安全在Gartner的报告里有专门的定义：身份安全称为身份管理，也称身份和访问管理。身份安全主要是为了确保正确的人能够在正确的时间，因为正确的原因访问正确的资源。身份安全更多的是解决越来越多在异构技术环境下确保对资源正确访问的需求，从而满足日益严格的合规要求。

因此，4A可以帮助企业建立统一身份管理、认证与授权平台，使企业的用户身份信息、授权信息、身份认证和访问控制机制规范化、标准化，帮助企业做到4A（账户Account、认证Authentication、授权Authorization、审计Audit）统一，提高控制安全风险的能力。

![](/articles/201806/images/article9/images9.1.png)

## 账号管理

同在现实世界中一样，在软件系统中我们每一个人都有一个身份，这个身份就是登陆某个系统的用户ID。这个身份一旦被盗用，那就意味着风险将至，这个风险的大小跟系统的价值密切相关。因此，自从有了软件系统，身份安全就一直被重视，无论是采用密码、双因素认证、安全令牌，亦或最近越来越火的生物特征识别等，它们的目的均是一个，保障身份安全而不被恶意使用。

随着信息化的发展，企业的各种业务系统越来越多，这导致企业员工的账号繁多，管理困难，管理成本较高，难以实现账号权限的有效监督和审核，难以维护有效的用户账号列表，当维护人员同时对多个系统进行维护时，工作复杂度会成倍增加；因此需要为用户提供统一集中的账号管理，不仅能够实现被管理资源账号的创建、删除及同步等账号管理生命周期所包含的基本功能，而且也可以通过平台进行账号密码策略，密码强度、生存周期的设定。

## 认证管理

虽说目前大多数系统采用基本的账号与口令方式进行认证，但是随着技术的进步，认证手段一直在发展和完善中，目前可以根据用户应用的实际需要，为用户提供不同强度的认证方式，既可以保持原有的静态口令方式，又可以提供具有双因子认证方式的高强度认证（一次性口令、数字证书、动态口令），而且还能够集成现有其它如生物特征等新型的认证方式，如指纹，人脸识别等。

身份认证以数据加密，数字签名等安全技术为基础，同时考虑身份认证、信息传输等安全因素，以实现强有力的身份认证功能。

目前的认证管理不仅可以实现用户认证的统一管理，并且能够为用户提供统一的认证门户，实现企业信息资源访问的单点登录。

## 授权管理

企业的各种业务系统越来越多，这就带来“分散”管理的问题——系统分别属于不同的专业进行管理，目前各系统都有一套独立的认证、授权和审计机制，分别由相应的系统管理员负责维护和管理。“分散”管理难于实现统一信息安全策略，不符合“维护集中化”“管理信息化”等改革思路。可以对用户的资源访问权限进行集中控制。它既可以实现对应用系统资源的访问权限控制，也可以实现对数据库、主机及网络设备的操作的权限控制，资源控制类型既包括功能模块，也包括数据库的数据、记录及主机、网络设备的操作命令、IP地址及端口。

## 审计管理

目前企业的各种业务系统，有些对用户行为的审计和跟踪缺失，同时日志和审计手段分散在各个系统和设备中，容易造成日志信息丢失，缺乏集中统一的系统访问审计，审计操作复杂，无法对支撑系统进行综合分析，不能及时发现危害系统安全的事件；因此将用户所有的操作日志集中记录管理和分析，不仅可以对用户行为进行监控，并且可以通过集中的审计数据进行数据挖掘，以便于事后的安全事故责任的认定。
综上所述，4A的首要目标就是：从用户登录系统到权限授予到登出系统的整个过程中，根据需要在恰当的条件下及时赋予正确的用户对企业内适当数据资源的访问权。
