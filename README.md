## API Guide


- All requests are http request, and use **POST** and **GET** method
- Http request content type is **application/json**
- All **POST** request will be verified by signature, with `accessKey` and `secretKey` provided for each account in bihao.pro
- Signature parameter `sign`, will be calculated by sort each key ,and then concat key and value, with concat secretKey last. Then do double MD5 digest. The algorithm is:
   ```js
   sign=MD5(MD5(key1+value1+key2+value2+...+secretKey))
   ```
- Bihao.pro production environment api prefix is https://www.bihao.pro/
- Signature require timestamp `time` to be sent to endpoint, the logic is as follow.
    ```js
        if (time < (serverTime + 30) && (serverTime - time) <= 300) {
          // process request
        } else {
          // reject request
        }
    ```
- All response data will be as follow format
    ```js
    {
        "code": Integer,
        "msg": String,
        "data": Object
    }
    ```
    `data` is response data, `code` indicates result status, `msg` is result message.
- Response data is UTF-8 encoded

## API Interfaces


### 1. Ticker

URL: /api/ticker/{symbol}, GET

Get latest market ticker

*Request parameters*:

|Param|Type|Required|Description|
|-------------|-------------|-----|----|
|symbol| String|Yes | Trade Pair, for example BTC_USDT, currency is uppercase and concat by underline `_`|


*Response Example*:
```json
{
    "code": 10000,
    "msg": "Success",
    "data": {
        "date": 1525966177,
        "ticker": {
            "buy": 0.10000000,
            "high": 123.00000000,
            "last": 0.12345000,
            "low": 0.10000000,
            "sell": 141.00000000,
            "volume": 0,
            "value": 0
        }
    }
}
```

*Parameter Description*:
1. `date`: last time of the request
2. `buy`: first buy price
3. `sell`: first sell price
4. `high`: the highest price in last 24 hours
5. `low`: the lowest price in last 24 hours
6. `volume`: trade volume in last 24 hours
7. `volue`: trade value in last 24 hours

### 2. Depth

URL: /api/depth/{symbol}, GET

Get market orderbook depth

*Request parameters*:

|Param|Type|Required|Description|
|-------------|-------------|-----|----|
|symbol| String|Yes | Trade Pair, for example BTC_USDT, currency is uppercase and concat by underline `_`|

*Response Example*:

```json
{
    "code": 10000,
    "msg": "Success",
    "data": {
        "asks": [
           [2.3000, 20.00],
           [2.2000, 200.00],
           [2.1000, 100.00]
        ],
        "bids": [
           [2.0000, 20.0],
           [1.9000, 10.0],
           [1.8000, 20.0],
           [1.5000, 10.0]
        ],
    }
}
```

*Parameter Description*:
1. `asks`: sell order[price, amount] array, sort by price desc
2. `bids`: buy order[price, amount] array, sort by price desc 



### 3. KLine data

URL: /api/kline/{symbol}/{resolution}, GET

Get Kline/candlestick bars for a symbol

*Request parameters*:

|Param|Type|Required|Description|
|-------------|-------------|-----|----|
|symbol| String|Yes | Trade Pair, for example BTC_USDT, currency is uppercase and concat by underline `_`|
|resolution| String| Yes| KLine period, 1, 60, 1D|


Query parameters:

|Param|Type|Required|Description|
|-------------|-------------|-----|----|
|from| Long|No | UNIX time of start time, default is zero time of current day|
|to|Long|No| UNIX time of end time, default is current time|
|size|Integer|No| max size of kline data, min 100, max 200|



*Response Example*:

```json
{
    "data": [
       [
           "1525639499",
           "10",
           "2",
           "2.0000",
           "1.0000",
           "1.5000"
       ],
       [
           "1525639499",
           "20",
           "2",
           "2.0000",
           "1.0000",
           "1.5000"
       ]
    ],
    "code": "10000",
    "msg": "Success"
}
```

*Parameter Description*:

1. `1525639499`: trade timestamp
2. `10`: trade volume
3. `2.0000`: open price in last 24 hours
4. `2.0000`: high price in last 24 hours
5. `1.0000`: low price in last 24 hours
6. `1.5000`: closed price in last 24 hours

### 4. User Info

URL: /api/user/info, POST

Get user information, include user balance

*Request parameters*:

|Param|Type|Required|Description|
|-------------|-------------|-----|----|
|api_key| String|Yes | User account's `accessKey`|
|time|Long|Yes| UNIX Time of request
|sign| String| Yes | Signature|

*Response Example*:

```json
{
    "code": 10000,
    "msg": "Success",
    "data": {
        "balance": [
            {
                "free": 0,
                "freezed": 0,
                "currency": "BTC"
            },
            {
                "free": 0,
                "freezed": 0,
                "currency": "ETH"
            },
            {
                "free": 0,
                "freezed": 0,
                "currency": "USDT"
            }
        ],
        "isAuth": 0
    }
}
```

*Parameter Description*:

1. `free`: user avilable balance
2. `freezed`: user locked balance
3. `currency`: user hold currency
4. `isAuth`: user verification, 0: unverified, 1: verified

### 5. New Order

URL: /api/user/create-order, POST

User set new order in orderbook

*Request parameters*:

|Param|Type|Required|Description|
|-------------|-------------|-----|----|
|api_key| String|Yes | User account's `accessKey`|
|time|Long|Yes| UNIX Time of request
|symbol| String|Yes | Trade Pair, for example BTC_USDT, currency is uppercase and concat by underline `_`|
|amount| String| Yes| Order amount|
|price| String| Yes| Order price|
|type| String|Yes| Order type, sell or buy|
|sign| String| Yes | Signature|

*Response Example*:

```json
{
    "code": "10000",
    "msg": "Success",
    "data": "156046894528701668726"
}
```

*Parameter Description*:

1. `data`: new created order no 

### 6. Cancel Order

URL: /api/user/cancel-order, POST

User cancel order

*Request parameters*:

|Param|Type|Required|Description|
|-------------|-------------|-----|----|
|api_key| String|Yes | User account's `accessKey`|
|time|Long|Yes| UNIX Time of request
|symbol| String|Yes | Trade Pair, for example BTC_USDT, currency is uppercase and concat by underline `_`|
|order_no| String| Yes| Order to be cancelled|
|sign| String| Yes | Signature|

*Response Example*:

```json
{
    "code": 10000,
    "msg": "Success",
    "data": null
}
```

### 7. Order Information

URL: /api/user/orderinfo, POST

Get User pending order detail information

*Request parameters*:

|Param|Type|Required|Description|
|-------------|-------------|-----|----|
|api_key| String|Yes | User account's `accessKey`|
|time|Long|Yes| UNIX Time of request|
|order_no| String| Yes| Order to be query|
|sign| String| Yes | Signature|

*Response Example*:

```json
{
    "code": 10000,
    "msg": "Success",
    "data": {
        "order_no": "156046877382821347392",
        "cancel": 0,
        "symbol": "CALL_CNT",
        "price": 2,
        "num": 10,
        "type": "sell",
        "add_time": 1560468774,
        "trade_num": 0
    }
}
```

*Parameter Description*:
1. `order_no`: order no
2. `symbol`: order trade pair, for example BTC_USDT
3. `type`: order type, sell or buy
2. `price`: order price
3. `num`: order amount
4. `trade_num`: order traded amount
7. `add_time`: order created time
8. `cancel`: is order cancelled


### 8. Order History

URL: /api/user/orders, POST

Get user order list, final orders limit to latest two weeks

*Request parameters*:

|Param|Type|Required|Description|
|-------------|-------------|-----|----|
|api_key| String|Yes | User account's `accessKey`|
|time|Long|Yes| UNIX Time of request|
|symbol| String|Yes | Trade Pair, for example BTC_USDT, currency is uppercase and concat by underline `_`|
|open|Boolean| Yes| if open return open orders, or return final orders in latest 2 weeks|
|sign| String| Yes | Signature|

Query parameters:

|Param|Type|Required|Description|
|-------------|-------------|-----|----|
|page| Integer|No | page of order list, from 1, default 1|
|size|Integer|No| page size of order list, min 10, max 200|


*Response Example*:

```json
{
    "msg": "Success",
    "code": 10000,
    "data": [
        {
            "order_no": "156046877382821347392",
            "cancel": 0,
            "symbol": "CALL_CNT",
            "price": 2,
            "num": 10,
            "type": "sell",
            "add_time": 1560468774,
            "trade_num": 0
        },
        {
            "order_no": "156033557914847337124",
            "cancel": 0,
            "symbol": "CALL_CNT",
            "price": 3,
            "num": 3,
            "type": "sell",
            "add_time": 1560335628,
            "trade_num": 1.1
        },
        {
            "order_no": "156033559403836097781",
            "cancel": 0,
            "symbol": "CALL_CNT",
            "price": 0.029,
            "num": 10,
            "type": "buy",
            "add_time": 1560335594,
            "trade_num": 0
        },
        {
            "order_no": "156032528961015696800",
            "cancel": 0,
            "symbol": "CALL_CNT",
            "price": 1,
            "num": 1,
            "type": "buy",
            "add_time": 1560325322,
            "trade_num": 0.5
        }
    ]
}
```

*Parameter Description*:

1. `order_no`: order no
2. `symbol`: order trade pair, for example BTC_USDT
3. `type`: order type, sell or buy
2. `price`: order price
3. `num`: order amount
4. `trade_num`: order traded amount
7. `add_time`: order created time
8. `cancel`: is order cancelled



## Error Code

| Code | Error Detail Information|
|-------------|-------------|
|10000| Success|
|10001| Missing parameters|
|10002| Please login first|
|10003| Invalid trade type|
|10004| Invalid trade amount|
|10005| Invalid trade price|
|10006| Invalid trade password |
|10007| Symbol not allow to trade|
|10008| Trade amount exceed max|
|10009| Trade amount less than min|
|10010| Trade price exceed max|
|10011| Trade prce less than min|
|10012| Balance not enough|
|10013| Trade return faile, report to admin|
|10014| Order not found|
|10015| Order not belong to user|
|10016| Order in final stat|
|10017| Cancel order failed|
|10018| Invalid resolution|
|10019| Invalid parent uids|
|10020| Email exists|
|10021| User not exists|
|10022| User account locked|
|10023| Invalid account password|
|10024| Try times exceed limit|
|10025| No image found|
|10026| Fail to read image data|
|10027| Image size to large|
|10028| Not support image type|
|10029| Identity info used|
|10030| Address exists|
|10031| Wallet server error, report to admin|
|10032| Invalid currency|
|10033| Invalid amount|
|10034| Not allow to withdraw|
|10035| Min withdraw amount required|
|10036| Exceed max withdraw amount|
|10037| User not verificatoin|
|10038| User locked|
|10039| Address not exists|
|10040| No agent available|
|10041| User should uniformity|
|10042| Bank account exists|
|10043| Invalid c2c action|
|10044| Bank not exists|
|10045| Still orders left|
|10046| Two factor auth failed|
|10047| User code invalid|
|10048| Send too frequently, try later 3 min|
|10049| Invalid sendcode action|
|10050| Trade password exists|
|10051| Fail to send email|
|10052| Invalid symbol|
|10053| Invalid code|
|10054| Invalid link|
|10061| Invalid address|
|10062| Invalid api|
|10063| Invalid api sign|
|10064| Invalid api time|



