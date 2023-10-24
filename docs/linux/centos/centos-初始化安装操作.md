###  初始化安装后查询不了 IP

```shell
#1、centos7 初始化安装后 通过 ip addr 命令查询 执行不了
ip addr
```

##### 1、查询IP

输入IP查询命令：ip addr

![在这里插入图片描述](https://img-blog.csdnimg.cn/2020122921261133.png#pic_center)

如图，centos的ip地址是ens33条目中的inet值。发现 ens33 没有 inet 这个属性，那么就没法通过IP地址连接虚拟机。

##### 2、修改ens33网卡的配置

输入 vi /etc/sysconfig/network-scripts/ifcfg-ens33命令，如图所示：

![在这里插入图片描述](https://img-blog.csdnimg.cn/2020122921271676.png#pic_center)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201229212942794.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mzc0ODgwMg==,size_16,color_FFFFFF,t_70#pic_center)

从配置清单中可以发现 CentOS 7 默认是不启动网卡的（ONBOOT=no）。 把这一项改为YES（ONBOOT=yes），如图：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201229213107873.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mzc0ODgwMg==,size_16,color_FFFFFF,t_70#pic_center)

##### 3、重启网络服务

输入 sudo service network restart命令，如图所示：

![[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-umSDGtYu-1609247747213)(C:%5CUsers%5CLFang%20Li%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20201224214345543.png)]](https://img-blog.csdnimg.cn/20201229213150842.png#pic_center)

如上图所示，network服务重启成功。如果执行service network restart命令后出现下面的错误，即为服务重启失败

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201229213214637.png#pic_center)

sudo service network restart失败，无法重启网络，解决方法

##### 4、查看IP

输入ip addr命令

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201229213238434.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mzc0ODgwMg==,size_16,color_FFFFFF,t_70#pic_center)

192.168.175.128即为该机器IP地址。