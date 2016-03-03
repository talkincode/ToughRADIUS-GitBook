## 资费套餐查询


### 接口描述

- 查询资费套餐

### 请求URL

- ` http://server:port/api/v1/product/query `
      
### 请求方式

- GET 或者 POST  

示例：

    GET /api/v1/product/query?sign=1BB40565D6C88276085719A5964BE3E0&product_id=1 HTTP/1.1


### 参数

| 参数名 | 必选 | 类型 | 说明 |
|---|:---|:---:|---:|
| product_id | 否 | string |资费ID |

### 返回结果

**返回示例：**



    {
      "code": 0,
      "msg": "success",
      "products": [
         {
           "id": 1,
           "product_name": "测试2M包月20元",
           "product_policy": 0,
           "product_status": 0,
           "bind_mac": 0,
           "bind_vlan": 0,
           "concur_number": 0,
           "fee_months": 0,
           "fee_times": 0,
           "fee_flows": 0,
           "fee_price": 2000,
           "input_max_limit": 1048576,
           "output_max_limit": 2097152,
           "create_time": "2016-02-20 17:59:09",
           "update_time": "2016-02-20 17:59:09"
         }
      ],
      "nonce": "1456369956",
      "sign": "AD1E70D8CEB98D4F6DDE193E7860F587"
    }

**返回结果描述：**

- code：返回结果码， 0 成功， 1 失败
- msg：返回消息
- products：产品套餐列表，如果参数product_id不为空，则返回指定套餐，若套餐不存在，返回空。
- nonce：随机时间戳
- sign：消息签名