## 添加区域节点


### 接口描述

- 系统区域节点添加

### 请求URL

- ` http://server:port/api/v1/node/add `

### 请求方式

- GET 或者 POST  

示例：

    GET /api/v1/node/add?node_name=tsnode&node_desc=%E6%B5%8B%E8%AF%95%E6%B7%BB%E5%8A%A0%E5%8C%BA%E5%9F%9F&sign=48D40D30F917BB393D948A34A3F64477 HTTP/1.1

### 参数

| 参数名 | 必选 | 类型 | 说明 |
|---|:---|:---:|---:|
| node_name | 是 | string |区域名称 |
| node_desc | 否 | string |区域描述 |

### 返回结果

**返回示例：**

~~~json
{
  "msg": "区域添加成功:tsnode",
  "nonce": "1458616584",
  "code": 0,
  "sign": "5C5845AF12948D559C4D61F2137B45B2"
}
~~~

**返回结果描述：**

- code：返回结果码
- msg：返回消息
- nonce：随机时间戳
- sign：消息签名
