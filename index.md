## HKDcom API Description
HKD.com API documentation provides guidance to help you access HKD.com’s endpoints, their expected outputs, and common errors. For further assistance or feedback, please email us at tech@hkd.com

**Signature Description**
The request parameters are sorted and spliced together in ascending dictionary order (the timestamp should also be added to verify the signature), and the string to be signed is generated. All parameters have values:

```markdown
Syntax highlighted code block

appKey=wehmslauewe&time=1594468475403&phone=13587690001&symbol=2

```

Generate the string to be signed & the private key parameters (agreed) to generate the final string to be signed. For example, the private key is: xsdlkfjs2234dskl32kjoj, splicing it at the end of the string, the generated string format is: All parameters have value:

```markdown

appKey=wehmslauewe&phone=13587690001&symbol=2&time=1594468475403&appSecretKey=xsdlkfjs2234dskl32kjoj One or more parameters have no value:

```

```markdown

appKey=wehmslauewe&phone=13587690001&symbol=2&email=&symbol=2&time=1594468475403&appSecretKey=xsdlkfjs2234dskl32kjoj

```
Assign this value to the signature parameter signature, and then put the signature in the request header. Note: For the following parameters to sign, please note: please remove the invalid 0 in the incoming parameters, such as coin_amount = 100, please do not pass in 100.00 for signature verification, generate a signature for the parameters according to the signature rules, and compare it with the signature in the request header, If they are consistent, the signature is passed.

### Description of all API requests

**HTTP Request:** https://www.hkd.com/api

**Request Parameters**
Parameter  | required  | Type  | Comment
------------- | ------------- | ------------- | -------------
channel  | true  | int  | Fill in 5, representing API_USER (api user)
time  | true  | long  | Fill in 5, representing API_USER (api user)
Timestamp when the merchant initiates the request, Hong Kong time UTC+8  | true  | string  | sign
api-version  | true  | string  | API version number, default v1

Parameter  | required  | Type  | Comment
------------- | ------------- | ------------- | -------------
channel  | true  | int  | Fill in 5, representing API_USER (api user)

Parameter  | required  | Type  | Comment
------------- | ------------- | ------------- | -------------
Fill in 5, representing API_USER (api user)  | true  | ...  | ...


**Response Example**

```markdown
{
code: 1,
data: {...},
message: "success",
success: true
}
```

**Response Parameters**

Parameter  | Type | Comment
------------- | ------------- | -------------
code  | int | Return code 1: Response value 1 indicates success, other values ​​indicate failure
data  | jsonObject | business data, json object
message  | string | Return code description success
success  | boolean | true=success, false=failure


# 2. Account Data Endpoints

## 2.1. Get Account Balance

**Description**
- Get personal balance

**HTTP Request:** /account/query/coin-account
**Request Method:** POST

**Request Parameters**
Parameter  | required  | Type  | Comment
------------- | ------------- | ------------- | -------------
coinName  | true  | string  | Currency name: USDT, BTC

Parameter  | required  | Type  | Comment
------------- | ------------- | ------------- | -------------
accountType  | true  | string  | account type


Parameter  | Comment
------------- | -------------
1  | Exchange Account
2  | Fiat Account
3  | Isolate-M
4  | USDⓈ-M

**Response Example**
```markdown
{
code: 1,
data: {coinName: "ETH", accountType: 1, amount: 15, frozenAmount: 20},
message: "success",
success: true
}
```
**Response Parameters**
Parameter  | Type  | Comment
------------- | ------------- | -------------
amount  | string  | Available Balance
frozenAmount  | string  | Frozen Balance

# 3. Ordering Endpoints

## 3.1. Order Api
**Description**
- Single order API

**HTTP Request:** /order/add/market-user-entrust

**Request Method:** POST

**Request Parameters**
Parameter  | required  | Type  | Comment
------------- | ------------- | ------------- | -------------
type  | true  | string  | string
orderType  | true  | string  | Order type: 1 limit price, 2 market price
coinMarket  | true  | string  | trading pair name
amount  | true  | BigDecimal  | number of orders
type  | true  | string  | string
price  | true  | BigDecimal  | Order price
userId  | true  | int  | User ID
uid  | true  | int  | User ID

**Response Example**
```markdown
{
code: 1,
data: {"78764432"},
message: "success",
success: true
}
```

## 3.2. Batch Ordering API

**Description**
Quantity - batch order API, now the quantity is within 15 each time < quantity

**HTTP Request:** /order/add/market-user-entrusts
**Request Method:** POST

Example of post request parameters


```markdown

{
    {
    ...,
entrustVos: [{ Single Order Parameter },{...}]
}

```

**Request Parameters**


Parameter  | required  | Type  | Comment
------------- | ------------- | ------------- | -------------
type  | true  | string  | Order direction: 1 buy, 2 sell
orderType  | true  | string  | Order type: 1 limit price, 2 market price
coinMarket  | true  | string  | trading pair name
amount  | true  | BigDecimal  | number of orders
price  | true  | BigDecimal  | Order price
userId  | true  | int  | User ID
uid  | true  | int  | User ID


**Response Example**
```markdown
{
    code: 1,
    data: {"78764432","78764431",...},
    message: "success",
    success: true
}
```

## 3.3. List of Pending Orders for Users

**Description**

- User's pending order list

**HTTP Request:** /order/market-user-entrust-list
**Request Method:** POST

**Request Parameters**
Parameter  | required  | Type  | Comment
------------- | ------------- | ------------- | -------------
type  | true  | string  | Order direction: 1 buy, 2 sell
coinMarket  | true  | string  | trading pair name
userId  | true  | int  | User ID

**Response Example**
```markdown
{
    code: 1,
    data: {78764432},
    message: "success",
    success: true
}
```

**Response Parameters**
Parameter  | Type  | Comment
------------- | ------------- | -------------
id  | int  | Return code description success
id  | string  | id
coinMarket  | string  | trading pair name
userId  | string  | User ID
entrustNo  | string  | Order number
orderStatus  | string  | 0 pending transaction 1 complete transaction 2 partial transaction 3 canceling 4 canceling successful
exchangeId  | string  | User ID
priceType  | string  | 1 limit price, 2 market price
amount  | string  | number of orders
turnover  | string  | The number of transactions
remainAmount  | string  | The remaining amount
price  | string  | Order price
dealAmount  | string  | Orignal transactions
averagePrice  | string  | Average transaction price
createTime  | string  | Creation time


## 3.4. Page Query Order Transaction Details

**Description**
- Paging query order transaction details

**HTTP Request:** /order/market-entrust-detail-page
**Request Method:** POST

**Request Parameters**
Parameter  | required  | Type  | Comment
------------- | ------------- | ------------- | -------------
pageNum  | true  | string  | request parameters
pageSize  | true  | string  | page number
entrustNo  | true  | String  | records per page


```markdown
{
    code: 1,
    data: { Back to Parameter },
    message: "success",
    success: true
}
```
**Response Parameters**
Parameter  | Type  | Comment
------------- | ------------- | -------------
dealNo  | string  | Transaction number
amount  | string  | The number of transactions
fee  | string  | Handling fee
sellFee  | string  | Sell Fee
buyFee  | string  | Buy Fee
targetEntrustNo  | string  | Opponent order number
Delegation No  | string  | Delegation number
Direction  | string  | Storage direction
Type  | string  | Storage direction
Transaction price  | string  | Transaction price
coinMarket  | string  | Trading pair name
creation time  | string  | creation time


## 3.5. Long Distance Single Interface

**Description**

- Batch cancellation interface, it is recommended to operate a single order

**HTTP Request:** /order/add/market-user-entrusts
**Request Method:** POST

**Request Parameters**
```markdown
{
...,
cancelEntrustList:[{entrustNo:"683948239"},...]
}
```
Parameter  | required  | Type  | Comment
------------- | ------------- | ------------- | -------------
entrustNo  | true  | string  | Order number


**Response Example**

```markdown
{
    code: 1,
    data: {},
    message: "success",
    success: true
}
```

Remark

## 3.6. Page Query User Order History
**Description**
- User order history

**HTTP Request:** /order/entrust-history-pagination
**Request Method:** POST

**Request Parameters**  
Parameter  | required  | Type  | Comment
------------- | ------------- | ------------- | -------------
type  | true  | string  | 	Order direction: 1 buy, 2 sell
coinMarket  | true  | string  | trading pair name
userId  | true  | int  | User ID

**Response Example**
```markdown
{
    "code":1,
    "message":"success",
    "data":{
    "records":[],
    "total":0,
    "size":10,
    "current":1,
    "orders":[Back to Parameter],
    "searchCount":true,
    "pages":0},
    "success":true
}
```

**Response Parameters**

Parameter  | Type  | Comment
------------- | ------------- | -------------
id  | string  | id
type  | string  | Order direction: 1 buy, 2 sell
coinMarket  | string  | trading pair name
userId  | string  | User ID
entrustNo  | string  | Order number
status  | string  | 0 pending transaction 1 complete transaction 2 partial transaction 3 canceling 4 canceling successful
exchangeId  | string  | Transaction pair ID
priceType  | string  | 1 limit price, 2 market price
turnover  | string  | number of orders
volume  | string  | The number of transactions
remainAmount  | string  | The remaining amount
exchangeId  | string  | Transaction pair ID
priceType  | string  | 1 buy, 2 sell
turnover  | string  | number of orders
volume  | string  | The number of transactions
remainAmount  | string  | The remaining amount
price  | string  | Order price
totalTurnover  | string  | Orignal transactions
averagePrice  | string  | Average transaction price
entrustFee  | string  | Order price
updateTime  | string  | Update time
createTime  | string  | Creation time

# 4. Quote Interface
## 4.1. Get Quotes

**Description**
- Get Quotes

**Request URL:** /market/kLine
**Request Method:** POST

**Request Parameters**
Parameter  | required  | Type  | Comment
------------- | ------------- | ------------- | -------------
coinMarket  | true  | string  | Pair
type  | true  | string  | Interval

Interval Value (lowercase/uppercase)

Value  | Comment
------------- | -------------
ONE_MINUTE  | 1 minutes
FIVE_MINUTE  | 5 minutes
FIFTEEN_MINUTE  | 15 minutes
THIRTY_MINUTE  | 30 minutes
ONE_HOUR  | 1 hour
FOUR_HOUR  | 4 hour
ONE_DAY  | 1 day
ONE_WEEK  | One week
ONE_MONTH  | One month

**Request Example**

```markdown
{coinMarket: "BTC/USDT", type: "one_minute"}
```

**Response Example**
```markdown
{
    code:1
    message:" success ",
    data:[{
    amount: 20.132175,
    close: 29991.55,
    coinMarket: "BTC/USDT",
    dimension: "one_minute",
    high: 30106.08,
    low: 29991.55,
    open: 30103.67,
    rangeAbility: -0.0037,
    rangeAbilityAmount: -112.12,
    time: 1652987700,
    turnover: 605233.18},...],
    success:true
}
```

**Response Parameters**
Parameter  | Type  | Comment
------------- | ------------- | -------------
amount  | string  | Volume
close  | string  | Close price
coinMarket  | string  | Pair
dimension  | string  | One week
high  | string  | Order number
One month  | string  | One month
Open  | string  | Open price
rangeAbility  | string  | different width
rangeAbilityAmount  | string  | Price width
Time  | string  | Time
Turnover  | string  | Transaction value

# 5. Market Data
## 5.1. Market Data Summary

**Description**
- The summary endpoint is to provide an overview of market data for all tickers and all market pairs on the exchange.

**Request URL:** /market/summary

**Request Method:** POST

**Response Example**

```markdown
{
    "code": 1,
    "message": "success",
    "data": [
        {
            "trading_pairs": "BTC_USDT",
            "last_price": "23793.73",
            "base_volume": "1371.276427",
            "quote_volume": "0.8055245229432614",
            "highest_bid": "23793.73",
            "lowest_ask": "23793.73",
            "highest_price_24h": "24226.01",
            "lowest_price_24h": "22807.09",
            "price_change_percent_24h": "811.130000"
        },
        {
            "trading_pairs": "ETH_USDT",
            "last_price": "1668.38",
            "base_volume": "1498.4312",
            "quote_volume": "48923086.32",
            "highest_bid": "1668.38",
            "lowest_ask": "1668.38",
            "highest_price_24h": "1694.43",
            "lowest_price_24h": "1559.56",
            "price_change_percent_24h": "92.8400"
        }
    ],
    "success": true
}
```
**Response Parameters**
Parameter  | Type
------------- |  -------------
code  | int  
message  | string
data  | array  
trading_pairs  | string  
last_price  | string  
base_volume  | string 
quote_volume  | string  
highest_bid  | string 
lowest_ask  | string
highest_price_24h  | string  
lowest_price_24h   | string
price_change_percent_24h   | string
success   | boolen

## 5.2. Assets

**Description**
- The assets endpoint is to provide a detailed summary for each currency available on the exchange.

**Request URL:** /market/assets

**Request Method:** POST

**Response Example**

```markdown
{
    "code": 1,
    "message": "success",
    "data": {
        "FIL": {
            "name": "filecoin",
            "unified_cryptoasset_id": null,
            "can_withdraw": "true",
            "can_deposit": "false",
            "min_withdraw": "0.2000000000000000",
            "max_withdraw": "10000.0000000000000000",
            "maker_fee": "0.1",
            "taker_fee": "0.1"
        },
        "EOS": {
            "name": "eos20",
            "unified_cryptoasset_id": null,
            "can_withdraw": "true",
            "can_deposit": "false",
            "min_withdraw": "1.0000000000000000",
            "max_withdraw": "10000.0000000000000000",
            "maker_fee": "0.2",
            "taker_fee": "0.2"
        }
    },
    "success": true
}
```
**Response Parameters**
Parameter  | Type
------------- |  -------------
code  | int  
message  | string
data  | Json Object  
name  | string  
unified_cryptoasset_id  | int  
can_withdraw  | string 
can_deposit  | string  
min_withdraw  | string 
max_withdraw  | string
maker_fee  | string  
taker_fee   | string
success   | boolen

## 5.3. Tickers

**Description**
- The ticker endpoint is to provide a 24-hour pricing and volume summary for each market pair available on the exchange.

**Request URL:** /market/v2/ticker

**Request Method:** POST

**Response Example**

```markdown
{
    "code": 1,
    "message": "success",
    "data": {
        "BTC_USDT": {
            "base_id": null,
            "quote_id": null,
            "base_volume": "1434.071094",
            "quote_volume": "33939184.831000",
            "last_price": "23419.11",
            "isFrozen": "0"
        },
        "ETH_USDT": {
            "base_id": null,
            "quote_id": null,
            "base_volume": "1505.1480",
            "quote_volume": "49146827.95",
            "last_price": "1666.18",
            "isFrozen": "0"
        }
    },
    "success": true
}
```
**Response Parameters**
Parameter  | Type
------------- |  -------------
code  | int  
message  | string
data  | Json Object  
base_id | int
quote_id | int
base_volume | string
quote_volume | string
last_price | string
isFrozen | string
success   | boolen

## 5.4. Order Book

**Description**
- The order book endpoint is to provide a complete order book (arranged by best asks/bids) with full depth returned for a given market pair.

**Request URL:** /market/orderbook/market_pair

**Request Method:** POST

**Request Parameters**
Parameter  | Type
------------- |  -------------
market_pair  | string  

**Request Example**
```markdown
{
    "market_pair": "BTC_USDT"
}
```

**Response Example**

```markdown
{
    "code": 1,
    "message": "success",
    "data": {
        "bids": [
            [
                "23799.29",
                "1.500000"
            ],
            [
                "23799.27",
                "1.500000"
            ],
            [
                "23799.26",
                "1.000000"
            ],
            [
                "23799.25",
                "2.500000"
            ],
            [
                "23792.89",
                "1.500000"
            ]
        ],
        "asks": [
            [
                "23799.30",
                "1.500000"
            ],
            [
                "23801.35",
                "0.500000"
            ],
            [
                "23801.37",
                "1.000000"
            ],
            [
                "23803.05",
                "0.500000"
            ],
            [
                "23803.06",
                "0.500000"
            ]
        ],
        "timestamp": 1675321704527
    },
    "success": true
}
```
**Response Parameters**
Parameter  | Type
------------- |  -------------
code  | int  
message  | string
data  | Json Object  
bids | array
asks | array
timestamp | int
success   | boolen

## 5.5. Trades

**Description**
- The trades endpoint is to return data on all recently completed trades for a given market pair.

**Request URL:** /market/trades/market_pair

**Request Method:** POST

**Request Parameters**
Parameter  | Type
------------- |  -------------
market_pair  | string  

**Request Example**
```markdown
{
    "market_pair": "BTC_USDT"
}
```

**Response Example**

```markdown
{
    "code": 1,
    "message": "success",
    "data": [
        {
            "trade_id": "47357514",
            "price": "23420.92",
            "timestamp": 1675418006,
            "type": "buy",
            "base_volume": "0.500000",
            "quote_volume": "11710.460000"
        },
        {
            "trade_id": "61739823",
            "price": "23422.58",
            "timestamp": 1675417960,
            "type": "sell",
            "base_volume": "0.500000",
            "quote_volume": "11711.290000"
        },
        {
            "trade_id": "24837589",
            "price": "23422.64",
            "timestamp": 1675417946,
            "type": "buy",
            "base_volume": "0.500000",
            "quote_volume": "11711.320000"
        }
    ],
    "success": true
}
```
**Response Parameters**
Parameter  | Type
------------- |  -------------
code  | int  
message  | string
data  | Json Object  
trade_id | string
price | string
timestamp | int
type | string
base_volume | string
quote_volume | string
success   | boolen
