## 客户认证账号删除

### 接口描述

- 客户账号删除，删除客户账号资料及相关数据，但不删除客户信息

### 请求URL

- ` http://server:port/api/v1/account/delete `
      
### 请求方式

- GET 或者 POST 

示例：

    GET /api/v1/account/delete?sign=EBB9DDBF180B35D7C7C8145DD13620D4&account_number=test03 HTTP/1.1

### 参数

| 参数名 | 必选 | 类型 | 说明 |
|---|:---|:---:|---:|
| account_number | 否 | string |客户认证账号 |


### 返回结果

**返回示例：**

    {
      "code": 0,
      "msg": "success",
      "nonce": "1456974137",
      "sign": "E65A4352B6DAD0576EBAD28AFCFCAA35"
    }

**返回结果描述：**

- code：返回结果码， 0 成功， 1 失败
- msg：返回消息
- nonce：随机时间戳
- sign：消息签名

