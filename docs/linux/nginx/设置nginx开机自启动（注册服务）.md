## 方法一：编辑/etc/rc.local，添加开机启动运行命令

直接编辑/etc/rc.local文件，文件内容最底下添加启动命令：
/usr/local/nginx/sbin/nginx
即可

``` shell
vi /etc/rc.local
# 文件内容最底下添加启动命令：
# /usr/local/nginx/sbin/nginx
```

+++

## 方法二： 添加服务方式

**第一步：进入到/lib/systemd/system/目录**

``` shell
cd /lib/systemd/system/
```

**第二步：创建nginx.service文件，并编辑**

```shell
vim nginx.service
# 仅修改 /usr/local/nginx/sbin/nginx 这个路径即可（修改为你的nginx路径）
```

内容如下：

```shell
[Unit]
Description=nginx service
After=network.target 
[Service] 
Type=forking 
ExecStart=/usr/local/nginx/sbin/nginx
ExecReload=/usr/local/nginx/sbin/nginx -s reload
ExecStop=/usr/local/nginx/sbin/nginx -s quit
PrivateTmp=true
[Install]
WantedBy=multi-user.target
#Description:描述服务
#After:描述服务类别
#[Service]服务运行参数的设置
#Type=forking是后台运行的形式
#ExecStart为服务的具体运行命令
#ExecReload为重启命令
#ExecStop为停止命令
#PrivateTmp=True表示给服务分配独立的临时空间
#注意：[Service]的启动、重启、停止命令全部要求使用绝对路径
#[Install]运行级别下服务安装的相关设置，可设置为多用户，即系统运行级别为3
```

保存退出。

**第四步：服务的启动/停止/刷新配置文件/查看状态**

``` shell
systemctl start nginx.service　 #启动nginx服务

# systemctl status nginx.service 查看服务当前状态

# systemctl stop nginx.service　 停止服务

# systemctl restart nginx.service　 重新启动服务

# systemctl list-units --type=service 查看所有已启动的服务

# systemctl enable nginx.service 设置开机自启动

# systemctl disable nginx.service 停止开机自启动
```

## ** 一个常见的错误**

### Warning: nginx.service changed on disk. Run 'systemctl daemon-reload' to reload units.

直接按照提示执行命令systemctl daemon-reload 即可。
 执行：  systemctl daemon-reload

** 一个常见的错误**

root@localhost ~]# systemctl status network.service

**Failed to get [properties](https://so.csdn.net/so/search?q=properties&spm=1001.2101.3001.7020): Access denied**

执行：    systemctl daemon-reexec