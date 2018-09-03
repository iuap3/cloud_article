# Docker实战

作者：（云平台-基础平台服务[**gPaaS**]-容器云平台）**技术架构师**

导读：本文系统性介绍Docker安装、Docker组件、Docker命令、Dockerfile语法和Docker应用。语言平实，介绍全面简介。


## 一、前言
本文将系统性的介绍Docker相关的知识；包含Docker命令，Dockerfile语法，如何用Docker进行构建运行。
## 二、Docker安装
本文以centos7及以上版本为例来说明Docker安装；Docker底层对应的是镜像，不可写的文件系统，它的存储方式比较多。
* AUFS：（AnotherUnionFS）是一种Union FS，是文件级的存储驱动
* Overlay：是一种Union FS，和AUFS的多层不同的是Overlay只有两层：一个upper文件系统和一个lower文件系统，分别代表Docker的镜像层和容器层
* Device mapper：是Linux内核2.6.9后支持的，提供的一种从逻辑设备到物理设备的映射框架机制，在该机制下，用户可以很方便的根据自己的需要制定实现存储资源的管理策略
* Btrfs：被称为下一代写时复制文件系统，并入Linux内核，也是文件级级存储，但可以像Device mapper一直接操作底层设备
* ZFS：文件系统是一个革命性的全新的文件系统，它从根本上改变了文件系统的管理方式，ZFS 完全抛弃了“卷管理”，不再创建虚拟的卷，而是把所有设备集中到一个存储池中来进行管理，用“存储池”的概念来管理物理存储空间
* Overlay2:要取代之前overlay的主要原因是它能“支持多个下层目录”，能解决原先驱动中inode耗尽的问题

本文将以Overlay2进行示例：

1. 升级内核CentOS7.0以上 

1)rpm --import https://www.elrepo.org/RPM-GPG-KEY-elrepo.org 

2)rpm-Uvhhttp://www.elrepo.org/elrepo-release-7.0-3.el7.elrepo.noarch.rpm 

3)yum --enablerepo=elrepo-kernel install kernel-ml-devel kernel-ml -y

4)grub2-mkconfig -o /boot/grub2/grub.cfg 

5)grub2-set-default 0 

6)yum install yum-plugin-ovl -y 

7)reboot重启系统

8)uname -sr看内核是否更新成功

2. 安装镜像仓库

1)清理旧版本

rpm -qa |grep docker
yum  -y  remove docker*

2)安装镜像仓库

yum install  docker-distribution

修改配置文件

vim/etc/docker-distribution/registry/config.yml

![](/articles/201807/images/articles/images1.1.png)

重启镜像仓库

systemctl daemon-reload
service  docker-distribution restart
service  docker-distribution status
访问镜像仓库服务：http://x.x.x.x:5000

3)安装Docker

配置官方yum源

yum install -y yum-utils device-mapper-persistent-data lvm2
yum-config-manager --add-repo http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
yum-config-manager --enable docker-ce-edge
yum-config-manager --enable docker-ce-testing
yum-config-manager --disable docker-ce-edge
yum erase docker-engine-selinux -y
yum makecache fast
安装docker
yum install docker-ce

或者

yum install  docker-ce-18.03.0.ce-1.el7.centos. x86_64


4)配置Docker存储

mkdir -p /etc/systemd/system/docker.service.d/
vi /etc/systemd/system/docker.service.d/docker.conf
[Service]
ExecStart=
ExecStart=/usr/bin/dockerd --exec-opt native.cgroupdriver=cgroupfs --storage-driver=overlay2 --insecure-registry 157.122.99.3:5000 --registry-mirror http://hub.docker.com --data-root /data/lib/docker
加载配置文件
systemctl daemon-reload

5)启动docker

systemctl start docker
查看docker信息
docker info
## 三、Docker组件
Docker基础组件
 
![](/articles/201807/images/articles/images1.2.png)

![](/articles/201807/images/articles/images1.3.png)

* dockerd: Dockerdaemon进程，访问总入口
* docker： Docker 客户端
* docker-containerd：一个控制runC的守护进程，containerd利用runC的高级功能（如seccomp和用户名称空间支持）以及用于容器克隆和实时迁移的检查点和恢复
* docker-containerd-ctr：docker-containerd客户端，基于gPRC APIs通信
* docker-containerd-shim：一个位于运行时实现前面的小垫片，它允许它重新分配来初始化并处理来自调用者的重新附加。
* docker-runc：根据OCI规范产生和运行容器的CLI工具。
## 四、Docker命令
1. 创建一个容器：docker run
eg: docker run –ti –v /var/data:/data/mysql–p 13306:3306 mysql bash
-i：允许我们对容器内的 (STDIN) 进行交互
-t：在新容器内指定一个伪终端或终端
-d: 以daemon方式启动，不能和ti混用
-v：是挂在宿机目录， /var/data是宿机目录，/data/mysq是当前docker容器的目录，宿机目录必须是绝对的。
-p：j将容器内端口映射到宿主机，13306为宿主机上端口，3306为容器端口
--name：是给容器起一个名字，可省略，省略的话docker会随机产生一个名字

2. 查看容器列表：docker ps

3. 查看所有容器：docker ps -a

4. 启动、停止、重启容器： docker start|stop|restart  容器ID｜容器名

5. 查看容器日志：docker logs –f容器ID｜容器名

6. 删除某个容器：docker rm –f容器ID｜容器名

7. 删除所有容器：docker rm $(docker ps -a -q)

8. 查看容器运行状态：docker stats容器ID｜容器名

9. 进入另一个容器：docker exec–ti 容器ID｜容器名

10. 进入容器观察运行情况： docker attach容器ID｜容器名

11. 查看容器详细信息 docker inspect容器ID｜容器名

12. 查看当前机器上镜像 docker images

13. 拉取镜像 docker pull 镜像名

14. 将镜像推送镜像仓库 docker push 镜像名

15. 构建镜像 docker build

16. 将镜像倒出成文件 docker save镜像 > xxx.tar.gz

17. 将文件加载成镜像 docker load < xxx.tar.gz

18. 从容器内复制文件到指定的路径上 docker cp container:path hostpath

19. 登录到Docker registry服务器 docker login

20. 杀掉容器 docker kill 容器ID｜容器名

21. 移除镜像 docker rmi
 
## 五、Dockerfile介绍
Dockerfile是由一些列命令和参数构成的脚本，这些命令应用于基础镜像并最终创建一个新的镜像

常见命令

1. FROM ----基础镜像来源

2. MAINTAINER----维护者是谁

3. RUN----当前基础镜像执行，并且提交新镜像

4. ADD----复制内容到容器中；普通文件，压缩文件，url

5. COPY----本地内容复制到容器中，只能是普通文件及文件夹

6. EXPOSE----告诉Docker服务端容器暴露的端口号,类似docker -p

7. CMD----容器执行命令，每个容器只能执行最后一条命令

8. ENTRYPOINT----容器启动后执行的命令，并且不可被 docker run 提供的参数覆盖

9. ENV----环境变量

10. VOLUME-----容器需要的挂载卷

11. WORKDIR-----后续的 RUN 、 CMD 、 ENTRYPOINT 指令配置工作目录

12. ONBUILD-----配置当所创建的镜像作为其它新创建镜像的基础镜像时，所执行的操作指令

13. USER-----指定运行容器时的用户名或UID，后续的 RUN 也会使用指定用户

## 六、Docker应用
本示例将以平台kubernetes集群日志采集fluentd容器来说明docker是如何使用的
1. 编写fluentd Dockerfile
FROM debian:stretch-slim
MAINTAINER zhangbins@yonyou.com

＃ copy local file to container
COPY clean-apt /usr/bin
COPY clean-install /usr/bin
COPY Gemfile /Gemfile

＃proxy setting， Over the wall
ENV http_proxy=http://10.3.15.206:8888
ENV https_proxy=http://10.3.15.206:8888

＃1.Install & configure dependencies.
＃2.Install fluentd via ruby.
＃3.Remove build dependencies.
＃4. Cleanup leftover caches & files.
RUN BUILD_DEPS="make patch gcc g++ libc6-dev ruby-dev" \
    && clean-install $BUILD_DEPS \
                     ca-certificates \
                     libjemalloc1 \
                     ruby \
    && echo 'gem: --no-document' >> /etc/gemrc \
    && gem install --file Gemfile \
    && apt-get purge -y --auto-remove \
                     -o APT::AutoRemove::RecommendsImportant=false \
                     $BUILD_DEPS \
    && apt-get update \
    && apt-get install -y telnetinetutils-ping vim \
    && clean-apt \
    # Ensure fluent has enough file descriptors
    &&ulimit -n 65536 \
    &&ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
    && echo "Asia/Shanghai" > /etc/timezone 

＃ Copy the Fluentd configuration file for logging Docker container logs.
COPY fluent.conf /etc/fluent/fluent.conf
COPY run.sh /run.sh

＃ Expose prometheus metrics.
EXPOSE 80

ENV LD_PRELOAD=/usr/lib/x86_64-linux-gnu/libjemalloc.so.1

＃ Start Fluentd to pick up our config that watches Docker container logs.
CMD /run.sh $FLUENTD_ARGS

2. 构建镜像
docker build –t10.3.15.191:5000/tools/fluentd-http:0.3 .

![](/articles/201807/images/articles/images1.4.png)

3.运行镜像
宿主机上的/var/log目录映射容器中进行日志采集

![](/articles/201807/images/articles/images1.5.png)

4.查看容器

![](/articles/201807/images/articles/images1.6.png)

5.进入容器

![](/articles/201807/images/articles/images1.7.png)

6.停止容器

![](/articles/201807/images/articles/images1.8.png)

7.查看容器

![](/articles/201807/images/articles/images1.9.png)

8.容器日志

![](/articles/201807/images/articles/images1.10.png)

9.运行状态

![](/articles/201807/images/articles/images1.11.png)

本次docker介绍到这里，还有很多知识没有涉及到，比如说docker网络、docker镜像导入导出等，整个docker知识还是比较广泛的，需要详细去了解和实践； 通过上述介绍我们已经对docker基本操作有了一定了解，下一篇我们将介绍基于docker技术的容器平台。