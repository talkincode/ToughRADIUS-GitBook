## 客户信息查询


### 接口描述

- 查询系统客户信息，以及客户的认证账号列表。

### 请求URL

- ` http://server:port/api/v1/customer/query `
      
### 请求方式

- GET 或者 POST 

示例：

    GET /api/v1/customer/query?sign=F1670B9A51DD7AE9882B36D32C48C89F&account_number=test01&customer_name=test01 HTTP/1.1

### 参数

> account_number 与 customer_name 必须有一个不为空

| 参数名 | 必选 | 类型 | 说明 |
|---|:---|:---:|---:|
| account_number | 是 | string |客户认证账号 |
| customer_name | 是 | string |客户账号名 |

### 返回结果

> 如果指定了 account_number参数，返回的accounts结果集中将只会包含 account_number的信息

**返回示例：**

    {
      "code": 0,
      "msg": "success",
      "customer": {
        "customer_id": 1,
        "node_id": 1,
        "customer_name": "test01",
        "realname": "tester",
        "idcard": "4123123",
        "sex": 1,
        "age": 0,
        "email": "",
        "mobile": "13655555555",
        "address": "小区E-01栋5楼",
        "customer_desc": null,
        "create_time": "2016-03-03 09:18:20",
        "update_time": "2016-03-03 09:18:20"
      },
      "accounts": [
        {
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
        }
      ],
      "nonce": "1456967907",
      "sign": "5F9FF91F9D761F0C4AD440B9CA7EEFC5"
    }

**返回结果描述：**

- code：返回结果码， 0 成功， 1 失败
- msg：返回消息
- customer：客户基本信息
- accounts：客户所有认证账号。
- nonce：随机时间戳
- sign：消息签名
