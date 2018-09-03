# 基于开发者中心〈DevOps流水线〉快速上云

作者：（云平台-基础平台服务[gPaaS]-DevOps平台）软件工程师

导读：“DevOps”这个词现在很流行，它具体指的是什么呢？本文介绍了DevOps和开发者中心DevOps流水线，图文
并茂，解答您的疑惑。

那么DevOps是什么？开发者中心〈DevOps流水线〉是什么？或许在这里能解决你的一些疑惑......

![](/articles/201807/images/articles5/images5.1.png)

**DevOps是什么？**

“DevOps”是现在非常流行的一个词，它代表的是什么呢？是一种理念？还是一种工具？还是一种技术？其实觉得
迷茫的绝对不止您一个人。
词意表述为“软件开发人员(Dev)”和“IT运维技术人员（Ops）”之间沟通合作的文化、运动或实践。其实可以理
解为通过自动化“软件交付”和“架构变更”的流程，来使得构建、测试、发布软件能够更加地敏捷、频繁和可靠
。

**那么开发者中心〈DevOps流水线〉是什么呢？**

可以理解为一种通过自动化“软件交付”的方案及实现,那么我们先来了解下整体架构。

开发者中心<DevOps流水线>部分流程总览

![](/articles/201807/images/articles5/images5.2.png)

开发者中心DevOps流水线运行效果

![](/articles/201807/images/articles5/images5.3.png)

![](/articles/201807/images/articles5/images5.4.png)

流水线基于Git获取代码源解惑
支持两种方式:ssh、 http

1. ssh方式

使用Git -i指定私钥文件。（借助一个shell脚本来实现）
脚本源码：


```
＃!/bin/bash

＃ The MIT License (MIT)
＃ Copyright (c) 2013 Alvin Abad

if [ $# -eq0 ]; then
echo"Git wrapper script that can specify an ssh-key file
Usage:
git.sh -issh-key-file git-command
"
exit 1
fi

＃ remove temporary file on exit
trap'rm -f /tmp/.git_ssh.$$' 0

if [ "$1" = "-i" ]; then
SSH_KEY=$2; shift; shift
echo"#!/bin/bash"> /tmp/.git_ssh.$$
echo"ssh -i$SSH_KEY \$@">> /tmp/.git_ssh.$$
chmod +x /tmp/.git_ssh.$$
export GIT_SSH=/tmp/.git_ssh.$$
fi

＃ in case the git command is repeated
[ "$1" = "git" ]&&shift

＃ Run the git command
git"$@"


```

2. http方式

使用git clone 命令直接下载,具体如下:


```
git clone http://${Password}:${UserName}@github.com/yangxyd/xxx.git
```
**流水线配置中心解惑**

使用配置中心功能：把需要修改的配置文件提取到配置中心，在容器启动前会从配置中心拉取相关配置到指定的目
录下。使用说明如下:

![](/articles/201807/images/articles5/images5.5.png)

配置后，通过容器控制台即可查看替换后的文件内容。

![](/articles/201807/images/articles5/images5.6.png)

![](/articles/201807/images/articles5/images5.7.png)

至此，先解惑到这儿，更多精彩，欢迎您来开发者中心体验。

有意向部署企业云平台或想了解用友云开发者中心的用户，欢迎拨打我们的服务热线：_010-86393388_或者进行在
线留言，我们将为您提供贴心到位的企业上云顾问服务。









