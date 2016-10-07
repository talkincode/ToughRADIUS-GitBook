## 客户信息删除


### 接口描述

- 删除客户资料，以及所有认证账号,相关数据

### 请求URL

- ` http://server:port/api/v1/customer/delete `
      
### 请求方式

- GET 或者 POST 

示例：

    GET /api/v1/customer/delete?sign=EBB9DDBF180B35D7C7C8145DD13620D4&customer_name=test03 HTTP/1.1

### 参数

| 参数名 | 必选 | 类型 | 说明 |
|---|:---|:---:|---:|
| customer_name | 否 | string |客户账号名 |


### 返回结果

**返回示例：**

~~~json
    {
      "code": 0,
      "msg": "success",
      "nonce": "1456973309",
      "sign": "6FDA5A8BFA9413E79F0F391783ECAD52"
    }
~~~

**返回结果描述：**

- code：返回结果码
- msg：返回消息
- nonce：随机时间戳
- sign：消息签名


