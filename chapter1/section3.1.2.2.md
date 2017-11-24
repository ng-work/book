# 登陆响应报文
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
