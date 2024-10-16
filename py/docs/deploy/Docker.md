[TOC]

# docker

### 为什么使用docker

- 更高效的利用系统资源
- 更快速的启动时间
- 一致的运行环境
- 持续交付和部署
- 更轻松的迁移
- 更轻松的维护和扩展

### 镜像（image）

```
分层存储
```

### 容器（container）

```shell
# 镜像和容器类似于面向对象的类和实例
```

### 仓库（repository）

### 安装docker

```shell
# ubuntu:20.04
sudo apt-get update

sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
    
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

echo \
  "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt-get update

sudo apt-get install docker-ce docker-ce-cli containerd.io

# 卸载
sudo apt-get purge docker-ce docker-ce-cli containerd.io
sudo rm -rf /var/lib/docker
sudo rm -rf /var/lib/containerd
```

```shell
# 镜像加速
# https://cr.console.aliyun.com/cn-beijing/instances/mirrors


# /etc/docker/daemon.json 文件不存在创建
{
  "registry-mirrors": [
    "https://registry.docker-cn.com"
  ]
}

sudo systemctl daemon-reload
sudo systemctl restart docker
```

### 操作docker相关命令

```dockerfile
# https://docs.docker.com/reference/
# 查看docker版本

docker -v
# 查看docker 命令
docker --help
# 查看docker 服务端与客户端版本详情
docker version
# 启动docker
systemctl start docker
# 关闭docker
systemctl stop docker
# 重启docker
systemctl stop docker
# 查看docker运行状态
systemctl status docker
# 关闭防火墙
systemctl stop firewalld

# 开启自动启动容器
docker update --restart=always 容器name
```

### Docker File 指令详解

###### FROM 指定基础镜像

```dockerfile
FROM python
# 必备指令 必须是第一条指令
FROM scratch  # 指定空白镜像
```

###### RUN 执行命令

```dockerfile
RUN 
# shell 格式：RUN <命令> 
# exec 格式：RUN["可执行文件","参数1","参数2"]

# 错误写法
FROM debian:jessie

RUN apt-get update
RUN apt-get install -y gcc libc6-dev make
RUN wget -O redis.tar.gz "http://download.redis.io/releases/redis-3.2.5.tar.gz"
RUN mkdir -p /usr/src/redis
RUN tar -xzf redis.tar.gz -C /usr/src/redis --strip-components=1
RUN make -C /usr/src/redis
RUN make -C /usr/src/redis install

# 正确写法
FROM debian:jessie


RUN buildDeps='gcc libc6-dev make' \
    && apt-get update \
    && apt-get install -y $buildDeps \
    && wget -O redis.tar.gz "http://download.redis.io/releases/redis-3.2.5.tar.gz" \
    && mkdir -p /usr/src/redis \
    && tar -xzf redis.tar.gz -C /usr/src/redis --strip-components=1 \
    && make -C /usr/src/redis \
    && make -C /usr/src/redis install \
    && rm -rf /var/lib/apt/lists/* \
    && rm redis.tar.gz \
    && rm -r /usr/src/redis \
    && apt-get purge -y --auto-remove $buildDeps
```

###### 构建镜像

```dockerfile
docker build -t nainx:v3 .
docker build [选项] <上下文路径/URL/->

```

###### COPY 复制文件

```dockerfile
COPY <原路径>...<目标路径>
COPY ["<原路径>",..."<目标路径>"]

COPY package.json /usr/src/app/
# 通配符要满足Go的filepath.Match
COPY hom* /mydir/
COPY hom?.txt /mydir/
```

###### ADD 更高级的复制文件

```dockerfile
ADD # 不实用不推荐使用 仅在需要自动解压缩的场合使用
```

###### CMD 容器启动命令

```dockerfile
shell格式： CMD <命令>
exec格式: CMD ["可执行文件","参数1","参数2"] # 推荐使用 必须使用",不能用单'

CMD ECHO $HMOE

CMD ["SH", "-C", "ECHO $HMOE"]

CMD ["nginx", "-g", "daemon off;"]


```

###### ENTRYPOINT 入口点

```
<ENTRYPOINT> "<CMD>"

```



###### ENV 设置环境变量

```dockerfile
ENV <key> <value>
ENV <key1>=<value1> <key2>=<value2>...

ENV VERSION=1.0 DEBUG=on \
	NAME="Happy Feet"
```



###### ARG 构建参数

###### VOLUME 定义匿名卷

```
VOLUME /data

docker run -d -v mydata:/data xxxx
```



###### EXPOSE 暴露端口

```
EXPOSE <端口1> [<端口2>...]

```

###### WORKDIR 指定工作目录

###### USER 指定当前用户

###### HEALTHCHECK 健康检查

###### ONBUILD 为他人做嫁衣裳



### 镜像操作

```dockerfile
# 查看本地镜像
docker images
# 搜索镜像 先本地 后默认地址
docker search tomcat
# 找到所有的镜像拉取 
docker pull tomcat # 最新版本
docker pull tomcat:7 # 最新版本
# 有了本地镜像可以创建容器  
docker create --name=mytomcat tomcat
# 查看容器
docker ps  # 查看在运行的容器
docker ps -a  # 查看所有的容器
# 运行容器
docker start myTomcat # start 后面可以跟 容器id(前2-3位) 或者name
# 停止容器
docker stop  myTomcat # stop 后面可以跟 容器id(前2-3位) 或者name
# 删除没有运行的容器
docker rm 容器id或者名字
# 删除在运行的容器
docker rm -f 容器id或者名字
# 删除所有容器
docker stop $(docker ps -a -q)  先停止所有的容器
# 删除
docker rm $(docker ps -a -q)
```

### 容器操作

```dockerfile
# 查看docker run 命令  创建并且启动容器 tomcat端口 8080
docker run --help
	-i  # 运行容器
	-t  # 容器启动后,进入命令行
	-v  # 目录映射  挂载
	-d  # 守护进程  后台运行
	-p  # 端口映射 
# 创建容器,并且进入命令行  进入容器
docker run -it --name=mytomcat tomcat/bin/bash
# 退出
exit
#创建运行一个守护的容器
docker run -id --name=mytomcat2 tomcat
# 进入容器
docker exec -it mytomcat2 /bin/bash
```

### 宿主机与docker容器的文件传递

#### 从宿主机到容器

```sh
# 创建 一个文件
touch 1.py
# 把文件复制到容器里去
docker cp 1.py mytomcat2:/
# 进入根目录
cd /
# 查看
ls
```

#### 从容器到宿主机

```sh
# 创建文件
touch adb.jpg
# 退出容器
exit
# 复制到宿主机
docker cp mytomcat2:/abc.jpg /root
```

```
docker tag local-image:tagname new-repo:tagname
docker push new-repo:tagname
```

