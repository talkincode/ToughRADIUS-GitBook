# ToughRADIUS接口协议文档

## 协议说明

- 协议采用基于http的接口调用方式。
- 消息发起方：第三方系统。
- 消息接受方：TOUGHRADIUS系统。
- 接口请求方法：HTTP GET 或者 POST，支持标准http1.1协议。
- 消息报文编码：UTF-8，注意对参数进行 urlencode 编码
- 接口鉴权：MD5签名，`md5(共享密钥+排序的参数值组合字符串)`,签名校验是双向的，消息接收方对请求消息进行签名验证，同时需对结果进行签名返回，消息发起方对响应结果的签名进行验证。

### 示例 

GET /api/nas/add?sign=C5219018DC9A71232A88606E48554F50&isp_code=default&bas_name=api%20add&ip_addr=10.10.10.1&dns_name=&time_type=0&vendor_id=0&portal_vendor=huaweiv2&bas_secret=123456&coa_port=3799&ac_port=2000 HTTP/1.1

将所有参数的值进行排序相加得到排序的参数值字符串，为了安全，可以增加一个随机参数值，比如nonce=123131414,保证nonce每次都不同，nonce的值参与签名计算。

除了直接GET提交，也可以通过Form表单提交

## 数据结构定义

### 资费套餐

- 资费类型 product_policy 0 预付费包月 1 预付费时长 2 买断包月 3 买断时长 4 预付费流量 5 买断流量
- 销售状态 product_status 0 正常 1 停用 资费停用后不允许再订购


|属性                    |类型（长度）       |可否为空           |描述                        |
|-----------------------|:-----------------|:----------------:|--------------------------:|
|id                     |INTEGER           |False             |资费id                      |
|product_name           |VARCHAR(64)       |False             |资费名称                  |
|product_policy         |INTEGER           |False             |资费策略                  |
|product_status         |SMALLINT          |False             |资费状态                  |
|bind_mac               |SMALLINT          |False             |是否绑定mac               |
|bind_vlan              |SMALLINT          |False             |是否绑定vlan              |
|concur_number          |INTEGER           |False             |并发数                     |
|fee_months             |INTEGER           |True              |买断授权月数            |
|fee_times              |INTEGER           |True              |买断时长(秒)             |
|fee_flows              |INTEGER           |True              |买断流量(kb)              |
|fee_price              |INTEGER           |False             |资费价格                  |
|fee_period             |VARCHAR(11)       |True              |计费认证时段            |
|input_max_limit        |INTEGER           |False             |上行速率                  |
|output_max_limit       |INTEGER           |False             |下行速率                  |
|create_time            |VARCHAR(19)       |False             |创建时间                  |
|update_time            |VARCHAR(19)       |False             |更新时间                  |

## 产品套餐查询


### 接口描述

- 查询系统套餐

### 请求URL

- ` http://server:port/api/nas/fetch `
      
### 请求方式

- POST 

### 参数

| 参数名 | 必选 | 类型 | 说明 |
|---|:---|:---:|---:|
| product_id | 否 | string | 用户名 |

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
