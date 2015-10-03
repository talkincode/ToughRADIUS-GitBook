# ToughRADIUS快速指南

## 准备

一台完整的服务器，或者远程VPS，给服务器安装Linux系统，CentOS6以上，ubuntu13以上，或者其他你自己熟悉的Linux发行版。

你要懂一点技术，比如安装操作系统，会在终端敲命令。

![][image-1]

ToughRADIUS 是Docker技术的拥抱者，当你决定使用ToughRADIUS，你也需要去学习关于Docker的知识。

## 安装部署

ToughRADIUS主要采用了Docker镜像部署的模式，ToughRADIUS的镜像基础是CentOS 7。

> 我们可以把Docker看作一个软件集装箱，半世纪之前，集装箱发挥了巨大的力量，改变了整个运输产业，也改变了人们的生活。而Docker就类似这样一个集装箱工具，只不过他封装的是软件。

> 还记得linux安装lamp的经历吗？现在可以对各种安装配置apache，php等繁琐的工作说再见了。

> 我们把ToughRADIUS相关的配置，运行依赖环境等全部打包在一个“Docker集装箱”里，我们只需要在我们的服务器上简单的安装一个支持运行“Docker集装箱”的环境，那么我们不用去折腾各种运行环境搭建就能简单的让ToughRADIUS跑起来。

> 通常我们把封装了软件应用的“Docker集装箱”叫做镜像，有点类似你可能了解的ISO文件。

### Docker 安装

*CentOS 6*

	$ sudo yum install http://mirrors.yun-idc.com/epel/6/i386/epel-release-6-8.noarch.rpm
	
	$ sudo yum install docker-io
	
	$ sudo service docker start

*CentOS 7*

	$ sudo yum install docker
	
	$ sudo service docker start

*Ubuntu*

	$ sudo apt-get update
	
	$ sudo apt-get install docker.io
	
	$ sudo ln -sf /usr/bin/docker.io /usr/local/bin/docker
	
	$ sudo sed -i '$acomplete -F _docker docker' /etc/bash_completion.d/docker.io

*Windows*

> 请下载[Windows安装文件][1]：[https://github.com/boot2docker/windows-installer/releases/download/v1.8.0/docker-install.exe][2]

> 注意：Window下的Docker服务是借助虚拟机来实现的，性能上远不如使用linux主机。

### Docker 容器创建

确认Docker服务已经运行，通过以下指令创建ToughRADIUS的容器实例，当看到一串hash打印时，说明容器创建成功了。

	 $ docker run -d --name trserver --net host index.alauda.cn/toughstruct/toughradius

这样我们的服务就已经运行了。我们可以通过浏览器来访问我们的应用了。

营业管理：http://ipaddr:1816   管理权限 admin/root

自助服务：http://ipaddr:1817

系统管理：http://ipaddr:1819   管理权限 ctlman/ctlroot

### 容器的基本管理

*启动容器*

	 $ docker start trserver

*停止容器*

	 $ docker stop trserver

*重启容器*

	 $ docker restart trserver

*查看容器日志，Ctrl＋c退出*

	 $ docker logs trserver

[1]:	https://github.com/boot2docker/windows-installer/releases/download/v1.8.0/docker-install.exe
[2]:	https://github.com/boot2docker/windows-installer/releases/download/v1.8.0/docker-install.exe

[image-1]:	../imgs/docker.png