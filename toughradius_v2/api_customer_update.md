## 客户资料修改

### 接口描述

- 客户基本信息修改，包括姓名，密码，手机，邮箱等基本资料。

### 请求URL

- ` http://server:port/api/v1/customer/update`

### 请求方式

- GET 或者 POST  

示例：
    GET /api/v1/customer/update?customer_name=test001&sign=F8B0443F64913C678D3D5722533B51E4&realname=%E5%85%89%E5%A4%B4%E5%BC%BA&password=890890&idcard=111111&email=test008%40163.com&mobile=13888888888&address=%E5%80%AA%E7%BE%8E%E9%95%87 HTTP/1.1

### 参数

> customer_name 必须不为空

| 参数名 | 必选 | 类型 | 说明 |
|---|:---|:---:|---:|
| customer_name | 是 | string |客户账号名 |
| password | 否 | string |客户密码 |
| idcard | 否 | string |客户账号证件号码 |
| email | 否 | string |客户Email地址 |
| mobile | 否 | string |客户手机号码 |
| address | 否 | string |客户地址 |
| realname | 否 | string |客户真实姓名 |

### 返回结果

> {"msg": "处理成功", "nonce": "1457594864", "code": 0, "sign": "662105AD679B4C6BBEC4622D6AB2CA28"}

**返回示例：**

~~~json
{
  "msg": "处理成功",
  "nonce": "1457594864",
  "code": 0,
  "sign": "662105AD679B4C6BBEC4622D6AB2CA28"
}
~~~

**返回结果描述：**

- code：返回结果码
- msg：返回消息
- nonce：随机时间戳
- sign：消息签名
