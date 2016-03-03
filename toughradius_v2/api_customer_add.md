## 客户信息新增

### 接口描述

- 新开客户账号，同时开通默认认证账号。

### 请求URL

- ` http://server:port/api/v1/customer/add `
      
### 请求方式

- GET 或者 POST

示例：

    GET /api/v1/customer/add?sign=880E93FA8FA22273F24DE5C0F2BE779D&account_number=test03&customer_name=test03&node_id=1&realname=test03&idcard=123&email=222%40qqq.com&mobile=133454646&address=12313&begin_date=2016-02-10&expire_date=2017-02-10&product_id=1&time_length=0&flow_length=0&balance=0&password=888888 HTTP/1.1

### 参数

| 参数名 | 必选 | 类型 | 说明 |
|---|:---|:---:|---:|
| realname | 否 | string |用户姓名 |
| node_id | 否 | int |区域id |
| idcard | 是 | string |证件号码 |
| mobile | 是 | string |用户手机号码 |
| email | 是 | string |用户Email |
| address | 是 | string |用户地址 |
| customer_name | 是 | string |客户自助服务账号 |
| account_number | 否 | string |用户认证账号 |
| product_id | 否 | int |资费id |
| password | 否 | string |用户密码 |
| begin_date | 否 | string |开通日期 |
| expire_date | 否 | string |过期日期 |
| balance | 是 | int |用户余额 |
| time_length | 是 | int |用户时长 |
| flow_length | 是 | int |用户流量 |


### 返回结果

**返回示例：**

    {
      "code": 0,
      "msg": "success",
      "nonce": "1456970950",
      "sign": "1E5AD43D7794267B1C08939B7A0871BC"
    }

    