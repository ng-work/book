# HiWallet 平台接口规范

---


<table>
    <tr>
        <th>版本号</th>
        <th>修改人</th>
        <th>审批人</th>
        <th>修改日期</th>
        <th>修改记录</th>
    </tr>
    <tr>
        <th>1.1.0</th>
        <th>Ailen</th>
        <th></th>
        <th>2017年7月17日</th>
        <th>创建</th>
    </tr>
    <tr>
        <th>1.2.0</th>
        <th>jack</th>
        <th></th>
        <th>2017年8月23日</th>
        <th>资产校验</th>
    </tr>
    <tr>
        <th>1.2.1</th>
        <th>jack</th>
        <th></th>
        <th>2017年8月25日</th>
        <th>修改校验</th>
    </tr>
    <tr>
        <th>1.2.2</th>
        <th>jack</th>
        <th></th>
        <th>2017年8月28日</th>
        <th>修改校验</th>
    </tr>
</table>

<!-- 
## 1. 引言

### 1.1 编写目的

本文档为各商户通过钱包平台与brewchain区块链交互的接口技术解决方案，作为钱包平台与商户的系统平台的数据接口的标准和规范，指导开发人员进行接口设计、开发和测试。

### 1.2 覆盖范围	
 第三方商户接入。
 


### 1.3 预期读者	
第三方商户开发人员，测试人员。

### 1.4 术语与缩略语	
资产：一切放入到区块链中的数据，统称为资产

### 1.5 参考文档



## 2. 接口方式
###2.1 接口说明	
钱包平台和商户系统平台之间的交互均采用规范报文进行数据传输与接口调用，报文的传输采用http方式实现。钱包平台提供http形式的交互接口，包括账户登录接口、资产创建接口、文件上传接口、资产信息校验接口、资产交易接口以及交易查询接口，参数采用 post 方式提交 Json格式报文。

###2.2 地址格式	
账本接口地址 + 具体接口后缀
例如：http://fbs-www.test.aws.fclink.cn/sys/upload.do
http://fbs-www.test.aws.fclink.cn 为网站中提供的链接口地址；
sys/upload.do 为文件上传接口

##3. 基础接口

###3.1 账户登录	

####3.1.1 接口描述

账本中的参与者账户进行登录接口，用于身份登陆，获取钱包 IP。
####3.1.2 接口定义

#####3.1.2.1 登录请求报文	
<table>
        <tr>
            <td colspan="6">报文格式</td>
        </tr>
        <tr>
            <th>参数名</th>
            <th>参数名称</th>
            <th>类型及长度</th>
            <th>备注</th>
            <th>是否可空</th>
            <th>样例</th>
        </tr>
        <tr>
             <td colspan="6">报文体</td>
        </tr>
        <tr>
            <td>orderNo</td>
            <td>订单号</td>
            <td>String(32)</td>
            <td>每次请求的唯一编号</td>
            <td>N</td>
            <td></td>
        </tr>
        <tr>
            <td>userName</td>
            <td>用户名</td>
            <td>String(64)</td>
            <td></td>
            <td>N</td>
            <td></td>
        </tr>
        <tr>
            <td>passwd</td>
            <td>密码</td>
            <td>String(64)</td>
            <td></td>
            <td>N</td>
            <td></td>
        </tr>
        <tr>
            <td>ledgerId</td>
            <td>账本ID</td>
            <td>String(32)</td>
            <td></td>
            <td>N</td>
            <td></td>
        </tr>
</table>

 例如：
``` javascript
    {
     "userName":"jack1",
     "passwd":"1223",
     "orderNo":"10011",
     "ledgerId":"123"
    }
```

#####3.1.2.2 登录响应报文	
<table>
        <tr>
            <td colspan="6">报文格式</td>
        </tr>
        <tr>
            <th>参数名</th>
            <th>参数名称</th>
            <th>类型及长度</th>
            <th>备注</th>
            <th>是否可空</th>
            <th>样例</th>
        </tr>
        <tr>
             <td colspan="6">报文体</td>
        </tr>
        <tr>
            <td>orderNo</td>
            <td>订单号</td>
            <td>String(32)</td>
            <td>返回与请求时相同的值</td>
            <td>N</td>
            <td></td>
        </tr>
        <tr>
            <td>errorCode</td>
            <td>返回的状态信息</td>
            <td>String(6)</td>
            <td>状态码</td>
            <td>N</td>
            <td></td>
        </tr>
        <tr>
            <td>errorDesc</td>
            <td>返回的信息</td>
            <td>String(256)</td>
            <td>如果error_code为成功标志，则为空，否则为返回描述</td>
            <td>N</td>
            <td></td>
        </tr>
        <tr>
            <td>userId</td>
            <td>用户ID</td>
            <td>String(64)</td>
            <td></td>
            <td>N</td>
            <td></td>
        </tr>
</table>

例如：
``` javascript
{
 "errorCode": "000000",
 "errorDesc": "success",
 "userId": "0001110101001",
 "userKey":"04005f56800c1c8a2961979f033cfa3507f72a44b25ea6efb25a6392485e55c5b3214ce37437418e397d723cedc52cb219524f2383b45010a3e5aab9ea9304c7fc",
 "orderNo": "10006"
} 
```

## 4. 交易接口

### 4.1 创建资产	

#### 4.1.1 接口描述
用于在区块链上创建资产。

#####4.1.2 接口定义

######4.1.2.1 请求报文	
<table>
        <tr>
            <td colspan="6">报文格式</td>
        </tr>
        <tr>
            <th>参数名</th>
            <th>参数名称</th>
            <th>类型及长度</th>
            <th>备注</th>
            <th>是否可空</th>
            <th>样例</th>
        </tr>
        <tr>
             <td colspan="6">报文体</td>
        </tr>
        <tr>
            <td>orderNo</td>
            <td>订单号</td>
            <td>String(32)</td>
            <td>每次请求的唯一编号</td>
            <td>N</td>
            <td></td>
        </tr>
        <tr>
            <td>userKey</td>
            <td>公钥hash</td>
            <td>String(64)</td>
            <td></td>
            <td>N</td>
            <td></td>
        </tr>
        <tr>
            <td>userId</td>
            <td>用户ID</td>
            <td>String(64)</td>
            <td></td>
            <td>N</td>
            <td></td>
        </tr>
        <tr>
            <td>alias</td>
            <td>资产别名</td>
            <td>String(32)</td>
            <td></td>
            <td>N</td>
            <td></td>
        </tr>
        <tr>
            <td>dataTable</td>
            <td>附加数据检索词</td>
            <td>String(50)</td>
            <td>多个用^符分隔</td>
            <td>N</td>
            <td></td>
        </tr>
         <tr>
            <td>filePath</td>
            <td>文件存放路径</td>
            <td>String(160)</td>
            <td>文件id，用^符分隔</td>
            <td>N</td>
            <td></td>
        </tr>
         <tr>
            <td>metadata</td>
            <td>附加数据</td>
            <td>String(1548)</td>
            <td></td>
            <td>N</td>
            <td></td>
        </tr>
         <tr>
            <td>lastHash</td>
            <td>上次资产hash</td>
            <td>String(160)</td>
            <td></td>
            <td>N</td>
            <td></td>
        </tr>
         <tr>
            <td>type</td>
            <td>资产类型</td>
            <td>String(2)</td>
            <td>资产类型（0:TOKEN,1:FBC,2:BTC,3:LTC）</td>
            <td>N</td>
            <td>默认0</td>
        </tr>
</table>

 例如：
``` javascript
 {
    "orderNo":"10013",
    "userKey":"11",
    "userId":"0001110101001",
    "alias":"def",
    "dataTable":"123",
    "filePath":"11",
    "type":"1",
    "lashHash":"3838238293j30238rj23rjsdljf23wkdfi9w3",
    "metadata":"1"
    }
    
```

###### 4.1.2.2 响应报文

<table>
        <tr>
            <td colspan="6">报文格式</td>
        </tr>
        <tr>
            <th>参数名</th>
            <th>参数名称</th>
            <th>类型及长度</th>
            <th>备注</th>
            <th>是否可空</th>
            <th>样例</th>
        </tr>
        <tr>
             <td colspan="6">报文体</td>
        </tr>
        <tr>
            <td>orderNo</td>
            <td>订单号</td>
            <td>String(32)</td>
            <td>返回与请求时相同的值</td>
            <td>N</td>
            <td></td>
        </tr>
        <tr>
            <td>errorCode</td>
            <td>返回的状态信息</td>
            <td>String(6)</td>
            <td>状态码,000000为成功</td>
            <td>N</td>
            <td></td>
        </tr>
        <tr>
            <td>errorDesc</td>
            <td>返回的信息</td>
            <td>String(256)</td>
            <td>成功，则为空，否则为返回描述</td>
            <td>N</td>
            <td></td>
        </tr>
        <tr>
            <td>assedId</td>
            <td>资产ID</td>
            <td>String max(64)</td>
            <td>成功，返回资产ID</td>
            <td>N</td>
            <td></td>
        </tr>
</table>


例如：

``` javascript
{
 "orderNo": "10013",
 "errorCode": "000000",
 "errorDesc": "success",
 "assetId": "ff808081000065c5015d7cf740460004"
}
```
#### 4.2 文件上传

##### 4.2.1 接口描述
用户接口，用于用户上传数据。文件上传是通过 form 表单的形式进行上传的。需
要在 URL 后面跟上下面这些参数。

##### 4.2.2 接口定义

###### 4.2.2.1请求报文

<table>
        <tr>
            <td colspan="6">报文格式</td>
        </tr>
        <tr>
            <th>参数名</th>
            <th>参数名称</th>
            <th>类型及长度</th>
            <th>备注</th>
            <th>是否可空</th>
            <th>样例</th>
        </tr>
        <tr>
             <td colspan="6">报文体</td>
        </tr>
        <tr>
            <td>orderNo</td>
            <td>订单号</td>
            <td>String(32)</td>
            <td></td>
            <td>N</td>
            <td></td>
        </tr>
        <tr>
            <td>userId</td>
            <td>用户ID</td>
            <td>String(64)</td>
            <td></td>
            <td>N</td>
            <td></td>
        </tr>
        <tr>
            <td>userKey</td>
            <td>用户公钥</td>
            <td>String(128)</td>
            <td></td>
            <td>N</td>
            <td></td>
        </tr>
</table>

例如：
``` javascript
orderNo=10039&userId=0001110101001&userKey=123 
```

###### 4.2.2.2 响应报文
<table>
        <tr>
            <td colspan="6">报文格式</td>
        </tr>
        <tr>
            <th>参数名</th>
            <th>参数名称</th>
            <th>类型及长度</th>
            <th>备注</th>
            <th>是否可空</th>
            <th>样例</th>
        </tr>
        <tr>
             <td colspan="6">报文体</td>
        </tr>
        <tr>
            <td>orderNo</td>
            <td>订单号</td>
            <td>String(32)</td>
            <td></td>
            <td>N</td>
            <td></td>
        </tr>
        <tr>
            <td>errorCode</td>
            <td>返回状态码</td>
            <td>String(6)</td>
            <td></td>
            <td>N</td>
            <td></td>
        </tr>
        <tr>
            <td>errorDesc</td>
            <td>返回状态信息</td>
            <td>String(256)</td>
            <td></td>
            <td>N</td>
            <td></td>
        </tr>
        <tr>
            <td>fileId</td>
            <td>文件ID</td>
            <td>String(32)</td>
            <td></td>
            <td>Y</td>
            <td></td>
        </tr>
</table>

例如：

``` javascript
{
 "fileId": "[ff80808100006f43015d7d8e0f500004]",
 "orderNo": "10039",
 "errorDesc": "success",
 "errorCode": "000000"
}
```

#### 4.3 文件下载

##### 4.3.1 接口描述
用户接口，用于用户下载数据。需要在 URL 后面跟上下面这些参数。

##### 4.3.2 接口定义

######4.3.2.1 请求报文	
<table>
        <tr>
            <td colspan="6">报文格式</td>
        </tr>
        <tr>
            <th>参数名</th>
            <th>参数名称</th>
            <th>类型及长度</th>
            <th>备注</th>
            <th>是否可空</th>
            <th>样例</th>
        </tr>
        <tr>
             <td colspan="6">报文体</td>
        </tr>
        <tr>
            <td>orderNo</td>
            <td>订单号</td>
            <td>String(32)</td>
            <td></td>
            <td>N</td>
            <td></td>
        </tr>
        <tr>
            <td>userId</td>
            <td>用户ID</td>
            <td>String(64)</td>
            <td></td>
            <td>N</td>
            <td></td>
        </tr>
        <tr>
            <td>fileId</td>
            <td>文件主键</td>
            <td>String(128)</td>
            <td></td>
            <td>N</td>
            <td></td>
        </tr>
</table>

例如：
``` javascript
fileId=ff8080810000705d015d7da921260001&orderNo=10057&userId=0001110101001 
```

###### 4.3.2.2 响应报文
<table>
        <tr>
            <td colspan="6">报文格式</td>
        </tr>
        <tr>
            <th>参数名</th>
            <th>参数名称</th>
            <th>类型及长度</th>
            <th>备注</th>
            <th>是否可空</th>
            <th>样例</th>
        </tr>
        <tr>
             <td colspan="6">报文体</td>
        </tr>
        <tr>
            <td>ErrorCode</td>
            <td>返回状态码</td>
            <td>String(6)</td>
            <td></td>
            <td>N</td>
            <td></td>
        </tr>
        <tr>
            <td>ErrorDesc</td>
            <td>返回状态信息</td>
            <td>String(256)</td>
            <td></td>
            <td>N</td>
            <td></td>
        </tr>
</table>

例如：

``` javascript
{
 "errorDesc": "000111010100133：用户不存在",
 "errorCode": "000001"
}
```

### 5.查询接口

#### 5.1 资产查询

##### 5.1.1 接口描述

##### 5.1.2 接口定义

###### 5.1.2.1 请求报文
<table>
        <tr>
            <td colspan="6">报文格式</td>
        </tr>
        <tr>
            <th>参数名</th>
            <th>参数名称</th>
            <th>类型及长度</th>
            <th>备注</th>
            <th>是否可空</th>
            <th>样例</th>
        </tr>
        <tr>
             <td colspan="6">报文体</td>
        </tr>
        <tr>
            <td>orderNo</td>
            <td>订单号</td>
            <td>String(32)</td>
            <td></td>
            <td>N</td>
            <td></td>
        </tr>
        <tr>
            <td>userId</td>
            <td>用户ID</td>
            <td>String(64)</td>
            <td></td>
            <td>N</td>
            <td></td>
        </tr>
        <tr>
            <td>userKey</td>
            <td>用户公钥</td>
            <td>String(128)</td>
            <td>登录时获得的公钥</td>
            <td>N</td>
            <td></td>
        </tr>
        <tr>
            <td>dataTable</td>
            <td>附加数据检索词</td>
            <td>String(50)</td>
            <td>以^分割</td>
            <td>Y</td>
            <td></td>
        </tr>
        <tr>
            <td>pageNo</td>
            <td>页码</td>
            <td>Int</td>
            <td></td>
            <td>Y</td>
            <td></td>
        </tr>
        <tr>
            <td>pageSize</td>
            <td>页容量</td>
            <td>Int</td>
            <td></td>
            <td>Y</td>
            <td></td>
        </tr>
</table>

例如：
``` javascript
{
"orderNo": "2000001",
 "userId": "xxxxxxxxxx",
 "userKey": "xxxxxxxxx",
 "dataTable": "金融^票据",
 "pageNo": 1,
 "pageSize": 20
} 
```


###### 5.1.2.2 响应报文
<table>
        <tr>
            <td colspan="6">报文格式</td>
        </tr>
        <tr>
            <th>参数名</th>
            <th>参数名称</th>
            <th>类型及长度</th>
            <th>备注</th>
            <th>是否可空</th>
            <th>样例</th>
        </tr>
        <tr>
             <td colspan="6">报文体</td>
        </tr>
        <tr>
            <td>orderNo</td>
            <td>订单号</td>
            <td>String(32)</td>
            <td></td>
            <td>N</td>
            <td></td>
        </tr>
        <tr>
            <td>ErrorCode</td>
            <td>返回状态码</td>
            <td>String(6)</td>
            <td></td>
            <td>N</td>
            <td></td>
        </tr>
        <tr>
            <td>ErrorDesc</td>
            <td>返回状态信息</td>
            <td>String(256)</td>
            <td></td>
            <td>N</td>
            <td></td>
        </tr>
        <tr>
            <td>assetcount</td>
            <td>资产总数量</td>
            <td>Int</td>
            <td></td>
            <td>N</td>
            <td></td>
        </tr>
        <tr>
            <td>pageNo</td>
            <td>页码</td>
            <td>Int</td>
            <td></td>
            <td>N</td>
            <td></td>
        </tr>
        <tr>
            <td>assets</td>
            <td>资产列表</td>
            <td>List<Asset></td>
            <td></td>
            <td>Y</td>
            <td></td>
        </tr>
</table>

例如：
``` javascript
{
 "orderNo": "10021",
 "errorCode": "000000",
 "errorDesc": "success",
 "assetCount": 3,
 "pageNo": 0,
 "assets": [
     {
         "assetId": "ff80808100006de4015d7d2b3a470001",
         "type": "1",
         "alias": "def",
         "dataTable": "123",
         "metadata": "1",
         "amount": 0,
         "count": 0,
         "status": "1",
         "createTime": "2017-07-26 12:32:52",
         "updateTime": "2017-07-26 12:32:52"
     },
     {
         "assetId": "ff808081000065c5015d7cf740460004",
         "type": "1",
         "alias": "def",
         "dataTable": "123",
         "metadata": "1",
         "filePath": "11",
         "amount": 0,
         "count": 0,
         "status": "1",
         "createTime": "2017-07-26 11:36:05",
         "updateTime": "2017-07-26 11:36:05"
     },
     {
         "assetId": "ff80808100006128015d7cb9ed1a0002",
         "type": "0",
         "alias": "default",
         "amount": 0,
         "count": 0,
         "status": "1",
         "createTime": "2017-07-26 10:29:06",
         "updateTime": "2017-07-26 10:29:06"
     }
 ]
}
```

#### 5.2 资产回溯

##### 5.2.1 接口描述

##### 5.2.2 接口定义

###### 5.2.2.1 请求报文
<table>
        <tr>
            <td colspan="6">报文格式</td>
        </tr>
        <tr>
            <th>参数名</th>
            <th>参数名称</th>
            <th>类型及长度</th>
            <th>备注</th>
            <th>是否可空</th>
            <th>样例</th>
        </tr>
        <tr>
             <td colspan="6">报文体</td>
        </tr>
        <tr>
            <td>orderNo</td>
            <td>订单号</td>
            <td>String(32)</td>
            <td></td>
            <td>N</td>
            <td></td>
        </tr>
        <tr>
            <td>userId</td>
            <td>用户ID</td>
            <td>String(64)</td>
            <td></td>
            <td>N</td>
            <td></td>
        </tr>
        <tr>
            <td>userKey</td>
            <td>用户公钥</td>
            <td>String(128)</td>
            <td>登录时获得的公钥</td>
            <td>N</td>
            <td></td>
        </tr>
        <tr>
            <td>assetId</td>
            <td>资产ID</td>
            <td>String(64)</td>
            <td></td>
            <td>N</td>
            <td></td>
        </tr>
        <tr>
            <td>level</td>
            <td>回溯层数</td>
            <td>Int</td>
            <td>回溯层数，最大为5</td>
            <td>N</td>
            <td></td>
        </tr>
</table>

例如：
``` javascript
    {
        "orderNo":"10025",
        "userKey":"11",
        "userId":"0001110101001",
        "assetId":"ff80808100006de4015d7d2b3a470001",
        "level":"1"
    }
 
```

###### 5.2.2.2 响应报文
<table>
        <tr>
            <td colspan="6">报文格式</td>
        </tr>
        <tr>
            <th>参数名</th>
            <th>参数名称</th>
            <th>类型及长度</th>
            <th>备注</th>
            <th>是否可空</th>
            <th>样例</th>
        </tr>
        <tr>
             <td colspan="6">报文体</td>
        </tr>
        <tr>
            <td>orderNo</td>
            <td>订单号</td>
            <td>String(32)</td>
            <td></td>
            <td>N</td>
            <td></td>
        </tr>
         <tr>
            <td>ErrorCode</td>
            <td>返回状态码</td>
            <td>String(6)</td>
            <td></td>
            <td>N</td>
            <td></td>
        </tr>
        <tr>
            <td>ErrorDesc</td>
            <td>返回状态信息</td>
            <td>String(256)</td>
            <td></td>
            <td>N</td>
            <td></td>
        </tr>
        <tr>
            <td>transactions</td>
            <td>交易</td>
            <td>List < Transaction></td>
            <td></td>
            <td>N</td>
            <td></td>
        </tr>
</table>

例如：
``` javascript
{
     "orderNo": "10025",
     "errorCode": "000000",
     "errorDesc": "success",
     "assets": [
         {
             "assetId": "ff80808100006de4015d7d2b3a470001",
             "type": "1",
             "alias": "def",
             "dataTable": "123",
             "metadata": "1",
             "amount": 0,
             "count": 0,
             "status": "1",
             "createTime": "2017-07-26 12:32:52",
             "updateTime": "2017-07-26 12:32:52"
         }
    ]
}
```
#### 5.4 账本共享存储信息查询

##### 5.3.1 接口描述
用户接口，查询用户占用共享存储信息

##### 5.3.2 接口定义

######5.3.2.1 请求报文
<table>
        <tr>
            <td colspan="6">报文格式</td>
        </tr>
        <tr>
            <th>参数名</th>
            <th>参数名称</th>
            <th>类型及长度</th>
            <th>备注</th>
            <th>是否可空</th>
            <th>样例</th>
        </tr>
        <tr>
             <td colspan="6">报文体</td>
        </tr>
        <tr>
            <td>orderNo</td>
            <td>订单号</td>
            <td>String(32)</td>
            <td></td>
            <td>N</td>
            <td></td>
        </tr>
        <tr>
            <td>userId</td>
            <td>用户ID</td>
            <td>String(64)</td>
            <td></td>
            <td>N</td>
            <td></td>
        </tr>
        <tr>
            <td>userKey</td>
            <td>用户公钥</td>
            <td>String(128)</td>
            <td></td>
            <td>N</td>
            <td></td>
        </tr>
</table>

例如：
``` javascript
    {
        "orderNo":"10055",
        "userKey":"11",
        "userId":"0001110101001"
    }
 
```
###### 5.3.2.2 响应报文
<table>
        <tr>
            <td colspan="6">报文格式</td>
        </tr>
        <tr>
            <th>参数名</th>
            <th>参数名称</th>
            <th>类型及长度</th>
            <th>备注</th>
            <th>是否可空</th>
            <th>样例</th>
        </tr>
        <tr>
             <td colspan="6">报文体</td>
        </tr>
        <tr>
            <td>orderNo</td>
            <td>订单号</td>
            <td>String(32)</td>
            <td></td>
            <td>N</td>
            <td></td>
        </tr>
        <tr>
            <td>errorCode</td>
            <td>返回状态码</td>
            <td>String(6)</td>
            <td></td>
            <td>N</td>
            <td></td>
        </tr>
        <tr>
            <td>errorDesc</td>
            <td>返回状态信息</td>
            <td>String(256)</td>
            <td></td>
            <td>N</td>
            <td></td>
        </tr>
        <tr>
            <td>size</td>
            <td>占用空间大小</td>
            <td>Decimal(10,3)</td>
            <td>M为单位</td>
            <td>N</td>
            <td></td>
        </tr>
</table>

例如：
``` javascript
    {
         "orderNo": "10055",
         "errorCode": "000000",
         "errorDesc": "success",
         "size": 0.117474
    }
```
### 6. 资产校验
#### 6.1 接口描述
#### 6.2 接口定义
##### 6.2.1 请求报文
<table>
        <tr>
            <td colspan="6">报文格式</td>
        </tr>
        <tr>
            <th>参数名</th>
            <th>参数名称</th>
            <th>类型及长度</th>
            <th>备注</th>
            <th>是否可空</th>
            <th>样例</th>
        </tr>
        <tr>
             <td colspan="6">报文体</td>
        </tr>
        <tr>
            <td>orderNo</td>
            <td>订单号</td>
            <td>String(32)</td>
            <td></td>
            <td>N</td>
            <td></td>
        </tr>
        <tr>
            <td>assets</td>
            <td>待校验资产</td>
            <td>Asset</td>
            <td></td>
            <td>N</td>
            <td></td>
        </tr>
        <tr>
            <td>userId</td>
            <td>用户ID</td>
            <td>String(32)</td>
            <td></td>
            <td>N</td>
            <td></td>
        </tr>
</table>

例如：
```js
{
"orderNo":"000202020202036",
"asset":
 {
 "assetId": "2c91808a00000010015e1882f6b9000c",
 "type": "0",
 "alias": "default",
 "amount": 0,
 "count": 0,
 "status": "1",
 "createTime": "2017-08-26 11:09:23",
 "updateTime": "2017-08-26 11:09:23"
 },
"userId":"842674455"
}
```

##### 6.2.2相应报文

<table>
        <tr>
            <td colspan="6">报文格式</td>
        </tr>
        <tr>
            <th>参数名</th>
            <th>参数名称</th>
            <th>类型及长度</th>
            <th>备注</th>
            <th>是否可空</th>
            <th>样例</th>
        </tr>
        <tr>
             <td colspan="6">报文体</td>
        </tr>
        <tr>
            <td>orderNo</td>
            <td>订单号</td>
            <td>String(32)</td>
            <td></td>
            <td>N</td>
            <td></td>
        </tr>
        <tr>
            <td>errorCode</td>
            <td>返回状态码</td>
            <td>String(32)</td>
            <td></td>
            <td>N</td>
            <td></td>
        </tr>
       <tr>
            <td>errorDesc</td>
            <td>返回状态信息</td>
            <td>String(256)</td>
            <td></td>
            <td>N</td>
            <td></td>
        </tr>
</table>

列如：
```js
{
 "orderNo": "10039",
 "errorDesc": "success",
 "errorCode": "000000"
}
```

### 附录
#### 1.1 接口类型
<table>
        <tr>
            <th>序号</th>
            <th>状态名称</th>
            <th>状态值</th>
        </tr>
        <tr>
            <td>1</td>
            <td>基础类接口</td>
            <td>01</td>
        </tr>
        <tr>
            <td>2</td>
            <td>交易类接口</td>
            <td>02</td>
        </tr>
       <tr>
            <td>3</td>
            <td>查询类接口</td>
            <td>03</td>
        </tr>
        <tr>
            <td>4</td>
            <td>校验类接口</td>
            <td>04</td>
        </tr>
</table>


#### 1.2 接口名称
<table>
        <tr>
            <th>接口名称</th>
            <th>模块名称</th>
            <th>接口编码</th>
            <th>接口类型</th>
        </tr>
        <tr>
            <td>用户登录</td>
            <td>user</td>
            <td>002</td>
            <td>01</td>
        </tr>
        <tr>
            <td>创建资产</td>
            <td>ast</td>
            <td>005</td>
            <td>02</td>
        </tr>
       <tr>
            <td>文件上传</td>
            <td>sys</td>
            <td>006</td>
            <td>02</td>
        </tr>
        <tr>
            <td>文件下载</td>
            <td>sys</td>
            <td>007</td>
            <td>02</td>
        </tr>
        <tr>
            <td>资产查询</td>
            <td>ast</td>
            <td>008</td>
            <td>03</td>
        </tr>
        <tr>
            <td>资产回溯</td>
            <td>ast</td>
            <td>009</td>
            <td>03</td>
        </tr>
        <tr>
            <td>账本共享储存信息</td>
            <td>sto</td>
            <td>010</td>
            <td>03</td>
        </tr>
        <tr>
            <td>资产校验</td>
            <td>ast</td>
            <td>011</td>
            <td>04</td>
        </tr>
</table>

#### 1.3接口地址
<table>
    <tr>
        <th>接口名称</th>
        <th>接口地址</th>
    </tr>
    <tr>
        <td>用户登录</td>
        <td>/usr/pblin.do?fh=LINUSR0000000J00&resp=bd&bd</td>
    </tr> 
    <tr>
        <td>创建资产</td>
        <td>/ast/pbcrt.do?fh=CRTAST0000000J00&resp=bd&bd</td>
    </tr> 
    <tr>
        <td>文件上传</td>
        <td>/sys/upload.do</td>
    </tr> 
    <tr>
        <td>文件下载</td>
        <td>/sys/download.do</td>
    </tr> 
    <tr>
        <td>资产查询</td>
        <td> /ast/pbqry.do?fh=QRYAST0000000J00&resp=bd&bd</td>
    </tr> 
    <tr>
        <td>资产回溯</td>
        <td>/ast/pbtra.do?fh=TRAAST0000000J00&resp=bd</td>
    </tr> 
    <tr>
        <td>账本共享存储信息</td>
        <td>/sto/pbsiz.do?fh=SIZSTO0000000J00&resp=bd</td>
    </tr> 
    <tr>
        <td>资产校验</td>
        <td>/ast/pbvry.do?fh=VRYAST0000000J00&resp=bd</td>
    </tr> 
</table>

#### 1.4 ASSET
<table>
 <tr>
            <th>名称</th>
            <th>说明</th>
            <th>类型及长度</th>
            <th>备注</th>
        </tr>
        <tr>
            <td>assetId</td>
            <td>资产 ID</td>
            <td>String(64)</td>
            <td></td>
        </tr>
        <tr>
            <td>type</td>
            <td>资产类型</td>
            <td>String(8)</td>
            <td>FBC | BTC | LTC | TOKEN</td>
        </tr>
       <tr>
            <td>alias</td>
            <td>别名</td>
            <td>String(32)</td>
            <td></td>
        </tr>
        <tr>
            <td>dataTable</td>
            <td>查询关键字</td>
            <td>String(50)</td>
            <td></td>
        </tr>
        <tr>
            <td>metadata</td>
            <td>附属信息</td>
            <td>String(1548)</td>
            <td></td>
        </tr>
        <tr>
            <td>filePath</td>
            <td>附件id</td>
            <td>String(1548)</td>
            <td>用^分隔</td>
        </tr>
        <tr>
            <td>amount</td>
            <td>金额</td>
            <td>Decimal(10,4)</td>
            <td></td>
        </tr>
         <tr>
            <td>count</td>
            <td>数量</td>
            <td>Decimal(10,0)</td>
            <td></td>
        </tr>
        <tr>
            <td>status</td>
            <td>状态</td>
            <td>int</td>
            <td>0=无效，1:创建，2:入链，3:有效</td>
        </tr>
        <tr>
            <td>createTime</td>
            <td>创建时间</td>
            <td>dateTime</td>
            <td></td>
        </tr>
        <tr>
            <td>update</td>
            <td>更新时间</td>
            <td>dateTime</td>
            <td></td>
        </tr>

</table> -->

