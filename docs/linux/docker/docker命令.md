###  重启docker

``` shell
systemctl daemon-reload 
systemctl restart docker
```

### 查询本机镜像

``` shell
docker images
```

### 查询本机容器

``` shell
#查询所有容器
docker ps -a
#查询活跃容器
dockers ps 
```

### 搜索线上镜像/拉取镜像

``` shell
#docker search 镜像名称
docker search jdk
#docker pull 镜像名称
docker pull dockette/jdk8
```

###  生成镜像文件

``` shell
# docker build -t 镜像名:tag  -f Dockerfile文件名 .   
docker build -t java8:v1 .
```

### 导出镜像文件

``` shell
#使用 save 和 load
#1，查看本机的容器
#这两个命令是通过镜像来保存、加载镜像文件的。首先我们使用 docker images 命令查看本机所有的镜像。

#2，保存镜像
#（1）下面使用 docker save 命令根据 ID 将镜像保存成一个文件。

docker save 0fdf2b4c26d3 > process_data.tar

#（2）我们还可以同时将多个 image 打包成一个文件，比如下面将镜像库中的 postgres 和 mongo 打包：

docker save -o images.tar postgres:9.6 mongo:3.4

#3，载入镜像
#使用 docker load 命令则可将这个镜像文件载入进来。

docker load < process_data.tar

```

### 运行镜像

``` shell
docker run --name process_data -it -p 8080:80 process_data:v1
```

### 移除镜像

``` shell
# docker rmi 镜像id
```

### 移除容器

``` shell
# docker remove 容器id
```

### 启动容器

``` shell
# docker start 容器id
```

### 关闭容器

``` shell
# docker stop 容器id
```





