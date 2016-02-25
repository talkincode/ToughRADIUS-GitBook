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