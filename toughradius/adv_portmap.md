## 服务端口映射

默认情况下，ToughRADIUS的Docker容器采用的是host模式的网络配置，注意缺省创建容器指令：

	 $ docker run -d --name trserver --net host index.alauda.cn/toughstruct/toughradius

其中 --net host  表示使用服务主机网络配置，这种模式无需任何NAT转换，这将获得最大的网络性能。如果需要灵活的改变端口，我们可以使用bridge模式，这种模式下容器将会创建虚拟的网络配置，并与主机网络进行桥接，我们需要将容器的端口映射到主机端口上：

	 $ docker run -d --name trserver -p 1812:1812/udp -p 1813:1813/udp -p 80:1816 -p 1815:1815 -p 1819:1819 index.alauda.cn/toughstruct/toughradius

如上所示，我们将主机端口与容器端口进行一对一映射，上面将主机的80端口映射到容器的管理控制台默认1816端口上。容器本身服务的端口保持不变，但主机映射端口可以灵活变化。

我们接着访问 http://主机地址 即可访问ToughRADIUS管理控制台。
