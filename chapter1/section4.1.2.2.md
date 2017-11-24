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
