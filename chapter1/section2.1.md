
## 接口说明	
钱包平台和商户系统平台之间的交互均采用规范报文进行数据传输与接口调用，报文的传输采用http方式实现。钱包平台提供http形式的交互接口，包括账户登录接口、资产创建接口、文件上传接口、资产信息校验接口、资产交易接口以及交易查询接口，参数采用 post 方式提交 Json格式报文。

## 接口地址

地址格式：账本接口地址 + 具体接口后缀  
例如：http://fbs-www.test.aws.fclink.cn/sys/upload.do  
http://fbs-www.test.aws.fclink.cn 为网站中提供的链接口地址；  
sys/upload.do 为文件上传接口
