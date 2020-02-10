## 机构api签名
### 获取你的 api_key 和 密钥

// 测试网地址

<a href="https://testnet.bybit.com/user/api-management">https://testnet.bybit.com/user/api-management</a>

// 主网地址

<a href="https://www.bybit.com/app/user/api-management">https://www.bybit.com/app/user/api-management</a>

### <span id="rest-rate-limit">频率限制</span>

#### 接口访问类限制
> 频率限制精确到毫秒
##### 如何查看你的频率限制
每个接口，都会返回如下字段：
```
"rate_limit_status":119,
"rate_limit_reset_ms":1572114055663,
"rate_limit":120
```
* rate_limit 你当前的频率限制；
* rate_limit_status 剩余请求次数；
* rate_limit_reset_ms 重置你请求限制的时间戳，如果未超过频率限制返回当前时间戳，单位是毫秒。

##### 接口频率限制详细

   <escape>
    <table>
      <tr>
        <th>频率限制</th>
        <th>path</th>
        <th>消耗</th>
      </tr>
      <tr>
        <td rowspan="10">100/min</td>
        <td>open-api/order/create </td>
        <td>1 / request</td>
      </tr>
      <tr><td>open-api/order/cancel       </td> <td>1 / request</td></tr>
      <tr><td>open-api/stop-order/create  </td> <td>1 / request</td></tr>
      <tr><td>open-api/stop-order/cancel  </td> <td>1 / request</td></tr>
      <tr><td>open-api/order/replace      </td> <td>1 / request</td></tr>
      <tr><td>open-api/stop-order/replace </td> <td>1 / request</td></tr>
      <tr><td>v2/private/order/create     </td> <td>1 / request</td></tr>
      <tr><td>v2/private/order/cancel     </td> <td>1 / request</td></tr>
      <tr><td>v2/private/order/cancelAll  </td> <td>10 / request</td></tr>
      <tr><td>v2/private/stop-order/cancelAll </td> <td>10 / request</td></tr>
      <tr>
        <td rowspan="3">600/min</td>
        <td>open-api/order/list </td>
         <td>1 / request</td>
      </tr>
      <tr>
        <td>open-api/stop-order/list </td> 
        <td>1 / request</td>
      </tr>
      <tr>
        <td>v2/private/order </td> 
        <td>1 / request</td>
      </tr>
      <tr>
        <td>120/min</td>
        <td>v2/private/execution/list</td>
         <td>1 / request</td>
      </tr>
      <tr>
        <td rowspan="3">75/min</td>
        <td>user/leverage/save  </td>
         <td>1 / request</td>
      </tr>
      <tr>
        <td>position/change-position-margin </td> 
        <td>1 / request</td>
      </tr>
      <tr>
        <td>position/trading-stop</td> 
        <td>1 / request</td>
      </tr>
      <tr>
        <td rowspan="2">120/min</td>
        <td>position/list</td>
         <td>1 / request</td>
      </tr>
      <tr>
        <td>user/leverage</td> 
        <td>1 / request</td>
      </tr>
      <tr>
        <td rowspan="3">120/min</td>
        <td>open-api/funding/prev-funding-rate</td>
        <td>1 / request</td>
      </tr>
      <tr>
        <td>open-api/funding/prev-funding</td>
        <td>1 / request</td>
      </tr>
      <tr>
        <td>open-api/funding/predicted-funding</td>
        <td>1 / request</td>
      </tr>
      <tr>
        <td rowspan="2">120/min</td>
        <td>open-api/wallet/fund/records</td>
        <td>1 / request</td>
      </tr>
    <tr>
      <td>open-api/wallet/withdraw/list</td>
      <td>1 / request</td>
    </tr>
    <tr>
        <td rowspan="1">600/min</td>
        <td>open-api/api-key</td>
        <td>1 / request</td>
      </tr>
    </table>
  </escape>


#### 业务类限制
  * 未完全成交的活动委托单最多可同时有200个
  * 条件单同一方向最多可同时有5个
  
#### IP频率限制 
  * `GET` 方法
    * 每秒不超过35个请求
    * 连续2分钟内每秒不超过25个请求
  * For `POST` method
    * 每秒不超过25个请求
    * 连续2分钟内每秒不超过10个请求

如果超过以上IP频率限制，服务器会返回 HTTP code `403`, 并且你的IP会被封禁至少10分钟

#### 如何提高频率限制
  * 请先阅读[`如何提高频率限制`](./API_Limit_ch.md)
  * 请发申请邮件到 api@bybit.com, 我们会在1-4个工作日内给您答复

### 认证

在调用 API 时，需要提供 API Key 作为每个请求的身份识别，并且通过secret对请求数据加签。[签名算法](#signature-algorithm)

#### 公共参数
字段名 | 字段释义 |  字段类型 | 是否必填 | 默认值 | 说明
:- | :- | :- | :- | :- | :-
api_key | 在平台申请的API_KEY |  string | 是 | 无 |用于身份识别
timestamp | 请求发起时的时间戳,单位:毫秒 | int64 | 是 | 无 | UTC时间戳,服务端收到请求时会校验此参数，校验规则: timestamp < server_time + 1000,其中server_time是服务器时间
recv_window| 配置请求的有效时间,单位:毫秒| int | 否 | 5000 | http请求将会在timestamp+recv_window这个时间点后失效，用于防重放攻击
sign | 签名信息 |  string | 是 | 无 | 按照一定规则形成的签名信息


#### 如何进行签名
1. 将对应业务的接口参数和除sign外的公共参数以http GET请求形式拼接，拼接顺序按照参数名升序排列,如调整杠杆接口业务参数有symbol和leverage,则拼接后如下

``` js
var param_str = 'api_key=B2Rou0PLPpGqcU0Vu2&leverage=100&symbol=BTCUSD&timestamp=1542434791000';

```

2. 对拼接后的字符串进行加签
```js
var secret = 't7T0YlFnYXk0Fx3JswQsDrViLg1Gh3DUU5Mr';
var sign = hex(HMAC_SHA256($secret, $param_str));
// sign = 670e3e4aa32b243f2dedf1dafcec2fd17a440e71b05681550416507de591d908
```

3.附加上sign参数，发送http请求,目前支持以下两种形式提交参数

GET请求

```http
GET /user/leverage?api_key=B2Rou0PLPpGqcU0Vu2&timestamp=1542434791000&sign=670e3e4aa32b243f2dedf1dafcec2fd17a440e71b05681550416507de591d908 HTTP/1.1
Host: api-testnet.bybit.com

```

或

```http
GET /user/leverage HTTP/1.1
Host: api-testnet.bybit.com
content-type: application/json

{
    "api_key":"B2Rou0PLPpGqcU0Vu2",
    "timestamp":1542434791000,
    "sign":"670e3e4aa32b243f2dedf1dafcec2fd17a440e71b05681550416507de591d908"
}
```

POST请求
```http
POST /user/leverage/save HTTP/1.1
Host: api-testnet.bybit.com
content-type: application/json

{
    "api_key":"B2Rou0PLPpGqcU0Vu2",
    "leverage":100,
    "symbol":"BTCUSD",
    "timestamp":1542434791000,
    "sign":"670e3e4aa32b243f2dedf1dafcec2fd17a440e71b05681550416507de591d908"
}
```

### 返回结果格式

字段名 | 字段释义 | 示例值 |
:-: | :-: | :-:
ret_code | 返回码(0：成功,其他失败) | 0 
ret_msg | 返回消息 | ok 
ext_code | 补充错误码 | null 
result | 不同业务接口返回与其对应的数据 | 

### <span id="signature-algorithm">签名算法示例</span>

* [C#](example/Encryption.cs)
* [Python](example/Encryption.py)
* [C++](example/Encryption.cpp)
* [Go](example/Encryption.go)
* [PHP](example/Encryption.php)


### Errors

`10004:error sign`

这个错误是发送方签名与服务端计算出的签名不一致，
可以通过上面的`如何进行签名`校验下发送的签名函数


<hr>

`10002:invalid request`

```
if (timestamp < (server_time + 1000) && (server_time - timestamp) <= recv_window) {
  // 执行请求
} else {
  // invalid request
  // 发送方的timestamp和recv_window不满足此逻辑校验导致
}
```


<hr>

`10007:登录失败`

```
request请求中未添加api_key参数
```