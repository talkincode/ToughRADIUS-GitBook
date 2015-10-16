
# mschapv2在Radius中的认证实现

在Radius的认证请求AccessRequest包中如果包含 MS-CHAP2-Response 和 MS-CHAP-Challenge 属性则意味着需要实现ms-chap-v2认证。


## 客户端 MS-CHAP2-Response 和 MS-CHAP-Challenge  生成的规则

### MS-CHAP-Challenge 

MS-CHAP-Challenge  (即AuthChallenge) 是客户端生成的随机16字节。

### MS-CHAP2-Response 

随机生成16字节属性 PeerChallenge，连同AuthChallenge，UserName，Password作为输入参数，调用方法 GenerateNTResponse 得到 NtResponse.

	GenerateNTResponse(AuthChallenge, PeerChallenge, UserName, Password) 

GenerateNTResponse 方法的实现参考 [http://tools.ietf.org/html/rfc2759.html#section-8.1][1]

封装50字节的 MS-CHAP2-Response 属性：

	[0 : 2]           Flags  \x00\x00
	[2 : 18]          PeerChallenge 
	[18 : 26]         Reserved \x00\x00\x00\x00\x00\x00\x00\x00
	[26 : 50]         NtResponse


## 服务端认证规则

校验 MS-CHAP2-Response 长度，长度不等于50应该丢弃，并发送拒绝认证。

从 MS-CHAP2-Response 提取 PeerChallenge，NtResponse

	NtResponse = MS-CHAP2-Response[26 : 50]
	PeerChallenge = MS-CHAP2-Response[2 : 18]

调用 GenerateNTResponse 方法得到 MyNtResponse

	GenerateNTResponse(AuthChallenge, PeerChallenge, UserName, Password)  

比较 MyNtResponse 与 NtResponse，不相等则验证失败。

## Radius 认证响应

调用 GenerateAuthenticatorResponse 方法得到 AuthenticatorResponse

	GenerateAuthenticatorResponse(
		Password,
		NtResponse,
		PeerChallenge, 
		AuthChallenge
		UserName
	) 

GenerateAuthenticatorResponse 方法的实现参考 [http://tools.ietf.org/html/rfc2759.html#section-8.7][2]

设置Radius响应消息属性  MS-CHAP2-Success  =  AuthenticatorResponse



[1]:	http://tools.ietf.org/html/rfc2759.html#section-8.1
[2]:	http://tools.ietf.org/html/rfc2759.html#section-8.7