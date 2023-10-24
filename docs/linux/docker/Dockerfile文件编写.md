### jdk镜像示例

``` dockerfile
From centos:7

RUN mkdir /usr/local/jdk8

ADD  jdk-8u202-linux-x64.tar.gz /usr/local/jdk8

ENV JAVA_HOME=/usr/local/jdk8/jdk1.8.0_202

ENV CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar

ENV PATH=$JAVA_HOME/bin:$PATH

```

### 生成jdk镜像

``` shell
docker build -t java8:v1 .
```



### jar包Dockerfile文件示例

``` dockerfile
FROM java8:v1
WORKDIR /usr/local/process_data
COPY  process_data-0.0.1.jar   /usr/local/process_data/process_data-0.0.1.jar
EXPOSE 80
CMD ["java","-jar","process_data-0.0.1.jar"]
```

### 生成jar镜像文件

``` shell
docker build -t process_data:v1 .
```

### Dockerfile文件说明

``` shell
FROM：指定基础镜像
RUN：容器构建时需要运行的命令
EXPOSE：当前容器对外暴露的端口号
WORKDIR：指定在创建容器后，终端默认登录进来的工作目录
ADD：将宿主机目录下的文件拷贝进镜像，ADD命令会自动处理URL和解压tar压缩包
CMD：指定一个容器启动时要运行的命令，参数为数组格式 CMD ["可执行文件", "参数1", "参数2" ...]
```

