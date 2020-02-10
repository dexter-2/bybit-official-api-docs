<hr>

## 2020-02-10

### REST API
- [Get Wallet Balance](./rest_api.md#open-apiwalletbalanceget) [new]

<hr>

## 2019-12-27

### REST API
- [Set risk limit](./rest_api.md#wallet-setrisklimit) [new]
- [Get risk limit list](./rest_api.md#wallet-getrisklimit) [new]

<hr>

## 2019-12-18

### REST API
- [My position-V2](./rest_api.md#positionlistv2get) [new]
### Websocket API
- [orderBookL2_200](./websocket.md#orderBook200_v2) [new]

<hr>

## 2019-12-13

### REST API
- [Query stop order (real-time)](./rest_api.md#v2-private-stop-order) [new]

<hr>

## 2019-12-02

### REST API

- [Place active order-V2](./rest_api.md#open-apiordercreatev2post) [new]
- [Cancel active order-V2](./rest_api.md#open-apiordercancelv2post) [new]
- [Cancel all active orders](./rest_api.md#open-apiordercancelallpost) [new]
- [Cancel all conditional orders](./rest_api.md#open-apistop-ordercancelallpost) [new]

<hr>

## 2019-11-19

### REST API

- [Get public trading records](./rest_api.md#trading-records) [new]

<hr>

## 2019-11-07

### REST API

- [Change leverage](./rest_api.md#userleveragesavepost) [update]
- [My position](./rest_api.md#positionlistget) [update]
- [Change margin](./rest_api.md#positionchange-position-marginpost) [update]
- [Set Trading-Stop](./rest_api.md#position-settradingstoppost) [update]

<hr>

## 2019-11-04

### REST API
- [Announcement](./rest_api.md#open-apiannouncement) [new]
- [Cancel order](./rest_api.md#open-apiordercancelpost) [update]
    - Support cancel order by `order_link_id`
- [Cancel conditional order](./rest_api.md#open-apistop-ordercancelpost) [update]
    - Support cancel conditional order by `order_link_id`
- [Get user API key info](./rest_api.md#open-apikeyget) [update]
    - Add extra info
    - Update `ips` field to return content
- [Update REST API rate limit](./rest_api_sign.md#api-request-rate-limits) [update]
	- The rate limit is accurate to milliseconds
	- Refine the rate limit of the endpoints
	- Add new response fields: `rate_limit_reset_ms`, `rate_limit`
### Websocket API
- [klineV2](websocket.md#kline_v2) [new]
- [stop_order](websocket.md#stop-order) [new]
<hr>


## 2019-10-22

### REST API
- [Query active order (real-time)](./rest_api.md#v2-private-order) [new]

### Websocket API
- [Topic position](./websocket.md#position) [update]
    - Add extra info, eg. wallet_balance
- [Topic trade](./websocket.md#trade) [update]
    - Fix issue of sometimes push same trade multi times
    - Support pushing multi trades in single message
<hr>
