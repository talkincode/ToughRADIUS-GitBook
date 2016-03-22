## 删除资费套餐


### 接口描述

- 删除资费套餐

### 请求URL

- ` http://server:port/api/v1/product/delete `

### 请求方式

- GET 或者 POST

示例：


    GET /api/v1/product/delete?sign=A1EDC435DB53A80C551BB7EE06209671&product_id=8 HTTP/1.1

### 参数

| 参数名 | 必选 | 类型 | 说明 |
|---|:---|:---:|---:|
| product_id | 否 | string |资费ID |

### 返回结果

**返回示例：**

~~~json
{
  "msg": "API删除资费套餐:测试product56",
  "nonce": "1458621053",
  "code": 0,
  "sign": "0200C7C4BD6D3E808EB94E12C435910B"
}
  ~~~

**返回结果描述：**

- code：返回结果码
- msg：返回消息
- nonce：随机时间戳
- sign：消息签名
