### REST 根URL

* 测试网
https://api-testnet.bybit.com

* 主网
https://api.bybit.com


### 通用请求

* [获取服务器时间](#open-apiservertimeget)
* [获取公告](#open-apiannouncement)

### API 密钥

* [API 密钥信息](#open-apikeyget)

### 活动委托单

* ~~[创建活动委托单](#open-apiordercreatepost)~~  ----推荐使用V2版本

* [创建活动委托单-v2](#open-apiordercreatev2post)

* [查询活动委托](#open-apiorderlistget)

* ~~[撤销活动委托单](#open-apiordercancelpost)~~  ----推荐使用V2版本

* [撤销活动委托单-v2](#open-apiordercancelv2post)

* [撤销全部活动委托单](#open-apiordercancelallpost)

* [活动单修改](#open-apiorderreplacepost)

* [实时查询活动委托](#v2-private-order)

### 条件委托单

* [创建条件委托单](#open-apistop-ordercreatepost)

* [查询条件委托](#open-apistop-orderlistget)

* [撤消条件委托单](#open-apistop-ordercancelpost)

* [撤消全部条件委托单](#open-apistop-ordercancelallpost)

* [修改条件委托单](#open-apistop-orderreplacepost)

* [实时查询条件委托单](#v2-private-stop-order)

### 持仓

* [用户杠杆](#userleverageget)

* [修改用户杠杆](#userleveragesavepost)

* ~~[我的仓位](#positionlistget)~~  ----推荐使用V2版本

* [我的仓位V2](#positionlistv2get)

* [更新保证金](#positionchange-position-marginpost)

* [设置止盈止损](#position-settradingstoppost)

### 钱包

* [获取入金记录](#wallet-fundrecordget)

* [获取出金记录](#wallet-withdrawrecordget)

* [查询用户资产](#open-apiwalletbalanceget)

* [设置风险限额](#wallet-setrisklimit)

* [查询风险限额表](#wallet-getrisklimit)

### 资金费用

* [查询上个周期的资金费率](#open-apifundingprev-funding-rateget)

* [查询上个周期资金费用结算信息](#open-apifundingprev-fundingget)

* [查询预测资金费率和资金费用](#open-apifundingpredicted-fundingget)

### 成交委托单

* [查询委托单成交历史](#open-apiexecutionrecordslistget)

### 市场数据

* [获取Order book](#orderbook-L2)

* [获取合约最新信息](#latest-information-for-symbol)

* [获取平台历史成交数据](#trading-records)

### K线图历史数据

* [查询K线图历史数据](https://bybit-exchange.github.io/bybit-official-api-docs/en/index.html#operation/query_kline)

### 货币

* [查询交易所内已上线交易的货币对](https://bybit-exchange.github.io/bybit-official-api-docs/en/index.html#operation/query_symbol)

### 枚举类型定义

 * [枚举类型定义](#ENUMs)


-----------
## <span id="open-apiservertimeget">服务器时间</span>
#### 接口功能

> 获取服务器时间。

#### HTTP请求方式

> GET   /v2/public/time

#### Request Parameters

|参数|必选|类型|说明|
|:----- |:-------|:-----|----- |


#### Response example

```js

   {
       'ret_code':0   //Error code - True
       'ret_msg':'ok' //Error message
       'ext_code':''  ,
       'result':{
       },
       'time_now':'1539778407.210858',    //UTC timestamp, used for time calibration
   }

```

-----------
## <span id="open-apiannouncement">获取公告</span>
#### 接口功能

> 获取Bybit API 过去30日的公告信息。

#### HTTP请求方式

> GET /v2/public/announcement

#### 请求参数

|参数|必选|类型|说明|
|:----- |:-------|:-----|----- |


#### 返回示例

```js

{
  "ret_code": 0,
  "ret_msg": "OK",
  "ext_code": "",
  "ext_info": "",
  "result": [{
    "id": 1,
    "title": "New API",
    "link": "https://github.com/bybit-exchange/bybit-official-api-docs/blob/master/en/CHANGELOG.md",
    "summary": "Add announcement api",
    "created_at": "2019-10-29T11:24:01Z"//publish time
  }, {
    "id": 3,
    "title": "Update API",
    "link": "https://github.com/bybit-exchange/bybit-official-api-docs/blob/master/en/CHANGELOG.md",
    "summary": "Update get stop order list",
    "created_at": "2019-10-29T12:26:43Z"
  }],
  "time_now": "1572580751.222836"
}

```

-----------
## <span id="open-apikeyget">密钥信息</span>
#### 接口功能

> 获取账户API密钥信息

#### HTTP请求方式

> GET   /open-api/api-key


#### 请求参数

|参数|必选|类型|说明|
|:----- |:-------|:-----|----- |


#### 返回示例

```js

    {
        'ret_code':0   错误码 - 正确,
        'ret_msg':'ok' 错误消息,
        'ext_code':''  ,
        "result": [
            {
            "api_key": "zh2PIPKrIH1ewaRZ1l",            //API key
            "user_id": 160249,                          //用户ID
            "type": "personal",                         //个人或第三方应用名称 如aicoin
            "ips": [                                    //绑定ip type为第三方应用则返回请求白名单列表
                "173.194.72.139"
            ],
            "note": "stephen",
            "permissions": [                            //权限
                "Order",
                "Position"
            ],          
            "created_at": "2019-08-13T10:07:17.000Z",   //创建时间
            "expired_at": null,                         //过期时间：null永久有效  
            "read_only": true                           //只读标志
            }
        ],
        'time_now':'1539778407.210858',    UTC时间戳
        'rate_limit_status': 0,            当前时间区间内(1分钟)该类型接口剩余访问次数
    }

```

-----------
## <span id="open-apiordercreatepost">创建活动委托单 </span>
#### 接口功能

> 所有活动委托都必须填写 &#39;side&#39;, &#39;symbol&#39;, &#39;order_type&#39;, &#39;qty&#39;, &#39;price&#39;, &#39;time_in_force&#39;参数，其它参数除非有特殊说明，否则都是可选的。
市价活动委托: 一个传统的市场价格订单,会以当前的最优价格为您成交订单。当且仅当选择市价单时，&#39;price&#39;可为空！

> 限价活动委托: 您可以为您的订单设置一个执行价格，当市场价格达到您的设置价格时，系统会为您成交订单。

> 止盈止损: 您仅能在开仓时设置止盈止损条件单，一旦持有仓位后提交活动委托时关联的止盈止损则不再有效。

> 委托数量: 表示您要购买/卖出的永续合约数，对于委托数量目前Bybit只允许提交正整数。

> 委托价格: 表示您期望购买/卖出永续合约的价格，对于委托价格目前Bybit只允许提交以0.5为增幅的正数。

> 自定义条件单ID: 您可以自定义活动委托订单ID，我们会为您关联到系统的订单ID，并把系统的唯一订单ID在活动委托创建成功后一并返回给您，您可以使用该订单ID去取消活动委托，同时要求您传递的自定义订单ID最大长度不超过36个字段且唯一。

> 请注意: 
>* 创建活动委托单上限为500个。
>* 'order_status' 字段含义:
>    * 'Created' 意味着Order以及被服务器接受，但还没有进入Order book
>    * 'New' 意味着Order以及进入Order book

#### HTTP请求方式

> POST  /open-api/order/create

#### 请求参数

|参数|必选|类型|说明|
|:----- |:-------|:-----|----- |
|side |true |string |方向, 有效选项:Buy, Sell (Buy Sell )    |
|symbol |true |string |产品类型, 有效选项:BTCUSD, ETHUSD (BTCUSD ETHUSD )    |
|order_type |true |string |委托单价格类型, 有效选项:Limit, Market (Limit Market )    |
|qty |true |integer |委托数量, 单比最大1百万 |
|price |false |number |委托价格, 在没有仓位时，做多的委托价格需高于市价的10%、低于1百万。如有仓位时则需优于强平价。单笔价格增减最小单位为0.5。如果下限价单，则price为必输字段 |
|time_in_force |true |string |执行策略, 有效选项:GoodTillCancel, ImmediateOrCancel, FillOrKill,PostOnly    |
|take_profit |false |number |止盈价格 |
|stop_loss |false |number |止损价格 |
|reduce_only |false |bool |只减仓|
|close_on_trigger |false |bool |触发后平仓. 如果下平仓单，请设置为`true`，避免因为保证金不足而导致下单失败|
|order_link_id |false |string |机构自定义订单ID, 最大长度36位，且同一机构下自定义ID不可重复 |


#### 返回示例

```js

	{
	  "ret_code": 0,
	  "ret_msg": "OK",
	  "ext_code": "",
	  "ext_info": "",
	  "result": {
	    "user_id": 160744,
	    "symbol": "BTCUSD",
	    "side": "Sell",
	    "order_type": "Limit",
	    "price": "8083",
	    "qty": 10,
	    "time_in_force": "GoodTillCancel",
	    "order_status": "New",
	    "ext_fields": {
	      "o_req_num": -308787,
	      "xreq_type": "x_create",
	      "xreq_offset": 4154640
	    },
	    "leaves_qty": 10,
	    "leaves_value": "0.00123716",
	    "cum_exec_qty": 0,
	    "reject_reason": "",
	    "order_link_id": "",
	    "created_at": "2019-10-21T07:28:19.396246Z",
	    "updated_at": "2019-10-21T07:28:19.396246Z",
	    "order_id": "efa44157-c355-4a98-b6d6-1d846a936b93"
	  },
	  "time_now": "1571651135.291930"
	}

```

-----------
## <span id="open-apiordercreatev2post">创建活动委托单 </span>
#### 接口功能

> 所有活动委托都必须填写 &#39;side&#39;, &#39;symbol&#39;, &#39;order_type&#39;, &#39;qty&#39;, &#39;price&#39;, &#39;time_in_force&#39;参数，其它参数除非有特殊说明，否则都是可选的。
市价活动委托: 一个传统的市场价格订单,会以当前的最优价格为您成交订单。当且仅当选择市价单时，&#39;price&#39;可为空！

> 限价活动委托: 您可以为您的订单设置一个执行价格，当市场价格达到您的设置价格时，系统会为您成交订单。

> 止盈止损: 您仅能在开仓时设置止盈止损条件单，一旦持有仓位后提交活动委托时关联的止盈止损则不再有效。

> 委托数量: 表示您要购买/卖出的永续合约数，对于委托数量目前Bybit只允许提交正整数。

> 委托价格: 表示您期望购买/卖出永续合约的价格，对于委托价格目前Bybit只允许提交以0.5为增幅的正数。

> 自定义条件单ID: 您可以自定义活动委托订单ID，我们会为您关联到系统的订单ID，并把系统的唯一订单ID在活动委托创建成功后一并返回给您，您可以使用该订单ID去取消活动委托，同时要求您传递的自定义订单ID最大长度不超过36个字段且唯一。

> 请注意: 
>* 创建活动委托单上限为500个。
>* 'order_status' 字段含义:
>    * 'Created' 意味着Order以及被服务器接受，但还没有进入Order book
>    * 'New' 意味着Order以及进入Order book

#### HTTP请求方式

> POST  /v2/private/order/create

#### 请求参数

|参数|必选|类型|说明|
|:----- |:-------|:-----|----- |
|side |true |string |方向, 有效选项:Buy, Sell (Buy Sell )    |
|symbol |true |string |产品类型, 有效选项:BTCUSD, ETHUSD (BTCUSD ETHUSD )    |
|order_type |true |string |委托单价格类型, 有效选项:Limit, Market (Limit Market )    |
|qty |true |integer |委托数量, 单比最大1百万 |
|price |false |number |委托价格, 在没有仓位时，做多的委托价格需高于市价的10%、低于1百万。如有仓位时则需优于强平价。单笔价格增减最小单位为0.5。如果下限价单，则price为必输字段 |
|time_in_force |true |string |执行策略, 有效选项:GoodTillCancel, ImmediateOrCancel, FillOrKill,PostOnly    |
|take_profit |false |number |止盈价格 |
|stop_loss |false |number |止损价格 |
|reduce_only |false |bool |只减仓 |
|close_on_trigger |false |bool |触发后平仓. 如果下平仓单，请设置为`true`，避免因为保证金不足而导致下单失败|
|order_link_id |false |string |机构自定义订单ID, 最大长度36位，且同一机构下自定义ID不可重复 |

#### 返回示例

```js

    {
        "ret_code": 0,
        "ret_msg": "OK",
        "ext_code": "",
        "ext_info": "",
        "result": {
            "user_id": 105008,
            "order_id": "335fd977-e5a5-4781-b6d0-c772d5bfb95b",
            "symbol": "BTCUSD",
            "side": "Buy",
            "order_type": "Limit",
            "price": 8800,
            "qty": 1,
            "time_in_force": "GoodTillCancel",
            "order_status": "Created",
            "last_exec_time": 0,
            "last_exec_price": 0,
            "leaves_qty": 1,
            "cum_exec_qty": 0,
            "cum_exec_value": 0,
            "cum_exec_fee": 0,
            "reject_reason": "",
            "order_link_id": "",
            "created_at": "2019-11-30T11:03:43.452Z",
            "updated_at": "2019-11-30T11:03:43.455Z"
        },
        "time_now": "1575111823.458705",
        "rate_limit_status": 99,
        "rate_limit_reset_ms": 1575111823448987,
        "rate_limit": 100
    }

```

-----------
## <span id="open-apiorderlistget">查询活动委托 </span>
#### 接口功能

> 获取我的活动委托单列表。

> 创建/取消订单是异步。如果要获取订单的实时信息，可以调用接口[实时查询活动单信息](#v2-private-order)


#### HTTP请求方式

> GET   /open-api/order/list

#### 请求参数

|参数|必选|类型|说明|
|:----- |:-------|:-----|----- |
|order_id |false |string |订单ID |
|order_link_id |false |string |机构自定义订单ID |
|symbol |false |string |产品类型, 默认 `BTCUSD` )    |
|order |false |string |排序字段是`created_at`, 升序降序， 默认降序 (desc asc )    |
|page |false |integer |页码，默认取第一页数据 |
|limit |false |integer |一页数量，一页默认展示20条数据; 最大支持50条每页 |
|order_status |false |string |指定订单状态查询订单列表。不传该参数则默认查询所有状态订单。该参数支持多状态查询，状态之间用英文逗号分割。状态参数：Created,New,PartiallyFilled,Filled,Cancelled,Rejected |


#### 返回示例

```js

    {
        'ret_code':0,
        'ret_msg':'ok',
        'ext_code':'',
        'result':{
            'data':[
                {
                    'order_id': 'string',       UUID类型订单唯一ID
                    'user_id': 0,               用户ID
                    'symbol': 'string',         产品类型
                    'side': 'string',           购买方向
                    'order_type': 'string',     订单类型
                    'price': 0,                 委托价格
                    'qty': 0,                   委托数量
                    'time_in_force': 'string',  执行策略
                    'order_status': 'string',   委托状态: Created:创建订单;Rejected:订单被拒绝;New:订单待成交;PartiallyFilled:订单部分成交;Filled:订单全部成交,Cancelled:订单被取消
                    'last_exec_time': 0.000000 ,最近一次成交时间
                    'last_exec_price': 0,       最近一次成交价格
                    'leaves_qty': 0,            剩余委托数量
                    'cum_exec_qty': 0,          累计成交数量
                    'cum_exec_value': 0,        累计成交的名义价值
                    'cum_exec_fee': 0,          累计已成交手续费
                    'reject_reason': 'string',  被拒单的原因
                    'order_link_id': 'string',  机构自定义订单ID
                    'created_at':'2018-10-15T04:12:19.000Z',
                    'updated_at':'2018-10-15T04:12:19.000Z',
                }
            ],
            'current_page': 1,
            'last_page': 1
        },
        'time_now':'1539781050.462841',    UTC时间戳
        'rate_limit_status': 0,            当前时间区间内(1分钟)该类型接口剩余访问次数
    }

```

-----------
## <span id="open-apiordercancelpost">撤销活动委托单 </span>
#### 接口功能

> 所有撤销活动委托都必须填写 &#39;order_id&#39;，在您创建活动委托成功时会为您返回36位唯一的订单ID。
> 强烈建议传symbol参数，否则可能会有很小的概率导致撤单失败，返回'Order not exists'错误.

> 您可以撤销未成交、部分成交的活动委托单。但全部成交的活动委托不可取消。


#### HTTP请求方式

> POST  /open-api/order/cancel

#### 请求参数

|参数|必选|类型|说明|
|:----- |:-------|:-----|----- |
|symbol |true |string | 合约 |
|order_id |false |string |活动委托单ID, 数据来自创建活动委托单返回的订单唯一ID。如果不填order_link_id则为必输 |
|order_link_id |false |string |机构用户ID.如果不填order_id则为必输|


#### 返回示例

```js

    {
        'ret_code':0   错误码 - 正确,
        'ret_msg':'ok' 错误消息,
        'ext_code':''  ,
        'result': {
            'order_id': 'string',        UUID类型订单唯一ID
            'user_id': 0,                用户ID
            'symbol': 'string',          产品类型
            'side': 'string',            购买方向
            'order_type': 'string',      订单类型
            'price': 0,                  委托价格
            'qty': 0,                    委托数量
            'time_in_force': 'string',   执行策略
            'order_status': 'string',    委托状态: Created:创建订单;Rejected:订单被拒绝;New:订单待成交;PartiallyFilled:订单部分成交;Filled:订单全部成交,Cancelled:订单被取消
            'last_exec_time': 0.000000,  最近一次成交时间
            'last_exec_price': 0,        最近一次成交价格
            'leaves_qty': 0,             剩余委托数量
            'cum_exec_qty': 0,           累计成交数量
            'cum_exec_value': 0,         累计成交的名义价值
            'cum_exec_fee': 0,           累计已成交手续费
            'reject_reason': 'string',   被拒单的原因
            'order_link_id': 'string',   机构自定义订单ID
            'created_at':'2018-10-15T04:12:19.000Z',
            'updated_at':'2018-10-15T04:12:19.000Z',
        },
        'time_now':'1539778407.210858',    UTC时间戳
        'rate_limit_status': 0,            当前时间区间内(1分钟)该类型接口剩余访问次数
    }

```

-----------
## <span id="open-apiordercancelv2post">撤销活动委托单 </span>
#### 接口功能

> 所有撤销活动委托都必须填写 &#39;order_id&#39;，在您创建活动委托成功时会为您返回36位唯一的订单ID。
> 强烈建议传symbol参数，否则可能会有很小的概率导致撤单失败，返回'Order not exists'错误.

> 您可以撤销未成交、部分成交的活动委托单。但全部成交的活动委托不可取消。


#### HTTP请求方式

> POST  /v2/private/order/cancel

#### 请求参数

|参数|必选|类型|说明|
|:----- |:-------|:-----|----- |
|symbol |true |string | 合约 |
|order_id |false |string |订单ID.如果未填order_link_id则为必填字段。|
|order_link_id |false |string |机构ID。如果未填order_id则为必填字段。|

#### 返回示例

```js

    {
        "ret_code": 0,
        "ret_msg": "OK",
        "ext_code": "",
        "ext_info": "",
        "result": {
            "user_id": 105008,
            "order_id": "3bd1844f-f3c0-4e10-8c25-10fea03763f6",
            "symbol": "BTCUSD",
            "side": "Buy",
            "order_type": "Limit",
            "price": 8800,
            "qty": 1,
            "time_in_force": "GoodTillCancel",
            "order_status": "New",
            "last_exec_time": 0,
            "last_exec_price": 0,
            "leaves_qty": 1,
            "cum_exec_qty": 0,
            "cum_exec_value": 0,
            "cum_exec_fee": 0,
            "reject_reason": "",
            "order_link_id": "",
            "created_at": "2019-11-30T11:17:18.396Z",
            "updated_at": "2019-11-30T11:18:01.811Z"
        },
        "time_now": "1575112681.814760",
        "rate_limit_status": 99,
        "rate_limit_reset_ms": 1575112681807671,
        "rate_limit": 100
    }

```

-----------
## <span id="open-apiordercancelallpost">撤销所有活动委托单 </span>
#### 接口功能

> 撤销所有未成交、部分成交的活动委托单。但全部成交的活动委托不可取消。

> 注意，此api每调用一次会导致`rate_limit`扣减10


#### HTTP请求方式

> POST  /v2/private/order/cancelAll

#### 请求参数

|参数|必选|类型|说明|
|:----- |:-------|:-----|----- |
|symbol |true |string | 合约 |


#### 返回示例

```js

    
    {
        "ret_code": 0,      //错误码
        "ret_msg": "OK",    //错误信息
        "ext_code": "",     
        "ext_info": "",
        "result": [
            {
                "clOrdID": "89a38056-80f1-45b2-89d3-4d8e3a203a79",  //订单ID
                "user_id": 105008,                                  //user id
                "symbol": "BTCUSD",                                 //合约类型
                "side": "Buy",                                      //方向
                "order_type": "Limit",                              //订单类型
                "price": "7693.5",                                  //价格
                "qty": 1,                                           //数量
                "time_in_force": "GoodTillCancel",                  //成交类型
                "create_type": "CreateByUser",                      //订单创建状态
                "cancel_type": "CancelByUser",                      //订单取消状态
                "order_status": "",                                 //订单状态
                "leaves_qty": 1,                                    //剩余未成交数量
                "leaves_value": "0",                                
                "created_at": "2019-11-30T10:38:53.564428Z",        //创建时间
                "updated_at": "2019-11-30T10:38:59.102589Z",        //更新时间
                "cross_status": "PendingCancel",                    //订单状态 PendingCancel指已经向撮合发送取消订单请求，但不一定成功取消。
                "cross_seq": 387734027                              //撮合序列号
            }
        ],
        "time_now": "1575110339.105675",
        "rate_limit_status": 98,
        "rate_limit_reset_ms": 1575110339100545,
        "rate_limit": 100
    }

```

-----------

## <span id="open-apiorderreplacepost">修改订单信息</span>
#### API Function

> 'order_id'和'symbol'是必传字段.'p_r_qty' 和 'p_r_price '分别是你想修改的订单的新的量价信息. 如果这两个字段没填，那么默认不修改.

> 请注意，只有未成交或未完全成交的订单才可以被修改。

#### HTTP请求方式

> POST  /open-api/order/replace

#### Request Parameters

|参数|必选|类型|说明|
|:----- |:-------|:-----|----- |
|order_id |true |string |订单id |
|symbol |true |string | 合约种类. |
|p_r_qty |false |int |修改后的订单数量。如果不修改这个字段，请不要传这个参数。 |
|p_r_price |false |number |修改后的订单价格。如果不修改这个字段，请不要传这个参数。 |


#### Response example

```js

    {
        'ret_code':0   错误码 - 正确,
        'ret_msg':'ok' 错误消息,
        'ext_code':''  ,
        'result': 'ok',
        'time_now':'1539778407.210858',    UTC时间戳
        'rate_limit_status': 0,            当前时间区间内(1分钟)该类型接口剩余访问次数
    }

```
-----------

## <span id="v2-private-order">实时查询活动委托</span>
#### API Function

> 实时查询活动委托

#### HTTP请求方式

> GET   /v2/private/order


#### Request Parameters

|参数|必选|类型|说明|
|:----- |:-------|:-----|----- |
|order_id |false |string |订单id。如果不填order_link_id则为必输 |
|order_link_id |false |string | 机构用户ID.如果不填order_id则为必输|
|symbol |true |string | 合约种类 |


#### Response example

```js

	{
	  "ret_code": 0,
	  "ret_msg": "OK",
	  "ext_code": "",
	  "ext_info": "",
	  "result": {
	    "user_id": 160744,
	    "symbol": "BTCUSD",
	    "side": "Sell",
	    "order_type": "Limit",
	    "price": "8083",
	    "qty": 10,
	    "time_in_force": "GoodTillCancel",
	    "order_status": "New",
	    "ext_fields": {
	      "o_req_num": -308787,
	      "xreq_type": "x_create",
	      "xreq_offset": 4154640
	    },
	    "leaves_qty": 10,
	    "leaves_value": "0.00123716",
	    "cum_exec_qty": 0,
	    "reject_reason": "",
	    "cancel_type": "CancelByUser",
	    "order_link_id": "",
	    "created_at": "2019-10-21T07:28:19.396246Z",
	    "updated_at": "2019-10-21T07:28:19.396246Z",
	    "order_id": "efa44157-c355-4a98-b6d6-1d846a936b93"
	  },
	  "time_now": "1571651135.291930"
	}

```

-----------
## <span id="open-apistop-ordercreatepost">创建条件委托单 </span>
#### 接口功能

> 所有条件委托都必须填写 &#39;side&#39;, &#39;symbol&#39;, &#39;order_type&#39;, &#39;qty&#39;, &#39;price&#39;, &#39;base_price&#39;, &#39;stop_px&#39;, &#39;time_in_force&#39;参数，其它参数除非有特殊说明，否则都是可选的。

市价条件委托: 一个传统的市场价格订单,会以当前的最优价格为您成交订单。当且仅当选择市价单时，&#39;price&#39;, &#39;可为空！

限价条件委托: 您可以为您的订单设置一个执行价格，当市场价格达到您的设置价格时，系统会为您成交订单。

委托数量: 表示您要购买/卖出的永续合约数，对于委托数量目前Bybit只允许提交正整数。

委托价格: 表示您期望购买/卖出永续合约的价格，对于委托价格目前Bybit只允许提交以0.5为增幅的正数。

条件委托触发价格: 您可以为您的条件委托单设置一个触发价格，条件委托单不进入委托表（Order Book)，只有触发条件成立如市场价格到达触发价格时，条件委托单才会进入交易系统。当市场价格到达触发价格：1）您的限价条件委托单进入Order Book，等待被执行；2）您的市价条件委托单将按照市场最优价格立即被执行。

自定义条件单ID: 您可以自定义活动委托订单ID，我们会为您关联到系统的订单ID，并把系统的唯一订单ID在活动委托创建成功后一并返回给您，您可以使用该订单ID去取消活动委托，同时要求您传递的自定义订单ID最大长度不超过36个字段且唯一。

请注意: 只允许最多创建10个条件委托单

#### HTTP请求方式

> POST  /open-api/stop-order/create

#### 请求参数

|参数|必选|类型|说明|
|:----- |:-------|:-----|----- |
|side |true |string |方向, 有效选项:Buy, Sell (Buy Sell )    |
|symbol |true |string |产品类型, 有效选项:BTCUSD, ETHUSD (BTCUSD ETHUSD )    |
|order_type |true |string |委托单价格类型, 有效选项:Limit, Market (Limit Market )    |
|qty |true |integer |委托数量 |
|price |false |integer |条件委托执行价格。如果条件委托是现价单，则price为必输字段 |
|base_price |true |integer |当前市价。用于和stop_px值进行比较，确定当前条件委托是看空到stop_px时触发还是看多到stop_px触发。主要是用来标识当前条件单预期的方向 |
|stop_px |true |integer |条件委托下单时市价 |
|time_in_force |true |string |执行策略, 有效选项:GoodTillCancel, ImmediateOrCancel, FillOrKill,PostOnly |
|trigger_by | false | string | 触发价格类型. 默认为上一笔成交价格 |
|close_on_trigger |false |bool |触发后平仓. 如果下平仓单，请设置为`true`，避免因为保证金不足而导致下单失败|
|order_link_id |false |string |机构自定义订单ID, 最大长度36位，且同一机构下自定义ID不可重复 |


#### 返回示例

```js

    {
        'ret_code':0   错误码 - 正确,
        'ret_msg':'ok' 错误消息,
        'ext_code':''  ,
        'result':{
            'stop_order_id': 'string',         UUID类型订单唯一ID
            'user_id': 0,                      用户ID
            'stop_order_status': 'string',     条件单状态: Untriggered: 等待市价触发条件单; Triggered: 市价已触发条件单; Cancelled: 取消; Active: 条件单触发成功且下单成功; Rejected: 条件触发成功但下单失败
            'symbol': 'string',                产品类型
            'side': 'string',                  购买方向
            'order_type': 'string',            价格类型
            'price': 0,                        委托价格
            'qty': 0,                          委托数量
            'time_in_force': 'string',         执行策略
            'stop_order_type': 'string',       订单类型
            'base_price': 0,                   下单时市价
            'stop_px': 0,                      触发价格
            'order_link_id': 'string',         机构自定义订单ID
            'created_at':'2018-10-15T04:12:19.000Z',
            'updated_at':'2018-10-15T04:12:19.000Z',
        }
        'time_now':'1539778407.210858',    UTC时间戳
        'rate_limit_status': 0,            当前时间区间内(1分钟)该类型接口剩余访问次数
    }

```

-----------
## <span id="open-apistop-orderlistget">查询条件委托 </span>
#### 接口功能

> 获取我的条件委托单列表。

#### HTTP请求方式

> GET   /open-api/stop-order/list

#### 请求参数

|参数|必选|类型|说明|
|:----- |:-------|:-----|----- |
|stop_order_id |false |string |条件委托订单ID |
|order_link_id |false |string |机构自定义订单ID |
|symbol |false |string |产品类型,默认`BTCUSD`    |
|stop_order_status |false |string |条件单状态   |
|order |false |string |排序字段为`created_at`,升序降序，默认降序 (desc asc )    |
|page |false |integer |页码，默认取第一页数据 |
|limit |false |integer |一页数量，默认一页展示20条数据;最大支持50条每页 |


#### 返回示例

```js

    {
        'ret_code':0,
        'ret_msg':'ok',
        'ext_code':'',
        'result':{
            'data':[
                {
                    'stop_order_id': 'string',      UUID类型订单唯一ID
                    'user_id': 0,                   用户ID
                    'stop_order_status': 'string',  条件单状态: Untriggered: 等待市价触发条件单; Triggered: 市价已触发条件单; Cancelled: 取消; Active: 条件单触发成功且下单成功; Rejected: 条件触发成功但下单失败
                    'symbol': 'string',             产品类型
                    'side': 'string',               购买方向
                    'order_type': 'string',         价格类型
                    'price': 0,                     委托价格
                    'qty': 0,                       委托数量
                    'time_in_force': 'string',      执行策略
                    'stop_order_type': 'string',    订单类型
                    'base_price': 0,                下单时市价
                    'stop_px': 0,                   触发价格
                    'order_link_id': 'string',      机构自定义订单ID
                    'created_at':'2018-10-15T04:12:19.000Z',
                    'updated_at':'2018-10-15T04:12:19.000Z',
                }
            ],
            'current_page':1,
            'last_page':1
        },
        'time_now':'1539781050.462841',    UTC时间戳
        'rate_limit_status': 0,            当前时间区间内(1分钟)该类型接口剩余访问次数
    }

```

-----------
## <span id="open-apistop-ordercancelpost">撤消条件委托单 </span>
#### 接口功能

> 所有撤销条件委托都必须填写 &#39;stop_order_id&#39;，在您创建条件委托成功时会为您返回36位唯一的订单ID。

您可以撤销所有未被激活的条件委托。本质上所有条件委托在被激活后都是属于活动委托，所以条件委托一旦被激活，您需要通过调用取消活动委托接口来取消所有未成交、部分成交的活动委托单。同样全部成交的活动委托不可取消。


#### HTTP请求方式

> POST  /open-api/stop-order/cancel

#### 请求参数

|参数|必选|类型|说明|
|:----- |:-------|:-----|----- |
|symbol |true |string |合约类型|
|stop_order_id |false |string |委托单ID, 数据来自创建活动委托单返回的订单唯一ID。如果不填order_link_id则为必输 |
|order_link_id |false |string | 机构用户ID.如果不填stop_order_id则为必输|


#### 返回示例

```js

    {
        'ret_code':0   错误码 - 正确,
        'ret_msg':'ok' 错误消息,
        'ext_code':''  ,
        'result':{
            'stop_order_id': 'string',      UUID类型订单唯一ID
            'user_id': 0,                   用户ID
            'stop_order_status': 'string',  条件单状态: Untriggered: 等待市价触发条件单; Triggered: 市价已触发条件单; Cancelled: 取消; Active: 条件单触发成功且下单成功; Rejected: 条件触发成功但下单失败
            'symbol': 'string',             产品类型
            'side': 'string',               购买方向
            'order_type': 'string',         价格类型
            'price': 0,                     委托价格
            'qty': 0,                       委托数量
            'time_in_force': 'string',      执行策略
            'stop_order_type': 'string',    订单类型
            'base_price': 0,                下单时市价
            'stop_px': 0,                   触发价格
            'order_link_id': 'string',      机构自定义订单ID
            'created_at':'2018-10-15T04:12:19.000Z',
            'updated_at':'2018-10-15T04:12:19.000Z',
        }
        'time_now':'1539778407.210858',    UTC时间戳
        'rate_limit_status': 0,            当前时间区间内(1分钟)该类型接口剩余访问次数
    }

```

-----------
## <span id="open-apistop-ordercancelallpost">撤消全部条件委托单 </span>
#### 接口功能

> 撤销所有未被激活的条件委托。本质上所有条件委托在被激活后都是属于活动委托，所以条件委托一旦被激活，您需要通过调用取消活动委托接口来取消所有未成交、部分成交的活动委托单。同样全部成交的活动委托不可取消。

> 注意，此api每调用一次会导致`rate_limit`扣减10


#### HTTP请求方式

> POST  /v2/private/stop-order/cancelAll

#### 请求参数

|参数|必选|类型|说明|
|:----- |:-------|:-----|----- |
|symbol |true |string |合约类型|


#### 返回示例

```js

    {
        "ret_code": 0,
        "ret_msg": "OK",
        "ext_code": "",
        "ext_info": "",
        "result": [
            {
                "clOrdID": "041e523d-2376-42c7-9998-252a5fff9e75",  //订单ID
                "user_id": 105008,                                  //user id
                "symbol": "BTCUSD",                                 //合约类型
                "side": "Buy",                                      //方向
                "order_type": "Limit",                              //订单类型
                "price": "7694.5",                                  //价格
                "qty": 1,                                           //数量
                "time_in_force": "GoodTillCancel",                  //执行策略
                "create_type": "CreateByUser",                      //创建方式
                "cancel_type": "CancelByUser",                      //取消方式
                "order_status": "",                                 //订单状态
                "leaves_qty": 1,                                    //未成交数量
                "leaves_value": "0",
                "created_at": "2019-11-30T10:49:48.139157Z",        //创建时间
                "updated_at": "2019-11-30T10:49:57.646802Z",        //更新时间
                "cross_status": "Deactivated",                      //Deactivated：条件单触发前被撤单
                "cross_seq": -1,                                    //未进入撮合
                "stop_order_type": "Stop",                          //条件订单
                "trigger_by": "LastPrice",                          //触发价格类型
                "base_price": "7689.5",                             //基准价格
                "expected_direction": "Rising"                      //触发方向
            }
        ],
        "time_now": "1575110997.668109",
        "rate_limit_status": 99,
        "rate_limit_reset_ms": 1575110997643683,
        "rate_limit": 100
    }

```
-----------


## <span id="open-apistop-orderreplacepost">修改条件委托单 </span>
#### 接口功能

> 修改活跃的条件单.

> 'order_id' 和 'symbol' 两个字段必输.'p_r_qty', 'p_r_price '和'p_r_trigger_price'这三个字段为修改后的条件单量价信息,以及触发价格. 如果不填则默认不会修改.

> 请注意，只有未触发的条件单才能被修改。


#### HTTP请求方式

> POST  /open-api/stop-order/replace

#### 请求参数

|参数|必选|类型|说明|
|:----- |:-------|:-----|----- |
|order_id |true |string |需要被修改的订单ID |
|symbol |true |string |合约种类. |
|p_r_qty |false |int | 修改后的条件单的量|
|p_r_price |false |number | 修改后的条件单的价格 |
|p_r_trigger_price |false |number | 修改后的条件单的触发价格 |


#### 返回示例

```js

    {
        'ret_code':0   错误码 - 正确,
        'ret_msg':'ok' 错误消息,
        'ext_code':''  ,
        'result':'ok' ,
        'time_now':'1539778407.210858',    UTC时间戳
        'rate_limit_status': 0,            当前时间区间内(1分钟)该类型接口剩余访问次数
    }

```

-----------

## <span id="v2-private-stop-order">实时查询活动委托</span>
#### API Function

> 实时查询活动委托

#### HTTP请求方式

> GET   /v2/private/stop-order


#### Request Parameters

|参数|必选|类型|说明|
|:----- |:-------|:-----|----- |
|stop_order_id |false |string |订单id。如果不填order_link_id则为必输 |
|order_link_id |false |string | 机构用户ID.如果不填order_id则为必输|
|symbol |true |string | 合约种类 |


#### Response example

```js

{
    "ret_code": 0,
    "ret_msg": "OK",
    "ext_code": "",
    "ext_info": "",
    "result": {
        "user_id": 611980,
        "symbol": "BTCUSD",
        "side": "Sell",
        "order_type": "Limit",
        "price": "7700.5",
        "qty": 2,
        "time_in_force": "GoodTillCancel",
        "order_status": "Untriggered",
        "ext_fields": {},
        "leaves_qty": 2,
        "leaves_value": "0.00028985",
        "order_link_id": "",
        "created_at": "2019-12-13T02:31:59.312314Z",
        "updated_at": "2019-12-13T02:31:59.312314Z",
        "order_id": "a2024127-6ef1-482e-bd9a-ed64a13c565d"
    },
    "time_now": "1576204515.018290",
    "rate_limit_status": 599,
    "rate_limit_reset_ms": 1576204515014913,
    "rate_limit": 600
}

```


-----------
## <span id="userleverageget">用户杠杆 </span>
#### 接口功能

> 获取用户杠杆。

#### HTTP请求方式

> GET   /user/leverage

#### 请求参数

|参数|必选|类型|说明|
|:----- |:-------|:-----|----- |


#### 返回示例

```js

{
    'ret_code':0   返回码(0：成功、-1：失败)
    'ret_msg':'ok' 错误消息,
    'ext_code':''  补充错误码,
    'result': {
        'BTCUSD': {
            'leverage': 100
        },
        'ETHUSD': {
            'leverage': 1
        }
    'time_now':'1539778407.210858',    UTC时间戳
    'rate_limit_status': 0,            当前时间区间内(1分钟)该类型接口剩余访问次数
}
 
```

-----------
## <span id="userleveragesavepost">修改用户杠杆 </span>
#### 接口功能

> 修改用户杠杆。


#### HTTP请求方式

> POST  /user/leverage/save

#### 请求参数

|参数|必选|类型|说明|
|:----- |:-------|:-----|----- |
|symbol |true |string |产品类型 (BTCUSD ETHUSD )    |
|leverage |true |string |杠杆. `杠杆为0 意味着全仓模式.全场模式下修改杠杆会变成逐仓模式`|


#### 返回示例

```js

{
    'ret_code':0   返回码(0：成功、-1：失败)
    'ret_msg':'ok' 错误消息,
    'ext_code':''  补充错误码,
    'result': null,根据 ret_code 判断是否请求成功，result返回恒为null
    'time_now':'1539778407.210858',    UTC时间戳
    'rate_limit_status': 0,            当前时间区间内(1分钟)该类型接口剩余访问次数
}
 
```

-----------
## <span id="positionlistget">我的仓位 </span>
#### 接口功能

> 获取我的仓位列表。通过该接口可以获取当前用户的持仓信息，如持仓数量、账户余额等信息


#### HTTP请求方式

> GET   /position/list

#### 请求参数

|参数|必选|类型|说明|
|:----- |:-------|:-----|----- |

#### 返回示例

```js

{
    'ret_code': 0,    返回码(0：成功、-1：失败)
    'ret_msg': 'ok',  错误消息
    'ext_code': '',   补充错误码
    'result': [
        {
            'id': 1,                仓位id
            'user_id': 1,           用户id
            'risk_id': 1,           风险限额id
            'symbol': 'BTCUSD',     产品类型  BTCUSD,ETHUSD
            'side': 'None',         仓位方向  None,buy,sell
            'size': 0,              仓位数量
            'position_value': 0,    仓位价值
            'entry_price': 0,       仓位开仓价
            'leverage': 1,          用户杠杆
            'auto_add_margin': 0,   0表示逐仓 1表示全仓
            'position_margin': 0,   仓位保证金
            'liq_price': 999999,    强平价格
            'bust_price': 999999,   破产价格
            'occ_closing_fee': 0,   平仓手续费
            'occ_funding_fee': 0,   预占用资金费用
            'take_profit': 0,       止盈价格
            'stop_loss': 0,         止损价格
            'trailing_stop': 0,     追踪止损点数
            'position_status': 'Normal',   仓位状态  Normal(正常),Liq(强平中),Adl(减仓中)
            'deleverage_indicator': 1,
            'oc_calc_data': '{\'blq\':\'0\',\'bmp\':\'0\',\'slq\':\'0\',\'smp\':\'0\'}',
            'order_margin': 0,      委托预占用保证金
            'wallet_balance': 0,    账户余额.注意，在全仓模式下，该数字减去未结亏损才是真实可用余额
            'unrealised_pnl': 0,    以标记价格计算的未结盈亏
            'realised_pnl': 0,      今日已结盈亏
            'cum_realised_pnl': 0,  累计已结盈亏
            'cum_commission': 0,    累计佣金
            'cross_seq': 0,         撮合返回版本号
            'position_seq': 2,      仓位版本号
            'created_at': '2018-10-18T07:15:51.000Z',
            'updated_at': '2018-10-20T13:43:21.000Z'
        }
    ],
    'time_now': '1540043097.995523',    UTC时间戳
    'rate_limit_status': 0,            当前时间区间内(1分钟)该类型接口剩余访问次数

}
 *    
```

-----------

## <span id="positionlistv2get">我的仓位V2 </span>
#### 接口功能

> 获取我的仓位列表。通过该接口可以获取当前用户的持仓信息，如持仓数量、账户余额等信息


#### HTTP请求方式

> GET   /v2/private/position/list

#### 请求参数

|参数|必选|类型|说明|
|:----- |:-------|:-----|----- |
|symbol |true |string |合约种类. |

#### 返回示例

```js

{
    "ret_code": 0,
    "ret_msg": "OK",
    "ext_code": "",
    "ext_info": "",
    "result": {
        "id": 20113,
        "user_id": 105008,
        "risk_id": 1,
        "symbol": "BTCUSD",
        "side": "Buy",
        "size": 11,
        "position_value": "0.00156216",
        "entry_price": "7041.53223741",
        "auto_add_margin": 0,
        "leverage": "1",
        "position_margin": "0.00156216",
        "liq_price": "3530",
        "bust_price": "3521",
        "occ_closing_fee": "0.00000235",
        "occ_funding_fee": "0",
        "take_profit": "0",
        "stop_loss": "0",
        "trailing_stop": "0",
        "position_status": "Normal",
        "deleverage_indicator": 3,
        "oc_calc_data": "{\"blq\":0,\"slq\":2,\"slv\":\"0.00025508\",\"bmp\":0,\"smp\":7840.6774,\"fq\":-9,\"bv2c\":1.00225,\"sv2c\":1.0007575}",
        "order_margin": "0",
        "wallet_balance": "0.48987387",
        "realised_pnl": "0",
        "unrealised_pnl": 0,
        "cum_realised_pnl": "-1.51626124",
        "cross_seq": 426783677,
        "position_seq": 269647204,
        "created_at": "2019-09-08T03:10:27Z",
        "updated_at": "2019-12-18T05:24:53.672158Z"
    },
    "time_now": "1576649493.869901",
    "rate_limit_status": 119,
    "rate_limit_reset_ms": 1576649493866093,
    "rate_limit": 120
}

 
```

-----------
## <span id="positionchange-position-marginpost">更新保证金 </span>
#### 接口功能

> 更新保证金

**如果当前为`全仓模式`则不能调整保证金**

#### HTTP请求方式

> POST  /position/change-position-margin

#### 请求参数

|参数|必选|类型|说明|
|:----- |:-------|:-----|----- |
|symbol |true |string |产品 (BTCUSD ETHUSD )    |
|margin |true |string |保证金 |


#### 返回示例

```js

{
    'ret_code':0   返回码(0：成功、-1：失败)
    'ret_msg':'ok' 错误消息,
    'ext_code':'', 补充错误码
    'result': null, 根据 ret_code 判断是否请求成功，result返回恒为null
    'time_now':'1539778407.210858',    UTC时间戳
    'rate_limit_status': 0,            当前时间区间内(1分钟)该类型接口剩余访问次数
}

```

-----------
## <span id="position-settradingstoppost">设置止盈止损 </span>
#### 接口功能

> 设置止盈止损

#### HTTP请求方式

> POST  /open-api/position/trading-stop

#### 请求参数

|参数|必选|类型|说明|
|:----- |:-------|:-----|----- |
|symbol |true |string |合约类型 |
|take_profit |false |string |不小于0,如果等于0则是取消止盈(TP)|
|stop_loss |false |string |不小于0,如果等于0则是取消止损(SL) |
|trailing_stop |false |string |不小于0,如果等于0则是取消追踪止损(TS)|


#### 返回示例

```js

{
  "ret_code": 0,                        //错误吗
  "ret_msg": "ok",                      //相应信息
  "ext_code": "",
  "result":         {
            'id': 1,                仓位id
            'user_id': 1,           用户id
            'risk_id': 1,           风险限额id
            'symbol': 'BTCUSD',     产品类型  BTCUSD,ETHUSD
            'side': 'None',         仓位方向  None,buy,sell
            'size': 0,              仓位数量
            'position_value': 0,    仓位价值
            'entry_price': 0,       仓位开仓价
            'leverage': 1,          用户杠杆
            'auto_add_margin': 0,   0表示逐仓 1表示全仓
            'position_margin': 0,   仓位保证金
            'liq_price': 999999,    强平价格
            'bust_price': 999999,   破产价格
            'occ_closing_fee': 0,   平仓手续费
            'occ_funding_fee': 0,   预占用资金费用
            'take_profit': 0,       止盈价格
            'stop_loss': 0,         止损价格
            'trailing_stop': 0,     追踪止损点数
            'position_status': 'Normal',   仓位状态  Normal(正常),Liq(强平中),Adl(减仓中)
            'deleverage_indicator': 1,
            'oc_calc_data': '{\'blq\':\'0\',\'bmp\':\'0\',\'slq\':\'0\',\'smp\':\'0\'}',
            'order_margin': 0,      委托预占用保证金
            'wallet_balance': 0,    账户余额.注意，在全仓模式，该数字减去未结亏损才是真实可用余额
            'unrealised_pnl': 0,    以标记价格计算的未结盈亏
            'realised_pnl': 0,      今日已结盈亏
            'cum_realised_pnl': 0,  累计已结盈亏
            'cum_commission': 0,    累计佣金
            'cross_seq': 0,         撮合返回版本号
            'position_seq': 2,      仓位版本号
            'created_at': '2018-10-18T07:15:51.000Z',
            'updated_at': '2018-10-20T13:43:21.000Z'
        },
  "time_now": "1569304018.857490"
}

```

-----------
## <span id="wallet-fundrecordget">获取入金记录 </span>
#### 接口功能

> 获取入金记录

#### HTTP请求方式

> GET   /open-api/wallet/fund/records

#### 请求参数

|参数|必选|类型|说明|
|:----- |:-------|:-----|----- |
|start_date |false |string |查询起始日期 |
|end_date |false |string |查询结束日期  |
|currency |false |string |币种|
|coin |false |string |别名 |
|wallet_fund_type |false |string |钱包类型|
|page |false |integer |页数，默认为1 |
|limit |false |integer |查询上线，最大50，默认显示20页 |



#### 返回示例

```js

{
  "ret_code": 0,                                //错误码 0为成功
  "ret_msg": "ok",                              //错误信息
  "ext_code": "",
  "result": {
    "data": [{
      "id": 128495,                             //id
      "user_id": 103669,                        //用户id
      "coin": "XRP",                            //币种
      "wallet_id": 14760,                       //钱包ID
      "type": "Realized P&L",                   //入金类型
      "amount": "1.18826225",                   //数量
      "tx_id": "",
      "address": "XRPUSD",                      //地址
      "wallet_balance": "999.12908894",         //可用余额
      "exec_time": "2019-09-25T00:00:15.000Z",
      "cross_seq": 0
    }]
  },
  "time_now": "1569395810.140869"
}

```

-----------
## <span id="orderbook-L2">获取Order book </span>
#### 接口功能

> 获取当前order book数据

#### HTTP请求方式

> GET   /v2/public/orderBook/L2

#### 请求参数

|参数|必选|类型|说明|
|:----- |:-------|:-----|----- |
|symbol |true |string |合约类型 |



#### 返回示例

```js

{
    "ret_code": 0,                              // 响应码 0 为成功
    "ret_msg": "OK",                            // 错误信息
    "ext_code": "",                             
    "ext_info": "",                          
    "result": [
        {
            "symbol": "BTCUSD",                 // 合约类型
            "price": "9487",                    // 价格
            "size": 336241,                     // 数量
            "side": "Buy"                       // 方向
        },
        {
            "symbol": "BTCUSD",                
            "price": "9487.5",                
            "size": 522147,                     
            "side": "Sell"                     
        }
    ],
    "time_now": "1567108756.834357"             // UTC timestamp
}

```

-----------
## <span id="latest-information-for-symbol">获取合约最新信息 </span>
#### 接口功能

> 获取合约最新信息

#### HTTP请求方式

> GET   /v2/public/tickers

#### 请求参数

|参数|必选|类型|说明|
|:----- |:-------|:-----|----- |
|symbol |false |string |合约类型 |



#### 返回示例

```js

{
    "ret_code": 0,                                   // 错误码 0为成功
    "ret_msg": "OK",                                 // 错误信息
    "ext_code": "",                                  
    "ext_info": "",                                  
    "result": [
        {
            "symbol": "BTCUSD",                             // 合约类型
            "bid_price": "9499.5",                          // 买1价格
            "ask_price": "9500",                            // 卖1价格
            "last_price": "9499.50",                        // 场内价格
            "last_tick_direction": "ZeroMinusTick",         // Tick方向:PlusTick,上涨 ,MinusTick跌,ZeroMinusTick平
            "prev_price_24h": "9659.00",                    // 昨日收盘价
            "price_24h_pcnt": "-0.02",                      // 昨日涨跌幅
            "high_price_24h": "9737.00",                    // 昨日最高价
            "low_price_24h": "9322.50",                     // 昨日最低价
            "prev_price_1h": "9469.00",                     // 前一小时收盘价
            "price_1h_pcnt": "0.00",                        // 前一小时涨跌幅
            "mark_price": "9509.24",                        // 标记价格
            "index_price": "9509.00",                       // 指数价格
            "open_interest": 78923133,                      // 未平仓合约数量，更新频率相对较慢，最慢一分钟更新一次
            "open_value": "8078.86",                        // 未平仓价值，更新频率相对较慢，最慢一分钟更新一次
            "total_turnover": "6540981.84",                 // 总成交量(BTC价值)
            "turnover_24h": "59236.52",                     // 24小时成交量(BTC价值
            "total_volume": 62971273761,                    // 总交易量(合约数)
            "volume_24h": 564198332,                        // 24小时总交易量(合约数)
            "funding_rate": "0.00",                         // 资金费率
            "predicted_funding_rate": "-0.00",              // 预测资金费率
            "next_funding_time": "2019-08-30T00:00:00Z",    // 下次结算资金费用时间
            "countdown_hour": 4                             // 结算时间间隔
        }
    ],
    "time_now": "1567109419.049271"
}

```

-----------
## <span id="trading-records">获取平台历史成交数据</span>
#### 接口功能

> 获取历史成交数据

#### HTTP请求方式

> GET   /v2/public/trading-records

#### 请求参数

|参数|必选|类型|说明|
|:----- |:-------|:-----|----- |
|symbol |true |string |合约类型 |
|from |false |int |查询起始ID.如果不填则返回最新数据 |
|limit |false |int |结果条数.单次默认500，最高1000 |



#### 返回示例

```js

{
    "ret_code": 0,                                   // 错误码 0为成功
    "ret_msg": "OK",                                 // 错误信息
    "ext_code": "",                                  
    "ext_info": "",                                  
    "result": [
        {
            "id":7724919,                                   // ID
            "symbol": "BTCUSD",                             // 合约类型
            "price": 9499.5,                                // 成交价格
            "qty": 9500,                                    // 成交数量
            "side": "Buy",                                  // 成交方向
            "time": "2019-11-19T08:03:04.077Z",             // UTC时间
        }
    ],
    "time_now": "1567109419.049271"
}

```

-----------
## <span id="wallet-withdrawrecordget">获取出金记录 </span>
#### 接口功能

> 获取出金记录

#### HTTP请求方式

> GET   /open-api/wallet/withdraw/list

#### 请求参数

|参数|必选|类型|说明|
|:----- |:-------|:-----|----- |
|start_date |false |string |查询起始日期 |
|end_date |false |string |查询结束日期  |
|currency |false |string |币种|
|coin |false |string |别名 |
|wallet_fund_type |false |string |钱包类型|
|page |false |integer |页数，默认为1 |
|limit |false |integer |查询上线，最大50，默认显示20页 |



#### 返回示例

```js

{
  "ret_code": 0,                                        //错误码0为成功
  "ret_msg": "ok",                                      //错误信息
  "ext_code": "",
  "result": {
    "data": [{
      "id": 137,                                        //id
      "user_id": 160249,                                //用户ID
      "coin": "XRP",                                    //币种
      "status": "Pending",                              //状态
      "amount": "20.00000000",                          //数量
      "fee": "0.25000000",                              //手续费
      "address": "rH7H595XYEVTEHU2FySYsWnmfACBnZS9zM",  //地址
      "tx_id": "",
      "submited_at": "2019-06-11T02:20:24.000Z",
      "updated_at": "2019-06-11T02:20:24.000Z"
    }]
  },
  "ext_info": null,
  "time_now": "1570863984.536136"
}

```

## <span id="open-apiwalletbalanceget">查询用户资产 </span>
#### 接口功能

> 获取用户资产信息。

#### HTTP请求方式

##### 方法
> GET   /v2/private/wallet/balance

#### 请求参数

|参数|必选|类型|说明|
|:----- |:-------|:-----|----- |
|coin |true |BTC,EOS,ERP,ETH,USDT |币种 |

#### 返回示例

```js

{
    "ret_code": 0,
    "ret_msg": "OK",
    "ext_code": "",
    "ext_info": "",
    "result": {
        "BTC": {
            "equity": 1002,                         //资产净值，equity = wallet_balance + unrealised_pnl
            "available_balance": 999.99987471,      //可用余额
            //逐仓模式下， available_balance = wallet_balance - (position_margin + occ_closing_fee + occ_funding_fee + order_margin)
            //全仓模式下，
            //如果unrealised_pnl大于0, available_balance = wallet_balance - (position_margin + occ_closing_fee + occ_funding_fee + order_margin)；
            //否则，available_balance = wallet_balance - (position_margin + occ_closing_fee + occ_funding_fee + order_margin) + unrealised_pnl 
            "used_margin": 0.00012529,              //已用保证金, used_margin = wallet_balance - available_balance
            "order_margin": 0.00012529,             //委托保证金
            "position_margin": 0,                   //仓位保证金
            "occ_closing_fee": 0,                   //平仓手续费
            "occ_funding_fee": 0,                   //预占用资金费用
            "wallet_balance": 1000,                 //钱包余额
            "realised_pnl": 0,                      //已结盈亏
            "unrealised_pnl": 2,                    //未结盈亏
            //  如果方向为sell, unrealised_pnl = size * (1.0 / mark_price -  1.0 / entry_price）
            //  如果方向为buy, unrealised_pnl = size * (1.0 / entry_price -  1.0 / mark_price）
            "cum_realised_pnl": 0,                  //总累计已结盈亏
            "given_cash": 0,                        //体验金
            "service_cash": 0                       //抵扣金
        }
    },
    "time_now": "1578284274.816029"
}

```


-----------
## <span id="wallet-setrisklimit">设置风险限额 </span>
#### 接口功能

> 设置风险限额

#### HTTP请求方式

> POST   /open-api/wallet/risk-limit

#### 请求参数

|参数|必选|类型|说明|
|:----- |:-------|:-----|----- |
|symbol |true |string |交易对 |
|risk_id |true |integer |风险限额id  |



#### 返回示例

```js

{
  "ret_code": 0,
  "ret_msg": "ok",
  "ext_code": "",
  "result": {
    "position": {
      "id": 1708,
      "user_id": 160245,
      "symbol": "BTCUSD",
      "side": "None",
      "size": 0,
      "position_value": 0,
      "entry_price": 0,
      "risk_id": 2,
      "auto_add_margin": 0,
      "leverage": 1,
      "position_margin": 0,
      "liq_price": 0,
      "bust_price": 0,
      "occ_closing_fee": 0,
      "occ_funding_fee": 0,
      "take_profit": 0,
      "stop_loss": 0,
      "trailing_stop": 0,
      "position_status": "Normal",
      "deleverage_indicator": 0,
      "oc_calc_data": "{\"blq\":1,\"blv\":\"0.000125\",\"slq\":0,\"bmp\":8000,\"smp\":0,\"fc\":-0.00012529,\"bv2c\":1.00225,\"sv2c\":1.0007575}",
      "order_margin": 0.00012529,
      "wallet_balance": 1000,
      "realised_pnl": 0,
      "cum_realised_pnl": 0,
      "cum_commission": 0,
      "cross_seq": 4376,
      "position_seq": 13689,
      "created_at": "2019-08-13T06:51:29.000Z",
      "updated_at": "2019-12-29T03:11:08.000Z",
      "ext_fields": {
        "v": 4
      }
    },
    "risk": {
      "id": 2,
      "coin": "BTC",
      "limit": 300,
      "maintain_margin": "1.00",
      "starting_margin": "1.50",
      "section": "[\"1\",\"2\",\"3\",\"5\",\"10\",\"25\",\"50\",\"66\"]",
      "is_lowest_risk": 0,
      "created_at": "2019-06-26T05:46:45.000Z",
      "updated_at": "2019-06-26T05:46:55.000Z"
    }
  },
  "ext_info": null,
  "time_now": "1577589068.435439",
  "rate_limit_status": 71,
  "rate_limit_reset_ms": 1577589068546,
  "rate_limit": "75"
}

```

-----------
## <span id="wallet-getrisklimit">查询风险限额表 </span>
#### 接口功能

> 查询风险限额表

#### HTTP请求方式

> GET   /open-api/wallet/risk-limit/list

#### 请求参数

|参数|必选|类型|说明|
|:----- |:-------|:-----|----- |



#### 返回示例

```js

{
  "ret_code": 0,
  "ret_msg": "ok",
  "ext_code": "",
  "result": [
    {
      "id": 1,
      "coin": "BTC",
      "limit": 150,
      "maintain_margin": "0.50",
      "starting_margin": "1.00",
      "section": [
        "1",
        "2",
        "3",
        "5",
        "10",
        "25",
        "50",
        "100"
      ],
      "is_lowest_risk": 1,
      "created_at": "2018-11-09T13:53:04.000Z",
      "updated_at": "2018-11-09T13:53:04.000Z"
    },
    {
      "id": 11,
      "coin": "ETH",
      "limit": 3000,
      "maintain_margin": "1.00",
      "starting_margin": "2.00",
      "section": [
        "1",
        "2",
        "3",
        "5",
        "15",
        "30",
        "40",
        "50"
      ],
      "is_lowest_risk": 1,
      "created_at": "2019-01-25T08:31:54.000Z",
      "updated_at": "2019-01-25T08:31:54.000Z"
    }
  ],
  "ext_info": null,
  "time_now": "1577587907.157396",
  "rate_limit_status": 599,
  "rate_limit_reset_ms": 1577587907162,
  "rate_limit": 600
}


```

-----------
## <span id="open-apifundingprev-funding-rateget">查询上个周期的资金费率 </span>
#### 接口功能

> UTC时间每天0点、8点、16点产生一个资金费率

假设当前时间是12点，则返回的是8点产生的资金费率
 
#### HTTP请求方式

> GET   /open-api/funding/prev-funding-rate

#### 请求参数

|参数|必选|类型|说明|
|:----- |:-------|:-----|----- |
|symbol |true |string |产品 (BTCUSD ETHUSD )    |


#### 返回示例

```js

{
    'ret_code':0   // 返回码(0：成功、-101：参数校验失败)
    'ret_msg':'ok' // 错误消息,
    'ext_code':'', // 补充错误码
    'result': {
        'symbol':'BTCUSD',
        'funding_rate':'0.00375000', // 资金费率,当资金费率是正数时，多仓向空仓支付资金费用.为负数时，空仓向多仓支付资金费用
        'funding_rate_timestamp':1539950401 //资金费率产生时间,UTC时间戳
    },
    'time_now':'1539778407.210858',    UTC时间戳
}

```

-----------
## <span id="open-apifundingprev-fundingget">查询上个周期资金费用结算信息 </span>
#### 接口功能

> UTC时间每天0点、8点、16点进行资金费用结算

当前周期的资金费用结算是根据上个周期的资金费率来进行结算

比如16点结算时是按照8点产生的资金费率来进行结算

而16点产生的资金费率则会在第二天0点结算时使用

#### HTTP请求方式

> GET   /open-api/funding/prev-funding

#### 请求参数

|参数|必选|类型|说明|
|:----- |:-------|:-----|----- |
|symbol |true |string |产品 (BTCUSD ETHUSD )    |


#### 返回示例

```js

{
    'ret_code':0   // 返回码(0：成功、-101：参数校验失败)
    'ret_msg':'ok' // 错误消息,
    'ext_code':'', // 补充错误码
    'result': {
        'symbol': 'BTCUSD',
        'side': 'Buy', // 进行结算时仓位的持仓方向
        'size': 10,   // 进行结算时仓位的数量
        'funding_rate': 0.00375 // 结算时的资金费率, 为正数时,多仓支付费用，空仓收取费用; 为负数时，多仓收取费用，空仓支付费用
        'exec_fee': 0.00000116, // 
        'exec_timestamp': 1539950401, // 结算时间，UTC时间戳
    },
    'time_now':'1539778407.210858',    UTC时间戳
}

```

-----------
## <span id="open-apifundingpredicted-fundingget">查询预测资金费率和资金费用</span>
#### 接口功能

> 查询预测资金费率和资金费用

#### HTTP请求方式

> GET   /open-api/funding/predicted-funding

#### 请求参数

|参数|必选|类型|说明|
|:----- |:-------|:-----|----- |
|symbol |true |string |产品 (BTCUSD ETHUSD )    |


#### 返回示例

```js

{
    'ret_code':0   // 返回码(0：成功、-101：参数校验失败)
    'ret_msg':'ok' // 错误消息,
    'ext_code':'', // 补充错误码
    'result': {
        'predicted_funding_rate': 0.001, // 预测资金费率,为正数时,多仓支付费用，空仓收取费用; 为负数时，多仓收取费用，空仓支付费用
        'predicted_funding_fee': 0.000234 // 预测资金费用
    },
    'time_now':'1539778407.210858',    UTC时间戳
}

```

-----------
## <span id="open-apiexecutionrecordslistget">查询委托单成交历史 </span>
#### 接口功能

> 获取委托单成交历史列表。

#### HTTP请求方式

> GET   /v2/private/execution/list

#### 请求参数

|参数|必选|类型|说明|
|:----- |:-------|:-----|----- |
|order_id |false |string |订单ID，如果不填则默认反馈用户所有订单 |
|symbol |false |string |合约类型。如果order_id不填，`symbol`字段为必填|
|start_time |false |int |起始时间|
|page |false |integer |页数|
|limit |false |integer |最大页数。最大为50，默认显示20页 |


#### 返回示例

```js

{
    'ret_code': 0,                                            // 返回码
    'ret_msg': 'OK',                                          // 错误消息
    'ext_code': '',                                           // 补充错误码
    'ext_info': '',                                           // 补充错误码
    'result': {
        'order_id': 'd854bb13-3fb9-4608-ade4-828f50210778',       // 订单号
        'trade_list': [{
            'closed_size': 0,                                     // 对应的平仓size
            'cross_seq': 3154097,                                 // 撮合返回号
            'exec_fee': '-0.00000005',                            // 资金/手续费 费用
            'exec_id': 'b3551383-19b1-4aa6-8ac2-f996bea6e07c',    // 交易执行id
            'exec_price': '4202',                                 // 成交价格
            'exec_qty': 1,                                         // 成交数量
            'exec_time': '1545203567',                             // 成交时间
            'exec_type': 'Trade',                                  // 交易记录类别 -- Trade: 普通交易  Funding: 资金费率  AdlTrade：自动减仓  BustTrade: 强制平仓
            'exec_value': '0.00023798',                            // 价值
            'fee_rate': '-0.00025',                                // 资金/手续费 费率
            'last_liquidity_ind': 'AddedLiquidity',                // AddedLiquidity/RemovedLiquidity
            'leaves_qty': 0,                                      // 剩余数量
            'nth_fill': 7,                                        // 该笔流水的第几笔成交
            'order_id': 'd854bb13-3fb9-4608-ade4-828f50210778', // 订单号
            'order_price': '4202',                                // 委托价格
            'order_qty': 1,                                     // 委托数量
            'order_type': 'Limit',                               // 交易记录类型
            'side': 'Sell',                                     // 购买方向
            'symbol': 'BTCUSD',                                  // 产品类别
            'user_id': 155446                                     // 所属用户
        }]
    },
    'time_now': '1551340186.761136'
}

```

-------
## <span id="ENUMs">枚举类型定义</span>
> 这是向API发送请求时不同参数的有效选项(和规则)列表
#### Side (`side`)
* `Buy`
* `Sell`

#### Symbol (`symbol`)
* `BTCUSD`
* `ETHUSD`
* `EOSUSD`
* `XRPUSD`

#### Currency (`currency`/`coin`)
* `BTC`
* `ETH`
* `EOS`
* `XRP`

#### Wallet fund type (`wallet_fund_type`)
* `Deposit`                 `存款`
* `Withdraw`                `提现`
* `RealisedPNL`             `已结盈亏`
* `Commission`              `佣金`
* `Refund`                  `退款`
* `Prize`                   `赠金`
* `ExchangeOrderWithdraw`   `资产兑换(扣钱)`
* `ExchangeOrderDeposit`    `资产兑换(加钱)`

#### Withdraw status (`status`)
* `ToBeConfirmed`   - `待确认`
* `UnderReview`     -`复核中`
* `Pending`         -`待转账`
* `Success`         -`成功`
* `CancelByUser`    -`由用户取消`
* `Reject`          -`被拒绝`
* `Expire`          -`过期`


#### Order type (`order_type`)
* `Limit`   -`限价单`
* `Market`  -`市价单`

#### Quantity (`qty`)
* 最大为1百万 (`1000000`)
* 只能为整数
  * `40` - 合法
  * `30.5` - 非法

#### Price (`price`)
* 活跃订单
  * 必须为合约最小变动价格的整数倍 `tick_size`
    * 使用取余符号(%), 来计算价格是否合法，如:
      ```js
      IF price % tick_size = 0
        // 发送订单
      ELSE
        // 不会发送订单，因为价格将不被系统接受
      ```
    * 当前合约信息可以参考: [https://api.bybit.com/v2/public/symbols](https://api.bybit.com/v2/public/symbols)
  * 最大为1百万 (`1000000`)
  * 如果用户没有未平仓，则价格必须大于市场价格的10%
    * 如, 若当前市场价(last price) 为 `10314`, 那么下单价格的最小值为 `1031.5`. 
    * 伪代码(假设价格是0.5的增量):
      ```js
      IF price > (last_price * 0.1)
        // 发送订单
      ELSE
        // 不会发送订单，因为价格将不被系统接受
      ```
  * 如果已持有仓位，那么价格必须高于强平价格
    * 如, 若多仓的强平价格为 `5176.5` 那么价格最小为 `5177`. 在做空的情况下，价格必须低于强平价格。
* 条件单
  * 必须大于等于 `1`

#### [Time in force](https://help.bybit.com/hc/en-us/articles/360007211974-Time-in-Force) (`time_in_force`) 
* `GoodTillCancel`      `挂单直到成交`
* `ImmediateOrCancel`   `下单后任何未完成部分立即被取消`
* `FillOrKill`          `订单要么完全成交要么取消`
* `PostOnly`            `只挂单`

#### Trigger price type (`trigger_by`)
* `LastPrice`       `市场价格`
* `IndexPrice`      `指数价格`
* `MarkPrice`       `标记价格`

#### Order status (`order_status`)
* `Created`         `订单待确认`
* `New`             `订单已确认`
* `PartiallyFilled` `部分成交`
* `Filled`          `全部成交`
* `Cancelled`       `已取消`
* `Rejected`        `订单被拒绝`
* `PendingCancel`   `撮合引擎收到取消指令但不一定会被成功取消`
* `Deactivated`     `条件单触发前被取消`

#### Order (`order`)
* __NOTE: currently broken for both get conditional order and get active order__
* `订单排序选项`
* `desc`    `降序排列`(default)
* `asc`     `升序排列`

#### Cancel type (`cancel_type`)
* `CancelByUser` 
* `CancelByReduceOnly` 
* `CancelByPrepareLiq`,`CancelAllBeforeLiq` - 仓位进入强平会取消订单 
* `CancelByPrepareAdl`,`CancelAllBeforeAdl` - 自动减仓导致取消订单
* `CancelByAdmin`
* `CancelByTpSlTsClear` - 止盈止损单被取消
* `CancelByPzSideCh` - 该订单在触发止盈止损后被取消

#### Create type (`create_type`)
* `CreateByUser` 
* `CreateByClosing` 
* `CreateByAdminClosing` 
* `CreateByStopOrder` 
* `CreateByTakeProfit` 
* `CreateByStopLoss` 
* `CreateByTrailingStop` 
* `CreateByLiq` - 部分平仓.用户触发强平时，可以通过调整风险限额，部分平仓，来避免强平
* `CreateByAdl_PassThrough` - 强平减仓
* `CreateByTakeOver_PassThrough` - 强平接管