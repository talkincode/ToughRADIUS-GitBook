## 客户认证账号生成

### 接口描述

预生成客户认证账号，我了避免客户端调用API开户时，账号规则的一致性，通过这个接口可以使用由toughradius自动生成的账号。该账号保证与系统账号风格一致以及唯一性。

### 请求URL

- ` http://server:port/api/v1/account/gen`
      
### 请求方式

- GET 或者 POST 

示例：

    GET /api/v1/account/gen?sign=D942914E240AB56A966B4A1718712BEC HTTP/1.1

### 参数

无

### 返回结果

**返回示例：**

~~~json
{
  "msg": "处理成功",
  "nonce": "1460090044",
  "account" : "201600002"
  "code": 0,
  "sign": "07778EF610E11DD4AA1ADE65A7301192"
}
~~~

**返回结果描述：**

- code：返回结果码
- msg：返回消息
- account: 生成的账号
- nonce：随机时间戳
- sign：消息签名

