# 使用ToughMySQL为ToughRADIUS系统提供数据存储

ToughMySQL是一个基于Docker技术的MySQL应用，一开始它就是为了ToughRADIUS提供一个简单可靠易用的数据库服务。

ToughRADIUS默认采用了SqLite存储数据，通常这足够运营上千的用户量了，不过当系统对数据的可管理性，系统的性能有更高的要求时，我们建议采用MySQL数据库来替换。

## 功能特性：

- 实现MySQL Docker容器部署。
- 提供针对不同服务器配置环境的优化配置。
- 提供一键脚本快速安装。
- 提供备份脚本，支持7天以上备份自动删除。
- 提供主从，互为主备的快速配置。

## 快速指南

### 备份当前数据库

如果是首次安装，可略过，如果是迁移数据库，则务必进行备份。

### 安装脚本

tmshell是一个自动化安装和管理脚本，通过这个脚本，提供了很多有用的管理功能

    $ wget https://github.com/talkincode/toughmysql/raw/master/tmshell -O /usr/local/bin/tmshell
    $ chmod +x /usr/local/bin/tmshell
    $ tmshell install

直接输入 tmshell 可以看到支持的指令操作

~~~sh
    usage: tmshell [OPTIONS] instance

        docker_setup                install docker, docker-compose
        pull                        mysql docker images pull
        install                     install default mysql instance
        remove                      uninstall mysql instance
        config                      mysql instance config edit
        status                      mysql instance status
        restart                     mysql instance restart
        stop                        mysql instance stop
        logs                        mysql instance logs
        showmaster                  mysql instance show master status
        showslave                   mysql instance show slave status
        upmaster                    mysql instance update master sync config
        backup                      mysql instance backup database
        dsh                         mysql instance bash term

    All other options are passed to the tmshell program.
~~~

### 完整的安装过程

安装过程是一个交互式的过程，根据实际情况修改具体参数

    [root@i-jahnm3dt ~]# tmshell install
    # 默认创建的mysql数据库用户
    mysql user [raduser]:
    # 默认创建的mysql数据库用户密码
    mysql user password [radpwd]:
    # 默认创建的mysql数据库名
    mysql database [radiusd]:
    # 默认mysqlroot密码
    mysql root password [none]:
    # 默认的mysql专用复制用户密码
    mysql replication password [replication]:
    # mysql服务端口
    mysql port [3306]:
    # 如果打算以热备模式部署，需要输入server id
    mysql server id [1,2](default none): 1
    # mysql服务使用的最大内存
    mysql max memary [512M,1G,4G](default none):

    ToughMySQL instance config:

    instance name: mysql
    mysql_user: raduser
    mysql_password: radpwd
    mysql_database: radiusd
    mysql_root_password:
    mysql_repl_password: replication
    mysql_port: 3306
    serverid: 1
    mysql_max_mem:


    database:
        container_name: db_mysql
        image: "index.alauda.cn/toughstruct/mysql"
        privileged: true
        ports:
            -"3306:3306"
        ulimits:
            nproc: 65535
            nofile:
                soft: 20000
                hard: 40000
            environment:
                - SERVERID=1
                - MYSQL_MAX_MEM=
                - MYSQL_USER=raduser
                - MYSQL_PASSWORD=radpwd
                - MYSQL_DATABASE=radiusd
                - MYSQL_ROOT_PASSWORD=
                - MYSQL_REPL_PASSWORD=replication
        restart: always
        volumes:
            /home/toughrun/mysql/dbmysql:/var/lib/mysql
            /home/toughrun/mysql/backup:/var/backup

    Creating db_mysql
      Name          Command         State           Ports
    ----------------------------------------------------------
    db_mysql   /usr/local/bin/run   Up      0.0.0.0:3306->3306/tcp

/home/toughrun/mysql/dbmysql 目录是映射到主机上的MySQL数据文件目录

/home/toughrun/mysql/backup 目录是映射到主机上的备份目录


### 双机热备模式部署

请参考 [《ToughMySQL，为ToughRADIUS提供数据库双机热备支持》](http://blog.toughradius.org/2016/02/04/toughmysql-v0-0-1/)

