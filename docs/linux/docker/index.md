一、前置条件
安装 Docker 之前，需要先准备 CentOS 环境

目前支持 CentOS 7, CentOS 8(stream) 和 CentOS 9(stream)

卸载 Docker 历史版本

```shell
sudo yum remove docker \
    docker-client \
    docker-client-latest \
    docker-common \
    docker-latest \
    docker-latest-logrotate \
    docker-logrotate \
    docker-engine
```

执行结果如下，表示之前没有安装过 Docker

```shell
No Packages marked for removal
```

二、安装Docker
安装方式
Docker 官网提供了 3 种安装方式

通过远程仓库安装 - 最常用
下载RPM包后手动安装 - 适用于某些无法联网的环境
通过快捷脚本安装 - 测试或者开发环境
本文采用第一种安装方式，由于国外的镜像比较慢，因此配置阿里云镜像

在一台机器上首次安装 Docker 前，还需要执行如下操作

```shell
sudo yum install -y yum-utils
```

配置镜像仓库
以下两种方式任选其一，如果国外镜像下载速度慢，可以考虑阿里云镜像加速器

Docker官方仓库

```shell
sudo yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo
```

阿里云镜像加速器

登录阿里云账号后，访问「阿里云镜像加速器」页面：https://cr.console.aliyun.com/cn-hangzhou/instances/mirrors，这个服务是免费的

![img](https://img-blog.csdnimg.cn/2caa1e3dfa2648f2863b2c62e14cc43a.png)

```shell
sudo mkdir -p /etc/docker
sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://xxx.mirror.aliyuncs.com"]
}
EOF
```


配置完成后，重新加载

```shell
sudo systemctl daemon-reload
```

执行安装
```shell
sudo yum install docker-ce docker-ce-cli containerd.io docker-compose-plugin
```

安装过程中，有 2 处停顿，询问是否继续，直接输入 y 即可

```shell
Is this ok [y/d/N]: y
Is this ok [y/N]: y
```

安装完成后，使用 docker -v 查看当前版本 

Docker version 20.10.21, build baeda1f

启动Docker

```shell
sudo systemctl start docker
```

# 设置开机启动Docker
```shell
sudo systemctl enable docker
```

检查Docker是否可以正常运行

```shell
sudo docker run hello-world
```

执行结果如下，Docker可以正常运行

![img](https://img-blog.csdnimg.cn/c2a6b97e96a04313b40050b4126caadc.png)

三、卸载Docker
卸载Docker核心组件

```shell
sudo yum remove docker-ce docker-ce-cli containerd.io docker-compose-plugin
```

清理Docker相关资源
```shell
sudo rm -rf /var/lib/docker
sudo rm -rf /var/lib/containerd
```

### 若报以下错误

![image-20230911091602541](G:\学习资料\linux\3、docker相关\image-20230911091602541.png)

查看服务器DNS网络配置

 ``` shell
 vi /etc/resolv.conf
 ```



把里面的内容清除，并改为：

> ```shell
> nameserver 8.8.8.8
> nameserver 8.8.8.4
> ```

重启网络服务

``` shell
systemctl restart network
```

