## 使用 toughcli 安装 Docker 

$ toughcli docker --install

以上指令将自动完成 docker 与 docker-compose 的安装。

实际上，该指令执行了如下语句：

    $ curl -sSL https://get.daocloud.io/docker | sh
    $ curl -L https://get.daocloud.io/docker/compose/releases/download/1.5.2/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose
    $ chmod +x /usr/local/bin/docker-compose
    $ chkconfig docker on
    $ service docker start

