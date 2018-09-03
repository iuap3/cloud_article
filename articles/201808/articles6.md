# 微服务项目实践之中建项目

作者：（云平台-基础平台服务[gPaaS]-微服务治理平台）技术专家

## 中建项目简介:

中建项目全程是”用友建筑分公司上云项目”目标是支撑建筑分公司将原有技术架构迁移到用友云的专属云上，完成上云过程，因此该项目是一场支持建筑分公司的”友谊战”。

用友建筑是用友股份的旗下子公司，在子公司"上云"战役中，中建是第一个从其他框架迁移到微服务的，支撑好中建项目的重要意义不言而喻; 

中建项目的迁移过程中遇到很多问题，比如:微服务框架兼容性问题、原项目规范如日志规范改变问题、开发者中心和微服务在一些细节方面用户提示不够人性化、环境本身问题等；

在模块多时间紧的情况下，建筑分公司将平台和模块划分给团队，落实到每个人负责迁移的项目；股份公司云平台也划分开发者中心和微服务给不同人员，分别通过瞩目远程会议，去武汉分公司出差及驻留北京建筑分公司的方式将问题一一排查和解决。

中建项目进展顺利，建筑同事和股份公司云平台同事群策群力，目标一致，基情满满，齐头并进一起加班是项目组的真实写照。



## 用友建筑上云过程:

用友建筑上云前分析了建筑的原有平台业务和技术框架, 制定了相关迁移方案:

### 原有业务架构分析:

用友建筑平台模块划分:

![](/articles/201808/images/articles6/images6.1.png)

用友建筑原有系统架构:

![](/articles/201808/images/articles6/images6.2.png)

### 迁移目标制定:

针对用友建筑的当前情况, 并且应总部818完成上线的要求, 制定了迁移目标:

首先迁移iCOP基础平台和i建造业务模块, i设计、i纪检、i审计及i合约这四个业务平台暂不做迁移;

iCOP基础平台在原有环境保留一份以支持未迁移的i设计、i纪检、i审计及i合约;

并且首先在测试环境完成迁移和功能测试，并做切流测试;

完成后将方案应用到线上环境, 完成线上环境切流迁移。

![](/articles/201808/images/articles6/images6.3.png)

### 迁移方案制定:

迁移的技术方案制定:
* 针对用友建筑原有的Dubbo框架,制定了迁移到用友云微服务迁移方案:

iCOP基础平台和i建造改造原有代码, 使用profile机制分别编译出Dubbo及用友微服务两套代码。

使用iris-dubbo-support组件支持使用dubbo的配置方式配置用友微服务。

![](/articles/201808/images/articles6/images6.4.png)

* 针对用友建筑原有的SpringCloudConfig方案, 为兼容用友云微服务制定了外挂方案:

![](/articles/201808/images/articles6/images6.5.png)

* 同一jenkins部署测试环境和线上环境的方案:

针对用友云持续集成插件app-upload-plugin设置推送到开发者中心的环境地址;

![](/articles/201808/images/articles6/images6.6.png)

### 上云相关流程/规范:

建筑上云流程:

![](/articles/201808/images/articles6/images6.7.png)


* 部署资源设置大小参考:

![](/articles/201808/images/articles6/images6.8.png)

## 用友建筑上云后...

### 上云后的部署形态:

![](/articles/201808/images/articles6/images6.9.png)

### 上云后的微服务优化分析:

传统业务迁移到用友云后, 用友云提供的各类功能有针对性的对微服务的各个维度进行分析和管理:

![](/articles/201808/images/articles6/images6.10.png)

通过以上功能分析出业务潜在的问题, 为微服务解耦和性能优化提供了参考依据, 举个栗子:
* 通过微服务依赖统计调用图分析出被严重依赖的微服务和频繁调用的微服务, 如下图中的icop-orgcenter-web无论在被依赖程度还是被调用次数上都是第一, 属于重点解耦和优化对象。

* 根据微服务热力图直观的看出耦合程度和被调用次数(被调用次数与颜色成正比: 绿 < 蓝 < 黄 < 红 < 深红):

![](/articles/201808/images/articles6/images6.11.png)

* 并且统计出了业务的潜在频繁调用问题:

自上线后的一周内所有项目共发起RPC调用21593770次,但约90%的RPC集中在一个API, 大部分API的RPC调用都在0-2万次之间。

以下是调用次数超过两万的相关API统计:

<table>
   <tr>
      <td>调用方</td>
      <td>被调用方</td>
      <td>调用接口</td>
      <td>调用API名称</td>
      <td>调用次数</td>
   </tr>
   <tr>
      <td>icop-technology-web</td>
      <td>icop-orgcenter-web</td>
      <td>com.yyjz.icop.orgcenter.company.service.ICompanyService</td>
      <td>getCompanyParentById (java.lang.String)</td>
      <td>1970，8554</td>
   </tr>
   <tr>
      <td>icop-support-web</td>
      <td>icop-orgcenter-web</td>
      <td>com.yyjz.icop.orgcenter.company.service.ICompanyService</td>
      <td>getChildrenCompanyById (java.lang.String)</td>
      <td>117，9889</td>
   </tr>
   <tr>
      <td>icop-usercenter-web</td>
      <td>icop-orgcenter-web</td>
      <td>com.yyjz.icop.orgcenter.staff.service.StaffService</td>
      <td>getStaffByUserId (java.lang.String)</td>
      <td>6，0645</td>
   </tr>   
</table>

## 总结：建筑上云1+1, 赋能用友建筑云:
	
用友云-专属云提供的能力支持:

![](/articles/201808/images/articles6/images6.12.png)

建筑服务上云, 用友云提供DevOps最佳实践和微服务框架及分析机制, 统一的监控平台和运维规范, 最终实现1+1大于2的效果, 助力用友建筑业务更快更好发展。

