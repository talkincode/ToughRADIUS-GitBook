## 客户认证账号续费

### 接口描述

- 客户账号删续费，只对预付费包月，买断包月，买断时长，买断流量资费有效，客户续费主要是针对用户账号已经订购的资费进行缴费延续使用。

### 请求URL

- ` http://server:port/api/v1/account/renew`
      
### 请求方式

- GET 或者 POST 

示例：

    GET /api/v1/account/renew?sign=D942914E240AB56A966B4A1718712BEC&account_number=userp2&fee_value=90.00&months=3&giftdays=0&pay_status=0 HTTP/1.1

### 参数

| 参数名 | 必选 | 类型 | 说明 |
|---|:---|:---:|---:|
| account_number | 是 | string |客户认证账号 |
| fee_value | 是 | string |缴费金额#.## |
| months | 否 | string |预付费包月资费授权月数 |
| giftdays | 否 | string |包月资费赠送天数 |
| pay_status | 否 | string |支付状态 0 未支付 1 已支付 |

注意，当pay_status为0时，toughradius不会立即新增订单，只会将订单数据存入定时缓存, 当pay_status 为1时，toughradius会首先探测缓存是否有该订单数据，如果有则新增缓存中存在的订单数据。该功能主要用在第三方支付未完成之前的数据预处理。


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

