# ToughRADIUS 安装进阶篇

在进阶篇里，我们将会提供本地化的安装参考，但相比起快速指南，进阶篇需要更强的专业知识和动手能力，为了节约您宝贵的时间，我们并不鼓励所有人都来尝试。

在安装成功之前，你可能会遇到关于 linux，git，python，mysql等一些列问题，如果你对这些都不熟悉，那么你只会遇到越来越多的问题，尽管这些问题在具备相关专业知识的人眼前不值一提。如果你觉得linux，git，python，mysql 这些都不是个事，那就继续吧。

*不适合这篇教程的人*

- 从来没有成功安装过 linux 的
- 装完 linux 系统连 make 指令都没有的
- 只会用界面，把 linux 当 windows 用的
- vi 的 打开，编辑，保存，退出这几个基本指令还不会的
- 特别懒的人
- 特别有钱的人

## linux 系统的选择

linux 的发行版世界实在是太多元化了，但万变不离其宗，理论上 ToughRADIUS 是可以运行在大部分linux 系统上的。

ToughRADIUS 依赖 Python2.7+ 运行环境，如果系统已经内置，则省略了升级 python 这一步，如果系统依然是 python2.4或 python2.6的版本，则需要先独立安装 python2.7版本。

为了更方便的安装，建议采用 centos7，ubuntu14等已经内置 python2.7 的系统。

## git 版本控制工具

git 是一个版本控制工具，通过 git 工具，你在服务器上安装的 ToughRADIUS 服务可以很方便的升级，或切换不同的版本，但git 并不是必须的，不使用 git，只是不能方便升级 ToughRADIUS，以后需要升级时，需要自己下载版本重新安装。

##  数据库的选择

ToughRADIUS默认是支持 sqlite 和 mysql 数据库的，其他数据库如 mssql，oracle 等目前只提供商业支持服务。ToughRADIUS V2版本经过重新架构，采用更好的缓存机制（Redis），数据库已经不是性能的决定性因素。

通常 sqlite 更易于使用，系统内置支持，无需额外安装，但没有提供基于网络的管理，带来维护上的不便，MySQL 在安装配置方面要复杂的多，但管理工具强大，更稳定可靠，依然是生产环境应用的首选。

## CentOS7 安装配置实例

ToughRADIUS 提供的默认安装指令是针对 CentOS 系统的，如果你希望在 ubuntu 下执行安装，可以自行修改Makefile文件，将 yum install 指令替换成对应的 apt-get install,Centos的软件名称与 ubuntu 也不相同，需要自行解决。

### 通过 git 工具安装

为了更方便的升级版本，建议通过使用 git 版本控制工具. 

请保证您的服务器网络畅通，如果您的服务器禁止访问网络，请首先解决网络问题。

- 安装 git 

    $ yum install -y git

- 克隆仓库（稳定版本）

    $ git clone -b release-stable https://github.com/talkincode/ToughRADIUS.git /opt/toughradius

- 克隆仓库（开发版本）

    $ git clone -b release-dev https://github.com/talkincode/ToughRADIUS.git /opt/toughradius

### 直接下载安装

- 下载解压稳定版

    $ wget https://github.com/talkincode/ToughRADIUS/archive/release-stable.zip -O /opt/release-stable.zip

    $ cd /opt

    $ unzip release-stable.zip

    $ mv ToughRADIUS-release-stable /opt/toughradius

- 下载解压开发版

    $ wget https://github.com/talkincode/ToughRADIUS/archive/release-dev.zip -O /opt/release-dev.zip

    $ cd /opt
    
    $ unzip release-dev.zip

    $ mv ToughRADIUS-release-dev /opt/toughradius


### 安装 toughradius

完成克隆仓库，稳定版或开发版任选一种。/opt/toughradius 是一个约定的的安装路径，暂时不要修改为其他路径。

按以下步骤执行安装任务

    $ cd /opt/toughradius   

    $ make all

make all 指令会完成 ToughRADIUS 所有相关的系统依赖下载安装，相关的 python 模块安装，已经配置文件的安装。在 make all 的过程中，有可能会出现失败，比如网络超时，缺少系统其它依赖，这对你通常是一个挑战，在 linux 的世界，很多东西是无法一一预料的，这还需要你具备一定的专业能力。

### 修改 ToughRADIUS 配置

make all 完成后，会存在以下配置文静：

    /etc/toughradius.json

这是 ToughRADIUS 的主要配置文件，我们可能需要修改关于数据库部分的配置。如果你只想使用内置的 sqlite 数据库，无需做任何更改。

默认的 sqlite 数据库文件在 /var/toughradius/toughradius.sqlite3，你可以下载到到本地计算机使用 sqlite 的管理工具打开查看数据。

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


### 初始化数据

    $ cd /opt/toughradius

    $ make initdb

如果配置文件数据库部分没有错误，这一步将顺利通过，会创建所有数据库表，以及初始化必须的配置参数。

### 管理 ToughRADIUS 服务

现在你可以运行 ToughRADIUS 服务了，假设前面的过程都顺利完成。ToughRADIUS 已经配置好系统的自启动服务。

    $ service toughradius start

如果你要停止 ToughRADIUS 服务，执行

    $ service toughradius stop

重启请执行

    $ service toughradius restart

查看运行状态请执行

    $ service toughradius status

### ToughRADIUS 数据备份

ToughRADIUS 提供了一个通用的不依赖数据库类型的数据备份服务，你可以通过ToughRADIUS的管理界面-系统管理子菜单下的数据备份来使用它。

备份数据默认在目录 /var/toughradius/data

### ToughRADIUS 的日志

所有的日志文件全部在 /var/toughradius 目录下

web 管理控制台日志文件是 /var/toughradius/radius-manage.log 

radius 的认证记账日志是 /var/toughradius/radius-worker.log

你可以通过 linux 下的vi,awk,more,less,tail 工具来查看分析日志，比如查看最后100行日志：

    $ tail -n 100 /var/toughradius/radius-manage.log

    $ tail -n 100 /var/toughradius/radius-worker.log

如果你在安装的过程中遇到问题，提供这些日志信息才是最有用的，如果你不是提供这些日志数据，那么你几乎肯定得不到答案。


### ToughRADIUS 服务进程管理

/etc/toughradius.conf 是ToughRADIUS服务进程配置，基于 supervisord 实现服务进程管理。

如果你实际不是安装在 /opt/toughradius 这个路径，可以修改这个配置文件中的/opt/toughradius 路径

- 调整 radius 子进程数量以提高 ToughRADIUS 在多核 CPU 下的性能

修改 numprocs 参数即可，设置为 CPU 核心数量或2倍都可以。

    [program:worker]
    command=python /opt/toughradius/radiusctl worker -c /etc/toughradius.json
    startretries = 10
    process_name = %(program_name)s%(process_num)d
    numprocs=4
    redirect_stderr=true
    stdout_logfile=/var/toughradius/radius-worker.log












