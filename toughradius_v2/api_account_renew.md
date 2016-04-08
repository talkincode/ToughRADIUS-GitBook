## 客户认证账号续费

### 接口描述

- 客户账号删续费，只对预付费包月，买断包月，买断时长，买断流量资费有效，客户续费主要是针对用户账号已经订购的资费进行缴费延续使用。

### 请求URL

- ` http://server:port/api/v1/account/renew`
      
### 请求方式

- GET 或者 POST 

示例：

    GET /api/v1/account/renew?sign=D942914E240AB56A966B4A1718712BEC&account_number=userp2&fee_value=90.00&months=3&giftdays=0 HTTP/1.1

### 参数

| 参数名 | 必选 | 类型 | 说明 |
|---|:---|:---:|---:|
| account_number | 是 | string |客户认证账号 |
| fee_value | 是 | string |缴费金额#.## |
| months | 否 | string |预付费包月资费授权月数 |
| giftdays | 否 | string |包月资费赠送天数 |



### 返回结果

**返回示例：**

~~~json
{
  "msg": "处理成功",
  "nonce": "1460090044",
  "code": 0,
  "sign": "07778EF610E11DD4AA1ADE65A7301192"
}
~~~

**返回结果描述：**

- code：返回结果码
- msg：返回消息
- nonce：随机时间戳
- sign：消息签名

