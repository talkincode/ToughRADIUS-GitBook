## 在线用户查询


### 接口描述

- 查询系统在线用户信息，支持客户认证账号,客户账号名二选其一为查询条件查询。

### 请求URL

- ` http://server:port/api/v1/online/query `

### 请求方式

- GET 或者 POST

示例：

    GET /api/v1/online/query?customer_name=test001&sign=007AEAA0EC6C19E8DF47E5EEC6CBC7A9 HTTP/1.1

### 参数

> account_number 与 customer_name 必须有一个不为空

| 参数名 | 必选 | 类型 | 说明 |
|---|:---|:---:|---:|
| account_number | 是 | string |客户认证账号 |
| customer_name | 是 | string |客户账号名 |

### 返回结果

> 返回的结果中包含所有满足条件的在线用户结果集

**返回示例：**

~~~json
{
  "msg": "处理成功",
  "nonce": "1457513036",
  "code": 0,
  "sign": "752608BE3DD7A07F9FECBF8E49EC1A3B",
  "onlines":[
      {
        "input_total": 0,
        "billing_times": 0,
        "framed_ipaddr": "198.168.8.139",
        "nas_port_id": "12312",
        "start_source": 1,
        "acct_session_id": "dengdengdeng",
        "nas_addr": "198.168.8.139",
        "account_number": "test001",
        "acct_start_time": "2016-03-09 16:42:37",
        "output_total": 0,
        "id": 1,
        "mac_addr": "0"
      },
      {
        "input_total": 0,
        "billing_times": 0,
        "framed_ipaddr": "198.168.8.139",
        "nas_port_id": "12312",
        "start_source": 1,
        "acct_session_id": "dengdengdeng2",
        "nas_addr": "198.168.8.139",
        "account_number": "test001",
        "acct_start_time": "2016-03-09 16:43:49",
        "output_total": 0,
        "id": 2,
        "mac_addr": "0"
      }]
      }
~~~

**返回结果描述：**

- code：返回结果码
- msg：返回消息
- onlines：在线用户信息。
- nonce：随机时间戳
- sign：消息签名
