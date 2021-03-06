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
            <td></td>
            <td>N</td>
            <td></td>
        </tr>
</table>

例如：
``` javascript
orderNo=10039&userId=0001110101001&userKey=123 
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
