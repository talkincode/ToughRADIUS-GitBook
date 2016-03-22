## NAS接入设备查询

### 接口描述

- 查询NAS接入设备。

### 请求URL

- ` http://server:port/api/v1/nas/fetch `

### 请求方式

- GET 或者 POST

示例：

    GET /api/v1/nas/fetch?sign=997C3346A786FD703D813AF3B65412F7&ip_addr=127.0.0.1 HTTP/1.1

### 参数

| 参数名 | 必选 | 类型 | 说明 |
|---|:---|:---:|---|
| ip_addr | 是 | string |接入设备地址 |


### 返回结果

**返回示例：**

~~~json
{
  "nonce": "1458621462",
  "code": 0,
  "coa_port": 3799,
  "vendor_id": "0",
  "ipaddr": "127.0.0.1",
  "sign": "13857232D10CC9D05F17309551D009D4",
  "secret": "secret",
  "msg": "ok"
}
~~~

**NAS设备编码对照：**

~~~json
{
    "0": "标准",
    "3041": "阿尔卡特",
    "2352": "爱立信",
    "2011": "华为",
    "25506": "H3C",
    "3902": "中兴",
    "10055": "爱快",
    "14988": "RouterOS"
}
~~~

**返回结果描述：**

- code：返回结果码
- ipaddr：NAS IP地址
- secret：共享秘钥
- coa_port：授权端口
- vendor_id：NAS设备厂家编码
- msg：返回消息
- nonce：随机时间戳
- sign：消息签名
