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



