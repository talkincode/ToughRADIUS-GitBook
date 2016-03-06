## 客户授权校验

### 接口描述

- 客户登陆校验，支持自助服务名登陆，支持上网账号登陆

### 请求URL

- ` http://server:port/api/v1/customer/auth`
      
### 请求方式

- GET 或者 POST

示例

    GET /api/v1/customer/auth?sign=45D0920A65AD46529FF9BCCC3CD45497&password=888888&customer_name=test03 HTTP/1.1


### 参数

customer_name 与 account_number 必须有一个不为空

| 参数名 | 必选 | 类型 | 说明 |
|---|:---|:---:|---:|
| customer_name | 是 | string |客户账号名 |
| account_number | 是 | string |客户认证账号 |
| password | 否 | string |客户账号密码或认证账号密码 |

### 返回结果

**返回示例：**

~~~json
{
  "code": 0,
  "msg": "success",
  "nonce": "1456970950",
  "sign": "1E5AD43D7794267B1C08939B7A0871BC"
}
~~~

**返回结果描述：**

- code：返回结果码
- msg：返回消息
- nonce：随机时间戳
- sign：消息签名

