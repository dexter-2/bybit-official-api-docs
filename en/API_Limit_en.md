# NOTICE: These docs are now OBSOLETE; please find the new documentation [here](https://bybit-exchange.github.io/docs/inverse). Thank you.

# Introduction
Bybit use `Order Fill Ratio (OFR)`, `Liquidity Contribution Points (LCP)` to measure customers' contribution to our executable liquidity.


The `LCP` and `OFR` of different symbols are calculated separately.

# Order Fill Ratio (OFR) Threshold
If you place more than `2000` orders per day on bybit, please maintain your 7-day OFR above a `Minimum OFR threshold`, or bybit may reduce your api request frequency limit.

## Order Fill Ratio (OFR)
> `Order Fill Ratio (OFR)` : the proportion of orders filled per orders submitted to bybit.

> `Orders Submitted to bybit`: Any order sent to bybit.

> `Orders Filled`: Any order that has been filled for any amount.

> `OFR = (number of Orders Filled / number of Orders Submitted to bybit)`

## Order Fill Ratio example
User A submited a limit order request which contains 4 bids and 4 asks, and these orders are placed in orderbook at different price levels. Then, User A cancelled 2 bids and submitted a new limit order request which contains 2 new bids.

At this time, User B submits a market order request, and matches with 2 of A's bids.

The OFR of this period is calculated as follows:



```
User A:
Orders Filled = 2
Orders Submitted to bybit = 8
QFR = 2/8 = 25%
```

```
User B:
Orders Filled = 1
Orders Submitted to bybit = 1
QFR = 1/1 = 100%
```

## Minimum OFR Threshold
7-day OFR must be kept above 0.1%.



---


# API Request Frequency Limits

Your API request frequency limit is based on your min `Liquidity Contribution Points (LCP)` of `7` days.


`LCP` and API request frequency threshold :

|  LCP     | Frequency Limit |
|  ----    | ----  |
| 20-100  | 800 times per minute |
| 10-20   | 600 times per minute |
| 5-10    | 400 times per minute |
| 2-5     | 200 times per minute |
| <2      | 100 times per minute |

## Liquidity Contribution Points (LCP)

> `Liquidity Contribution Points (LCP) = POU * POA * 100`

## Explanation
### Effective Price Range

> `effective price range`: 6 tick sizes range around middle of best bid price and best ask price.

> Min `effective price` is  (Best bid price + Best ask price) / 2 - (3 * tick_size)

> max `effective price` is  (Best bid price + Best ask price) / 2 + (3 * tick_size)

#### Effective Price Range example
```
BTC best bid = 10000
BTC best ask = 10001
Effective Price Range: [(10000 + 10001) / 2 - 3* 0.5, (10000 + 10001) / 2 + 3* 0.5] = [9999,10002]
```


### POU
> `POU`: the proportion of your orders within `effective price range` to all your orders in orderbook

Bybit calculates your amount of orders within `effective price range` / amount of all your orders in orderbook, and then performs a 1-Day Time-Weighted-Average over the series of seconds rates.

#### POU example
User C bids 2000 contracts for $9995 and bids 8000 contracts for $9999, while effective price range is [9999,10002]

```
amount of User C's orders within effective price range = 8000
amount of all User C's orders = 2000 + 8000 = 10000
POU = 8000 / 10000 = 0.8
```



#### POA
> `POA`: the proportion of your orders within `effective price range` to all orders within `effective price range` in orderbook.

Bybit calculates your amount of orders within `effective price range` / amount of all orders within `effective price range` in orderbook, and then performs a 1-Day Time-Weighted-Average over the series of seconds rates.

#### POA example
User C only has 8000 contracts within effective price range, while bybit have 200000 contracts within effective price range in orderbook.

```
amount of User C's orders within effective price range = 8000
amount of all orders within effective price range = 200000
POA = 8000 / 200000 = 0.04
```


Prior notice will be given via website if we update the mechanism.
