# ToughRADIUS接口协议文档

## 协议说明

- 协议采用基于http的接口调用方式。
- 消息发起方：第三方系统。
- 消息接受方：TOUGHRADIUS系统。
- 接口请求方法：HTTP GET 或者 POST，支持标准http1.1协议。
- 消息报文编码：UTF-8，注意对参数进行 urlencode 编码
- 接口鉴权：MD5签名，`md5(共享密钥+排序的参数值组合字符串)`,签名校验是双向的，消息接收方对请求消息进行签名验证，同时需对结果进行签名返回，消息发起方对响应结果的签名进行验证。
- 当前接口版本：v1

### 示例 

    GET /api/v1/nas/add?sign=C5219018DC9A71232A88606E48554F50&isp_code=default&bas_name=api%20add&ip_addr=10.10.10.1&dns_name=&time_type=0&vendor_id=0&portal_vendor=huaweiv2&bas_secret=123456&coa_port=3799&ac_port=2000 HTTP/1.1

将所有参数的值进行排序相加得到排序的参数值字符串，为了安全，可以增加一个随机参数值，比如nonce=123131414,保证nonce每次都不同，nonce的值参与签名计算。

除了直接GET提交，也可以通过Form表单提交


### 签名代码参考

- python

    请参考：https://github.com/talkincode/toughlib/blob/master/toughlib/apiutils.py


        `#!/usr/bin/env python`
        `#coding:utf-8`
        import logging
        from hashlib import md5

        `def make_sign(api_secret, params=[]):`
            """
                >>> make_sign("123456",[1,'2',u'中文'])
                '33C9065427EECA3490C5642C99165145'
            """
            _params = [p for p in params if p is not None]
            _params.sort()
            _params.insert(0, api_secret)
            strs = ''.join(_params)
            mds = md5(strs.encode('utf-8')).hexdigest()
            return mds.upper()

        `def check_sign(api_secret, msg):`
            """
                >>>  check_sign("123456",dict(code=1,s='2',msg=u'中文',sign='33C9065427EECA3490C5642C99165145'))
                True
            """
            if "sign" not in msg:
                return False
            sign = msg['sign']
            params = [msg[k].encode('utf-8') for k in msg if k != 'sign']
            local_sign = make_sign(api_secret, params)
            result = (sign == local_sign)
            if not result:
                logging.error("check_sign failure, sign:%s != local_sign:%s" %(sign,local_sign))

            return result


