## 客户认证账号密码更新

### 接口描述

- 客户上网账号密码更新

### 请求URL

- ` http://server:port/api/v1/account/pw/update `

### 请求方式

- GET 或者 POST

示例：

    GET /api/v1/account/pw/update?account_number=test001&sign=0F26DD6788C8FAF507B720AE2EA8A9C4&password=123456789 HTTP/1.1

### 参数

| 参数名 | 必选 | 类型 | 说明 |
|---|:---|:---:|---:|
| account_number | 是 | string |客户认证账号 |
| password | 是 | string |客户认证账号密码 |


### 返回结果

**返回示例：**

~~~json
{
  "msg": "处理成功",
  "nonce": "1457597044",
  "code": 0,
  "sign": "72E6A444CE083B55BBA95B3D4B9EC4AD"
}
~~~

**返回结果描述：**

- code：返回结果码
- msg：返回消息
- nonce：随机时间戳
- sign：消息签名
