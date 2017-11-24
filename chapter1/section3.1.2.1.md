# 登录请求报文	
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


