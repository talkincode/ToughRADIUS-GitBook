## 客户认证账号详细信息


### 接口描述

- 查询单个客户的认证账号信息。

### 请求URL

- ` http://server:port/api/v1/account/query `
      
### 请求方式

- GET 或者 POST 

示例：

    GET /api/v1/account/query?sign=F1670B9A51DD7AE9882B36D32C48C89F&account_number=test01 HTTP/1.1

### 参数

| 参数名 | 必选 | 类型 | 说明 |
|---|:---|:---:|---:|
| account_number | 是 | string |客户认证账号 |


### 返回结果

**返回示例：**

~~~json
{
  "code": 0,
  "msg": "success",
  "accounts": {
      "account_number": "test01",
      "customer_id": 1,
      "product_id": 1,
      "group_id": null,
      "status": 1,
      "install_address": "小区E-01栋5楼",
      "balance": 0,
      "time_length": 0,
      "flow_length": 0,
      "expire_date": "2017-03-03",
      "user_concur_number": 0,
      "bind_mac": 0,
      "bind_vlan": 0,
      "mac_addr": "",
      "vlan_id1": 0,
      "vlan_id2": 0,
      "ip_address": null,
      "last_pause": null,
      "account_desc": null,
      "create_time": "2016-03-03 09:18:20",
      "update_time": "2016-03-03 09:18:20"
  },
  "nonce": "1456967907",
  "sign": "5F9FF91F9D761F0C4AD440B9CA7EEFC5"
}
~~~

**返回结果描述：**

- code：返回结果码
- msg：返回消息
- account：客户认证账号详细信息。
- nonce：随机时间戳
- sign：消息签名
