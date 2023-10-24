## PostgreSQL安装

### 1、导入yum源

```shell
sudo yum install -y https://download.postgresql.org/pub/repos/yum/reporpms/EL-7-x86_64/pgdg-redhat-repo-latest.noarch.rpm
```

### 1、安装PostgreSQL服务

```shell
sudo yum install -y postgresql12 postgresql12-server
```

安装PostgreSQL 11就是 yum install postgresql12 postgresql12-server 

安装PostgreSQL 9.5就是 yum install postgresql95 postgresql95-server 依此类推 

### 2、初始化数据库

```shell
sudo /usr/pgsql-12/bin/postgresql-12-setup initdb 

#Initializing database ... OK
```

### 3、启动PostgreSQL服务

```shell
#启动PostgreSQL服务
sudo systemctl start postgresql-12

#设置PostgreSQL服务为开机启动
sudo systemctl enable postgresql-12
```

## 二、修改postgres账号密码

PostgreSQL安装成功之后，会默认创建一个名为postgres的Linux用户，初始化[数据库](https://cloud.tencent.com/solution/database?from_column=20065&from=20065)后，会有名为postgres的数据库，来存储数据库的基础信息，例如用户信息等等，相当于[MySQL](https://cloud.tencent.com/product/cdb?from_column=20065&from=20065)中默认的名为mysql数据库。

postgres数据库中会初始化一名超级用户`postgres`

为了方便我们使用postgres账号进行管理，我们可以修改该账号的密码

### 1、进入PostgreSQL命令行

通过su命令切换linux用户为postgres会自动进入命令行

```shell
su postgres
```

### 2、启动SQL Shell

```shell
psql
```

### 3、修改密码

```shell
ALTER USER postgres WITH PASSWORD 'NewPassword';
```

## 三、配置远程访问

### 1、开放端口

```shell
sudo firewall-cmd --add-port=5432/tcp --permanent
sudo firewall-cmd --reload
```

### 2、修改IP绑定

```shell
#修改配置文件
vi /var/lib/pgsql/12/data/postgresql.conf

#将监听地址修改为*
#默认listen_addresses配置是注释掉的，所以可以直接在配置文件开头加入该行
listen_addresses='*'
```

### 3、允许所有IP访问

```shell
#修改配置文件
vi /var/lib/pgsql/12/data/pg_hba.conf

#在问价尾部加入
host  all  all 0.0.0.0/0 md5
```

### 4、重启PostgreSQL服务

```shell
#重启PostgreSQL服务
sudo systemctl restart postgresql-12
```

复制

配置完成后即可使用客户端进行连接

## 四、PostgreSQL shell常用语法示例

启动SQL shell：

```shell
su postgres
psql
```

### 1、数据库相关语法示例

```shell

#查询数据存储目录
show data_directory;
#创建数据库
CREATE DATABASE mydb;

#查看所有数据库
\l

#切换当前数据库
\c mydb

#创建表
CREATE TABLE test(id int,body varchar(100));

#查看当前数据库下所有表
\d
```

### 2、用户与访问授权语法示例

```shell
#新建用户
CREATE USER test WITH PASSWORD 'test';

#赋予指定账户指定数据库所有权限
GRANT ALL PRIVILEGES ON DATABASE mydb TO test;

#移除指定账户指定数据库所有权限
REVOKE ALL PRIVILEGES ON DATABASE mydb TO test
```

>  权限代码：SELECT、INSERT、UPDATE、DELETE、TRUNCATE、REFERENCES、TRIGGER、CREATE、CONNECT、TEMPORARY、EXECUTE、USAGE