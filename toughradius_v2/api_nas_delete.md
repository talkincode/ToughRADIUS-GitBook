## 删除NAS接入设备

### 接口描述

- 删除NAS接入设备。

### 请求URL

- ` http://server:port/api/v1/nas/delete `

### 请求方式

- GET 或者 POST

示例：

    GET /api/v1/nas/delete?sign=997C3346A786FD703D813AF3B65412F7&ip_addr=127.0.0.1 HTTP/1.1

### 参数

| 参数名 | 必选 | 类型 | 说明 |
|---|:---|:---:|---|
| ip_addr | 是 | string |接入设备地址 |


### 返回结果

**返回示例：**

~~~json
{
  "code":0,
  "msg": "API delete bas:127.0.0.1 success",
  "nonce": "1458622202",
  "sign": "0E5124CAF82424148C82363EB1C885C1"}
~~~



**返回结果描述：**

- code：返回结果码
- msg：返回消息
- nonce：随机时间戳
- sign：消息签名
