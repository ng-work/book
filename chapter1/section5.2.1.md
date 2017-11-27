# 接口描述



# 请求报文
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

# 响应报文

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