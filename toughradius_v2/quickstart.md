# ToughRADIUS快速指南

## 准备

一台完整的服务器，或者远程VPS，给服务器安装Linux系统，CentOS6以上，ubuntu14以上，或者其他你自己熟悉的Linux发行版。

你要懂一点技术，比如安装操作系统，会在终端敲命令。

![][image-1]

ToughRADIUS 是Docker技术的拥抱者，如果想更好的使用ToughRADIUS，你也需要去学习关于Docker的知识。

## 关于 Docker 安装模式

ToughRADIUS主要采用了Docker镜像部署的模式，ToughRADIUS的镜像基础是ubuntu 14。

> 我们可以把Docker看作一个软件集装箱，半世纪之前，集装箱发挥了巨大的力量，改变了整个运输产业，也改变了人们的生活。而Docker就类似这样一个集装箱工具，只不过他封装的是软件。

> 还记得linux安装lamp的经历吗？现在可以对各种安装配置apache，php等繁琐的工作说再见了。

> 我们把ToughRADIUS相关的配置，运行依赖环境等全部打包在一个“Docker集装箱”里，我们只需要在我们的服务器上简单的安装一个支持运行“Docker集装箱”的环境，那么我们不用去折腾各种运行环境搭建就能简单的让ToughRADIUS跑起来。

> 通常我们把封装了软件应用的“Docker集装箱”叫做镜像，有点类似你可能了解的ISO文件。

### 使用 toughcli 专用安装配置工具

toughcli 是一个toughradius以及相关软件的安装配置命令行接口 (Command Line Interface)。在 linux 下可以通过以下指令快速安装

	$ easy_install toughcli 

> 关于 toughcli 的详细介绍，请参考《[toughcli使用参考](../toughcli/intro.md)》


### Docker环境安装

我们首先应该安装配置服务器的Docker运行环境(Docker engine, Docker Compose)，toughcli提供了一个快速安装指令，以下指令会自动根据当前linux版本下载对应的docker版本进行自动安装。

	$ toughcli docker --install

![](../imgs/docker_install.gif)

> 如果安装遇到问题，请参考《[使用 toughcli 安装 Docker](../toughcli/docker.md)》


### ToughRADIUS 应用实例创建

> 注意，创建容器指令需要交互式完成，请根据提示进行输入操作

一键部署 TOUGHRADIUS，默认使用sqlite数据库


    $ toughcli radius --install  

![](../imgs/toughcli_radius_install.gif)

指定实例名

    $ toughcli radius --install  -i myradius 

指定版本类型

    $ toughcli radius --install -r dev 


> 注意： 默认使用的数据库是嵌入式 sqlite，如果你需要采用 mysql，请务必先安装 MySQL 数据库，如果没有安装 MySQL 数据库而在安装 ToughRADIUS 选择 mysql 类型，会导致无法使用系统，toughcli提供了一个MySQL Docker 实例的快速安装指令，以下指令进行自动安装。


    toughcli mysql --install

![](../imgs/toughcli_mysql_install.gif)

### 应用管理

这样我们的服务就已经运行了。我们可以通过浏览器来访问我们的应用了。

营业管理：http://ipaddr:1816   管理权限 admin/root


#### 防火墙设置

注意：如果访问不了web，可能是防火墙禁止了相关端口，如果不打算用内置防火墙，可以关闭防火墙。

	systemctl stop firewalld.service

禁止firewall开机启动，防火墙就永久性关闭了。

	systemctl disable firewalld.service



[image-1]:	../imgs/docker.png