### https://www.bihao.pro/api/v1/order_history.do  获取历史订单信息，只返回最近两天的信息 访问频率 20次/2秒 ###

**请求参数：**

|参数名|参数类型|必填|描述|
|-------------|-------------|-----|-----|
|api_key| String|是 |用户申请的apiKey|
|symbol| String|是 |币 btc swtc moac cnt eth bhb|
|status| Integer|是 |查询状态 0：未完成的订单 1：已经完成的订单 （最近两天的数据）|
|current_page| Integer|是 |当前页数|
|page_length|Integer|是 |每页数据条数，最多不超过200|
|sign| String|是 |请求参数的签名|

**返回结果示例：**

{

    "data": {
        "orders": [
            {
                "id": "29",
                "member_id": "5",
                "currency_id": "1",
                "currency_trade_id": "5",
                "price": "13.00000000",
                "num": "2.00000000",
                "trade_num": "2.00000000",
                "fee": "0.10000000",
                "type": "sell",
                "add_time": "1524666399",
                "trade_time": "1524666399",
                "status": "2",
                "currency_mark": "BTC",
                "digit_num": "5",
                "currency_trade_mark": "CNY"
            },
            {
                "id": "28",
                "member_id": "5",
                "currency_id": "1",
                "currency_trade_id": "5",
                "price": "13.00000000",
                "num": "2.00000000",
                "trade_num": "2.00000000",
                "fee": "0.10000000",
                "type": "buy",
                "add_time": "1524666393",
                "trade_time": "1524666399",
                "status": "2",
                "currency_mark": "BTC",
                "digit_num": "5",
                "currency_trade_mark": "CNY"
            }        
        ],
        "current_page": 1,
        "page_length": 8
    },
    "code": "1001",
    "msg": "请求成功"
}

**返回值说明:**

1. id:订单id
2. member_id:用户id
3. currency_id：币种id
4. currency_trade_id:分区币种id
5. price：单价
6. num：数量
7. trade_num：成交数量
8. fee：手续费
9. type：类型buy买入，sell卖出
10. add_time:下单时间
11. trade_time:成交时间
12. status：0代表挂单1代表部分成交2代表全部成交
13. currency_mark：交易币种英文标识
14. digit_num：交易币种小数位
15. currency_trade_mark：分区币种英文标识
16. current_page: 当前页码
17. page_length: 每页显示条数


###https://www.bihao.pro/v1/order_info.do 获取用户的订单信息 访问频率 20次/2秒 (未成交)###
**请求参数：**

| 参数名 | 参数类型|必填|描述|
|-------------|-------------|-----|
|api_key| String|是 |用户申请的apiKey|
|symbol| String|是 |币 btc swtc moac cnt eth bhb|
|order_id| Integer|是 |订单ID 1:要查询的订单id|
|sign| String|是 |请求参数的签名|
**返回结果示例：**

{

    "data": {
        "orders": [
            {
                "id": "29",
                "member_id": "5",
                "currency_id": "1",
                "currency_trade_id": "5",
                "price": "13.00000000",
                "num": "2.00000000",
                "trade_num": "2.00000000",
                "fee": "0.10000000",
                "type": "sell",
                "add_time": "1524666399",
                "trade_time": "1524666399",
                "status": "2",
                "currency_mark": "BTC",
                "digit_num": "5",
                "currency_trade_mark": "CNY"
            }       
        ]
    },
    "code": "1001",
    "msg": "请求成功"
}

**返回值说明:**

1. id:订单id
2. member_id:用户id
3. currency_id：币种id
4. currency_trade_id:分区币种id
5. price：单价
6. num：数量
7. trade_num：成交数量
8. fee：手续费
9. type：类型buy买入，sell卖出
10. add_time:下单时间
11. trade_time:成交时间
12. status：0代表挂单1代表部分成交2代表全部成交
13. currency_mark：交易币种英文标识
14. digit_num：交易币种小数位
15. currency_trade_mark：分区币种英文标识

###URL https://www.bihao.pro/V1/cancel_order.do 撤销订单 访问频率 20次/2秒###
**请求参数：**

| 参数名 | 参数类型|必填|描述|
|-------------|-------------|-----|---|
|api_key| String|是 |用户申请的apiKey|
|symbol| String|是 |币 btc swtc moac cnt eth bhb|
|order_id| Integer|是 |订单ID 1:要查询的订单id|
|sign| String|是 |请求参数的签名|
**返回结果示例：**

{

    "code": "1002",
    "msg": "撤销成功"

}

**返回值说明:**

1. code:返回码
2. msg：返回信息


###https://www.bihao.pro/v1/order_info.do 获取用户的订单信息 访问频率 20次/2秒 (未成交)###
**请求参数：**

| 参数名 | 参数类型|必填|描述|
|-------------|-------------|-----|----|
|api_key| String|是 |用户申请的apiKey|
|symbol| String|是 |币 btc swtc moac cnt eth bhb|
|sign| String|是 |请求参数的签名|
**返回结果示例：**

{

    "data": {
        "trades": [
            {
                "id": "521",
                "trade_no": "T1524559015",
                "member_id": "405",
                "currency_id": "33",
                "currency_trade_id": "34",
                "price": "10.0000",
                "num": "1000.0000",
                "money": "10000.0000",
                "fee": "1.0000",
                "type": "buy",
                "add_time": "1524559015",
                "status": "0",
                "b_mark": "ETH",
                "email": "1287418206@qq.com",
                "phone": "13716204891",
                "type_name": "买入",
                "currency_trade_name": "CNT",
                "currency_trade_mark": "CNT",
                "trade_pair": "ETH/CNT"
            }  
        ]
    },
    "code": "1001",
    "msg": "请求成功"
}

**返回值说明:**

1. id:成交记录id
2. trade_no：交易记录号
3. member_id:用户id
4. currency_id：币种id
5. currency_trade_id:分区币种id
6. price：单价
7. num：数量
8. money：金额
9. fee：手续费
10. type：类型buy买入，sell卖出
11. add_time:成交时间
12. status：0状态
13. b_mark：交易币种英文标识
14. email：用户邮箱账户
15. phone：用户电话
16. type_name：交易类型
17. currency_trade_name:交易分区币种名,
18. currency_trade_mark: 交易分区币种英文标识,
19. trade_pair":交易市场名


###https://www.bihao.pro/v1/ticker 好币行情 ###
**请求参数：**

| 参数名 | 参数类型|必填|描述|
|-------------|-------------|-----|----|
|api_key| String|是 |用户申请的apiKey|
|symbol| String|是 |币 btc swtc moac cnt eth bhb|
|sign| String|是 |请求参数的签名|
**返回结果示例：**

{

    "data": {
		"date"  : 1525854774,
        "ticker": [
            {
                "buy":"33.15",
				"high":"34.15",
				"last":"33.15",
				"low":"32.05",
				"sell":"33.16",
				"vol":"10532696.39199642"
            }  
        ]
    },
    "code": "1001",
    "msg": "请求成功"
}

**返回值说明:**

1.date: 返回数据时服务器时间
2.buy: 买一价
3,high: 最高价
4.last: 最新成交价
5.low: 最低价
6.sell: 卖一价
7.vol: 成交量(最近的24小时)



###https://www.bihao.pro/v1/depth 市场深度 ###
**请求参数：**

| 参数名 | 参数类型|必填|描述|
|-------------|-------------|-----|----|
|api_key| String|是 |用户申请的apiKey|
|symbol| String|是 |币 btc swtc moac cnt eth bhb|
|sign| String|是 |请求参数的签名|
**返回结果示例：**

{

    "data": {
        "asks": [
            [
                "2.0000",
                0
            ],
            [
                "0.2000",
                0
            ]
        ],
        "bids": [
			[
                "2.0000",
                0
            ],
            [
                "0.2000",
                0
            ]
		]
    },
    "code": "1001",
    "msg": "请求成功"
}

**返回值说明:**

1.asks - 委买单[价格, 委单量]，价格从高到低排序
2.bids - 委卖单[价格, 委单量]，价格从高到低排序


###https://www.bihao.pro/v1/orders 最近的市场交易 ###
**请求参数：**

| 参数名 | 参数类型|必填|描述|
|-------------|-------------|-----|----|
|api_key| String|是 |用户申请的apiKey|
|symbol| String|是 |币 btc swtc moac cnt eth bhb|
|sign| String|是 |请求参数的签名|
**返回结果示例：**

{

	"data": [
        {
            "id": "37",
            "date": "1524669669",
            "amount": "100.00000000",
            "price": "10.00000000",
            "type": "sell"
        },
 		{
            "id": "37",
            "date": "1524669669",
            "amount": "100.00000000",
            "price": "10.00000000",
            "type": "sell"
        }
        
    ],
    "code": "1001",
    "msg": "请求成功"
}

**返回值说明:**

1. id:交易id
2. date：交易时间
3. amount:交易数量
4. price：价格
5. type:交易类型


###https://www.bihao.pro/v1/kline K线 ###
**请求参数：**

| 参数名 | 参数类型|必填|描述|
|-------------|-------------|-----|----|
|api_key| String|是 |用户申请的apiKey|
|symbol| String|是 |币 btc swtc moac cnt eth bhb|
|sign| String|是 |请求参数的签名|
**返回结果示例：**

{

    "data": [
        [
            1525639499,
            0,
            2,
            "2.0000",
            "1.0000",
            "1.5000"
        ],
        [
            1525639499,
            0,
            2,
            "2.0000",
            "1.0000",
            "1.5000"
         ],
	]
    "code": "1001",
    "msg": "请求成功"
}

**返回值说明:**

1. 1525639499:时间戳
2. 0：交易量
3. 2: 开盘
4. 2.0000：高
5. 1.0000：低
6. 1.5000：收


###https://www.bihao.pro/v1/userinfo 获取用户信息 ###
**请求参数：**

| 参数名 | 参数类型|必填|描述|
|-------------|-------------|-----|----|
|api_key| String|是 |用户申请的apiKey|
|symbol| String|是 |币 btc swtc moac cnt eth bhb|
|sign| String|是 |请求参数的签名|
**返回结果示例：**

{

    "data": {
        "free": {
            "SWT": "1000062.0000"
        },
        "freezed": {
            "SWT": "8.0000"
        },
        "nameauth": "1"
    },
    "code": "1001",
    "msg": "请求成功"
}

**返回值说明:**

1. free:用户可用余额
2. freezed：用户冻结余额
3. nameauth:0 未实名 1 等待确认 2 已经认证成功


###https://www.bihao.pro/v1/trade 下单 ###
**请求参数：**

| 参数名 | 参数类型|必填|描述|
|-------------|-------------|-----|----|
|api_key| String|是 |用户申请的apiKey|
|symbol| String|是 |币 btc swtc moac cnt eth bhb|
|sign| String|是 |请求参数的签名|
**返回结果示例：**


{

    "code": "1001",
    "msg": "下单成功"

}

**返回值说明:**

1. code:返回码
2. msg：返回信息
