# Linux PPTP 对接

以 ubuntu14 为例，谈谈PPTP对接ToughRADIUS

### 安装pptpd服务

	sudo apt-get update -y
	sudo apt-get install -y pptpd iptables libfreeradius-client2 libfreeradius-client-dev

如果/etc/radiusclient目录不存在，建立一个radius配置目录链接 

	ln -s /usr/local/etc/radiusclient /etc/radiusclient


### 配置pptpd与radius

修改配置文件 /etc/pptpd.conf

	option /etc/ppp/pptpd-options
	#debug
	#stimeout 10
	logwtmp
	#bcrelay eth1
	#delegate
	#connections 100
	localip 10.79.97.1
	remoteip 10.79.97.10-200

修改配置文件 /etc/ppp/pptpd-options，注意这里采用了maschapv2认证方式，并采用mppe128位加密模式。

	name pptpd
	refuse-pap
	refuse-chap
	refuse-mschap
	require-mschap-v2
	require-mppe-128

	# Network and Routing
	ms-dns 8.8.8.8
	ms-dns 8.8.4.4
	proxyarp
	nodefaultroute

	#Logging
	#debug
	#dump
	#logfile /var/log/pptpd.log

	# Miscellaneous
	lock
	nobsdcomp
	novj
	novjccomp
	#nologfd

	plugin /usr/lib/pppd/2.4.5/radius.so
	plugin /usr/lib/pppd/2.4.5/radattr.so
	radius-config-file /etc/radiusclient/radiusclient.conf

配置/etc/radiusclient/radiusclient.conf , 注意配置authserver，acctserver为你实际的radius服务器地址和端口。

	auth_order radius
	login_tries 4
	login_timeout 60
	nologin /etc/nologin
	authserver radius.toughctruc.net:1812
	acctserver radius.toughctruc.net:1813
	servers /etc/radiusclient/servers
	dictionary /etc/radiusclient/dictionary
	seqfile /var/run/radius.seq
	mapfile /etc/radiusclient/port-id-map
	default_realm
	radius_timeout 10
	radius_retries 3
	login_local /bin/login

如果 /etc/radiusclient/port-id-map 不存在，建立一个空文件

	echo "" > /etc/radiusclient/port-id-map

配置radius服务器和共享密钥 /etc/radiusclient/servers

	radius.toughstruct.net     testing123

为了支持mschapv2认证，需要加入 dictionary.microsoft字典， 修改字典文件 /etc/radiusclient/dictionary，在末尾务必加上 ：

	INCLUDE /etc/radiusclient/dictionary.microsoft

如果目录中没有这个字典，可以下载：[https://raw.githubusercontent.com/talkincode/ToughVPN/master/radius/dictionary/dictionary.microsoft][1]

### 修改防火墙配置并修改内核转发支持

注意IP地址与/etc/pptpd.conf中配置的一致

	iptables -t nat -A POSTROUTING -s 10.79.97.0/24 -o eth0 -j MASQUERADE
	iptables -A FORWARD -s 10.79.97.0/24 -p tcp -m tcp --tcp-flags FIN,SYN,RST,ACK SYN -j TCPMSS --set-mss 1356

设置内核转发支持

	sysctl -w net.ipv4.ip_forward=1

启动pptpd服务

	service pptpd start 

### 配置ToughRADIUS

在ToughRADIUS系统中，需要把PPTP作为接入设备加入，在BAS信息管理里增加一个标准配置即可。

增加资费，新增用户信息，接下来就可以进行拨号测试了。

在拨号过程中，可以通过用户消息跟踪或系统日志查看进行调试，使用mschapv2认证时，用户消息必定会有两个特定属性：MS-CHAP-Challenge 和 MS-CHAP2-Response，如果用户消息中没有此属性，则可能的原因是：

- pptp服务没有配置require-mschap-v2  和 require-mppe-128
- 系统内核不支持mppe
- 没有加入dictionary.microsoft
- 如果没有上面的问题，试着修改 require-mppe-128 为 require-mppe


### 注意事项

要支持mschapv2，需要系统内核支持MPPE，输入指令：

	modprobe ppp-compress-18 && echo ok

如果输出ok，则系统内核支持。

在测试过程中，可以开启debug收集日志进行诊断，以及配合Radius服务器的日志进行诊断。

更多帮助，请参考 [http://poptop.sourceforge.net/dox/][2]

另外，你也可以关注我们的这个开源项目：[https://github.com/talkincode/ToughVPN  ][3]  ，这个项目计划实现更简单的一键安装以及常识Docker模式的部署。 

[1]:	https://raw.githubusercontent.com/talkincode/ToughVPN/master/radius/dictionary/dictionary.microsoft
[2]:	http://poptop.sourceforge.net/dox/
[3]:	https://github.com/talkincode/ToughVPN