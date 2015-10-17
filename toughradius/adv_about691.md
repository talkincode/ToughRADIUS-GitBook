
## 客户端认证报691的问题诊断

通常用户终端拨号会出现一个常见的691错误，一般客户端都会说是密码错误，这实在是太草率太过时的一个提示。

要诊断691背后的错误，还真的去求助于RADIUS系统，以RADIUS协议来说，只要返回一个认证拒绝消息，客户端就会收到一个691错误，我们需要找到RADIUS系统认证拒绝的原因。

### 通过系统日志来诊断691

要通过系统日志来诊断，请务必开启系统的DEBUG开关，以获取尽量多的信息。

通过终端进行日志定位，这要求对linux下的环境和指令都很熟悉。

如果你的ToughRADIUS部署的容器名是 trserver，通过以下指令进入容器终端：

docker exec  -it  trserver bash

ToughRADIUS的radius日志默认保存在 /var/log/radiusd.log，你可以通过grep, awk, vim等工具来定位与指定用户相关的输出信息。

另外，ToughRADIUS的系统控制管理台，也提供了一个日志查看功能，不过只能查看最近的一部分内容，如果内容滚动过快，很难找到相关信息，如果系统用户很少，日志滚动不是很快，则通过这个功能也是可行的。

![][image-1]

### 通过用户日志来诊断691

在ToughRADIUS管理界面的维护管理栏目下，提供了一个用户消息跟踪的功能，该功能提供了对用户RADIUS认证和记账消息的实时跟踪，以及查询最近消息的功能，可以很方便的查找用户认证失败的原因。

![][image-2]

### 常见的691原因

- 接入设备没有在ToughRADIUS中注册，请在BAS信息管理里添加，注意信息准确，如果不准确也会导致认证被拒绝。
- 用户授权时间已经过期，请提醒用户续费。
- 用户密码错误，请与用户核对修正。
- 用户余额不足，请提醒用户充值。
- 用户并发控制，即已经有用户认证成功在线，但用户并发数被限制，请确认该在线是不是异常断开导致挂死，如果是，使用解锁或强制下线。
- 用户MAC或VLAN已经绑定，如果用户需要更换认证设备，请解绑。

[image-1]:	../imgs/control_logger.png
[image-2]:	../imgs/ops_trace_user.jpg