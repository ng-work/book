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


