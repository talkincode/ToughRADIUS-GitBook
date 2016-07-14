# ToughRADIUS快速指南

### 安装环境

操作系统建议：centos6/7, ubuntu 14+,其他linux x64系统，推荐使用 centos7

服务器配置建议: CPU：1核心(或以上)，内存：1G(或以上)，硬盘：50G(或以上)


### 下载 ToughRADIUS 安装包

    cd /opt
    wget http://download.toughradius.net/toughradius-stable-v2-linux-x64.tar.xz -O toughradius-v2-linux-x64.tar.xz

### 部署系统

    cd /opt
    tar Jxvf toughradius-v2-linux-x64.tar.xz

解压缩得到 /opt/toughradius 目录

>> 注意： /opt/toughradius 是默认目录，如果要修改此目录，必须同时修改 Makefile 和 toughctl, toughradius.conf 文件中的对应路径。

执行 make all 安装

    cd /opt/toughradius 
    make all

首次使用还需初始化数据库，根据实际情况修改 /opt/toughradius/etc/toughradius.json 的数据库配置，默认采用 sqlite 数据库。

    toughctl initdb

#### mysql 配置案例

如果你希望使用 mysql 数据库，请首先自己完成 mysql 的安装配置，并保证 mysql服务已经正常运行，同时创建一个空的数据库，创建一个专用的用户名和密码。

mysql 示例：

进入 mysql 终端管理:

    mysql >  create database raddb DEFAULT CHARACTER SET utf8 COLLATE utf8_general_ci;
    mysql >  GRANT ALL ON raddb.* TO raduser@'%' IDENTIFIED BY 'radpwd' WITH GRANT OPTION;
    mysql >  FLUSH PRIVILEGES;

修改数据库配置部分,具体参数请根据实际填写。

    "database": {
        "backup_path": "/var/toughradius/data",
        "dbtype": "mysql",
        "dburl": "mysql://raduser:radpwd@127.0.0.1:3306/raddb?charset=utf8",
        "echo": 0,
        "pool_recycle": 300,
        "pool_size": 60
    }


###  运行系统

启动 Radius 服务

    toughctl daemon -s startup                     # 启动 Radius 服务进程，

停止服务

    toughctl daemon -s shutdown                    # 停止 Radius 服务进程

查看状态

    toughctl daemon -s status                      # 查看 Radius 服务进程运行状态

重载配置

    toughctl daemon -s reload                      # 修改配置文件后重新加载服务

查看日志

    toughctl daemon -s "tail -f manage"            # tail 模式查看管理控制台日志
    toughctl daemon -s "tail -f worker:worker0"    # tail 模式查看 radius 认证记账日志
    toughctl daemon -s "tail -f task"              # tail 模式查看定时任务日志

> 注意，worker 进程可以配置多个, 进程名为 worker:worker0， worker:worker1 ...

### 使用系统

系统使用的端口可以在 /opt/toughradius/etc/toughradius.json 中修改

默认端口如下：

- 16370 默认 redis 服务端口，与 toughradius.json 配置相符合
- 1816  默认管理控制台端口，可以通过http://服务器地址:1816 访问 
- 1812  默认 Radius 认证端口，提供路由器接入设备访问
- 1813  默认 Radius 记账端口，提供路由器接入设备访问



### 防火墙设置

注意：如果访问不了web，可能是防火墙禁止了相关端口，如果不打算用内置防火墙，可以关闭防火墙。

	systemctl stop firewalld.service

禁止firewall开机启动，防火墙就永久性关闭了。

	systemctl disable firewalld.service
