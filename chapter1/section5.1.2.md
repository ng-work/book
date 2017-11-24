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



