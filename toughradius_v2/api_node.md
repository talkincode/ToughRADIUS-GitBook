## 区域节点查询


### 接口描述

- 查询系统区域节点

### 请求URL

- ` http://server:port/api/v1/node/query `
      
### 请求方式

- POST 

示例：

    GET /v1/api/node/query?sign=1BB40565D6C88276085719A5964BE3E0&node_id=1 HTTP/1.1

### 参数

| 参数名 | 必选 | 类型 | 说明 |
|---|:---|:---:|---:|
| node_id | 否 | string |区域ID |

### 返回结果

**返回示例：**

    {
      "code": 0,
      "msg": "success",
      "nodes": [
        {
          "id": 1,
          "node_name": "default",
          "node_desc": "默认区域"
        }
      ],
      "nonce": "1456377457",
      "sign": "91FBD7D83B5F9069E456E3DDCF1CCF9C"
    }

**返回结果描述：**

- code：返回结果码， 0 成功， 1 失败
- msg：返回消息
- nodes：区域节点列表，如果参数node_id不为空，则返回指定区域，若区域不存在，返回空。
- nonce：随机时间戳
- sign：消息签名
