## 在线用户解锁下线


### 接口描述

- 解锁下线已在线的用户。

### 请求URL

- ` http://server:port/api/v1/online/unlock `

### 请求方式

- GET 或者 POST

示例：

    GET /api/v1/online/unlock?account_number=test001&sign=48AEC96D4DD371E9DE7F668D285D4E7E&acct_session_id=81200012&nas_addr=192.168.88.1 HTTP/1.1

### 参数

| 参数名 | 必选 | 类型 | 说明 |
|---|:---|:---:|---:|
| account_number | 是 | string |客户认证账号 |
| nas_addr | 是 | string |接入设备地址 |
| acct_session_id | 是 | string |在线用户会话ID |

### 返回结果

**返回示例：**

~~~json
{
  "msg": "下线成功",
  "nonce": "1458631355",
  "code": 0,
  "sign": "BCA299532FB26FF019337E66038484F4"}
~~~

**返回结果描述：**

- code：返回结果码
- msg：返回消息
- onlines：在线用户信息。
- nonce：随机时间戳
- sign：消息签名
