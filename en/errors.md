# NOTICE: These docs are now OBSOLETE; please find the new documentation [here](https://bybit-exchange.github.io/docs/inverse). Thank you.

# Errors codes and messages

Example error response:
```javascript
{
  'ret_code': 10001,
  'ret_msg': 'error in params'
}
```
Note: `[%s]` acts as a placeholder, usually for invalid values which are sent to the system that have been rejected. This helps show the user exactly what is wrong in their request.


## Authentication
### ERROR IN PARAMS
* ```'ret_code': 10001,```
* ```'ret_msg': 'error in params'```
### INVALID REQUEST
* ```'ret_code': 10002,```
* ```'ret_msg': 'invalid request, please check timestamp and recv_window'```
### INVALID API_KEY OR ILLEGAL IP
* ```'ret_code': 10003,```
* ```'ret_msg': 'invalid api_key or illegal IP'```
### SIGN ERROR
* ```'ret_code': 10004,```
* ```'ret_msg': 'sign error'```
### PERMISSION DENIED!
* ```'ret_code': 10005,```
* ```'ret_msg': 'permission denied'```
### REQUEST LIMIT EXCEEDED
* ```'ret_code': 10006,```
* ```'ret_msg': 'rate limit exceeded'```
### INVALID/UNMATCHED IP
* ```'ret_code': 10010,```
* ```'ret_msg': 'invalid IP, request IP: xx.xxx.xxx.x'```

## Order
### ORDER DOES NOT EXIST
* ```'ret_code': 20001,```
* ```'ret_msg': 'order does not exist'```
### SIDE IS REQUIRED
* ```'ret_code': 20003,```
* ```'ret_msg': 'missing param: side'```
### SIDE VALUE IS INVALID
* ```'ret_code': 20004,```
* ```'ret_msg': 'invalid value for param: side'```
### SYMBOL IS REQUIRED
* ```'ret_code': 20005,```
* ```'ret_msg': 'missing param: symbol'```
### SYMBOL VALUE IS INVALID
* ```'ret_code': 20006,```
* ```'ret_msg': 'invalid value for param: symbol'```
### ORDER_TYPE IS REQUIRED
* ```'ret_code': 20007,```
* ```'ret_msg': 'missing param: order_type'```
### ORDER_TYPE VALUE IS INVALID
* ```'ret_code': 20008,```
* ```'ret_msg': 'invalid value for param: order_type'```
### QTY IS REQUIRED
* ```'ret_code': 20009,```
* ```'ret_msg': 'missing param: qty'```
### QTY MUST BE GREATER THAN ZERO
* ```'ret_code': 20010,```
* ```'ret_msg': 'qty must be greater than zero'```
### QTY MUST BE AN INTEGER
* ```'ret_code': 20011,```
* ```'ret_msg': 'qty must be an integer'```
### QTY MUST BE BETWEEN 1 AND 1000000
* ```'ret_code': 20012,```
* ```'ret_msg': 'qty must be greater than zero and less than 1 million'```
### PRICE IS REQUIRED
* ```'ret_code': 20013,```
* ```'ret_msg': 'missing param: price'```
### PRICE MUST BE GREATER THAN ZERO
* ```'ret_code': 20014,```
* ```'ret_msg': 'price must be greater than zero'```
### TIME_IN_FORCE IS REQUIRED
* ```'ret_code': 20015,```
* ```'ret_msg': 'missing param: time_in_force'```
### TIME_IN_FORCE VALUE IS INVALID
* ```'ret_code': 20016,```
* ```'ret_msg': 'invalid value for param: time_in_force'```
### ORDER_ID IS REQUIRED
* ```'ret_code': 20017,```
* ```'ret_msg': 'missing param: order_id'```
### THE DATE FORMAT IS INVALID
* ```'ret_code': 20018,```
* ```'ret_msg': 'date format is invalid'```
### STOP_PX IS REQUIRED
* ```'ret_code': 20019,```
* ```'ret_msg': 'missing param: stop_px'```
### BASE_PRICE IS REQUIRED
* ```'ret_code': 20020,```
* ```'ret_msg': 'missing param: base_price'```
### STOP_ORDER_ID IS REQUIRED
* ```'ret_code': 20021,```
* ```'ret_msg': 'missing param: stop_order_id'```
### LEVERAGE IS REQUIRED
* ```'ret_code': 20022,```
* ```'ret_msg': 'missing param: leverage'```
### LEVERAGE MUST BE A NUMBER
* ```'ret_code': 20023,```
* ```'ret_msg': 'leverage must be a number'```
### LEVERAGE MUST BE GREATER THAN ZERO
* ```'ret_code': 20031,```
* ```'ret_msg': 'leverage must be greater than zero'```
### ORDER_ID OR ORDER_LINK_ID IS REQUIRED
* ```'ret_code': 20084,```
* ```'ret_msg': 'order_id or order_link_id is required'```
### ORDER_LINK_ID MUST BE UNIQUE
* ```'ret_code': 30001,```
* ```'ret_msg': 'invalid value for param: order_link_id sent: [%s]'```
### ALREADY HAVE ACTIVE EXIT ORDER
* ```'ret_code': 30002,```
* ```'ret_msg': 'already have active [%s] exit order'```
### THE NUMBER OF CONTRACTS IS TOO SMALL
* ```'ret_code': 30003,```
* ```'ret_msg': 'qty must be more than the minimum allowed'```
### THE NUMBER OF CONTRACTS IS TOO LARGE
* ```'ret_code': 30004,```
* ```'ret_msg': 'qty must be less than the maximum allowed'```
### ORDER PRICE IS OUT OF PERMISSIBLE RANGE
* ```'ret_code': 30005,```
* ```'ret_msg': 'price exceeds maximum allowed'```
### LAST_PRICE IS REQUIRED
* ```'ret_code': 30006,```
* ```'ret_msg': 'no last_price'```
### ORDER PRICE IS OUT OF PERMISSIBLE RANGE
* ```'ret_code': 30007,```
* ```'ret_msg': 'price exceeds minimum allowed'```
### ORDER_TYPE VALUE IS INVALID
* ```'ret_code': 30008,```
* ```'ret_msg': 'invalid value for param: order_type sent: [%s]'```
### NO POSITION FOR [%s], [%s] (eg UID, SYMBOL)
* ```'ret_code': 30009,```
* ```'ret_msg': 'no position for [%s], [%s]'```
### INSUFFICIENT WALLET BALANCE
* ```'ret_code': 30010,```
* ```'ret_msg': 'insufficient wallet balance'```
### OPERATION NOT ALLOWED AS POSITION IS UNDERGOING LIQUIDATION
* ```'ret_code': 30011,```
* ```'ret_msg': 'operation not allowed as position is undergoing liquidation'```
### OPERATION NOT ALLOWED AS POSITION IS UNDERGOING ADL
* ```'ret_code': 30012,```
* ```'ret_msg': 'operation not allowed as position is undergoing ADL'```
### POSITION IS IN OTHER STATUS
* ```'ret_code': 30013,```
* ```'ret_msg': 'position is in [%s] status'```
### INVALID EXIT ORDER: QTY SHOULD MATCH POSITION SIZE
* ```'ret_code': 30014,```
* ```'ret_msg': 'invalid exit order: qty != size'```
### INVALID EXIT ORDER: SIDE SHOULD BE OPPOSITE OF POSITION
* ```'ret_code': 30015,```
* ```'ret_msg': 'invalid exit order: side should be opposite'```
### CANCEL TAKE PROFIT AND STOP LOSS FIRST
* ```'ret_code': 30016,```
* ```'ret_msg': 'TS and SL must be cancelled first'```
### ESTIMATED FILL PRICE: [%s] CANNOT BE LOWER THAN CURRENT BUY LIQ_PRICE: [%s]
* ```'ret_code': 30017,```
* ```'ret_msg': 'estimated fill price: [%s] cannot be lower than current buy liq_price: [%s]'```
### ESTIMATED FILL PRICE: [%s] CANNOT BE HIGHER THAN CURRENT SELL LIQ_PRICE: {$POSITION->LIQ_PRICE}
* ```'ret_code': 30018,```
* ```'ret_msg': 'estimated fill price: [%s] cannot be higher than current sell liq_price: {$position-liq_price}'```
### CANNOT ATTACH TP/SL PARAMS TO NON-ZERO POSITION
* ```'ret_code': 30019,```
* ```'ret_msg': 'cannot attach TP/SL params for non-zero position'```
### POSITION ALREADY HAS TP/SL PARAMS
* ```'ret_code': 30020,```
* ```'ret_msg': 'position already has TP/SL params'```
### CANNOT AFFORD ESTIMATED POSITION_MARGIN: [%s]
* ```'ret_code': 30021,```
* ```'ret_msg': 'cannot afford estimated position_margin: [%s]'```
### ESTIMATED BUY LIQ_PRICE: [%s] CANNOT BE HIGHER THAN CURRENT MARK_PRICE: [%s]
* ```'ret_code': 30022,```
* ```'ret_msg': 'estimated buy liq_price: [%s] cannot be higher than current mark_price: [%s]'```
### ESTIMATED SELL LIQ_PRICE: [%s] CANNOT BE LOWER THAN CURRENT MARK_PRICE: [%s]
* ```'ret_code': 30023,```
* ```'ret_msg': 'estimated sell liq_price: [%s] cannot be lower than current mark_price: [%s]'```
### CANNOT SET [%s] FOR ZERO POSITION
* ```'ret_code': 30024,```
* ```'ret_msg': 'cannot set [%s] for zero position'```
### SHOULD BE BIGGER THAN 10% OF MARK PRICE AND LESS THAN 1000000
* ```'ret_code': 30025,```
* ```'ret_msg': '[%s]: [%s] < 10% of base: [%s]'```
### PRICE IS TOO HIGH
* ```'ret_code': 30026,```
* ```'ret_msg': 'trigger price [%s]: [%s] exceeds maximum allowed'```
### PRICE SET FOR TAKE PROFIT SHOULD BE HIGHER THAN LAST TRADED PRICE
* ```'ret_code': 30027,```
* ```'ret_msg': 'take profit price should be greater than last traded price'```
### PRICE SET FOR STOP LOSS SHOULD BE BETWEEN LIQUIDATION PRICE AND LAST TRADED PRICE
* ```'ret_code': 30028,```
* ```'ret_msg': 'stop loss price should be between liquidation price and last traded price'```
### PRICE SET FOR STOP LOSS SHOULD BE BETWEEN LAST TRADED PRICE AND LIQUIDATION PRICE
* ```'ret_code': 30029,```
* ```'ret_msg': 'stop loss price should be between last traded price and liquidation price'```
### PRICE SET FOR TAKE PROFIT SHOULD BE LOWER THAN LAST TRADED PRICE
* ```'ret_code': 30030,```
* ```'ret_msg': 'take profit price should be less than last traded price'```
### INSUFFICIENT AVAILABLE BALANCE: [%s] FOR ORDER COST: [%s]
* ```'ret_code': 30031,```
* ```'ret_msg': 'insufficient available balance: [%s] for order cost: [%s]'```
### ORDER HAS BEEN COMPLETED OR CANCELLED
* ```'ret_code': 30032,```
* ```'ret_msg': 'order has been finished or canceled'```
### THE NUMBER OF STOP ORDERS [%s] EXCEEDS MAXIMUM LIMIT ALLOWED
* ```'ret_code': 30033,```
* ```'ret_msg': 'the number of stop orders [%s] exceeds maximum limit allowed'```
### NO STOP ORDER FOR [%s]
* ```'ret_code': 30034,```
* ```'ret_msg': 'no stop order for [%s]'```
### CANCELLED TOO FAST
* ```'ret_code': 30035,```
* ```'ret_msg': 'too fast to cancel, please try again'```
### THE EXPECTED POSITION VALUE AFTER ORDER EXECUTION EXCEEDS THE CURRENT RISK LIMIT
* ```'ret_code': 30036,```
* ```'ret_msg': 'the expected position value after order execution exceeds the current risk limit'```
### ORDER ALREADY CANCELLED
* ```'ret_code': 30037,```
* ```'ret_msg': 'order already cancelled'```
### NO POSITION RECORD FOR [%s], [%s] (eg USER_ID, SYMBOL)
* ```'ret_code': 30041,```
* ```'ret_msg': 'no position record for [%s], [%s]'```
### INSUFFICIENT WALLET BALANCE
* ```'ret_code': 30042,```
* ```'ret_msg': 'insufficient wallet balance'```
### OPERATION NOT ALLOWED AS POSITION IS UNDERGOING LIQUIDATION
* ```'ret_code': 30043,```
* ```'ret_msg': 'operation not allowed as position is undergoing liquidation'```
### OPERATION NOT ALLOWED AS POSITION IS UNDERGOING ADL
* ```'ret_code': 30044,```
* ```'ret_msg': 'operation not allowed as position is undergoing ADL'```
### POSITION IS IN OTHER STATUS
* ```'ret_code': 30045,```
* ```'ret_msg': 'position is in [%s] status'```
### REQUESTED QUANTITY OF CONTRACTS EXCEEDS RISK LIMIT, PLEASE ADJUST YOUR RISK LIMIT LEVEL BEFORE TRYING AGAIN
* ```'ret_code': 30057,```
* ```'ret_msg': 'requested quantity of contracts exceeds risk limit, please adjust your risk limit level before trying again'```
### REDUCE-ONLY RULE NOT SATISFIED
* ```'ret_code': 30063,```
* ```'ret_msg': 'reduce-only rule not satisfied'```

## Position
### ORDER PRICE IS OUT OF PERMISSIBLE RANGE
* ```'ret_code': 30005,```
* ```'ret_msg': 'price exceeds maximum allowed'```
### LAST_PRICE IS REQUIRED
* ```'ret_code': 30006,```
* ```'ret_msg': 'no last_price'```
### LEVERAGE IS REQUIRED
* ```'ret_code': 20022,```
* ```'ret_msg': 'missing param: leverage'```
### LEVERAGE MUST BE NUMERIC
* ```'ret_code': 20023,```
* ```'ret_msg': 'leverage must be a number'```
### LEVERAGE MUST BE GREATER THAN ZERO
* ```'ret_code': 20031,```
* ```'ret_msg': 'leverage must be greater than zero'```
### MARGIN IS REQUIRED
* ```'ret_code': 20070,```
* ```'ret_msg': 'missing param: margin'```
### MARGIN MUST BE GREATER THAN ZERO
* ```'ret_code': 20071,```
* ```'ret_msg': 'margin must be greater than zero'```
### INSUFFICIENT AVAILABLE BALANCE
* ```'ret_code': 30049,```
* ```'ret_msg': 'insufficient available balance'```
### ANY ADJUSTMENTS MADE WILL TRIGGER IMMEDIATE LIQUIDATION
* ```'ret_code': 30050,```
* ```'ret_msg': 'any adjustments made will trigger immediate liquidation'```
### CANNOT SET LEVERAGE TO [%s] AS IT WOULD EXCEED YOUR RISK_LIMIT
* ```'ret_code': 30051,```
* ```'ret_msg': 'due to risk limit, cannot set leverage to [%s]'```
### CANNOT SET LEVERAGE TO [%s]
* ```'ret_code': 30052,```
* ```'ret_msg': 'cannot set leverage to [%s]'```
### FIXED_NEW_POSITION_MARGIN[%s] INVALID
* ```'ret_code': 30054,```
* ```'ret_msg': 'fixed_new_position_margin [%s] invalid'```
### INSUFFICIENT AVAILABLE BALANCE
* ```'ret_code': 30067,```
* ```'ret_msg': 'insufficient available balance'```
### EXIT VALUE MUST BE POSITIVE
* ```'ret_code': 30068,```
* ```'ret_msg': 'exit value must be positive'```
### RISK LIMIT NOT MODIFIED
* ```'ret_code': 34026,```
* ```'ret_msg': 'the draftPzVo limit is same to the old limit'```
