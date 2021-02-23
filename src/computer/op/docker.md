# Docker 教程

以对 `zookeeper`进行使用为例

## 调研

- VMware
- KVM
- Docker

[docker - trust_sandbox](https://docs.docker.com/engine/security/trust/trust_sandbox/)

[Making Containers More Isolated: An Overview of Sandboxed Container Technologies](https://unit42.paloaltonetworks.com/making-containers-more-isolated-an-overview-of-sandboxed-container-technologies/)



## 参考

参考了以下教程

- [阮一峰 - Docker 入门教程](http://www.ruanyifeng.com/blog/2018/02/docker-tutorial.html)
- [Building a Golang Docker image](https://bitfieldconsulting.com/golang/docker-image)



## 概念

### 镜像（Image）

特殊的文件系统，程序、库、资源、配置文件

### 容器（Container）

### 仓库（Repository）



## 安装环境

- [Mac](https://docs.docker.com/docker-for-mac/install/)
- [Windows](https://docs.docker.com/docker-for-windows/install/)
- [Ubuntu](https://docs.docker.com/install/linux/docker-ce/ubuntu/)
- [Debian](https://docs.docker.com/install/linux/docker-ce/debian/)
- [CentOS](https://docs.docker.com/install/linux/docker-ce/centos/)
- [Fedora](https://docs.docker.com/install/linux/docker-ce/fedora/)
- [其他 Linux 发行版](https://docs.docker.com/install/linux/docker-ce/binaries/)

把用户加入 Docker 用户组。

```
sudo groupadd docker          #添加docker用户组
sudo gpasswd -a $XXX docker   #检测当前用户是否已经在docker用户组中，其中XXX为用户名，例如我的，liangll
sudo gpasswd -a $USER docker  #将当前用户添加至docker用户组
newgrp docker                 #更新docker用户组
```

查看状态

```
# 启动
systemctl start docker

# 列出本机的所有 image 文件
docker image ls
```



## 基础

#### 搜索镜像

```shell
docker search zookeeper
```

#### 安装镜像

```shell
docker pull zookeeper
```

#### 将镜像放到容器中

```shell
# 下面可以一整行的内容
docker run --privileged=true -d --name zookeeper --publish 2181:2181 -d zookeeper:latest
```

#### 查看镜像

```shell
docker ps
-a # 查看所有的容器
```

#### 启动和停止容器

```shell
docker start name
docker stop name
```

#### 进入 `zookeeper`的运行环境

```
docker exec -it 45850daa6b9b bash
```

#### 执行应用的命令

[ZooKeeper客户端 zkCli.sh 节点的增删改查](https://www.cnblogs.com/sherrykid/p/5813148.html)  

下面是使用相应的命令：

```shell
# 运行 zkCli
./bin/zkCli.sh

# 重启
./bin/zkServer.sh restart
```

## 进阶

#### 重命名

```shell
docker rename old_name new_name
```

#### 删除镜像

```
docker rm zookeeper
```
