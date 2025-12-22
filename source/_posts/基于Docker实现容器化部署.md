---
title: 基于Docker实现容器化部署
date: 2025-12-21 12:28:05
tags: 学习
categories: Java开发
cover: /medias/基于Docker实现容器化部署.png
---

# **基于Docker实现容器化部署**

## **一.Docker安装**

**1.如果系统中已经存在旧的Docker，则先卸载：**

运行指令如下

```cmd
yum remove docker \
  docker-client \
  docker-client-latest \
  docker-common \
  docker-latest \
  docker-latest-logrotate \
  docker-logrotate \
  docker-engine \
  docker-selinux 
```

**2.配置Docker的yum库（yum库用于后续拉取安装的操作）**

**（1）首先要安装一个yum工具**

```cmd
sudo yum install -y yum-utils device-mapper-persistent-data lvm2
```

**（2）安装成功后，执行命令，配置Docker的yum源（已更新为阿里云源）**

```cmd
sudo yum-config-manager --add-repo https://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo

sudo sed -i 's+download.docker.com+mirrors.aliyun.com/docker-ce+' /etc/yum.repos.d/docker-ce.repo
```

**（3）更新yum，建立缓存**

```cmd
sudo yum makecache fast
```

**3.安装Docker**

```cmd
yum install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

**4.启动校验**

```cmd
systemctl start docker # 启动Docker
```

```cmd
systemctl stop docker # 停止Docker
```

```cmd
systemctl restart docker #重启
```

```cmd
systemctl enable docker # 设置开机自启
```

```cmd
docker ps # 执行docker ps命令，如果不报错，说明安装启动成功
```

**5.配置镜像加速（配置第三方镜像库，用于下载加速）**

**镜像地址可能会变更，如果失效可以百度找最新的docker镜像。配置镜像步骤如下：**

```cmd
rm -f /etc/docker/daemon.json # 创建目录
```

```cmd
tee /etc/docker/daemon.json <<-'EOF'

{

  "registry-mirrors": [

​    "http://hub-mirror.c.163.com",

​    "https://mirrors.tuna.tsinghua.edu.cn",

​    "http://mirrors.sohu.com",

​    "https://ustc-edu-cn.mirror.aliyuncs.com",

​    "https://ccr.ccs.tencentyun.com",

​    "https://docker.m.daocloud.io",

​    "https://docker.awsl9527.cn"

  ]

}
EOF \# 复制内容
```

```cmd
systemctl daemon-reload # 重新加载配置
```

```cmd
systemctl restart docker # 重启Docker
```

## **二.Mysql安装(linux中的安装步骤太繁琐)**

**1.前置知识补充**

**（1）镜像和容器**

**镜像=应用本身+运行环境+配置信息+系统函数库。**

**容器：与外界隔离的独立环境，用来运行镜像。**

{% asset_img image-20251220163252332.png%}

**（2）Mysql安装命令解读**

**代码块如下：**

```
docker run -d \
 --name mysql \
 -p 3307:3306 \
 -e TZ=Asia/Shanghai \
 -e MYSQL_ROOT_PASSWORD=123 \
 mysql:8
```

{% asset_img image-20251220163406797.png%}

**（3）镜像命名规范**

**格式：[repository]:[tag]-----repository镜像名，tag镜像版本**

**Eg: mysql:8** **若不指定tag，则默认是latest代表最新版本的镜像。**

## **三.Docker核心**

**1.镜像，容器的常用操作命令**

{% asset_img image-20251220163441907.png%}

补充：

默认情况下，每次重启虚拟机我们都需要手动启动Docker和Docker中的容器。通过命令可以实现开机自启：

\# Docker开机自启

systemctl enable docker

\# Docker容器开机自启

docker update --restart=always [容器名/容器id]

**2.数据卷挂载**

**数据卷：是一个虚拟目录，是容器内目录与宿主机目录之间映射的桥梁。**

{% asset_img image-20251220163508159.png%}

{% asset_img image-20251220163513488.png%}

注意：容器与数据卷的挂载要在创建容器时配置，对于创建好的容器，是不能设置数据卷的。而且创建容器的过程中，数据卷会自动创建。（默认创建的数据卷是匿名数据卷与普通数据卷没差别，就是名字有点长）

{% asset_img image-20251220163525468.png%}

html为宿主机目录，/usr/后的为容器内目录

**3.本地目录挂载**

{% asset_img image-20251220163601534.png%}

{% asset_img image-20251220163552058.png%}

**4.自定义镜像**

前面我们一直在使用别人准备好的镜像（mysql,nginx都是由官方上传供我们直接使用的），那如果我要部署一个Java项目，把它打包为一个镜像该怎么做呢？ 那接下来，我们就来介绍一下如何自定义镜像。

**（1）镜像结构**

镜像之所以能让我们快速跨操作系统部署应用而忽略其运行环境、配置，就是因为镜像中包含了程序运行需要的系统函数库、环境、配置、依赖。

{% asset_img image-20251220163627110.png%}

上述步骤中的每一次操作其实都是在生产一些文件（系统运行环境、函数库、配置最终都是磁盘文件），所以镜像就是一堆文件的集合。

但需要注意的是，镜像文件不是随意堆放的，而是按照操作的步骤分层叠加而成，每一层形成的文件都会单独打包并标记一个唯一id，称为Layer（层）。这样，如果我们构建时用到的某些层其他人已经制作过，就可以直接拷贝使用这些层，而不用重复制作。

例如，第一步中需要的Linux运行环境，通用性就很强，所以Docker官方就制作了这样的只包含Linux运行环境的镜像。我们在制作java镜像时，就无需重复制作，直接使用Docker官方提供的CentOS或Ubuntu镜像作为基础镜像。然后再搭建其它层即可，这样逐层搭建，最终整个Java项目的镜像结构如图所示：

{% asset_img image-20251220163639273.png%}

**（2）Dockerfile**

由于制作镜像的过程中，需要逐层处理和打包，比较复杂，所以Docker就提供了自动打包镜像的功能。我们只需要将打包的过程，每一层要做的事情用固定的语法写下来，交给Docker去执行即可。而这种记录镜像结构的文件就称为**Dockerfile。**

{% asset_img image-20251220163652846.png%}

{% asset_img image-20251220163658409.png%}

{% asset_img image-20251220163703759.png%}

**（3）容器间的网络通信**

问题：

前面我们创建了一个Java项目的容器，而Java项目往往需要访问其它各种中间件，例如MySQL、Redis等。但是，容器的网络IP其实是一个虚拟的IP，其值并不固定与某一个容器绑定，如果我们在开发时写死某个IP，而在部署时很可能MySQL容器的IP会发生变化，连接会失败。

解决：

引入自定义网络。（如果多个容器桥接在同一个网络上，那么容器之间便可直接通过名字实现相互通信，即使ip变化也不影响）

{% asset_img image-20251220163716756.png%}

{% asset_img image-20251220163721897.png%}

{% asset_img image-20251220163728067.png%}

## **四.项目部署**

### 1.服务端部署

{% asset_img image-20251220163748127.png%}

**(1) 修改项目的配置文件，修改数据库服务地址（打包package）**

{% asset_img image-20251220163800459.png%}

{% asset_img image-20251220163804844.png%}

修改application.yml和logback.xml文件

{% asset_img image-20251220163818058.png%}

192.168.100.128为宿主机访问地址，因为在windows系统中不能直接访问虚拟机中容器的地址，同时通过宿主机的端口3307通过端口映射到容器的3306端口。（通过图形化界面工具DataGrip检验数据情况）。

**(2) 执行maven中的package生命周期，进行打包(跳过测试)，并将打包后的jar包命名为 tlias.jar**

{% asset_img image-20251220163851439.png%}

**（3）构建镜像**

{% asset_img image-20251220163909954.png%}

{% asset_img image-20251220163916412.png%}

构建镜像指令的最后的点.表示Dockerfile文件所在目录。

**（4）部署容器**

{% asset_img image-20251220163928786.png%}

### **2.前端部署**

{% asset_img image-20251220163950397.png%}

