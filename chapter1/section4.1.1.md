# 接口描述

用于在区块链上创建资产。

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

