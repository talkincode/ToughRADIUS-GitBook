## 更新NAS接入设备

### 接口描述

- 更新NAS接入设备。

### 请求URL

- ` http://server:port/api/v1/nas/update `

### 请求方式

- GET 或者 POST

示例：

    GET /api/v1/nas/update?sign=B973F46C4FD4E0DBE6F330460EAFEA9E&ip_addr=127.0.0.1&dns_name=test.org&bas_name=%E6%B5%8B%E8%AF%95bas123&vendor_id=14988&coa_port=3788 HTTP/1.1

### 参数

| 参数名 | 必选 | 类型 | 说明 |
|---|:---|:---:|---|
| ip_addr | Y | string |接入设备地址 |
| dns_name | N | string |接入设备域名地址 |
| bas_name | N | string |接入设备名称 |
| vendor_id | N | int |接入设备地址厂商标识 |
| coa_port | N | int |接入设备地址授权端口 |

### 返回结果

**返回示例：**

~~~json
{
  "msg": "API更新BAS:127.0.0.1",
  "nonce": "1458627748",
  "code": 0,
  "sign": "227E2DFC436F6CA0F7E01B6AB749AC40"
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
- msg：返回消息
- nonce：随机时间戳
- sign：消息签名
