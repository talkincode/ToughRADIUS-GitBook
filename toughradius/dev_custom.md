# 定制你的ToughRADIUS专有版本

想拥有自己的ToughRADIUS专有版本吗，想保持与官方版本的同步同时加入自己的定制特性而不冲突吗，这当然是可以的。

## 准备

你是一个程序猿或接近猿类。

拥有一个自己的Github帐号，[https://github.com/][1]

拥有一个Docker容器云平台的帐号，推荐国内灵雀云，[http://www.alauda.cn/][2]

## fork一个ToughRADIUS仓库

![][image-1]

在windows平台，你可以使用 [GitHub Desktop][3] 来进行本地仓库管理。

遵循git版本管理的规范进行开发是你要自己把控的，保证自己的定制特性，同时保持对官方版本的同步合并。

## 选择开发工具

通常pycharm这样的ide是不错的选择。

![][image-2]

但ide并非必须的，一个编辑器足以胜任，尤其是像sublime text 这样的精品。

![][image-3]

## 定制Docker构建脚本

修改 Dockerfile构建脚本，修改以下内容：

	RUN git clone -b stable https://github.com/talkincode/ToughRADIUS.git /opt/toughradius

修改为：

	RUN git clone -b master <你的仓库地址>  /opt/toughradius

修改服务脚本 toughrad 修改以下内容：

	upgrade()
	{
		echo 'starting upgrade...'
		cd ${appdir} && git checkout stable && git pull origin stable
		supervisorctl restart radiusd
		supervisorctl restart admin
		supervisorctl restart customer
		supervisorctl status
		echo 'upgrade done'
	}

修改为：

	upgrade()
	{
		echo 'starting upgrade...'
		cd ${appdir} && git checkout master && git pull origin master
		supervisorctl restart radiusd
		supervisorctl restart admin
		supervisorctl restart customer
		supervisorctl status
		echo 'upgrade done'
	}

## 开始定制你的专有版本

现在可以开始加入你自己的代码了。

> 广告：欢迎加入ToughRADIUS的QQ开发群组讨论：487229323

可以修改一个自己的酷炫版本号：

文件在 ../toughradius/\_\_init\_\_.py

	＃!/usr/bin/env python
	
	__version__ = 'ohmyradius_v1.2.0.1'
	__license__ = 'AGPL'
	__auther__ = 'jamiesun.net@gmail.com'

完成之后就提交你的代码吧。

## 在灵雀云建立自己的构建镜像库

使用你的帐号进入灵雀云控制台，选择镜像仓库，创建镜像构建仓库。

![][image-4]

你可以在灵雀云关联绑定你的Github仓库，也可以选择快速创建。

![][image-5]

修改构建配置，在构建节点的选择上注意，如果选择国际节点，在构建速度上会有优势，因为ToughRADIUS依赖的很多开发库在国外，但是如果你的部署服务器国际带宽不够大，那么在初次部署时会比较慢。选择国内节点则反过来，如何选择请根据自己的情况判断，可以随时重新调整。

![][image-6]

点击开始构建按钮，等待构建完成。

![][image-7]

可以实时查看构建过程：

![][image-8]

构建完成后，就可以在你的服务器上使用Docker模式部署了，只是Docker仓库地址是你自己的了。

	 $ docker run -d --name trserver --net host index.alauda.cn/toughtech/ohmyradius

是不是酷毙了，你甚至可以把你得意的定制版本向更多朋友分享。

继续保持对你专有ToughRADIUS版本的更新维护吧。



[1]:	https://github.com/
[2]:	http://www.alauda.cn/
[3]:	https://desktop.github.com/ "GitHub Desktop"

[image-1]:	../imgs/fork_repo.jpg
[image-2]:	../imgs/dev_pycharm.jpg
[image-3]:	../imgs/dev_subm.jpg
[image-4]:	../imgs/docker_new_repo.jpg
[image-5]:	../imgs/docker_new_repo2.jpg
[image-6]:	../imgs/docker_new_repo3.jpg
[image-7]:	../imgs/docker_new_repo4.jpg
[image-8]:	../imgs/docker_new_repo5.jpg