## 删除区域节点


### 接口描述

- 删除系统区域节点

### 请求URL

- ` http://server:port/api/v1/node/delete `

### 请求方式

- GET 或者 POST  

示例：

    GET /api/v1/node/delete?sign=ED9C5A0B8399BE0A6AA98B83E0AA4089&node_id=2 HTTP/1.1

### 参数

| 参数名 | 必选 | 类型 | 说明 |
|---|:---|:---:|---:|
| node_id | 是 | string |区域ID |

### 返回结果

**返回示例：**

~~~json
{
  "msg": "API删除区域成功:2",
  "nonce": "1458617283",
  "code": 0,
  "sign": "233074ABC15C7C7FB5BEA4D9372E17A5"
}
~~~

**返回结果描述：**

- code：返回结果码
- msg：返回消息
- nonce：随机时间戳
- sign：消息签名
