# ToughRADIUS快速指南

## 准备

一台完整的服务器，或者远程VPS，给服务器安装Linux系统，CentOS6以上，ubuntu14以上，或者其他你自己熟悉的Linux发行版。

你要懂一点技术，比如安装操作系统，会在终端敲命令。

![][image-1]

ToughRADIUS 是Docker技术的拥抱者，如果想更好的使用ToughRADIUS，你也需要去学习关于Docker的知识。

## 安装部署

ToughRADIUS主要采用了Docker镜像部署的模式，ToughRADIUS的镜像基础是ubuntu 14。

> 我们可以把Docker看作一个软件集装箱，半世纪之前，集装箱发挥了巨大的力量，改变了整个运输产业，也改变了人们的生活。而Docker就类似这样一个集装箱工具，只不过他封装的是软件。

> 还记得linux安装lamp的经历吗？现在可以对各种安装配置apache，php等繁琐的工作说再见了。

> 我们把ToughRADIUS相关的配置，运行依赖环境等全部打包在一个“Docker集装箱”里，我们只需要在我们的服务器上简单的安装一个支持运行“Docker集装箱”的环境，那么我们不用去折腾各种运行环境搭建就能简单的让ToughRADIUS跑起来。

> 通常我们把封装了软件应用的“Docker集装箱”叫做镜像，有点类似你可能了解的ISO文件。

### 使用 toughcli 专用安装配置工具

	easy_install toughcli 或者 pip install toughcli   

看看这个工具为我们提供了那些功能

	$ toughcli --help
    Usage: toughcli [OPTIONS] COMMAND [ARGS]...

    Options:
    --version
    --info         Show Server info
    --help         Show this message and exit.

    Commands:
    docker
    mysql
    radius
    redis
    upgrade
    wlan

查看子模块的指令帮助信息

    $ toughcli radius --help
    Usage: toughcli radius [OPTIONS]

    Options:
    --install
    -e, --edit-config               edit radius docker-compose.yml config
    -o, --docker-operate [|ps|config|pull|logs|start|stop|restart|kill|rm|down|pause|unpause|status]
                                  docker instance operate
    -d, --rundir TEXT               default:/home/toughrun
    -i, --instance TEXT
    -n, --worker-num INTEGER
    -r, --release [dev|stable|commcial]
    --help                          Show this message and exit.


查看服务器信息：

    $ toughcli --info
    Linux distribution: CentOS Linux,7.2.1511,Core
    Cli version toughcli: 0.0.7
    Env_home: /root
    Env_path: /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/root/bin:/usr/local/bin
    Server platform: Linux-3.10.0-327.4.5.el7.x86_64-x86_64-with-centos-7.2.1511-Core,x86_64
    Python version: CPython,2.7.5
    Docker version 1.8.2-el7.centos, build a01dc02/1.8.2
    docker-compose version 1.5.2, build 7240ff3


### Docker环境安装

我们首先应该安装配置服务器的Docker运行环境(Docker engine, Docker Compose)，toughcli提供了一个快速安装指令，以下指令会自动根据当前linux版本下载对应的docker版本进行自动安装。

	toughcli docker --install

####  Docker 自定义安装

如果在 docker 安装过程中遇到问题，可以参考最原始最全面的 docker 安装指南。

- [Ubuntu](https://docs.docker.com/engine/installation/linux/ubuntulinux/)
- [Arch Linux](https://docs.docker.com/engine/installation/linux/archlinux/)
- [CentOS](https://docs.docker.com/engine/installation/linux/centos/)
- [CRUX Linux](https://docs.docker.com/engine/installation/linux/cruxlinux/)
- [Debian](https://docs.docker.com/engine/installation/linux/debian/)
- [Fedora](https://docs.docker.com/engine/installation/linux/fedora/)
- [FrugalWare](https://docs.docker.com/engine/installation/linux/frugalware/)
- [Gentoo](https://docs.docker.com/engine/installation/linux/gentoolinux/)
- [Oracle Linux](https://docs.docker.com/engine/installation/linux/oracle/)
- [Red Hat Enterprise Linux](https://docs.docker.com/engine/installation/linux/rhel/)
- [openSUSE and SUSE Linux Enterprise](https://docs.docker.com/engine/installation/linux/SUSE/)

遇到困难不要轻易放弃，你还可以尝试使用[二进制安装](https://docs.docker.com/engine/installation/binaries/)

#### Docker Compose

Docker Compose是在使用Docker容器部署分布式应用时的工具，可以定义哪个容器运行哪个应用。要使用 Docker Compose，Docker 版本必须在1.7+

[官方安装文档](https://docs.docker.com/compose/install/)


### ToughRADIUS 应用实例创建

> 注意，创建容器指令需要交互式完成，请根据提示进行输入操作

一键部署 TOUGHRADIUS，默认使用sqlite数据库


    $ toughcli radius --install  

指定实例名

    $ toughcli radius --install  -i myradius 

指定版本类型

    $ toughcli radius --install -r dev 


> 注意： 默认使用的数据库是嵌入式 sqlite，如果你需要采用 mysql，请务必先安装 MySQL 数据库，如果没有安装 MySQL 数据库而在安装 ToughRADIUS 选择 mysql 类型，会导致无法使用系统，toughcli提供了一个MySQL Docker 实例的快速安装指令，以下指令进行自动安装。


    toughcli mysql --install


### 应用管理

这样我们的服务就已经运行了。我们可以通过浏览器来访问我们的应用了。

营业管理：http://ipaddr:1816   管理权限 admin/root


#### 防火墙设置

注意：如果访问不了web，可能是防火墙禁止了相关端口，如果不打算用内置防火墙，可以关闭防火墙。

	systemctl stop firewalld.service

禁止firewall开机启动，防火墙就永久性关闭了。

	systemctl disable firewalld.service



[image-1]:	../imgs/docker.png