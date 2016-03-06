## NAS 接入设备新增

### 接口描述

- 增加NAS接入设备。

### 请求URL

- ` http://server:port/api/v1/nas/add `
      
### 请求方式

- GET 或者 POST

示例：

    GET /api/v1/nas/add?ip_addr=192.168.31.153&bas_name=test%20bas&dns_name=&bas_secret=123456&vendor_id=0&coa_port=3799&sign=6441D2C41A0E3161F926344DCE48DC54 HTTP/1.1

### 参数

支持的设备类型
~~~json
{
    '0': '标准',
    '3041': '阿尔卡特',
    '2352': '爱立信',
    '2011': '华为',
    '25506': 'H3C',
    '3902': '中兴',
    '10055': '爱快',
    '14988': 'RouterOS'
}
~~~

| 参数名 | 必选 | 类型 | 说明 |
|---|:---|:---:|---|
| ip_addr | 否 | string |接入设备地址 |
| dns_name | 否 | string |DNS域名 |
| bas_name | 是 | string |接入设备名称 |
| bas_secret | 是 | string |共享秘钥 |
| vendor_id | 是 | int |接入设备类型|
| coa_port | 是 | int |授权端口 默认3799|


### 返回结果

**返回示例：**

~~~json
{
  "code": 0,
  "msg": "success",
  "nonce": "1456970950",
  "sign": "1E5AD43D7794267B1C08939B7A0871BC"
}
~~~

**返回结果描述：**

- code：返回结果码
- msg：返回消息
- nonce：随机时间戳
- sign：消息签名