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
