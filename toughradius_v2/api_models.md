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
|input_max_limit        |INTEGER           |False             |上行速率                  |
|output_max_limit       |INTEGER           |False             |下行速率                  |
|create_time            |VARCHAR(19)       |False             |创建时间                  |
|update_time            |VARCHAR(19)       |False             |更新时间                  |

### 客户信息


|属性                    |类型（长度）       |可否为空           |描述                        |
|-----------------------|:-----------------|:----------------:|--------------------------:|
|customer_id            |INTEGER           |False             |用户id                      |
|node_id                |INTEGER           |False             |区域id                      |
|customer_name          |VARCHAR(64)       |False             |用户登录名               |
|password               |VARCHAR(128)      |False             |用户登录密码            |
|realname               |VARCHAR(64)       |False             |用户真实姓名           |
|idcard                 |VARCHAR(32)       |True              |用户证件号码            |
|sex                    |SMALLINT          |True              |用户性别0/1               |
|age                    |INTEGER           |True              |用户年龄                  |
|email                  |VARCHAR(255)      |True              |用户邮箱                  |
|mobile                 |VARCHAR(16)       |True              |用户手机                  |
|address                |VARCHAR(255)      |True              |用户地址                  |
|customer_desc          |VARCHAR(255)      |True              |用户描述                  |
|create_time            |VARCHAR(19)       |False             |创建时间                  |
|update_time            |VARCHAR(19)       |False             |更新时间                  |


### 客户账号

- 认证账号表，每个会员可以同时拥有多个账号
- account_number 为每个套餐对应的上网账号，每个账号全局唯一
- 用户状态 0:"预定",1:"正常", 2:"停机" , 3:"销户", 4:"到期"
       

|属性                    |类型（长度）       |可否为空           |描述                        |
|-----------------------|:-----------------|:----------------:|--------------------------:|
|account_number         |VARCHAR(32)       |False             |上网账号                  |
|customer_id            |INTEGER           |False             |用户id                      |
|product_id             |INTEGER           |False             |资费id                      |
|password               |VARCHAR(128)      |False             |上网密码                  |
|status                 |INTEGER           |False             |用户状态                  |
|install_address        |VARCHAR(128)      |False             |装机地址                  |
|balance                |INTEGER           |False             |用户余额-分              |
|time_length            |INTEGER           |False             |用户时长-秒              |
|flow_length            |INTEGER           |False             |用户流量-kb               |
|expire_date            |VARCHAR(10)       |False             |过期时间- ####-##-##      |
|user_concur_number     |INTEGER           |False             |用户并发数               |
|bind_mac               |SMALLINT          |False             |是否绑定mac               |
|bind_vlan              |SMALLINT          |False             |是否绑定vlan              |
|mac_addr               |VARCHAR(17)       |True              |mac地址                     |
|vlan_id1               |INTEGER           |True              |内层vlan                    |
|vlan_id2               |INTEGER           |True              |外层vlan                    |
|ip_address             |VARCHAR(15)       |True              |静态IP地址                |
|last_pause             |VARCHAR(19)       |True              |最后停机时间            |
|account_desc           |VARCHAR(255)      |True              |用户描述                  |
|create_time            |VARCHAR(19)       |False             |创建时间                  |
|update_time            |VARCHAR(19)       |False             |更新时间                  |


