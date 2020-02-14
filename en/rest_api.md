# NOTICE: These docs are now OBSOLETE; please find the new documentation [here](https://bybit-exchange.github.io/docs/inverse). Thank you.

### Base Endpoint

* For testnet
https://api-testnet.bybit.com

* For mainnet
https://api.bybit.com

### Common

* [Server time](#open-apiservertimeget)
* [Announcement](#open-apiannouncement)

### API key

* [API key info](#open-apikeyget)

### Active Order

* ~~[Place active order](#open-apiordercreatepost)~~ ----The V2 version is recommended to use.

* [Place active order-V2](#open-apiordercreatev2post)

* [Get active order](#open-apiorderlistget)

* ~~[Cancel active order](#open-apiordercancelpost)~~ ----The V2 version is recommended to use.

* [Cancel active order-V2](#open-apiordercancelv2post)

* [Cancel all active orders](#open-apiordercancelallpost)

* [Replace order](#open-apiorderreplacepost)

* [Query active order (real-time)](#v2-private-order)

### Conditional Order

* [Place conditional order](#open-apistop-ordercreatepost)

* [Get conditional order](#open-apistop-orderlistget)

* [Cancel conditional order](#open-apistop-ordercancelpost)

* [Cancel all conditional orders](#open-apistop-ordercancelallpost)

* [Replace conditional order](#open-apistop-orderreplacepost)

* [Query stop order (real-time)](#v2-private-stop-order)

### Positions

* [User leverage](#userleverageget)

* [Change leverage](#userleveragesavepost)

* ~~[My position](#positionlistget)~~ ----The V2 version is recommended to use.

* [My position-V2 (real-time)](#positionlistv2get)

* [Change margin](#positionchange-position-marginpost)

* [Set Trading-Stop](#position-settradingstoppost)

### Wallet

* [Get Wallet fund records](#wallet-fundrecordget)

* [Get Withdraw records](#wallet-withdrawrecordget)

* [Get Account Balance](#open-apiwalletbalanceget)

* [Set risk limit](#wallet-setrisklimit)

* [Get risk limit list](#wallet-getrisklimit)

### Funding

* [Funding rate](#lastfundingrate)

* [My funding fee](#userlastfundingfee)

* [Predicted funding](#open-apifundingpredicted-fundingget)

### Execution

* [Get user's trade records](#open-apiexecutionrecordslistget)

### Market data

* [Get the orderbook](#orderbook-L2)

* [Get latest information for symbol](#latest-information-for-symbol)

* [Get public trading records](#trading-records)

### Kline data

* [Query historical kline](https://bybit-exchange.github.io/bybit-official-api-docs/en/index.html#operation/query_kline)

### Symbol

* [Query symbols](https://bybit-exchange.github.io/bybit-official-api-docs/en/index.html#operation/query_symbol)

### ENUM definitions

 * [ENUM definitions and descriptions](#ENUMs)

-----------
## <span id="open-apiservertimeget">Server time</span>
#### API Function

> Get bybit server time。

#### HTTP Request

##### Method
> GET ```/v2/public/time```

#### Request Parameters

|parameter|required|type|comments|
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
## <span id="open-apiannouncement">Announcement</span>
#### API Function

> Get bybit OpenAPI announcements in the last 30 days。

#### HTTP Request

##### Method
> GET ```/v2/public/announcement```

#### Request Parameters

|parameter|required|type|comments|
|:----- |:-------|:-----|----- |


#### Response example

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
## <span id="open-apikeyget">API key info</span>
#### API Function

> Get User API key Info。

#### HTTP Request

##### Method
> GET ```/open-api/api-key```

#### Request Parameters

|parameter|required|type|comments|
|:----- |:-------|:-----|----- |


#### Response example

```js

{
  "ret_code": 0,
  "ret_msg": "ok",
  "ext_code": "",
  "result": [
    {
      "api_key": "zh2PIPKrIH1ewaRZ1l",          //API key
      "user_id": 160249,                        //user id
      "type": "personal",                       //personal or third-party application name such as aicoin
      "ips": [                                  //bind ip type to a third-party application to return a request whitelist
        "173.194.72.139"
      ],
      "note": "stephen",
      "permissions": [                          //permissions
        "Order",
        "Position"
      ],
      "created_at": "2019-08-13T10:07:17.000Z", //create time
      "expired_at": null,                       // expire time: null is forever
      "read_only": true                         //read only flag
    }
  ],
  "ext_info": null,
  "time_now": "1570869813.399178"
}

```

-----------
## <span id="open-apiordercreatepost">Place Active Order</span>
#### API Function

>Parameters of 'side', 'symbol', 'order_type', 'qty', 'price', 'time_in_force' are required for all active orders. Other parameters are optional unless specified.

>Market price active order: A traditional market price order, will be filled at the best available price. 'price'  can set to be "" if and only if you are placing market price order.

>Limit price active order: You can set an execution price for your order. Only when last traded price reaches the order price, the system will fill your order.

>Take profit/Stop loss: You may only set a take-profit/stop-loss conditional order upon opening the position. Once you hold a position, the take profit and stop loss information u sent when placing an order will no longer be valid.

>Order quantity: This parameter indicates the quantity of perpetual contracts you want to buy or sell, currently Bybit only support order quantity in an integer.

>Order price: This parameter indicates the price of perpetual contracts you want to buy or sell, you can get price increment by [Query symbols endpoint](https://bybit-exchange.github.io/bybit-official-api-docs/en/index.html#operation/query_symbol)

>Customize conditional order ID: You may customize order IDs for active orders. We will link it to the system order ID , and return the unique system order ID to you after the active order is created successfully. You may use this order ID to cancel your active order. The customized order ID is asked to be unique, with a maximum length of 36 characters.

>Notes:
>* Each account can hold up to 500 active orders yet to be filled entirely simultaneously.
>* 'order_status' values explained:
>    * 'Created' indicates the order has been accepted by the system but not yet entered into the orderbook
>    * 'New' indicates the order has entered into the orderbook.

#### HTTP Request

##### Method
> POST ```/open-api/order/create```

#### Request Parameters

|parameter|required|type|comments|
|:----- |:-------|:-----|----- |
|side |true |string |Side    |
|symbol |true |string |Contract type.    |
|order_type |true |string |Active order type   |
|qty |true |integer |Order quantity. |
|price |false |number |Order price. Required if you make limit price order |
|time_in_force |true |string |Time in force |
|take_profit |false |number |take profit price|
|stop_loss |false |number |stop loss price|
|reduce_only |false |bool |reduce only
|close_on_trigger |false |bool |close on trigger. When creating closing order, highly recommend to set as `true` to avoid failing by insufficient avaliable margin|
|order_link_id |false |string |Customized order ID, maximum length at 36 characters, and order ID under the same agency has to be unique.|


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
	    "order_link_id": "",
	    "created_at": "2019-10-21T07:28:19.396246Z",
	    "updated_at": "2019-10-21T07:28:19.396246Z",
	    "order_id": "efa44157-c355-4a98-b6d6-1d846a936b93"
	  },
	  "time_now": "1571651135.291930"
	}

```

-----------
## <span id="open-apiordercreatev2post">Place Active Order-V2</span>
#### API Function

>Parameters of 'side', 'symbol', 'order_type', 'qty', 'price', 'time_in_force' are required for all active orders. Other parameters are optional unless specified.

>Market price active order: A traditional market price order, will be filled at the best available price. 'price' can set to be "" if and only if you are placing market price order.

>Limit price active order: You can set an execution price for your order. Only when last traded price reaches the order price, the system will fill your order.

>Take profit/Stop loss: You may only set a take-profit/stop-loss conditional order upon opening the position. Once you hold a position, the take profit and stop loss information u sent when placing an order will no longer be valid.

>Order quantity: This parameter indicates the quantity of perpetual contracts you want to buy or sell, currently Bybit only support order quantity in an integer.

>Order price: This parameter indicates the price of perpetual contracts you want to buy or sell, you can get price increment by [Query symbols endpoint](https://bybit-exchange.github.io/bybit-official-api-docs/en/index.html#operation/query_symbol).

>Customize conditional order ID: You may customize order IDs for active orders. We will link it to the system order ID , and return the unique system order ID to you after the active order is created successfully. You may use this order ID to cancel your active order. The customized order ID is asked to be unique, with a maximum length of 36 characters.

>Notes:
>* Each account can hold up to 500 active orders yet to be filled entirely simultaneously.
>* 'order_status' values explained:
>    * 'Created' indicates the order has been accepted by the system but not yet entered into the orderbook
>    * 'New' indicates the order has entered into the orderbook.

#### HTTP Request

> POST  `/v2/private/order/create`

#### Request Parameters

|parameter|required|type|comments|
|:----- |:-------|:-----|----- |
|side |true |string |Side    |
|symbol |true |string |Contract type.    |
|order_type |true |string |Active order type   |
|qty |true |integer |Order quantity. |
|price |false |number |Order price. Required if you make limit price order |
|time_in_force |true |string |Time in force |
|take_profit |false |number |take profit price|
|stop_loss |false |number |stop loss price|
|reduce_only |false |bool |reduce only
|close_on_trigger |false |bool |close on trigger. When creating closing order, highly recommend to set as `true` to avoid failing by insufficient avaliable margin|
|order_link_id |false |string |Customized order ID, maximum length at 36 characters, and order ID under the same agency has to be unique.|

#### Response example

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
            "order_status": "New",
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
        "rate_limit_reset_ms": 1575111823448,
        "rate_limit": 100
    }

```

-----------
## <span id="open-apiorderlistget">Get Active Order</span>
#### API Function

> Get my active order list

> Order creation/cancellation is asynchronous.If you want real-time information about an order, you can call [Real-time query Active Order information](#v2-private-order)

#### HTTP Request

##### Method
> GET ```/open-api/order/list```


#### Request parameters

|parameters|required|type|comments|
|:----- |:-------|:-----|----- |
|order_id |false |string |Order ID |
|order_link_id |false |string |Customized order ID |
|symbol |false |string |Contract type. Default `BTCUSD`    |
|order |false |string |Sort orders by creation date   |
|page |false |integer |Page. Default getting first page data |
|limit |false |integer |Limit for data size per page, max size is 50. Default as showing 20 pieces of data per page |
|order_status |false |string | Query your orders for all statuses if 'order_status' is empty. If you want to query orders with specific statuses , you can pass the order_status split by ','.  

#### Response example

```js

   {
       'ret_code':0,
       'ret_msg':'ok',
       'ext_code':'',
       'result':{
           'data':[
               {
                   'order_id': 'string',       //Unique order ID
                   'user_id': 0,               //User ID
                   'symbol': 'string',         //Contract type
                   'side': 'string',           //Side
                   'order_type': 'string',     //Order type
                   'price': 0,                 //Order price
                   'qty': 0,                   //Order quantity
                   'time_in_force': 'string',  //Time in force
                   'order_status': 'string',   //Order status: Created: order created; Rejected: order rejected; New: order pending; PartiallyFilled: order filled partially; Filled: order filled fully, Cancelled: order cancelled
                   'last_exec_time': 0.000000 , //Last execution time
                   'last_exec_price': 0,       //Last execution price
                   'leaves_qty': 0,            //Remaining order quantity
                   'cum_exec_qty': 0,          //Accumulated execution quantity
                   'cum_exec_value': 0,        //Accumulated execution value
                   'cum_exec_fee': 0,          //Accumulated execution fee
                   'reject_reason': 'string',  //Reason for rejection
                   'order_link_id': 'string',  //Agency customized order ID
                   'created_at':'2018-10-15T04:12:19.000Z',
                   'updated_at':'2018-10-15T04:12:19.000Z',
               }
           ],
           'current_page': 1,
           'total': 1
       },
       'time_now':'1539781050.462841'
   }

```

-----------
## <span id="open-apiordercancelpost">Cancel Active Order</span>
#### API Function

> 'order_id' is required for cancelling active order. The unique 36 characters order ID was returned to you when the active order was created successfully.
> 'symbol' is highly recommend filled, Otherwise, there will be a small probability of failure.

>You may cancel active order that are unfilled and partially filled. Fully filled order cannot be cancelled.

#### HTTP Request

##### Method
> POST ```/open-api/order/cancel```

####  Request Parameters

|parameters|required|type|comments|
|:----- |:-------|:-----|----- |
|symbol |true |string |Contract type. |
|order_id |false |string |Your active order ID. The unique order ID returned to you when the corresponding active order was created. `Required` if not pass order_link_id|
|order_link_id |false |string |Agency customized order ID. `Required` if not pass order_id |


#### Response example

```js

   {
       'ret_code':0   //Error code - True
       'ret_msg':'ok' //Error message
       'ext_code':''  ,
       'result':{
           'order_id': 'string',              //Unique order ID
           'user_id': 0,                      //User ID
           'symbol': 'string',                //Contract type
           'side': 'string',                  //Side
           'order_type': 'string',            //Order type
           'price': 0,                        //Order price
           'qty': 0,                          //Order quantity
           'time_in_force': 'string',         //Time in force
           'order_status': 'string',          //Order status: Created: order created; Rejected: order rejected; New: order pending; PartiallyFilled: order filled partially; Filled: order filled fully, Cancelled: order cancelled
           'last_exec_time': 0.000000,        //Last execution time
           'last_exec_price': 0,              //Last execution price
           'leaves_qty': 0,                   //Remaining order quantity
           'cum_exec_qty': 0,                 //Accumulated execution quantity
           'cum_exec_value': 0,               //Accumulated execution value
           'cum_exec_fee': 0,                 //Accumulated execution fee
           'reject_reason': 'string',         //Reason for rejection
           'order_link_id': 'string',         //Agency customized order ID
           'created_at':'2018-10-15T04:12:19.000Z',
           'updated_at':'2018-10-15T04:12:19.000Z',
       },
       'time_now':'1539778407.210858',    //UTC timestamp
   }

```

-----------
## <span id="open-apiordercancelv2post">Cancel Active Order-V2</span>
#### API Function

> 'order_id' is required for cancelling active order. The unique 36 characters order ID was returned to you when the active order was created successfully.
> 'symbol' is highly recommend filled, Otherwise, there will be a small probability of failure.

>You may cancel active order that are unfilled and partially filled. Fully filled order cannot be cancelled.

#### HTTP Request

> POST  `/v2/private/order/cancel`

####  Request Parameters

|parameters|required|type|comments|
|:----- |:-------|:-----|----- |
|symbol |true |string | Contract type |
|order_id |false |string |Order Id。Required if without order_link_id|
|order_link_id |false |string |Order link id. Required if without order_id|


#### Response example

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
        "rate_limit_reset_ms": 1575112681807,
        "rate_limit": 100
    }

```

-----------
## <span id="open-apiordercancelallpost">Cancel All Active Orders</span>
#### API Function

> Cancel all active orders that are unfilled or partially filled. Fully filled orders cannot be cancelled.

> This endpoint's `rate_limit` will decrease by 10 per request


#### HTTP Request

> POST  `/v2/private/order/cancelAll`

#### Request Parameters

|parameter|required|type|comments|
|:----- |:-------|:-----|----- |
|symbol |true |string | Contract type |


#### Response example

```js


    {
        "ret_code": 0,      
        "ret_msg": "OK",    
        "ext_code": "",     
        "ext_info": "",
        "result": [
            {
                "clOrdID": "89a38056-80f1-45b2-89d3-4d8e3a203a79",  
                "user_id": 105008,                                  
                "symbol": "BTCUSD",                                
                "side": "Buy",                                      
                "order_type": "Limit",                              
                "price": "7693.5",                                  
                "qty": 1,                                           
                "time_in_force": "GoodTillCancel",                  
                "create_type": "CreateByUser",                     
                "cancel_type": "CancelByUser",                      
                "order_status": "",                                 
                "leaves_qty": 1,                                    
                "leaves_value": "0",                                
                "created_at": "2019-11-30T10:38:53.564428Z",        
                "updated_at": "2019-11-30T10:38:59.102589Z",        
                "cross_status": "PendingCancel",  // `PendingCancel` means the matching engine received the cancellation but there is no guarantee that the cancellation will be successful.
                "cross_seq": 387734027                              
            }
        ],
        "time_now": "1575110339.105675",
        "rate_limit_status": 98,
        "rate_limit_reset_ms": 1575110339100,
        "rate_limit": 100
    }

```

-----------

## <span id="open-apiorderreplacepost">Replace Order</span>
#### API Function

> Replace-order can modify your active order.

> 'order_id' and 'symbol' is required for finding an active order.'p_r_qty' and 'p_r_price 'are the modified price and quantity. If these two fields are not provided, nothing will be modified.

> Please note that only orders that are unfilled and partially filled can be modified by the replace-order api


#### HTTP Request

##### Method
> POST ```/open-api/order/replace```

####  Request Parameters

|parameters|required|type|comments|
|:----- |:-------|:-----|----- |
|order_id |true |string |Your active order ID. The unique order ID returned to you when the corresponding active order was created |
|symbol |true |string |Contract type. |
|p_r_qty |false |int |New order quantity. Do not pass this field if you don't want modify it. |
|p_r_price |false |number |New order price. Do not pass this field if you don't want modify it. |

#### Response example

```js

    {
    'ret_code':0   //Error code,
    'ret_msg':'ok' //Error message,
    'ext_code':'',
    'result':{
      'order_id': '89a38056-80f1-45b2-89d3-4d8e3a203a79'
    },
    'time_now':'1539778407.210858',    // UTC timestamp
    'rate_limit_status': 0,            // The remaining number of accesses in one minute
}
```

-----------

## <span id="v2-private-order">Query active order (real-time)</span>
#### API Function

> Query real-time active order information

#### HTTP Request

##### Method
> GET `/v2/private/order`


#### Request Parameters

|parameter|required|type|comments|
|:----- |:-------|:-----|----- |
|order_id |false |string | Your active order ID. The unique order ID returned to you when the corresponding active order was created. `Required` if not pass order_link_id. |
|order_link_id |false |string | Agency customized order ID. `Required` if not pass order_id .|
|symbol |true |string |Contract type |


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
## <span id="open-apistop-ordercreatepost">Place Conditional Order</span>
#### API Function

>Parameters of 'side', 'symbol', 'order_type', 'qty', 'price', 'base_price', 'stop_px', 'time_in_force' are required for all active orders. Other parameters are optional unless specified.

>Market price conditional order: A traditional market price order, will be filled at the best available price. 'price' can set to be "" if and only if you are placing market price order.

>Limit price conditional order: You can set an execution price for your order. Only when last traded price reaches the order price, the system will fill your order.

>Take profit/Stop loss: You may only set a take-profit/stop-loss conditional order upon opening the position. Once you hold a position, the take profit and stop loss information u sent when placing an order will no longer be valid.

>Order quantity: This parameter indicates the quantity of perpetual contracts you want to buy or sell, currently Bybit only support order quantity in an integer.

>Order price: This parameter indicates the price of perpetual contracts you want to buy or sell, you can get price increment by [Query symbols endpoint](https://bybit-exchange.github.io/bybit-official-api-docs/en/index.html#operation/query_symbol).

>Conditional order trigger price: You may set a trigger price for your conditional order. conditional order will not enter the order book until the last price hits the trigger price. When last price hits trigger price: 1) your limit conditional order will enter order book, and wait to be executed; 2) your market conditional order will be executed immediately at the best available market price.

>Customize conditional order ID: You may customize order IDs for active orders. We will link it to the system order ID , and return the unique system order ID to you after the active order is created successfully. You may use this order ID to cancel your active order. The customized order ID is asked to be unique, with a maximum length of 36 characters.

>Note: Take profit/Stop loss is not supported in placing conditional orders. One can only use these 2 functions when placing active orders. Moreover, each account can hold up to 10 conditional orders yet to be filled entirely simultaneously.

#### HTTP Request

##### Method
> POST ```/open-api/stop-order/create```

#### Request Parameters


 |parameter|required|type|comments|
|:----- |:-------|:-----|----- |
|side |true |string |Side.    |
|symbol |true |string |Contract type.    |
|order_type |true |string |Conditional order type. |
|qty |true |integer |Order quantity. |
|price|false | number | Execution price for conditional order. Required if you make limit price order|
|base_price |true |number | It will be used to compare with the value of 'stop_px', to decide whether your conditional order will be triggered by crossing trigger price from upper side or lower side. Mainly used to identify the expected direction of the current conditional order. |
|stop_px | true | number | Trigger price |
|time_in_force |true |string |Time in force |
|trigger_by | false | string | Trigger price type. Default `LastPrice` |
|close_on_trigger |false |bool |close on trigger. When creating closing order, highly recommend to set as `true` to avoid failing by insufficient avaliable margin|
|order_link_id |false |string |Customized order ID, maximum length at 36 characters, and order ID under the same agency has to be unique.|


#### Response example

```js

   {
       'ret_code':0   //Error code - True
       'ret_msg':'ok' //Error message
       'ext_code':''  ,
       'result':{
           'stop_order_id': 'string',         //Unique order ID
           'user_id': 0,                      //User ID
           'stop_order_status': 'string',     //Order status: Untriggered: order waits to be triggered; Triggered: order is triggered; Cancelled: order is cancelled, Active: order is triggered and placed successfully; Rejected: Order is triggered but fail to be placed
           'symbol': 'string',                //Contract type
           'side': 'string',                  //Side
           'order_type': 'string',            //Price type
           'price': 0,                        //Order price
           'qty': 0,                          //Order quantity
           'time_in_force': 'string',         //Time in force
           'stop_order_type': 'string',       //Order type
           'base_price': 0,                   //
           'stop_px': 0,                      //trigger price
           'order_link_id': 'string',         //Agency customized order ID
           'created_at':'2018-10-15T04:12:19.000Z',
           'updated_at':'2018-10-15T04:12:19.000Z',
       },
       'time_now':'1539778407.210858',    //UTC timestamp
   }

```

-----------
## <span id="open-apistop-orderlistget">Get Conditional Order</span>
#### API Function

> Get my conditional order list。

#### HTTP Request

##### Method
> GET ```/open-api/stop-order/list```

#### Request Parameters

|parameter|required|type|comments|
|:----- |:-------|:-----|----- |
|stop_order_id |false |string |Order ID of conditional order|
|order_link_id |false |string |Agency customized order ID|
|symbol |false |string |Contract type. Default `BTCUSD`    |
|stop_order_status |false |string |stop order status   |
|order |false |string |Sort orders by creation date   |
|page |false |integer |Page. Default getting first page data |
|limit |false |integer |Limit for data size per page, max size is 50. Default as showing 20 pieces of data per page |


#### Response example

```js

   {
       'ret_code':0,
       'ret_msg':'ok',
       'ext_code':'',
       'result':{
           'data':[
               {
                   'stop_order_id': 'string',         //Unique order ID
                   'user_id': 0,                      //User ID
                   'stop_order_status': 'string',     //Order status: Untriggered: Pending order waits to be triggered; Triggered: order is triggered; Cancelled: order is cancelled, Active: order is triggered and placed successfully; Rejected: Order is triggered but fail to be placed
                   'symbol': 'string',                //Contract type
                   'side': 'string',                  //Side
                   'order_type': 'string',            //Price type
                   'price': 0,                        //Order price
                   'qty': 0,                          //Order quantity
                   'time_in_force': 'string',         //Time in force
                   'stop_order_type': 'string',       //Order type
                   'base_price': 0,                   //
                   'stop_px': 0,                      //trigger price
                   'order_link_id': 'string',         //Agency customized order ID
                   'created_at':'2018-10-15T04:12:19.000Z',
                   'updated_at':'2018-10-15T04:12:19.000Z',
               }
           ],
           'current_page': 1,
           'total': 1
       },
       'time_now':'1539781050.462841'
   }
```

-----------
## <span id="open-apistop-ordercancelpost">Cancel Conditional Order </span>
#### API Function


>'stop_order_id' is required for cancelling conditional order. The unique 36 characters order ID was returned to you when the condional order was created successfully.

>You may cancel all untriggered conditional orders. Essentially, after a conditional order is triggered, it will become an active order. So, when a conditional order is triggered, cancellation has to be done through the active order port for all unfilled or partial filled active order. Similarly, order that has been fully filled cannot be cancelled.

#### HTTP Request

##### Method
> POST ```/open-api/stop-order/cancel```

#### Request Parameters

|parameter|required|type | comments|
|:----- |:-------|:-----|----- |
|symbol |true |string |Contract type|
|stop_order_id |false |string | Order ID. The unique order ID returned to you when the corresponding order was created. `Required` if not pass order_link_id|
|order_link_id |false |string | Agency customized order ID. `Required` if not pass stop_order_id|

#### Response example

```js

   {
       'ret_code':0   //Error code - True
       'ret_msg':'ok' //Error message
       'ext_code':''  ,
       'result':{
           'stop_order_id': 'string',         //Unique order ID
           'user_id': 0,                      //User ID
           'stop_order_status': 'string',     //Order status: Untriggered: order waits to be triggered; Triggered: order is triggered; Cancelled: order is cancelled, Active: order is triggered and placed successfully; Rejected: Order is triggered but fail to be placed
           'symbol': 'string',                //Contract type
           'side': 'string',                  //Side
           'order_type': 'string',            //Price type
           'price': 0,                        //Order price
           'qty': 0,                          //Order quantity
           'time_in_force': 'string',         //Time in force
           'stop_order_type': 'string',       //Order type
           'base_price': 0,                   //
           'stop_px': 0,                      //trigger price
           'order_link_id': 'string',         //Agency customized order ID
           'created_at':'2018-10-15T04:12:19.000Z',
           'updated_at':'2018-10-15T04:12:19.000Z',
       },
       'time_now':'1539778407.210858',    //UTC timestamp
   }

```

-----------
## <span id="open-apistop-ordercancelallpost">Cancel All Conditional Orders</span>
#### API Function

> Cancel all untriggered conditional orders.

> This endpoint's `rate_limit` will decrease by 10 per request


#### HTTP Request

> POST  `/v2/private/stop-order/cancelAll`

#### Request Parameters

|parameter|required|type | comments|
|:----- |:-------|:-----|----- |
|symbol |true |string |Contract type|


#### Response example

```js

    {
        "ret_code": 0,
        "ret_msg": "OK",
        "ext_code": "",
        "ext_info": "",
        "result": [
            {
                "clOrdID": "041e523d-2376-42c7-9998-252a5fff9e75",  
                "user_id": 105008,                                  
                "symbol": "BTCUSD",                                 
                "side": "Buy",                                     
                "order_type": "Limit",                            
                "price": "7694.5",                                 
                "qty": 1,                                           
                "time_in_force": "GoodTillCancel",                  
                "create_type": "CreateByUser",
                "cancel_type": "CancelByUser",                                           
                "order_status": "",                                 
                "leaves_qty": 1,                                    
                "leaves_value": "0",
                "created_at": "2019-11-30T10:49:48.139157Z",        
                "updated_at": "2019-11-30T10:49:57.646802Z",       
                "cross_status": "Deactivated",  // `Deactivated` means the conditional order was cancelled before triggering
                "cross_seq": -1,                                    
                "stop_order_type": "Stop",                          
                "trigger_by": "LastPrice",                          
                "base_price": "7689.5",                             
                "expected_direction": "Rising"                      
            }
        ],
        "time_now": "1575110997.668109",
        "rate_limit_status": 99,
        "rate_limit_reset_ms": 1575110997643,
        "rate_limit": 100
    }

```

-----------


## <span id="open-apistop-orderreplacepost">Replace conditional order</span>
#### API Function

> Replace conditional order can modify your conditional order.

> 'p_r_qty', 'p_r_price' and 'p_r_trigger_price' will be set to your new conditional order. If these fields are not provided, nothing will be modified.

> Please note that you can only modify untriggered conditional order.


#### HTTP Request

##### Method
> POST ```/open-api/stop-order/replace```

####  Request Parameters

|parameters|required|type|comments|
|:----- |:-------|:-----|----- |
|order_id |true |string |**Abandoned!** Alias for `stop_order_id` |
|stop_order_id |true |string |Your stop order ID. The unique order ID returned to you when the corresponding conditional order was created |
|symbol |true |string |Contract type. |
|p_r_qty |false |int |New conditional order's quantity |
|p_r_price |false |number |New conditional order's price |
|p_r_trigger_price |false |number |New conditional order's tirgger price |

#### Response example

```js

    {
    'ret_code':0   //Error code,
    'ret_msg':'ok' //Error message,
    'ext_code':'',
    'result':{
      'stop_order_id':'041e523d-2376-42c7-9998-252a5fff9e75'
    },
    'time_now':'1539778407.210858',    // UTC timestamp
    'rate_limit_status': 0,            // The remaining number of accesses in one minute
}

```

-----------

## <span id="v2-private-stop-order">Query stop order (real-time)</span>
#### API Function

> Query real-time stop order information

#### HTTP Request

##### Method
> GET `/v2/private/stop-order`


#### Request Parameters

|parameter|required|type|comments|
|:----- |:-------|:-----|----- |
|stop_order_id |false |string | Your stop order ID. The unique order ID returned to you when the corresponding active order was created. `Required` if not pass order_link_id. |
|order_link_id |false |string | Agency customized order ID. `Required` if not pass order_id.|
|symbol |true |string |Contract type |


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
	    "order_link_id": "",
	    "created_at": "2019-10-21T07:28:19.396246Z",
	    "updated_at": "2019-10-21T07:28:19.396246Z",
	    "order_id": "efa44157-c355-4a98-b6d6-1d846a936b93"
	  },
	  "time_now": "1571651135.291930"
	}

```

-----------
## <span id="userleverageget">User Leverage</span>
#### API Function

> Get user leverage

#### HTTP Request

##### Method
> GET ```/user/leverage```

#### Request Parameters

|parameter|required|type|comments|
|:----- |:-------|:-----|----- |


#### Response example

```js

{
    'ret_code': 0,    // return code (0: successful, -1: failed)
    'ret_msg': 'ok',  // error message
    'ext_code': '',   // error code
    'result': {
        'BTCUSD': {
            'leverage': 1
        },
        'EOSUSD': {
            'leverage': 1
        },
        'ETHUSD': {
            'leverage': 1
        },
        'XRPUSD': {
            'leverage': 1
        }
    },
    'ext_info': null,
    'time_now': '1567608910.732004',  // UTC timestamp
    'rate_limit_status': 74
}

```

-----------
## <span id="userleveragesavepost"> Change User Leverage</span>
#### API Function

> Change user leverage
> Note that your position mode will be changed to Isolated Margin mode if you change your leverage from 0 to any other value

#### HTTP Request

##### Method
> POST ```/user/leverage/save```

#### Request Parameters

|parameter|required|type|comments|
|:----- |:-------|:-----|----- |
|symbol |true |string |Contract type    |
|leverage |true |string |Leverage. `0` means Cross Margin mode - any other value means Isolated Margin mode` |


####  Response example

```js

{
   'ret_code':0   //return code (0: successful, -1: failed)
   'ret_msg':'ok' //error message,
   'ext_code':''  //error code,
   'result': null, //One can decide whether a request is successful depending on ret_code. Will always return 'null'
   'time_now':'1539778407.210858',    //UTC timestamp
}

```

-----------
## <span id="positionlistget"> My Position</span>
#### API Function

> Get my position list

#### HTTP Request

##### Method
> GET ```/position/list```

#### Request Parameters

|parameter|required|type|comments|
|:----- |:-------|:-----|----- |


#### Response example

```js

{
   'ret_code': 0,    //return code (0: successful, -1: failed)
   'ret_msg': 'ok',  //error message
   'ext_code': '',   //error code
   'result': [
       {
           'id': 1,                //position ID
           'user_id': 1,           //user ID
           'risk_id': 1,           //risk limit ID
           'symbol': 'BTCUSD',     //Contract type
           'side': 'None',         //position Side  (None, buy, sell)
           'size': 0,              //position size
           'position_value': 0,    //position value
           'entry_price': 0,       //entry price
           'leverage': 1,          //user leverage
           'auto_add_margin': 0,   //1 means Cross Margin mode, 0 means Isolated Margin mode
           'position_margin': 0,   //position margin
           'liq_price': 999999,    //liquidation price
           'bust_price': 999999,   //bankruptcy price
           'occ_closing_fee': 0,   //position closing
           'occ_funding_fee': 0,   //funding fee
           'take_profit': 0,       //take profit price
           'stop_loss': 0,         //stop loss price
           'trailing_stop': 0,     //trailing stop point
           'position_status': 'Normal',   //Status Normal (normal), Liq (Liquidation in process), ADL (ADL in process)
           'deleverage_indicator': 1,
           'oc_calc_data': '{\'blq\':\'0\',\'bmp\':\'0\',\'slq\':\'0\',\'smp\':\'0\'}',
           'order_margin': 0,      //Used margin by order
           'wallet_balance': 0,    //wallet balance .When in Cross Margin mode, the number minus your unclosed loss is your real wallet balance.
           'unrealised_pnl': 0,    //unrealised profit and loss
           'realised_pnl': 0,      //daily realized profit and loss
           'cum_realised_pnl': 0,  //Total realized profit and loss
           'cum_commission': 0,    //Total commissions
           'cross_seq': 0,         //
           'position_seq': 2,      //position sequence number
           'created_at': '2018-10-18T07:15:51.000Z',
           'updated_at': '2018-10-20T13:43:21.000Z'
       }
   ],
   'time_now': '1540043097.995523'      //UTC timestamp
}
*    
```

-----------
## <span id="positionlistv2get"> My Position-V2</span>
#### API Function

> Get my position list

#### HTTP Request

##### Method
> GET ```/v2/private/position/list```

#### Request Parameters

|parameter|required|type|comments|
|:----- |:-------|:-----|----- |
|symbol |true |string |Contract type    |

#### Response example

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
    "rate_limit_reset_ms": 1576649493866,
    "rate_limit": 120
}  
```

-----------
## <span id="positionchange-position-marginpost"> Change Position Margin</span>
#### API Function

> Update margin

***Note that you can't change margin when your position is in Cross Margin mode***

#### HTTP Request

##### Method
> POST ```/position/change-position-margin```

#### Request Parameters

|parameter|required|type|comments|
|:----- |:-------|:-----|----- |
|symbol |true |string |Contract type    |
|margin |true |string |margin  |


#### Response example

```js

{
   'ret_code':0   //return code (0: successful, -1: failed)
   'ret_msg':'ok' //error message
   'ext_code':'', //error code
   'result': null,  //One can decide whether a request is successful depending on ret_code. Will always return 'null'
   'time_now':'1539778407.210858',    //UTC timestamp
}

```

-----------
## <span id="position-settradingstoppost"> Set Trading-Stop</span>
#### API Function

> Set Trading-Stop Condition

#### HTTP Request

##### Method
> POST ```/open-api/position/trading-stop```

#### Request Parameters

|parameter|required|type|comments|
|:----- |:-------|:-----|----- |
|symbol |true |string |Contract type |
|take_profit |false |string |Not less than 0, 0 means cancel TP |
|stop_loss |false |string |Not less than 0, 0 means cancel SL |
|trailing_stop |false |string |Not less than 0, 0 means cancel TS |


#### Response example

```js

{
  "ret_code": 0,
  "ret_msg": "ok",
  "ext_code": "",
  "result": {
           'id': 1,                //position ID
           'user_id': 1,           //user ID
           'risk_id': 1,           //risk limit ID
           'symbol': 'BTCUSD',     //Contract type
           'side': 'None',         //position Side  (None, buy, sell)
           'size': 0,              //position size
           'position_value': 0,    //position value
           'entry_price': 0,       //entry price
           'leverage': 1,          //user leverage
           'auto_add_margin': 0,   //1 means Cross Margin mode, 0 means Isolated Margin mode
           'position_margin': 0,   //position margin
           'liq_price': 999999,    //liquidation price
           'bust_price': 999999,   //bankruptcy price
           'occ_closing_fee': 0,   //position closing
           'occ_funding_fee': 0,   //funding fee
           'take_profit': 0,       //take profit price
           'stop_loss': 0,         //stop loss price
           'trailing_stop': 0,     //trailing stop point
           'position_status': 'Normal',   //Status Normal (normal), Liq (Liquidation in process), ADL (ADL in process)
           'deleverage_indicator': 1,
           'oc_calc_data': '{\'blq\':\'0\',\'bmp\':\'0\',\'slq\':\'0\',\'smp\':\'0\'}',
           'order_margin': 0,      //Used margin by order
           'wallet_balance': 0,    //wallet balance. When in Cross Margin mod, the number minus your unclosed loss is your real wallet balance.
           'unrealised_pnl': 0,    //unrealised profit and loss
           'realised_pnl': 0,      //daily realized profit and loss
           'cum_realised_pnl': 0,  //Total realized profit and loss
           'cum_commission': 0,    //Total commissions
           'cross_seq': 0,         //
           'position_seq': 2,      //position sequence number
           'created_at': '2018-10-18T07:15:51.000Z',
           'updated_at': '2018-10-20T13:43:21.000Z'
       },
  "time_now": "1569304018.857490"
}

```

-----------
## <span id="wallet-fundrecordget"> Get wallet fund records</span>
#### API Function

> Get wallet fund records

#### HTTP Request

##### Method
> GET ```/open-api/wallet/fund/records```

#### Request Parameters

|parameter|required|type|comments|
|:----- |:-------|:-----|----- |
|start_date |false |string |Start point for result  |
|end_date |false |string |End point for result  |
|currency |false |string |Currency type |
|coin |false |string |`currency` alias |
|wallet_fund_type |false |string |Wallet fund type |
|page |false |integer |Page. Default getting first page data |
|limit |false |integer |Limit for data size per page, max size is 50. Default as showing 20 pieces of data per page |


#### Response example

```js

{
  "ret_code": 0,                            //Error code 0 means success
  "ret_msg": "ok",                          //Error message
  "ext_code": "",
  "result": {
    "data": [{
      "id": 128495,                         //id
      "user_id": 103669,                    //user id
      "coin": "XRP",                        //coin type
      "wallet_id": 14760,                   //wallet id
      "type": "Realized P&L",               //funding type
      "amount": "1.18826225",
      "tx_id": "",
      "address": "XRPUSD",                  //address
      "wallet_balance": "999.12908894",     //balance
      "exec_time": "2019-09-25T00:00:15.000Z",
      "cross_seq": 0
    }]
  },
  "time_now": "1569395810.140869"
}

```

-----------
## <span id="wallet-withdrawrecordget"> Get withdraw records</span>
#### API Function

> Get withdraw records

#### HTTP Request

##### Method
> GET ```/open-api/wallet/withdraw/list```

#### Request Parameters

|parameter|required|type|comments|
|:----- |:-------|:-----|----- |
|start_date |false |string |Start point for result |
|end_date |false |string |End point for result |
|coin |false |string |Currency |
|status |false |string |Withdraw status |
|page |false |integer |Page. Default getting first page data |
|limit |false |integer |Limit for data size per page, max size is 50. Default as showing 20 pieces of data per page |


#### Response example

```js
{
  "ret_code": 0,                                        //Error code 0 means success
  "ret_msg": "ok",                                      //error message
  "ext_code": "",
  "result": {
    "data": [{
      "id": 137,                                        //id
      "user_id": 160249,                                //user id
      "coin": "XRP",                                    //coin type
      "status": "Pending",                              //status
      "amount": "20.00000000",                          //amount
      "fee": "0.25000000",
      "address": "rH7H595XYEVTEHU2FySYsWnmfACBnZS9zM",
      "tx_id": "",
      "submited_at": "2019-06-11T02:20:24.000Z",
      "updated_at": "2019-06-11T02:20:24.000Z"
    }]
  },
  "ext_info": null,
  "time_now": "1570863984.536136"
}

```



## <span id="open-apiwalletbalanceget">Get Wallet Balance </span>
#### API Function

> get wallet balance info

#### HTTP Request

##### Method
> GET   /v2/private/wallet/balance

#### Request Parameters

|parameter|required|type|comments|
|:----- |:-------|:-----|----- |
|coin |true |BTC,EOS,XRP,ETH,USDT |coin |

#### Response example

```js

{
    "ret_code": 0,
    "ret_msg": "OK",
    "ext_code": "",
    "ext_info": "",
    "result": {
        "BTC": {
            "equity": 1002,                         //equity = wallet_balance + unrealised_pnl
            "available_balance": 999.99987471,      //available_balance
            //In Isolated Margin Mode， available_balance = wallet_balance - (position_margin + occ_closing_fee + occ_funding_fee + order_margin)
            //In Cross Margin Mode，if unrealised_pnl > 0, available_balance = wallet_balance - (position_margin + occ_closing_fee + occ_funding_fee + order_margin)；otherwise，available_balance = wallet_balance - (position_margin + occ_closing_fee + occ_funding_fee + order_margin) + unrealised_pnl
            "used_margin": 0.00012529,              //used_margin = wallet_balance - available_balance
            "order_margin": 0.00012529,             //Used margin by order
            "position_margin": 0,                   //position margin
            "occ_closing_fee": 0,                   //position closing fee
            "occ_funding_fee": 0,                   //funding fee
            "wallet_balance": 1000,                 //wallet balance. When in Cross Margin mod, the number minus your unclosed loss is your real wallet balance.
            "realised_pnl": 0,                      //daily realized profit and loss
            "unrealised_pnl": 2,                    //unrealised profit and loss
                //  when side is sell, unrealised_pnl = size * (1.0 / mark_price -  1.0 / entry_price）
                //  when side is buy,  unrealised_pnl = size * (1.0 / entry_price -  1.0 / mark_price）
            "cum_realised_pnl": 0,                  //total relised profit and loss
            "given_cash": 0,                        //given_cash
            "service_cash": 0                       //service_cash
        }
    },
    "time_now": "1578284274.816029"
}

```


-----------
## <span id="wallet-setrisklimit">Set risk limit </span>
#### API Function

> Set risk limit

#### HTTP Request

##### Method
> POST `/open-api/wallet/risk-limit`

#### Request Parameters

|parameter|required|type|comments|
|:----- |:-------|:-----|----- |
|symbol |true |string |symbol |
|risk_id |true |integer |risk ID. Can be found with the <a href="#wallet-getrisklimit">Get risk limit list</a> endpoint  |



#### Response example

```js

{
  "ret_code": 0,
  "ret_msg": "ok",
  "ext_code": "",
  "result": {
    "position": {
      "id": 1,
      "user_id": 1,
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
## <span id="wallet-getrisklimit">Get risk limit list </span>
#### API Function

> Get risk limit list

#### HTTP Request

##### Method
> GET `/open-api/wallet/risk-limit/list`

#### Request Parameters

|parameter|required|type|comments|
|:----- |:-------|:-----|----- |



#### Response example

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
## <span id="lastfundingrate"> Get the Last Funding Rate</span>
#### API Function

> Funding rate is generated every 8 hours at 00:00 UTC, 08:00 UTC and 16:00 UTC.
> If it's 12:00 UTC now, what you will get is the funding rate generated at 08:00 UTC.

#### HTTP Request

##### Method
> GET ```/open-api/funding/prev-funding-rate```

#### Request Parameters

|parameter|required|type|comments|
|:----- |:-------|:-----|----- |
|symbol |true |string |Contract type    |


#### Response example

```js

{
    'ret_code':0   // return code (0: successful. -101: Parameters verification failed)
    'ret_msg':'ok' // error message
    'ext_code':'', // additional error code
    'result': {
        'symbol':'BTCUSD',
        'funding_rate':'0.00375000', // When the funding rate is positive, longs pay shorts. When it is negative, shorts pay longs.
        'funding_rate_timestamp':1539950401 // The time of funding rate generation, UTC timestamp
    },
    'time_now':'1539778407.210858',    // UTC timestamp
}

```


-----------
## <span id="userlastfundingfee"> Get My Last Funding Fee</span>
#### API Function

> Funding settlement occurs every 8 hours at 00:00 UTC, 08:00 UTC and 16:00 UTC.
> The current interval's fund fee settlement is based on the previous interval's fund rate.
> For example, at 16:00, the settlement is based on the fund rate generated at 8:00.
> The fund rate generated at 16:00 will be used at 0:00 on the next day.

#### HTTP Request

##### Method
> GET ```/open-api/funding/prev-funding```

#### Request Parameters

|parameter|required|type|comments|
|:----- |:-------|:-----|----- |
|symbol |true |string |Contract type    |


#### Response example

```js

{
    'ret_code':0   // return code (0: successful, -101: Parameters verification failed)
    'ret_msg':'ok' // error message
    'ext_code':'', // additional error code
    'result': {
        'symbol':'BTCUSD',
        'side': 'Buy', // Your position side at the time of settlement
        'size': 10,   // Your position size at the time of settlement
        'funding_rate':'0.00375000', // Funding rate for settlement. When the funding rate is positive, longs pay shorts. When it is negative, shorts pay longs.
        'exec_fee': 0.00000116, // Funding fee.  
        'exec_timestamp': 1539950401, // The time of funding settlement occurred, UTC timestamp
    },
    'time_now':'1539778407.210858',    // UTC timestamp
    'rate_limit_status':10, // The number of remaining calls for this type of API in the current period (1 min).
}

```

-----------
## <span id="open-apifundingpredicted-fundingget">Get Predicted Funding Rate and Funding Fee</span>
#### API Function

> Get predicted funding rate and funding fee

#### HTTP Request

##### Method
> GET ```/open-api/funding/predicted-funding```

#### Request Parameters

|parameter|required|type|comments|
|:----- |:-------|:-----|----- |
|symbol |true |string |Contract type    |


#### Response example

```js

{
    'ret_code':0   // return code (0: successful, -101: Parameters verification failed)
    'ret_msg':'ok' // error message
    'ext_code':'', // additional error code
    'result': {
        'predicted_funding_rate': 0.001, // predicted funding rate. When the funding rate is positive, longs pay shorts. When it is negative, shorts pay longs.
        'predicted_funding_fee': 0.000234 // predicted funding fee
    },
    'time_now':'1539778407.210858',    // UTC timestamp
}

```


 -----------
## <span id="open-apiexecutionrecordslistget">Get user's trade records</span>
#### API Function

> Get user's trade records

#### HTTP Request

##### Method
> GET ```/v2/private/execution/list```

#### Request parameters

|parameter|required|type|comments|
|:----- |:-------|:-----|----- |
|order_id |false |string |OrderID. If not provided, will return user's trading records |
|symbol |false |string |Contract type. If `order_id` not provided, `symbol` is required |
|start_time |false |int |Start timestamp point for result |
|page |false |integer |Page. Default getting first page data |
|limit |false |integer |Limit for data size per page, max size is 50. Default as showing 20 pieces of data per page |

#### Response example

```js

{
    'ret_code': 0,                                        // return code
    'ret_msg': 'OK',                                      // error message
    'ext_code': '',                                       // additional error code
    'ext_info': '',                                       // additional error info
    'result': {
        'order_id': '',   // always empty
        'trade_list': [{
            'closed_size': 0,                                // Closed size
            'cross_seq': 3154097,                            // CrossSeq
            'exec_fee': '-0.00000005',                       // Execution fee
            'exec_id': 'b3551383-19b1-4aa6-8ac2-f996bea6e07c', // Unique exec ID
            'exec_price': '4202',                              // Exec Price
            'exec_qty': 1,                                   // Exec Qty
            'exec_time': '1545203567',                       // Exec time
            'exec_type': 'Trade',                            // Exec type -- Trade: normal  Funding: funding  AdlTrade：ADL  BustTrade:  liquidation trade
            'exec_value': '0.00023798',                      // Exec value
            'fee_rate': '-0.00025',                          // Fee rate
            'last_liquidity_ind': 'AddedLiquidity',          // AddedLiquidity/RemovedLiquidity
            'leaves_qty': 0,                                 // Leave Qty
            'nth_fill': 7,                                   // Nth Fill
            'order_id': 'd854bb13-3fb9-4608-ade4-828f50210778', // Unique order ID
            'order_price': '4202',                           // Order's price
            'order_qty': 1,                                  // Order's qty
            'order_type': 'Limit',                           // Order's type
            'side': 'Sell',                                  // Side
            'symbol': 'BTCUSD',                              // Symbol
            'user_id': 155446                                // UserID
        }]
    },
    'time_now': '1551340186.761136'
}

```

-------
## <span id="orderbook-L2">Get Orderbook</span>
#### API Function

> Get the orderbook

> Response is in the snapshot format

#### HTTP Request

##### Method
> GET ```/v2/public/orderBook/L2```

#### Request parameters

|parameters|required|type|comments|
|:----- |:-------|:-----|----- |
|symbol |true |string |Contract type |

#### Response example

```js

{
    "ret_code": 0,                              // return code
    "ret_msg": "OK",                            // error message
    "ext_code": "",                             // additional error code
    "ext_info": "",                             // additional error info
    "result": [
        {
            "symbol": "BTCUSD",                 // symbol
            "price": "9487",                    // price
            "size": 336241,                     // size (in USD contracts)
            "side": "Buy"                       // side
        },
        {
            "symbol": "BTCUSD",                 // symbol
            "price": "9487.5",                  // price
            "size": 522147,                     // size (in USD contracts)
            "side": "Sell"                      // side
        }
    ],
    "time_now": "1567108756.834357"             // UTC timestamp
}

```

-------
## <span id="latest-information-for-symbol">Latest information for symbol</span>
#### API Function

> Get the latest information for symbol

#### HTTP Request

##### Method
> GET ```/v2/public/tickers```

#### Request parameters

|parameters|required|type|comments|
|:----- |:-------|:-----|----- |
|symbol |false |string |Contract type |

#### Response example

```js

// other symbols omitted - the normal response will have additional dictionaries within the "result" class detailing the
// different symbols
{
    "ret_code": 0,                                   // return code
    "ret_msg": "OK",                                 // error message
    "ext_code": "",                                  // additional error code
    "ext_info": "",                                  // additional error info
    "result": [
        {
            "symbol": "BTCUSD",                             // instrument name
            "bid_price": "9499.5",                          // the bid price
            "ask_price": "9500",                            // the ask price
            "last_price": "9499.50",                        // the latest price
            "last_tick_direction": "ZeroMinusTick",         // the direction of last tick:PlusTick,ZeroPlusTick,MinusTick,ZeroMinusTick
            "prev_price_24h": "9659.00",                    // the price of prev 24h
            "price_24h_pcnt": "-0.02",                      // the current last price percentage change from prev 24h price
            "high_price_24h": "9737.00",                    // the highest price of prev 24h
            "low_price_24h": "9322.50",                     // the lowest price of prev 24h
            "prev_price_1h": "9469.00",                     // the price of prev 1h
            "price_1h_pcnt": "0.00",                        // the current last price percentage change from prev 1h price
            "mark_price": "9509.24",                        // mark price
            "index_price": "9509.00",                       // index price
            "open_interest": 78923133,                      // open interest quantity - updates every minute (updates may be more frequent than every 1 minute)
            "open_value": "8078.86",                        // open value quantity - updates every minute (updates may be more frequent than every 1 minute)
            "total_turnover": "6540981.84",                 // total turnover
            "turnover_24h": "59236.52",                     // 24h turnover
            "total_volume": 62971273761,                    // total volume
            "volume_24h": 564198332,                        // 24h volume
            "funding_rate": "0.00",                         // funding rate
            "predicted_funding_rate": "-0.00",              // predicted funding rate
            "next_funding_time": "2019-08-30T00:00:00Z",    // next funding time
            "countdown_hour": 4                             // the rest time to settle funding fee
        }
    ],
    "time_now": "1567109419.049271"
}

```

-----------
## <span id="trading-records">Get public trading records</span>
#### API Function

> Get recent trades

#### HTTP Request

##### Method

> GET `/v2/public/trading-records`

#### Request parameters

|parameters|required|type|comments|
|:----- |:-------|:-----|----- |
|symbol |true |string |Contract type |
|from |false |int |From id. Default returns latest data|
|limit |false |int |Number of result. Default 500; max 1000|



#### Response example

```js

{
    "ret_code": 0,                                   // error code 0 means success
    "ret_msg": "OK",                                 // error message
    "ext_code": "",                                  
    "ext_info": "",                                  
    "result": [
        {
            "id":7724919,                                   // ID
            "symbol": "BTCUSD",                             // contract type
            "price": 9499.5,                                // execution price
            "qty": 9500,                                    // execution quantity
            "side": "Buy",                                  // side
            "time": "2019-11-19T08:03:04.077Z",             // UTC time
        }
    ],
    "time_now": "1567109419.049271"
}

```

-------
## <span id="ENUMs">ENUM definitions</span>
> This is a list of valid options (and rules) for the different parameters when sending a request to the API
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
* `Deposit`
* `Withdraw`
* `RealisedPNL`
* `Commission`
* `Refund`
* `Prize`
* `ExchangeOrderWithdraw`
* `ExchangeOrderDeposit`

#### Withdraw status (`status`)
* `ToBeConfirmed`
* `UnderReview`
* `Pending` - Pending transfer
* `Success`
* `CancelByUser`
* `Reject`
* `Expire`


#### Order type (`order_type`)
* `Limit`
* `Market`

#### Quantity (`qty`)
* Maximum quantity of 1 million (`1000000`)
* Must be an integer - no decimals, only a whole number of USD contracts
  * `40` - allowed
  * `30.5` - illegal

#### Price (`price`)
* Active order
  * Must be an increment of that market's `tick_size`
    * Use modulo(`%`) to calculate whether or not a price will be accepted, like so:
      ```js
      IF price % tick_size = 0
        // send request
      ELSE
        // do not send request as the price will not be accepted by the system
      ```
    * Current symbol information (like tick sizes) can be found here: [https://api.bybit.com/v2/public/symbols](https://api.bybit.com/v2/public/symbols)
  * Must be less than 1 million (`1000000`)
  * If the user has no open position then the price must be greater than 10% of the market price
    * For example, if the current market price (last price) is `10314`, then the absolute minimum the price may be is `1031.5`. It may not be `1031` or below.
    * In pseudocode (assuming the price is an increment of 0.5):
      ```js
      IF price > (last_price * 0.1)
        // send request
      ELSE
        // do not send request as the price will not be accepted by the system
      ```
  * If the user holds a position, the order price must be better than the liquidation price.
    * For example, if the liquidation price of an open long position is `5176.5` then the price may be a minimum of `5177`. In the case of a short position the price must be less than the liquidation price.
* Conditional order
  * Must be equal to order greater than `1`

#### Time in force (`time_in_force`)
* `GoodTillCancel`
* `ImmediateOrCancel`
* `FillOrKill`
* `PostOnly`

#### Trigger price type (`trigger_by`)
* `LastPrice`
* `IndexPrice`
* `MarkPrice`

#### Order status (`order_status`)
* `Created`
* `New`
* `PartiallyFilled`
* `Filled`
* `Cancelled`
* `Rejected`

#### Order (`order`)
* __NOTE: currently broken for both get conditional order and get active order__
* This is for sorting the orders by creation date
* `desc` (default)
* `asc`

#### Order status (`order_status`)
* Filter fetched orders by their order statuses
* To filter by multiple statuses, separate with a comma like so: `Filled,New`
* `Created`
* `Rejected`
* `New`
* `PartiallyFilled`
* `Filled`
* `Cancelled`
* `PendingCancel` - The matching engine has received the cancellation but there is no guarantee that it will be successful
* `Deactivated` - The conditional order was cancelled before triggering

#### Cancel type (`cancel_type`)
* `CancelByUser`
* `CancelByReduceOnly`
* `CancelByPrepareLiq`,`CancelAllBeforeLiq` - Canceled by force liquidation
* `CancelByPrepareAdl`,`CancelAllBeforeAdl` - Canceled by ADL
* `CancelByAdmin`
* `CancelByTpSlTsClear` - Means this is a cancelled TP/SL order
* `CancelByPzSideCh` - Means this order is cancelled after TP/SL

#### Create type (`create_type`)
* `CreateByUser`
* `CreateByClosing`
* `CreateByAdminClosing`
* `CreateByStopOrder`
* `CreateByTakeProfit`
* `CreateByStopLoss`
* `CreateByTrailingStop`
* `CreateByLiq` - Created by partial liquidation
* `CreateByAdl_PassThrough` - Created by ADL
* `CreateByTakeOver_PassThrough` - Created by liquidation takeover.
