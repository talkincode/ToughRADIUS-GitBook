## 修改区域节点


### 接口描述

- 系统区域节点修改

### 请求URL

- ` http://server:port/api/v1/node/update `

### 请求方式

- GET 或者 POST  

示例：

    GET /api/v1/node/update?node_name=tsnode2&node_desc=%E6%B5%8B%E8%AF%95%E6%B7%BB%E5%8A%A0%E5%8C%BA%E5%9F%9F2&sign=B85174D3CE4D3EEBD8707FC84E2D4A05&node_id=2 HTTP/1.1

### 参数

| 参数名 | 必选 | 类型 | 说明 |
|---|:---|:---:|---:|
| node_id | 是 | string |区域ID |
| node_name | 否 | string |区域名称 |
| node_desc | 否 | string |区域描述 |

### 返回结果

**返回示例：**

~~~json
{
  "msg": "区域修改成功:2",
  "nonce": "1458616961",
  "code": 0,
  "sign": "06634CA59F9D15675EFA65B1E6157613"
}
~~~

**返回结果描述：**

- code：返回结果码
- msg：返回消息
- nonce：随机时间戳
- sign：消息签名
