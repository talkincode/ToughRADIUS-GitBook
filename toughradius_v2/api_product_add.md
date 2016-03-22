## 资费套餐增加


### 接口描述

- 增加资费套餐

### 请求URL

- ` http://server:port/api/v1/product/add `

### 请求方式

- GET 或者 POST

示例：


    GET /api/v1/product/add?product_name=%E6%B5%8B%E8%AF%95product5&product_policy=2&fee_months=12&fee_times=0&fee_flows=0&fee_price=12&concur_number=3&bind_mac=1&bind_vlan=1&input_max_limit=12&output_max_limit=25&product_status=0&sign=EFB09A8FCAEBD6D928901E7D875613B4 HTTP/1.1

### 参数

| 参数名 | 必选 | 类型 | 说明 |
|---|:---|:---:|---:|
| product_name | Y | string |资费名称 |
| product_policy | Y | int |资费策略 |
| fee_times | Y | int |时长(小时) |
| fee_flows | Y | int |流量(MB) |
| fee_price | Y | int |价格(元) |
| concur_number | Y | int |并发数 |
| bind_mac | Y | int |是否绑定MAC地址 (0：不绑定，1：绑定)|
| bind_vlan | Y | int |是否绑定VLAN ID |
| input_max_limit | Y | int |上行最大速率(MBPS) |
| output_max_limit | Y | int |下行最大速率(MBPS) |
| product_status | Y | int |状态(0：正常，1：停用) |

### 返回结果

**返回示例：**

~~~json
{
  "msg": "资费添加成功",
  "nonce": "1458620128",
  "code": 0,
  "sign": "183D9EBA72C6882EA15E842B5E6BFBAF"
}
  ~~~

**返回结果描述：**

- code：返回结果码
- msg：返回消息
- nonce：随机时间戳
- sign：消息签名
