## 资费套餐修改


### 接口描述

- 修改资费套餐

### 请求URL

- ` http://server:port/api/v1/product/update `

### 请求方式

- GET 或者 POST

示例：


    GET /api/v1/product/add?product_name=%E6%B5%8B%E8%AF%95product5&product_policy=2&fee_months=12&fee_times=0&fee_flows=0&fee_price=12&concur_number=3&bind_mac=1&bind_vlan=1&input_max_limit=12&output_max_limit=25&product_status=0&sign=EFB09A8FCAEBD6D928901E7D875613B4 HTTP/1.1

### 参数

| 参数名 | 必选 | 类型 | 说明 |
|---|:---|:---:|---:|
| product_id | Y | int |资费ID |
| product_name | N | string |资费名称 |
| fee_price | N | int |价格(元) |
| concur_number | N | int |并发数 |
| bind_mac | N | int |是否绑定MAC地址 (0：不绑定，1：绑定)|
| bind_vlan | N | int |是否绑定VLAN ID |
| input_max_limit | N | int |上行最大速率(MBPS) |
| output_max_limit | N | int |下行最大速率(MBPS) |
| product_status | N | int |状态(0：正常，1：停用) |

### 返回结果

**返回示例：**

~~~json
{
  "msg": "product update success",
  "nonce": "1458620859",
  "code": 0,
  "sign": "2CF23C9936D94706BEC75798CA617485"
}
  ~~~

**返回结果描述：**

- code：返回结果码
- msg：返回消息
- nonce：随机时间戳
- sign：消息签名
