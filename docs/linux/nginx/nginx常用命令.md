### 检测nginx 配置是否正常

``` shell
cd /usr/local/nginx/sbin
./nginx -t
```

### 重新加载配置文件

``` shell
./nginx -s reload
```

``` shell
./nginx #启动
./nginx -s stop #关闭
./nginx -s quit #关闭  //优雅关闭
./nginx -s reload #重启  // 快速关闭
```

### 加载指定配置文件重启

``` shell
/usr/local/nginx/sbin/nginx -s reload -c /usr/local/nginx/conf/nginx.conf
```

### 开放防火墙端口

``` shell
sudo firewall-cmd --add-port=5432/tcp --permanent
sudo firewall-cmd --reload
```

###  防火墙常用命令

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



