<hr>

## 2020-02-10

### REST API
- [查询用户资产](./rest_api.md#open-apiwalletbalanceget) [新增]

<hr>

## 2019-12-27

### REST API
- [设置风险限额](./rest_api.md#wallet-setrisklimit) [新增]
- [查询风险限额表](./rest_api.md#wallet-getrisklimit) [新增]

<hr>

## 2019-12-18

### REST API
- [我的仓位V2](./rest_api.md#positionlistv2get) [新增]
### Websocket
- [orderBookL2_200](./websocket.md#orderBook200_v2) [新增]

<hr>

## 2019-12-13

### REST API
- [实时查询条件单单信息](./rest_api.md#v2-private-stop-order) [新增]

<hr>

## 2019-12-2

### REST API
- [创建活动委托单-v2](./rest_api.md#open-apiordercreatev2post) [新增]
- [撤销活动委托单-v2](./rest_api.md#open-apiordercancelv2post) [新增]
- [撤销全部活动委托单](./rest_api.md#open-apiordercancelallpost) [新增]
- [撤消全部条件委托单](./rest_api.md#open-apistop-ordercancelallpost)  [新增]

<hr>

## 2019-11-19

### REST API
- [获取平台历史成交数据](./rest_api.md#trading-records) [新增]

<hr>

## 2019-11-07

### REST API
- [修改用户杠杆](./rest_api.md#userleveragesavepost) [更新]
- [我的仓位](./rest_api.md#positionlistget) [更新]
- [更新保证金](./rest_api.md#positionchange-position-marginpost) [更新]
- [设置止盈止损](./rest_api.md#position-settradingstoppost) [更新]

<hr>

## 2019-11-04

### REST API
- [获取公告](./rest_api.md#open-apiannouncement) [新增]
- [撤销活动委托单](./rest_api.md#open-apiordercancelpost) [更新]
    - 支持通过`order_link_id`撤单
- [撤消条件委托单](./rest_api.md#open-apiordercancelpost) [更新]
    - 支持通过`order_link_id`撤单
- [密钥信息](./rest_api.md#open-apikeyget) [更新]
    - 新增额外字段
    - 更新ips字段返回内容
- [更新频率限制](./rest_api_sign.md#rest-rate-limit)[更新]
	- 频率限制精确到毫秒
	- 细化接口的频率限制
	- 新增字段rate_limit_reset_ms、rate_limit
### Websocket
- [klineV2](./websocket.md#kline_v2) [新增]
- [stop_order](websocket.md#stop-order) [新增]

<hr>

## 2019-10-22

### REST API
- [实时查询活动单信息](./rest_api.md#v2-private-order) [新增]

### Websocket API
- [Topic position](./websocket.md#position) [更新]
	- 添加了额外字段
- [Topic trade](./websocket.md#trade) [更新]
	- 修复重复推送交易数据的问题
	- 现在支持在一个消息中推送多条交易
	
<hr>

## 2018-11-09

### Web Socket
- 身份认证的expires参数单位`由秒改为毫秒`
- insurance topic: walletBalance字段名由`walletBalance`改为`wallet_balance`
- execution topic: data字段类型由`object`改为`array`
- order topic: data字段类型由`object`改为`array`
- 订阅公共类topic不再需要先进行身份验证
- 增加auth指令，用于身份验证

<hr>

## 2018-11-07

### Rest API

- api_key参与加签
- 取消对sign的base64 encode
- 增加recv_window参数说明
- 增加示例加签sign，方便快速验证sign是否一致

<hr>
