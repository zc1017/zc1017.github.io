## Centos7安装nginx

###   卸载nginx

先查看是否启动了 nginx 服务

```  shell
ps -ef|grep nginx
```

出现这个则 nginx 没启动服务

![image-20230913130909010](G:\学习资料\linux\4、软件安装\image-20230913130909010.png)

出现这个则 nginx 启动了服务

![[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-TgC9wq4m-1675936376960)(CentOs7搭建mysql主从.assets/image-20230209162631886.png)]](https://img-blog.csdnimg.cn/74e4dba70fa04f338ccd95018204605c.png)

如果 nginx 启动了服务，则需要先关闭 nginx 服务 【没启动就略过这一步】

``` shell
# kill 进程id
```

![[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-5G4oC4oo-1675936376960)(CentOs7搭建mysql主从.assets/image-20230209162830842.png)]](https://img-blog.csdnimg.cn/cfe17562845141919847744f3598c9b0.png)






查看所有与 nginx 有关的文件夹

``` shell
find / -name nginx
```


删除与 nginx 有关的文件夹

```shell
rm -rf file /usr/local/nginx*
```

卸载Nginx相关的依赖

``` shell
yum remove nginx
```

这样就卸载完成了

### 安装nginx

1、 查看安装nginx所需要的环境

``` shell
#查看 C++ 环境是否安装（查看版本号）
gcc -v
#查看 zlib 是否安装
cat /usr/lib64/pkgconfig/zlib.pc
#查看 pcre 是否安装（查版本号）
pcre-config --version
```

2、 配置 nginx 安装所需的环境

``` shell
#一次安装4个插件
yum -y install gcc pcre pcre-devel zlib zlib-devel openssl openssl-devel
```

``` shell
#一次安装如果有问题，可以试一下分开安装（上面命令执行成功了就无需执行以下命令了）
 	#安装 nginx 需要先将官网下载的源码进行编译，编译依赖 gcc 环境
yum install gcc-c++
 	#pcre是一个perl库，包括perl兼容的正则表达式库，nginx的http模块使用pcre来解析正则表达式，所以需要安装pcre库
yum install -y pcre pcre-devel
 	#zlib库提供了很多种压缩和解压缩方式nginx使用zlib对http包的内容进行gzip，所以需要安装
yum install -y zlib zlib-devel
 	#nginx 不仅支持 http 协议，还支持 https（即在ssl协议上传输http），所以需要在 Centos 安装 OpenSSL 库
yum install -y openssl openssl-devel
```


3、安装 nginx

方法一：在官网直接下载.tar.gz安装包，然后通过远程工具拉取到 linux 里面【在 /usr/local 里面创建个nginx文件夹，拉进来。（也可以拉到其他地方）】
方法二：使用wget命令下载，确保系统已经安装了wget，<font color="red">如果没有安装，执行 yum install wget 安装</font>。
这里使用方法二进行安装：

进入 usr/local 里面创建 nginx 文件夹，方便后期删除干净

``` shell
#进入usr下的local目录
cd /usr/local
#在local目录下创建 mysql 文件夹
mkdir nginx
#进入nginx目录
cd nginx
```




通过 wget 下载 nginx 安装包

``` shell
wget https://nginx.org/download/nginx-1.21.6.tar.gz
```


解压 并进入解压后的目录

``` shell
#解压
tar zxvf nginx-1.21.6.tar.gz
#进入解压后的目录
cd nginx-1.21.6
```


配置（带有https模块）【需要进入解压后的目录】

``` shell
./configure --prefix=/usr/local/nginx --with-http_stub_status_module --with-http_ssl_module
```

![[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-YrbGEnOh-1675936376963)(CentOs7搭建mysql主从.assets/image-20230209171620795.png)]](https://img-blog.csdnimg.cn/43cf5eec75d54e1d8dc477ed252ae7a8.png)

编译和安装【需要进入解压后的目录】

``` shell
#编译
make
#安装
make install
```


启动、关闭 nginx 服务

``` shell
###启动服务
#需要先进入sbin目录下
cd /usr/local/nginx/sbin
#启动nginx服务
./nginx

###关闭服务
#需要先进入sbin目录下
cd /usr/local/nginx/sbin
#关闭nginx服务
./nginx -s stop
```


到这里 nginx 就安装完成了

其他命令

``` shell
####端口号操作
#查询开启的所有端口
firewall-cmd --list-port
#设置80端口开启
firewall-cmd --zone=public --add-port=80/tcp --permanent
#验证80端口是否开启成功 (单个端口查询)
firewall-cmd --zone=public --query-port=80/tcp
#设置80端口关闭
firewall-cmd --zone=public --remove-port=80/tcp --permanent

####防火墙操作
#检查防火墙是否开启
systemctl status firewalld
#开机自启防火墙
systemctl enable firewalld
#开机禁止自启防火墙
systemctl disable firewalld
#启动
systemctl start firewalld
#关闭
systemctl stop firewalld
#重启
firewall-cmd --reload
```

