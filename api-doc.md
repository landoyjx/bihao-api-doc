## 一、请求说明 ##

	1、POST请求头信息中必须声明 Content-Type:application/json;
	
	2、所有请求参数请按照 API 说明进行参数封装。
	
	3、将封装好参数的 API 请求通过 POST 的方式提交到服务器。
	
	4、币好网处理请求，并返回相应的 JSON 格式结果。
	
	5、请使用 https 请求。

	6、所有的 API 都需要认证 Api的申请可以到用户中心 -> 交易设置 -> 申请API

	   申请得到私钥和公钥，私钥币好将不做储存，一旦丢失将无法找回 
	
	7、签名机制：$param = array(

				amount 	=> 1,

				price  	=> 10000,

				type   	=> 'buy',

				api_key => 7dab89b3b0d46a13772d980ed4b63096

				sign    => e28f207fd85cebdd0a12259e8776d2b4

			);

	        api_key 是申请到的公钥。
				
		sign是签名，是将amount price type key等键名进行按字母顺序排序，将键值连接，再连接私钥，通过双层md5加密为得到的值。


## 二、接口说明 ##

### 2.1 市场行情  ### 

POST https://www.bihao.pro/index.php/v1/ticker

**请求参数：**

|参数名|参数类型|必填|描述|
|-------------|-------------|-----|----|
|api_key| String|是 |用户申请的apiKey|
|symbol| String|是 |交易对 BTC_USDT|
|sign| String|是 |请求参数的签名|

**返回结果示例：**

	{
    "data": {
        "date": 1525966177,
        "ticker": {
            "buy": "0.10000000",
            "high": "123.00000000",
            "last": "0.12345000",
            "low": "0.10000000",
            "sell": "141.00000000",
            "vol": 0
        }
    },
    "code": "10000",
    "msg": "请求成功"
}

**返回值说明:**

1. date: 返回数据时服务器时间
2. buy: 买一价
3, high: 最高价
4. last: 最新成交价
5. low: 最低价(最近的24小时)
6. sell: 卖一价
7. vol: 成交量(最近的24小时)

### 2.2 市场深度 ###

POST https://www.bihao.pro/index.php/v1/depth 

**请求参数：**

| 参数名 | 参数类型|必填|描述|
|-------------|-------------|-----|----|
|api_key| String|是 |用户申请的apiKey|
|symbol| String|是 |交易对 BTC_USDT|
|sign| String|是 |请求参数的签名|

**返回结果示例：**

	{
	    "data": {
	        "asks": [
	            ["2.0000",0]
	        ],
	        "bids": [
		   ["2.0000",0]
		]
	    },
	    "code": "10000",
	    "msg": "请求成功"
	}

**返回值说明:**

1. asks - 委买单[价格, 委单量]，价格从高到低排序
2. bids - 委卖单[价格, 委单量]，价格从高到低排序

### 2.3 最近的市场交易  ###

POST https://www.bihao.pro/index.php/v1/orders

**请求参数：**

| 参数名 | 参数类型|必填|描述|
|-------------|-------------|-----|----|
|api_key| String|是 |用户申请的apiKey|
|symbol| String|是 |交易对 BTC_USDT|
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
	    "code": "10000",
	    "msg": "请求成功"
	}

**返回值说明:**

1. id:交易id
2. date：时间戳
3. amount:交易数量
4. price：价格
5. type:交易类型


### 2.4 K线 ###

POST  https://www.bihao.pro/index.php/v1/kline

**请求参数：**

| 参数名 | 参数类型|必填|描述|
|-------------|-------------|-----|----|
|api_key| String|是 |用户申请的apiKey|
|symbol| String|是 |交易对 BTC_USDT|
|type| String|是 |用户请求K线时长1min,15min,30min,1hour,1day,2day,3day,1week,3week,1month,6month|
|size| String|否 |用户一次请求条数|
|since| String|否 |用户请求某个时间之后的数据|
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
	    "code": "10000",
	    "msg": "请求成功"
	}

**返回值说明:**

1. 1525639499:时间戳
2. 0：交易量
3. 2: 开盘
4. 2.0000：高
5. 1.0000：低
6. 1.5000：收


### 2.5 获取用户信息  ###

POST  https://www.bihao.pro/index.php/v1/userinfo

**请求参数：**

| 参数名 | 参数类型|必填|描述|
|-------------|-------------|-----|----|
|api_key| String|是 |用户申请的apiKey|
|sign| String|是 |请求参数的签名|

**返回结果示例：**

	{
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
                "currency": "BNB"
            },
            {
                "free": 0,
                "freezed": 0,
                "currency": "SWT"
            },
            {
                "free": 0,
                "freezed": 0,
                "currency": "CNY"
            },
            {
                "free": 0,
                "freezed": 0,
                "currency": "MOAC"
            },
            {
                "free": 0,
                "freezed": 0,
                "currency": "USDT"
            },
            {
                "free": 0,
                "freezed": 0,
                "currency": "BCH"
            },
            {
                "free": 0,
                "freezed": 0,
                "currency": "BHB"
            },
            {
                "free": 0,
                "freezed": 0,
                "currency": "ADA"
            },
            {
                "free": 0,
                "freezed": 0,
                "currency": "ELF"
            },
            {
                "free": 0,
                "freezed": 0,
                "currency": "STM"
            }
        ],
        "nameauth": 0
    },
    "code": "10000",
    "msg": "请求成功"
}

**返回值说明:**

1. free:用户可用余额
2. freezed：用户冻结余额
3. currency：币种名称 
4. nameauth:0 未实名 1 认证成功 2 认证失败


### 2.6 下单 ###

POST https://www.bihao.pro/index.php/orders

**请求参数：**

| 参数名 | 参数类型|必填|描述|
|-------------|-------------|-----|----|
|symbol| String|是 |交易对 BTC_USDT|
|num| String|是 |用户下单数量|
|price| String|是 |用户下单价格|
|type| String|是 |用户下单类型 sell卖出 buy买入|
|api_key| String|是 |用户申请的apiKey|
|sign| String|是 |请求参数的签名|

**返回结果示例：**

	{
	    "code": "10000",
	    "msg": "下单成功"
	}

**返回值说明:**

1. code:返回码
2. msg：返回信息

### 2.7  获取历史订单信息，只返回最近两天的信息   ###

POST https://www.bihao.pro/index.php/v1/order_history

**请求参数：**

|参数名|参数类型|必填|描述|
|-------------|-------------|-----|-----|
|api_key| String|是 |用户申请的apiKey|
|status| Integer|是 |查询状态 0：未完成的订单 1：已经完成的订单 （最近两天的数据）|
|current_page| Integer|是 |当前页数|
|page_length|Integer|是 |每页数据条数，最多不超过200|
|sign| String|是 |请求参数的签名|

**返回结果示例：**

{

    "data": {
        "orders": [
             {
                "id": "134",
                "price": "1.00000000",
                "num": "243.99980000",
                "trade_num": "243.00000000",
                "fee": "0.10000000",
                "type": "sell",
                "add_time": "1524677232",
                "trade_time": "1524678034",
                "status": "1",
                "currency_id": "1",
                "currency_trade_id": "5",
                "currency_mark": "BTC",
                "digit_num": "6",
                "currency_trade_mark": "CNY"
            },
            {
                "id": "134",
                "price": "1.00000000",
                "num": "243.99980000",
                "trade_num": "243.00000000",
                "fee": "0.10000000",
                "type": "sell",
                "add_time": "1524677232",
                "trade_time": "1524678034",
                "status": "1",
                "currency_id": "1",
                "currency_trade_id": "5",
                "currency_mark": "BTC",
                "digit_num": "6",
                "currency_trade_mark": "CNY"
            }        
        ],
        "current_page": 1,
        "page_length": 8
    },
    "code": "10000",
    "msg": "请求成功"
}

**返回值说明:**

1. id:订单id
2. currency_id：币种id
3. currency_trade_id:分区币种id
4. price：单价
5. num：数量
6. trade_num：成交数量
7. fee：手续费
8. type：类型buy买入，sell卖出
9. add_time:下单时间
10. trade_time:成交时间
11. status：0代表挂单1代表部分成交2代表全部成交
12. currency_mark：交易币种英文标识
13. digit_num：交易币种小数位
14. currency_trade_mark：分区币种英文标识
15. current_page: 当前页码
16. page_length: 每页显示条数


### 2.8 获取历史交易信息 ###

POST https://www.bihao.pro/index.php/v1/trade_history

**请求参数：**

| 参数名 | 参数类型|必填|描述|
|-------------|-------------|-----|----|
|api_key| String|是 |用户申请的apiKey|
|sign| String|是 |请求参数的签名|
|symbol| String|是 |交易对 BTC_USDT|

**返回结果示例：**

	{
	    "data": {
	        "current_page": 1,
	        "page_length": 8,
	        "trades": [
	            {
	                "price": "1.00000000",
	                "num": "1.00000000",
	                "money": "1.00000000",
	                "fee": "0.00100000",
	                "type": "sell",
	                "add_time": "1526884311",
	                "status": "0",
	                "b_mark": "SWT",
	                "email": "",
	                "phone": "13701331454",
	                "type_name": "卖出",
	                "trade_pair": "SWT/"
	            },
	            {
	                "price": "1.00000000",
	                "num": "10.00000000",
	                "money": "10.00000000",
	                "fee": "0.01000000",
	                "type": "buy",
	                "add_time": "1526639996",
	                "status": "0",
	                "b_mark": "BTC",
	                "email": "",
	                "phone": "13701331454",
	                "type_name": "买入",
	                "trade_pair": "BTC/"
	            }
	        ]
	    },
	    "code": "10000",
	    "msg": "请求成功"
	}

**返回值说明:**

1. price：单价
2. num：数量
3. money：总价
4. fee：手续费
5. type：类型buy买入，sell卖出
6. add_time:下单时间
7. status：0代表挂单1代表部分成交2代表全部成交
8. email：用户邮箱
9. phone：用户电话
10. type_name：交易类型
11. current_page: 当前页码
12. trade_pair：交易市场
13. page_length: 每页显示条数

### 2.9 撤销订单 ###

POST  URL https://www.bihao.pro/index.php/v1/cancel_order

**请求参数：**

| 参数名 | 参数类型|必填|描述|
|-------------|-------------|-----|---|
|api_key| String|是 |用户申请的apiKey|
|sign| String|是 |请求参数的签名|
|order_id| String|是 |订单id|

**返回结果示例：**

	{
	    "code": "10020",
	    "msg": "撤销成功"
	}

**返回值说明:**

1. code:返回码
2. msg：返回信息


### 2.10 获取用户的订单信息  (未成交) ###

POST  https://www.bihao.pro/index.php/v1/order_info

**请求参数：**

| 参数名 | 参数类型|必填|描述|
|-------------|-------------|-----|----|
|api_key| String|是 |用户申请的apiKey|
|sign| String|是 |请求参数的签名|
|order_id| String|是 |订单id|

**返回结果示例：**

	{
	    "data": {
	        "id": "1",
	        "price": "10.00000000",
	        "num": "2.00000000",
	        "trade_num": "2.00000000",
	        "fee": "0.10000000",
	        "type": "buy",
	        "add_time": "1524662244",
	        "trade_time": "1524666228",
	        "status": "2",
	        "currency_id": "1",
	        "currency_trade_id": "5",
	        "currency_mark": "BTC",
	        "digit_num": "6",
	        "currency_trade_mark": "CNY"
	    },
	    "code": "10000",
	    "msg": "请求成功"
	}

**返回值说明:**

1. id:成交记录id
2. price：单价
3. num：数量
2. currency_id：币种id
3. currency_trade_id:分区币种id
6. fee：手续费
7. type：类型buy买入，sell卖出
8. add_time:成交时间
9. status：0状态
10. currency_mark：交易币种英文标识
11. currency_trade_name:交易分区币种名,
12. currency_trade_mark: 交易分区币种英文标识,
13. trade_pair":交易市场名
14. trade_num 成交数量



## 三、错误代码对照表 ##

| 错误代码 | 详细描述|
|-------------|-------------|
|10000| 请求成功|
|10001| 签名失败|
|10002| api_key不能为空|
|10003| 必选参数不能为空|
|10004| 非法参数|
|10005| 币种不存在|
|10006| order_id不能为空|
|10007| 交易未开始|
|10008| 交易未开启|
|10009| 下单金额或数量不正确|
|10010| 下单数量超过最大数量|
|10011| 下单数量低于最小下单数量|
|10012| 价格小于跌停价格|
|10013| 价格大于涨停价格|
|10014| 账户余额不足|
|10015| 下单失败！请重新再试或联系管理员|
|10016| 价格和数量不正确|
|10017| 超过最大买入量|
|10018| 低于最小买入量|
|10019| 订单不存在|
|10020| 撤销成功|
|10021| 撤销失败|



