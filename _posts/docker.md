---

title: Getting Started
author: MR yan
date: 2020-10-19 20:55:00 +0800
categories: [devolp, deploy]
tags: [开发-部署]
pin: true
---

# 应用容器平台-Docker

# 0. 课程目标

- 熟悉Docker的基本概念
- 理解Docker的几个对象概念
- 掌握Docker的安装和启动
- 掌握Docker的镜像操作
- 掌握Docker的容器操作
- 掌握Docker的部署案例
- 熟悉Docker的备份和迁移
- 掌握Dockerfile构建镜像的基本使用
- 了解Docker私有注册中心

# 1.Docker的基本概念

## 1.1 什么是容器？

先来看看容器较为官方的解释：

一句话概括容器：容器就是将软件打包成标准化单元，以用于开发、交付和部署。

如果需要通俗的描述容器的话，容器就是一个存放东西的地方，就像书包可以装各种文具、衣柜可以放各种衣服、鞋架可以放各种鞋子一样。我们现在所说的容器存放的东西可能更偏向于应用比如网站、程序甚至是系统环境。

[![1.png](assets/0eb95638b712ca6ad211c76f73a366af.png)](http://dockone.io/uploads/article/20190626/0eb95638b712ca6ad211c76f73a366af.png)

## 1.2  容器 VS 虚拟机

物理机：

![2.jpeg](assets/e9444d264eeaea2b178a71c9ed823c9c.jpeg)

虚拟机：

![3.jpeg](assets/bb23f04f2b23b2312b04ba87dc8ad31d.jpeg)

容器：

![4.jpeg](assets/e34f0f2a4b8718f09c8b366a14d5e9a9.jpeg)

相信通过上面的解释大家对于容器这个既陌生又熟悉的概念有了一个初步的认识，下面我们就来谈谈Docker的一些概念。

**两者对比图**

简单来说： 容器和虚拟机具有相似的资源隔离和分配优势，但功能有所不同，因为容器虚拟化的是操作系统，而不是硬件，因此容器更容易移植，效率也更高。

虚拟机技术：是虚拟出一套计算机硬件后，在这套硬件上安装并运行一个完整的操作系统，然后就可以像使用一台真实计算机一样，在该机器上安装被运行各种应用。

容器技术：是一个共享操作系统内核的虚拟化技术。不会虚拟化硬件，容器的运行要依赖于宿主的内核，容器内没有自己的内核。因此容器要比传统虚拟机更为轻便。

[![7.png](assets/2e2b95eebf60b6d03f6c1476f4d7c697.png)](http://dockone.io/uploads/article/20190626/2e2b95eebf60b6d03f6c1476f4d7c697.png)

**容器与虚拟机 (VM) 总结**

[![8.png](assets/4ef8691d67eb1eb53217099d0a691eb5.png)](http://dockone.io/uploads/article/20190626/4ef8691d67eb1eb53217099d0a691eb5.png)

- 容器: 用于将代码和依赖资源打包在一起。 多个容器可以在同一台机器上运行，共享操作系统内核，但各自作为独立的进程在用户空间中运行 。与虚拟机相比， 容器占用的空间较少（容器镜像大小通常只有几十兆），瞬间就能完成启动 。
- 虚拟机（VM）是一个物理硬件层抽象，用于将一台服务器变成多台服务器。 管理程序允许多个VM在一台机器上运行。每个VM都包含一整套操作系统、一个或多个应用、必要的二进制文件和库资源，因此占用大量空间。而且VM启动也十分缓慢 。

两者有不同的使用场景,虚拟机更擅长于彻底隔离整个运行环境。

**并且两者也可以共存的：**

[![9.png](assets/056c87751b9dd7b56f4264240fe96d00.png)](http://dockone.io/uploads/article/20190626/056c87751b9dd7b56f4264240fe96d00.png)



## 1.3 什么是Docker

Docker 是一个开源的应用容器引擎，让开发者可以打包他们的应用以及依赖包到一个可移植的容器中,然后发布到任何流行的[Linux](https://baike.baidu.com/item/Linux)机器或Windows 机器上。



![img](assets/f703738da977391281957edbf0198618377ae2dd.jpg)

#### Docker服务器与客户端

```
Docker是一个客户端/服务端(C/S)架构程序。Docker客户端只需要向Docker服务器或者守护进程发送请求，服务器或者守护进程完成所有工作并返回结果。Docker提供了一个命令行工具Docker以及一整套的Restful API。 你可以在同一台宿主机上运行Docker守护进程和客户端。也可以从本地的Docker客户端连接到运行在另一台宿主机上的远程Docker守护进程
```

![1564158400842](assets/docker002.png)

英文官网：

https://www.docker.com/

中文社区：

http://www.docker.org.cn/

## 1.4 Docker的优点

```
(1) 上手快、体积小、性能高
	用户只需要几分钟，就可以把自己的程序"Docker化"。就可以创建容器来运行程序了，大多数Docker容器只需要不到1秒中即可启动。由于去除了管理程序的开销，Docker容器拥有很高的性能，同时同一台宿主机中也可以运行更多的容器，使用户尽可能的充分利用系统资源。
	
（2）职责的逻辑分类
	使用Docker,开发人员只需要关心容器中运行的应用程序，而运维人员只需要关心如何管理容器。Docker设计的目的就是要加强开发人员写代码的开发环境与应用程序要部署的生产环境一致性。从而降低那种“开发时一切正常，肯定是运维的问题 （测试环境都是正常，一上线就出问题肯定是运维的问题）
	
（3）快速高效的开发生命周期
	Docker的目标之一就是是缩短代码从开发、测试到部署、上线运行的周期，让你的应用程序具备可一致性，易于构建，并易于协作。（通俗点说，Docker就像一个盒子，里面可以装很多物件，如果需要这些物件的可以直接将该大盒子拿走，而不需要从该盒子中一件件的取）
	
（4）鼓励使用面向服务的架构
	Docker还鼓励面向服务的体系结构和微服务架构。Docker推荐单个容器只运行一个应用程序或进程，这样就形成了一个分布式的应用程序模型，在这种模型下，应用程序或者服务都可以表示为一系列内部互联的容器，从而使分布式部署应用程序，扩展或调试应用程序都变得非常简单。

```

# 2.Docker的安装和启动

## 2.1 Docker的安装和配置

资源中提供了虚拟机镜像，已经安装了Docker 

具体操作详见 资源中Docker安装文档

## 2.2 Docker服务的启动停止

刚安装好的Docker并没有启动，需要通过系统服务命令的方式来启动。

比如：要运行查看Docker的概要信息的命令`info`:

```
docker info
```

控制台会出现：

```shell
[root@bobohost ~]# docker info
Client:
 Debug Mode: false

Server:
ERROR: Cannot connect to the Docker daemon at unix:///var/run/docker.sock. Is the docker daemon running?
errors pretty printing info
```

在Centos7中，可以使用系统服务管理器指令`systemctl`来启动Docker服务，该命令可以认为是 `service` 和 `chkconfig` 两个命令组合。Centos6中只能使用`service`指令。

相关命令如下：

查看docker服务的启动状态

```shell
systemctl status docker
```

启动docker服务：

```shell
systemctl start docker
```

停止docker服务：

```shell
systemctl stop docker
```

重启docker服务：

```shell
systemctl restart docker
```

加入到开机启动（生产环境下一般要系统启动时自动运行Docker服务）：

```shell
systemctl enable docker
```

查看docker所有命令：

```
docker --help
```

官方命令手册地址：

https://docs.docker.com/engine/reference/commandline/

## 2.3 Docker中的组件

#### 镜像（Image）——一个特殊的文件系统

```
Docker镜像是一个特殊的文件系统，除了提供容器运行时所需的程序、库、资源、配置等文件外，还包含了一些为运行时准备的一些配置参数（如匿名卷、环境变量、用户等）。 镜像不包含任何动态数据，其内容在构建之后也不会被改变。
```

#### 容器（Container）——镜像运行时的实体

```
镜像（Image）和容器（Container）的关系，就像是面向对象程序设计中的类和实例一样，镜像是静态的定义，容器是镜像运行时的实体。容器可以被创建、启动、停止、删除、暂停等 。
```

#### 注册中心（Registry）——集中存放镜像仓库的地方

```
镜像构建完成后，可以很容易的在当前宿主上运行，但是， 如果需要在其它服务器上使用这个镜像，我们就需要一个集中的存储、分发镜像的服务，Docker Registry就是这样的服务。

一个Docker Registry中可以包含多个仓库（Repository）；
每个仓库可以包含多个标签（Tag）；
每个标签对应一个镜像。
所以说：镜像仓库是Docker用来集中存放镜像文件的地方类似于我们之前常用的代码仓库。

通常，一个仓库会包含同一个软件不同版本的镜像，而标签就常用于对应该软件的各个版本 。我们可以通过<仓库名>:<标签>的格式来指定具体是这个软件哪个版本的镜像。
```

```
Docker Registry 分为 公开服务和私有服务的概念：
Docker Registry公开服务是开放给用户使用、允许用户管理镜像的Registry服务。

最常使用的Registry公开服务是官方的Docker Hub，这也是默认的Registry，并拥有大量的高质量的官方镜像，网址为：hub.docker.com/ 。在国内访问Docker Hub可能会比较慢国内也有一些云服务商提供类似于Docker Hub的公开服务。
```

# 3. Image镜像操作

## 4.1 查找镜像

需求：

查询一下Docker Hub上有没有需要的镜像。

语法：

```none
docker search [OPTIONS] TERM
```

选项参数：

| Name, shorthand | Default | Description                                                  |
| --------------- | ------- | ------------------------------------------------------------ |
| `--automated`   |         | [**deprecated**](https://docs.docker.com/engine/deprecated/) Only show automated builds |
| `--filter , -f` |         | Filter output based on conditions provided                   |
| `--format`      |         | Pretty-print search using a Go template                      |
| `--limit`       | `25`    | Max number of search results                                 |
| `--no-trunc`    |         | Don’t truncate output                                        |
| `--stars , -s`  |         | [**deprecated**](https://docs.docker.com/engine/deprecated/) Only displays with at least x stars |

示例：

列出Docker Hub上包含“centos”关键字的的镜像：

```
docker search centos
```

该命令一般只用于查看是否存在拥有关键字的镜像。

![1564128665346](E:/AB%E5%A4%87%E8%AF%BE%E8%AF%BE%E4%BB%B6/10_%E9%A1%B9%E7%9B%AE%E4%BA%8C%E5%89%8D%E7%BD%AE%E8%AF%BE%E7%A8%8B/%E5%BC%A0%E6%B3%A2%E9%A1%B9%E7%9B%AE%E4%BA%8C%E5%89%8D%E7%BD%AE%E8%AF%BE/01_%E5%BA%94%E7%94%A8%E5%AE%B9%E5%99%A8-Docker/01_%E8%AE%B2%E4%B9%89/docker.assets/1564128665346.png)

- NAME：仓库名称
- DESCRIPTION：镜像描述
- STARS：用户评价，反应一个镜像的受欢迎程度
- OFFICIAL：是否官方
- AUTOMATED：自动构建，表示该镜像由Docker Hub自动构建流程创建的

通常，我们更喜欢使用docker hub提供的一个网站来搜索需要的镜像：[https://hub.docker.com](https://hub.docker.com/)

![1564128580902](E:/AB%E5%A4%87%E8%AF%BE%E8%AF%BE%E4%BB%B6/10_%E9%A1%B9%E7%9B%AE%E4%BA%8C%E5%89%8D%E7%BD%AE%E8%AF%BE%E7%A8%8B/%E5%BC%A0%E6%B3%A2%E9%A1%B9%E7%9B%AE%E4%BA%8C%E5%89%8D%E7%BD%AE%E8%AF%BE/01_%E5%BA%94%E7%94%A8%E5%AE%B9%E5%99%A8-Docker/01_%E8%AE%B2%E4%B9%89/docker.assets/1564128580902.png)



## 4.2 拉取镜像

说明：

从注册中心上拉取下载需要的镜像。

语法：

```shell
docker pull [OPTIONS] NAME[:TAG|@DIGEST]
```

选项参数：

| Name, shorthand           | Default | Description                                                  |
| ------------------------- | ------- | ------------------------------------------------------------ |
| `--all-tags , -a`         |         | Download all tagged images in the repository                 |
| `--disable-content-trust` | `true`  | Skip image verification                                      |
| `--platform`              |         | [**experimental (daemon)**](https://docs.docker.com/engine/reference/commandline/dockerd/#daemon-configuration-file)[**API 1.32+**](https://docs.docker.com/engine/api/v1.32/) Set platform if server is multi-platform capable |
| `--quiet , -q`            |         | Suppress verbose output                                      |

【示例】

（1）拉取centos仓库中的镜像

```shell
docker pull centos
```

docker镜像名字组成：`注册中心/仓库名字:标记`，如：`docker.io/library/centos:7.6.1810`

但如果是从官方docker hub下载镜像，可以省略注册中心，可以写成：`仓库名字:标记`，例如`centos:7.6.1810`

标记一般是类似于版本号的组成方式，它支持`x.y.z`语义化版本方式，并能自动识别。

比如拉取镜像操作中的使用：

```
centos:7.6.1810----->下载的就是7.6.1810
centos:7.6  ------->下载7.5.最高版本 的版本
centos:7    ------->下载7系列最高的版本
centos:6    ------->下载6系列最高的版本
centos:latest   ------->下载最高的版本,省略版本号时就是latest
centos   ------->下载最高的版本,省略版本号时就是latest

```

如果要下载指定版本的镜像，可以执行命令：

```shell
docker pull centos:7.6.1810
```

对于本节案例，标记不写，将使用默认的标记latest，即下载的是centos最新版本，即相当于下载的命令为：

```
docker pull centos:latest

```

因为最新版本不断的会更新，因此，企业中使用Docker一般会使用完整的语义化版本的标记方式。

【了解】

要退出终止正在进行的下载，可以在终端中使用`CTRL-c` 。



## 4.3 查看镜像

说明：

查看本地已有的镜像，镜像可以是下载的，也可以是自己构建的。

语法：

```shell
docker images  [OPTIONS] [REPOSITORY[:TAG]]
```

选项参数：

| Name, shorthand | Default | Description                                         |
| --------------- | ------- | --------------------------------------------------- |
| `--all , -a`    |         | Show all images (default hides intermediate images) |
| `--digests`     |         | Show digests                                        |
| `--filter , -f` |         | Filter output based on conditions provided          |
| `--format`      |         | Pretty-print images using a Go template             |
| `--no-trunc`    |         | Don’t truncate output                               |
| `--quiet , -q`  |         | Only show numeric IDs                               |

示例：

列出本地所有的镜像：

```shell
docker images
```

根据仓库名字和标记来列出本地镜像，

```shell
#列出"centos"仓库中的所有镜像：
docker images centos

#列出标记为7.6.1810的"centos"仓库中的所有镜像：
docker images centos:7.6.1810

#列出镜像信息中有centos的镜像
docker images |grep centos
```



## 4.4 本地镜像的删除

说明：

删除一个或多个镜像

语法：

```none
docker rmi [OPTIONS] IMAGE [IMAGE...]
```

选项：

| Name, shorthand | Default | Description                    |
| --------------- | ------- | ------------------------------ |
| `--force , -f`  |         | Force removal of the image     |
| `--no-prune`    |         | Do not delete untagged parents |

【示例】

删除centos的镜像

```
docker rmi centos

```

删除所有镜像（慎用）

```
docker rmi `docker images -q`
```



# 4. Container容器操作

Docker 借鉴了标准集装箱的概念。标准集装箱将货物运往世界各地，Docker 将这个模型运用到自己的设计中，唯一不同的是：集装箱运输货物，而 Docker 运输软件。

和集装箱一样，Docker 在执行上述操作时，并不关心容器中到底装了什么，它不管是web 服务器，还是数据库，或者是应用程序服务器什么的。所有的容器都按照相同的方式将内容“装载”进去。

像标准集装箱一样，Docker 容器方便替换，可以叠加，易于分发，并且尽量通用。



## 5.1 查看容器

用途：列出容器。

语法：

```none
docker ps [OPTIONS]
```

选项参数：

| Name, shorthand | Default | Description                                             |
| --------------- | ------- | ------------------------------------------------------- |
| `--all , -a`    |         | Show all containers (default shows just running)        |
| `--filter , -f` |         | Filter output based on conditions provided              |
| `--format`      |         | Pretty-print containers using a Go template             |
| `--last , -n`   | `-1`    | Show n last created containers (includes all states)    |
| `--latest , -l` |         | Show the latest created container (includes all states) |
| `--no-trunc`    |         | Don’t truncate output                                   |
| `--quiet , -q`  |         | Only display numeric IDs                                |
| `--size , -s`   |         | Display total file sizes                                |

【示例】

（1）列出所有正在运行的容器：

```shell
docker ps
```



（2）显示所有容器，包括正在运行的和停止的。

```shell
docker ps -a
```

- -a：显示正在运行的和停止的容器。该参数也可以写成`--all`或`--all=true`。



（3）查看停止了的容器列表（了解）

```
docker ps -f status=exited
#或
docker ps -a |grep exited

```

- -f：过滤结果，该参数也可以写成`--filter`。
- status：是`-f`参数中的参数，指的是容器的状态，该状态的值有：`created`, `restarting`, `running`, `removing`, `paused`, `exited`,或 `dead`。



4.2 容器的创建

语法：

```none
docker run [选项] 镜像名称:版本号 [命令] [ARG...]
```

```
常用选项：
	-i: 以交互模式运行容器，通常与 -t 同时使用；
	-t: 为容器重新分配一个伪输入终端，通常与 -i 同时使用；
	
	-d: 在run后面加上-d参数，则会创建一个守护式容器在后台运行（这样容器创建后，就不会登陆到容器中）
	
	--name: 创建容器的名称
	
	-v: 表示目录映射关系（前者是宿主机目录，后者是映射到容器上的目录），可以使用多个-v做多个目录的映射。注意：做好映射后，最好在宿主机中更改文件
	
	-p: 表示端口映射，前者是宿主机端口，后者是容器内的映射端口。可以使用多个-p做多个端口映射
```

根据平时的使用方式，我们分别以交互式容器和守护式容器的创建来讲解：

（一）交互式容器

创建一个用于测试的容器，容器创建成功后自动分配伪终端，可进行人机交互。

创建运行一个centos的容器：

```shell
docker run -it --name=mycentos centos /bin/bash
#或
docker run -i -t --name=mycentos centos /bin/bash

# 退出容器
exit
```

```
bash：分配伪终端时要在容器上执行的命令，这里使用的linux的bash脚本命令，该命令完整写法为`/bin/bash`。

提示：

`run`和镜像名字之间的选项没有顺序，但命令必须放到镜像名字之后。

优点：

创建完容器后，自动运行容器，并可以直接进入到子容器系统中操作了，主要用于测试使用。

缺点：

当退出子容器后，该容器会自动停止运行。
```

（二）守护式容器：

创建一个需要长期运行的容器，就可以创建一个守护式容器（后台运行的容器），下面的命令用于在后台创建运行容器并打印容器ID：

```shell
docker run -id --name=mycentos2 centos:7.6.1810
#或
docker run -id --name mycentos2 centos:7.6.1810
```

- -d：在后台运行容器并打印容器ID。

登录守护式容器方式：

```
docker exec -it container_name (或者 container_id)  /bin/bash（exit退出时，容器不会停止）
```

比如：

```
方式1：使用名字进入
docker exec -it mycentos2 bash 
[root@2c32a5cb4a71 /]# 
方式2：使用id进入
docker exec -it 2c32a5cb4a71 bash
[root@2c32a5cb4a71 /]#  
```

优点：

从守护式容器中退出，并不影响容器的运行。

缺点：

必须的手动命令进入到容器。

小结：

【理解】

run命令的本质是两个命令的结合：create+start

## 4.3 容器的停止启动挂起

一、容器的停止

说明：

停止一个或多个正在运行的容器

语法：

```none
docker stop [OPTIONS] CONTAINER [CONTAINER...]
```

选项：

| Name, shorthand | Default | Description                                |
| --------------- | ------- | ------------------------------------------ |
| `--time , -t`   | `10`    | Seconds to wait for stop before killing it |

【示例】

停止正在运行的mycentos2容器：

```
docker stop mycentos2

```

二、容器的启动

说明：

启动一个或多个已经停止了的容器

语法：

```none
docker start [OPTIONS] CONTAINER [CONTAINER...]
```

选项：

| Name, shorthand      | Default | Description                                                  |
| -------------------- | ------- | ------------------------------------------------------------ |
| `--attach , -a`      |         | Attach STDOUT/STDERR and forward signals                     |
| `--checkpoint`       |         | [**experimental (daemon)**](https://docs.docker.com/engine/reference/commandline/dockerd/#daemon-configuration-file) Restore from this checkpoint |
| `--checkpoint-dir`   |         | [**experimental (daemon)**](https://docs.docker.com/engine/reference/commandline/dockerd/#daemon-configuration-file) Use a custom checkpoint storage directory |
| `--detach-keys`      |         | Override the key sequence for detaching a container          |
| `--interactive , -i` |         | Attach container’s STDIN                                     |

【示例】

启动mycentos2容器

```shell
docker start mycentos2
```

三、重启容器

说明：

重启一个或多个容器。

语法：

```none
docker restart [OPTIONS] CONTAINER [CONTAINER...]
```

选项：

| Name, shorthand | Default | Description                                           |
| --------------- | ------- | ----------------------------------------------------- |
| `--time , -t`   | `10`    | Seconds to wait for stop before killing the container |

【示例】

重启mycentos2容器

```shell
docker restart mycentos2
```

四、暂停容器

说明：

暂停（挂起）一个或多个容器中的进程。

语法：

```
docker pause CONTAINER [CONTAINER...]

```

【示例】

暂停挂起mycentos2容器

```shell
docker pause mycentos2
```

四、取消暂停容器

说明：

取消暂停（挂起）一个或多个容器中的进程

语法：

```
docker unpause CONTAINER [CONTAINER...]

```

【示例】

取消暂停挂起mycentos2容器

```shell
docker pause mycentos2
```

## 4.4 文件的拷贝

说明：

在容器和本地文件系统之间复制文件/文件夹。

```
# 如果我们需要将文件拷贝到容器内可以使用cp命令
docker cp 需要拷贝的文件或目录 容器名称:容器目录
```

如：将宿主机的文件拷贝到mycentos2中

```shell
#在宿主机上创建一个空文件test.txt
touch test.txt
#将test.txt拷贝到mycentos2容器的根目录中：
docker cp test.txt mycentos2:/
```

验证效果：进入到容器中，可以查看到刚拷贝的文件。

也可以将文件从容器内拷贝出来

```
docker cp 容器名称:容器目录或文件 需要拷贝的文件或目录
```

如：从mycentos2容器拷贝文件到宿主机器的当前目录中：

```shell
#在宿主机先删除test.txt文件
rm -f test.txt
#将mycentos2容器中的根目录的test.txt拷贝到宿主机的当前目录中：
docker cp mycentos2:/test.txt ./
```

## 4.5 目录挂载 

说明：

宿主机的目录的挂载映射到容器中。

我们可以在创建容器的时候，将宿主机的目录与容器内的目录进行映射，这样我们就可以通过修改宿主机某个目录的文件从而去影响容器。 

语法：

```
docker run -v `宿主机目录`:`容器目录` image
```

- -v：将当前工作目录装载到容器中。绑定装载卷的宿主机目录不存在时，Docker会自动在宿主机上为您创建这个目录。

【示例】

将宿主机上的`/root/myvolume`目录挂载到`mycentos3`中的`/myvolume`目录中：

```
#进入到宿主机目录，建立新目录和新的文件：
#mkdir myvolume
docker run -id --name=mycentos3 -v /root/myvolume:/myvolume centos:7.6.1810
或
docker run -id --name=mycentos3 -v $(pwd)/myvolume:/myvolume centos:7.6.1810
```

提示：宿主机的目录必须是以`/`或`~`开头。



## 4.6 容器的删除

删除一个或多个容器。

语法：

```none
docker rm [OPTIONS] CONTAINER [CONTAINER...]
```

选项：

| Name, shorthand  | Default | Description                                             |
| ---------------- | ------- | ------------------------------------------------------- |
| `--force , -f`   |         | Force the removal of a running container (uses SIGKILL) |
| `--link , -l`    |         | Remove the specified link                               |
| `--volumes , -v` |         | Remove the volumes associated with the container        |

【示例】

（1）先停止运行的mycentos3的容器，再删除它。

```shell
docker stop mycentos3
docker rm mycentos3
```

提示：

上述命令默认只能删除停止了的容器。若容器是启动的状态，则可以先停止容器，再删除。

（2）直接强制删除正在运行的mycentos2容器

```shell
docker rm -f redis
#或者
docker rm --force redis
```

（3）强制删除所有的容器

```shell
docker rm -f `docker ps -qa`
#或
docker rm -f $(docker ps -a -q)
```

（4）删除容器时，将其关联的卷也删掉（了解）

此命令将删除容器及其关联的任何卷。请注意，如果使用名称指定了卷，则不会删除该卷。

```shell
#docker create -v awesome:/foo -v /bar --name hello redis
docker run -id -v /root/myvolume:/myvolume -v mycentosfoo:/foo -v /bar --name=mycentos5 centos:7.6.1810
docker rm -v mycentos5
```

在此示例中，/foo的卷将保持不变，但/bar的卷将被删除。对于继承了--volumes-from的卷，同样的行为也适用。

# 6. 部署案例

## 6.1 MySQL部署

目标：使用Docker部署一个MySQL，并通过客户端连接访问。

第一步：拉取MySQL镜像

```shell
docker pull mysql:5.7
```

提示：如果已经下载过到本地了，则无需下载。

第二步：创建MySQL容器并映射端口和改密码

```
docker run -di --name=my_mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=123456 mysql:5.7
```

- -e：代表添加环境变量  MYSQL_ROOT_PASSWORD是root用户的登陆密码

测试一：进入容器内部，登陆MySQL测试

（1）进入mysql容器

```
docker exec -it my_mysql bash
```

（2）登陆mysql

```
mysql -uroot -p123456
```

测试二：远程登陆MySQL

（1）我们在我们本机的电脑上去连接虚拟机Centos中的Docker容器，这里192.168.40.130是虚拟机操作系统的IP：

![1564160746670](assets/1564160746670.png)

## 6.2 Tomcat部署

目标：使用Docker部署一个Tomcat，并部署应用来访问。

第一步：拉取tomcat镜像

```
docker pull tomcat

```

第二步：创建tomcat容器

创建容器，并映射端口等

```
docker run -id --name=my_tomcat -p 9001:8080 -v /usr/local/mytomcat:/usr/local/tomcat/webapps tomcat
```

测试：

部署web应用

1）将程序拷贝到宿主机的`/usr/local/mytomcat`下面

比如：再建立目录`myapp`，里面编辑一个`index.html`页面作为测试主页

2）在虚拟机的宿主机上的浏览器地址栏中输入：http://192.168.40.141:9001/myapp

## 6.3 Nginx部署

目标：使用Docker部署一个Nginx,并将网页部署到nginx中

第一步：拉取nginx镜像

```
docker pull nginx
```

第二步：创建nginx容器

```
docker run -di --name=mynginx -p 80:80 nginx
```

这一次我们并没有选择挂载文件目录，那么如果我们想向nginx中部署一些资源文件该怎么做呢？

```
# 在我们不知道目录的情况 可以使用查找文件命令
find / -name 'nginx'

# 找到nginx 安装在了etc目录下
cd /etc/nginx

# 查看nginx的配置文件 nginx.conf
cat nginx.conf

# 发现这个文件中没有我们要找到安装目录
# 实际上是nginx 用到了其它的配置文件
# include /etc/nginx/conf.d/*.conf;
# 进入其他的配置文件目录
cd /etc/nginx/conf.d/

cat default.conf
# 得到 资源目录/usr/share/nginx/html

# 将我们需要部署的资源拷贝到该目录
docker cp 我们的资源 mynginx:/usr/share/nginx/html
```

## 6.4 Redis部署

目标：使用Docker部署一个Redis，并通过客户端连接访问。

第一步：拉取Redis镜像

```
docker pull redis
```

第二步：创建Redis容器

```
docker run -di --name=myredis -p 6379:6379 redis
```

- -p：代表端口映射，格式为  宿主机映射端口:容器运行端口

客户端测试

在你的本地电脑命令提示符下，用window版本redis测试

```
redis-cli -h 192.168.18.131 –p 6379
```

提示：

如果远程无法连接虚拟机，则可能是虚拟机防火墙没有关闭。

解决方案：

关闭即可：

```
#查看防火墙状态
systemctl status firewalld
#关闭防火墙
systemctl stop firewalld
#禁止开机启动防火墙
systemctl disable firewalld
```



# 7. 备份与迁移 

## 7.1 容器保存为新镜像

说明：

根据容器的更改创建新镜像，即基于原始镜像，将其运行的容器中更改的内容，来生成新的镜像。

语法：

```none
docker commit 容器名称 镜像名称
```

```shell
# 将`my_redis`容器提交为一个新的镜像`myredis:1.0.1`：
docker commit mynginx mynewnginx
```

运行结果：本地镜像中新增了`mynewnginx`的镜像

简单快速测试：使用自定义的镜像来运行容器，发现也可正常使用,并且之前存放的静态资源也存在。

## 7.2 镜像的备份

说明：将一个或多个镜像保存到tar存档（默认流到标准输出-STDOUT）

语法：

```none
docker save [OPTIONS] IMAGE [IMAGE...]
```

【示例】

（1）创建一个镜像的备份到磁盘文件：

```shell
#               输出到指定文件           镜像名   tag
docker save -o myredis-1.0.1.save.tar myredis:1.0.1
#或             镜像名         输出到指定文件
docker save myredis:1.0.1 > myredis-1.0.1.save.tar
```



（2）对多个镜像打包备份到一个磁盘文件：

```shell
docker save -o xxx.tar 镜像1 镜像2...
#如将redis所有标记版本镜像和ngix的1.17.2版本的镜像，都打包到一个文件中。
docker save -o mybak20190726.save.tar redis nginx：1.17.2
```

【应用场景】

docker save的主要应用场景是，你要部署的客户服务器并不能连外网。这时，你可以使用docker save将用到的相关镜像打个包，然后拷贝到客户服务器上，再使用docker load一次性载入。



## 7.3 镜像的加载

说明：

从tar归档文件或标准输入（stdin）加载镜像，归档文件即使是使用gzip、bzip2或xz压缩后的，也能自动识别和处理。

语法：

```none
docker load [OPTIONS]
```

【示例】

先删除已有的镜像，然后通过备份的归档文件加载还原镜像到docker中：

```shell
docker load -i myredis-1.0.1.save.tar
#或
docker load < myredis-1.0.1.save.tar
```



# 8. Dockerfile构建镜像

## 什么是Dockerfile

Dockerfile是由一系列命令和参数构成的脚本，这些命令应用于基础（原始）镜像并最终创建一个自定义的新的镜像。

1、对于开发人员：可以为开发团队提供一个完全一致的开发环境；

2、对于测试人员：可以直接拿开发时所构建的镜像或者通过Dockerfile文件构建一个新的镜像开始工作了；

3、对于运维人员：在部署时，可以实现应用的无缝移植。

## 常用命令(参考)

| 命令                               | 作用                                                         |
| ---------------------------------- | ------------------------------------------------------------ |
| FROM image_name:tag                | 定义了使用哪个基础镜像启动构建流程                           |
| MAINTAINER user_name               | 声明镜像的创建者                                             |
| ENV key value                      | 设置环境变量 (可以写多条)                                    |
| RUN command                        | 是Dockerfile的核心部分(可以写多条) mkdir /usr/xxx            |
| ADD source_dir/file dest_dir/file  | 将宿主机的文件复制到容器内，如果是一个压缩文件，将会在复制后自动解压 |
| COPY source_dir/file dest_dir/file | 和ADD相似，但是如果有压缩文件并不能解压                      |
| WORKDIR path_dir                   | 设置工作目录                                                 |
| EXPOSE port1 prot2                 | 用来指定端口，使容器内的应用可以通过端口和外界交互           |
| CMD argument                       | 在构建容器时使用，会被docker run 后的argument覆盖            |
| ENTRYPOINT argument                | 入口点，容器启动后会执行的命令，比如启动mysql。效果和CMD相似，但是并不会被docker run指定的参数覆盖 |
| VOLUME                             | 将本地文件夹或者其他容器的文件挂载到容器中                   |



## 使用脚本创建镜像

目标：创建一个安装有jdk1.8的centos的docker基础镜像



步骤：

（1）创建目录，用来存放脚本、要安装的资源等。

```shell
mkdir -p ~/dockerjdk8

```

（2）下载jdk-8u181-linux-x64.tar.gz并上传到服务器（虚拟机）中的/usr/local/dockerjdk8目录

```shell
#Alt+p打开sftp,然后在sftp中执行下列命令上传(或者直接将文件拖放进去)：
put E:\jdk-8u181-linux-x64.tar.gz
#如果带有目录，则
put -r E:\jdk-8u181-linux-x64.tar.gz
#将文件移动到指定目录：
mv ~/jdk-8u181-linux-x64.tar.gz ~/dockerjdk8

```

（3）创建文件Dockerfile

```
vi Dockerfile
```

内容参考如下：

```shell
#依赖的基础镜像名称和ID，如果本地不存在，则自动下载
FROM centos:7.6.1810
#指定镜像创建者信息
MAINTAINER ITCAST_BoBo
#切换当前的工作目录，进入容器化，默认进入的目录
WORKDIR /usr
#容器中创建java的目录
RUN mkdir /usr/local/java
#将容器外的文件（相对、绝对路径均可）拷贝到容器内指定的目录，并自动解压
ADD jdk-8u161-linux-x64.tar.gz /usr/local/java/
#容器中配置java环境变量
ENV JAVA_HOME /usr/local/java/jdk1.8.0_161
ENV JRE_HOME $JAVA_HOME/jre
ENV CLASSPATH $JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar:$JRE_HOME/lib:$CLASSPATH
ENV PATH $JAVA_HOME/bin:$PATH
```

【提示】

基础镜像暂无需设置入口点。

（4）执行命令构建镜像

参考命令：

```shell
# 注意后边的空格和点，不要省略
docker build -t centos-jdk8 .
#或
docker build -t 'centos-jdk8' .
```

****

执行情况：

```
[root@pinyoyougou-docker dockerjdk8]# docker build -t 'itcast.cn/centos-jdk8' .
Sending build context to Docker daemon  185.7MB
Step 1/9 : FROM centos:7
7: Pulling from library/centos
256b176beaff: Pull complete 
Digest: sha256:6f6d986d425aeabdc3a02cb61c02abb2e78e57357e92417d6d58332856024faf
Status: Downloaded newer image for centos:7
 ---> 5182e96772bf
Step 2/9 : MAINTAINER ITCAST
 ---> [Warning] IPv4 forwarding is disabled. Networking will not work.
 ---> Running in 42d3d623a482
Removing intermediate container 42d3d623a482
 ---> 4f98432cc7e9
Step 3/9 : WORKDIR /usr
Removing intermediate container dec88e91bd57
 ---> 35493ede840d
Step 4/9 : RUN mkdir /usr/local/java
 ---> [Warning] IPv4 forwarding is disabled. Networking will not work.
 ---> Running in cccbf0aa02ba
Removing intermediate container cccbf0aa02ba
 ---> 672c668ad17b
Step 5/9 : ADD jdk-8u181-linux-x64.tar.gz /usr/local/java/
 ---> 92db16a7f941
Step 6/9 : ENV JAVA_HOME /usr/local/java/jdk1.8.0_181
 ---> [Warning] IPv4 forwarding is disabled. Networking will not work.
 ---> Running in 6c01f5cc4a5c
Removing intermediate container 6c01f5cc4a5c
 ---> 7520a12e17a4
Step 7/9 : ENV JRE_HOME $JAVA_HOME/jre
 ---> [Warning] IPv4 forwarding is disabled. Networking will not work.
 ---> Running in f7afa99da91e
Removing intermediate container f7afa99da91e
 ---> a153addf4d67
Step 8/9 : ENV CLASSPATH $JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar:$JRE_HOME/lib:$CLASSPATH
 ---> [Warning] IPv4 forwarding is disabled. Networking will not work.
 ---> Running in 1ac4b1dd8ed1
Removing intermediate container 1ac4b1dd8ed1
 ---> a5df2bdfc6fa
Step 9/9 : ENV PATH $JAVA_HOME/bin:$PATH
 ---> [Warning] IPv4 forwarding is disabled. Networking will not work.
 ---> Running in 095f193b12f6
Removing intermediate container 095f193b12f6
 ---> 42585050b9b3
Successfully built 42585050b9b3
```



参考官网：https://docs.docker.com/engine/reference/builder

（5）查看镜像是否建立完成

```
docker images
```

执行结果：

```
[root@pinyoyougou-docker dockerjdk8]# docker images
REPOSITORY                TAG                 IMAGE ID            CREATED             SIZE
centos-jdk8     latest              42585050b9b3        6 minutes ago       581MB
```



（6）创建容器

```shell
#退出容器命令后，容器自动停止但不会被删除
docker run -it --name=mycentosjdk8 itcast.cn/centos-jdk8 /bin/bash
```

果然可以创建哟~

进入到容器中查看当前目录、jdk的环境`java -version`、jdk安装目录等

# 9. Docker私有Registry

## 私有注册中心搭建

（1）拉取私有仓库镜像（此步可省略）

```
docker pull registry
```

（2）启动私有仓库容器

```
docker run -id -p 5000:5000 --name myregistry registry
```

（3）查看检验是否安装启动成功。

打开浏览器 输入地址

```
http://192.168.18.131:5000/v2/_catalog
```

看到 {"repositories":[]} ，表示私有仓库搭建成功并且内容为空

## 镜像上传至私有注册中心

目标：将前面自己制作的`centos-jdk8`的镜像上传到私服仓库中。

第一步：当前docker信任私有注册中心

（1）修改daemon.json，让 docker信任私有仓库地址

修改文件：

```shell
vi /etc/docker/daemon.json
```

添加如下内容，保存退出。

```json
{
"insecure-registries":["192.168.18.131:5000"]
}

```

注意：该文件中如有多个内容，比如有之前配置的私服镜像地址，用英文逗号隔开，参考如下：

```json
{
"registry-mirrors": ["https://docker.mirrors.ustc.edu.cn"]
,"insecure-registries":["192.168.18.131:5000"]
}
```

（2）重启docker 服务和私服

```
systemctl restart docker
#可以省略（如果创建容器时带有--restart always）
docker start registry
```

第二步：修改镜像的相关信息，重打标记

（1）创建标记（tag）此镜像为私有仓库的镜像

```shell
docker tag centos_jdk1.8 192.168.18.131:5000/centos_jdk1.8
```

提示：打标记从某中角度说，就是复制一份，重命名一下。

（2）上传标记的镜像

```
docker push 192.168.18.131:5000/centos_jdk1.8
```

稍等片刻，完成后，通过浏览器访问私服仓库镜像列表即可。

```
{"repositories":["centos-jdk8"]}
```

【了解】

名称空间默认是仓库的名字，

如192.168.40.128:5000/centos-jdk8，则默认在http://192.168.40.128:5000/v2中寻找centos-jdk8镜像。

如itcast.cn/centos-jdk8，则默认在https://itcast.cn:5000/v2中寻找centos-jdk8镜像。


