## 使用 toughcli 安装管理  mysql

查看mysql指令模块的帮助信息

    $ toughcli mysql --help

    Usage: toughcli mysql [OPTIONS]

        install mysql by docker mode

    Options:
        --install                       install mysql docker instance
        -e, --edit-config               edit mysql docker-compose.yml config
        -o, --docker-operate [|ps|config|pull|logs|start|stop|restart|kill|rm|down|pause|unpause|status|backup|showdbs|makedb|upgrade]
                                      docker instance operate
        -d, --rundir TEXT               default:/home/toughrun
        -i, --instance TEXT             mysql instance, default:mydb
        --help                          Show this message and exit.


### 参数说明：

    --install 新安装 mysql 实例，可选参数 -d,-i

    -e/--edit-config 编辑 toughcli 生成的 docker-compose配置文件，用来调整各项参数实现优化。可选参数 -d,-i

    -o/--docker-operate mysql 实例的维护指令,可选参数 -d,-i

    子参数

    -d/--rundir 运行主目录，会在主目录中再次创建实例目录，一个主目录下可以安装多个实例。
    -i/--instance 实例名，可以创建多个 toughradius 实例，但必须保证端口不冲突。


### 示例

- 安装 MySQL docker 实例


    $ toughcli mysql --install  


- 指定实例名


    $ toughcli mysql --install  -i m1 


- 升级版本


    $ toughcli mysql -o upgrade

- 启动服务


    $ toughcli mysql -o start

- 停止服务


    $ toughcli mysql -o stop

- 查看日志


    $ toughcli mysql -o logs

- 查看存在的数据库名称


    $ toughcli mysql -o  showdbs

    Database
    information_schema
    mydb
    mysql
    newdb
    performance_schema

- 创建一个新的空数据库


    $ toughcli mysql -o  makedb

根据提示交互式输入数据库用户名，密码，数据库名

    mysql user : newuser
    mysql user password : newpwd
    mysql database : newdb

- 备份数据库


    $ toughcli mysql -o  backup

增加一条定时任务就可以实现每日自动备份

    $ crontab -e

    01 3 * * * toughcli mysql -o  backup 

