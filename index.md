## Global API Description

Signature description

The request parameters are sorted and spliced ​​together in ascending dictionary order (the timestamp should also be added to verify the signature), and the string to be signed is generated. All parameters have values:


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

```markdown

Assign this value to the signature parameter signature, and then put the signature in the request header. Note: For the following parameters to sign, please note: please remove the invalid 0 in the incoming parameters, such as coin_amount = 100, please do not pass in 100.00 for signature verification, generate a signature for the parameters according to the signature rules, and compare it with the signature in the request header, If they are consistent, the signature is passed.

```

### Description of all API requests

Request address:https://www.hkd.com/api

Parameter  | required  | Type  | caption
------------- | ------------- | ------------- | -------------
channel  | true  | int  | Fill in 5, representing API_USER (api user)
time  | true  | long  | Fill in 5, representing API_USER (api user)
Timestamp when the merchant initiates the request, Beijing time UTC+8  | true  | string  | sign
api-version  | true  | string  | API version number, default v1

Parameter  | required  | Type  | caption
------------- | ------------- | ------------- | -------------
channel  | true  | int  | Fill in 5, representing API_USER (api user)

Parameter  | required  | Type  | caption
------------- | ------------- | ------------- | -------------
Fill in 5, representing API_USER (api user)  | true  | ...  | ...


Return the sample

```markdown

{
code: 1,
data: {...},
message: "success",
success: true
}

```

Return parameter description

Parameter  | Type | caption
------------- | ------------- | -------------
code  | int | Return code 1: Response value 1 indicates success, other values ​​indicate failure
data  | jsonObject | business data, json object
message  | string | Return code description success
success  | boolean | true=success, false=failure true


# 2. User related

## 2.1. Get personal balance

[TOC]

A brief description

- Get personal balance

** request URL

/account/query/coin-account
request method


Parameter  | required  | Type  | caption
------------- | ------------- | ------------- | -------------
coinName  | true  | string  | Currency name :USDT,BTC

Parameter  | required  | Type  | caption
------------- | ------------- | ------------- | -------------
accountType  | true  | string  | account type


Parameter  | caption
------------- | -------------
1  | Exchange Account
2  | Fiat Account
3  | Isolate-M
4  | USDⓈ-M


Return the sample

```markdown

{
code: 1,
data: {coinName: "ETH", accountType: 1, amount: 15, frozenAmount: 20},
message: "success",
success: true
}

```


Return parameter description

Parameter  | Type  | caption
------------- | ------------- | -------------
amount  | string  | Available Balance
frozenAmount  | string  | Frozen Balance

# 3. Order Api

## 3.1、 Order Api

[TOC]

**A brief description**

- Single order Api

**request URL**

/order/add/market-user-entrust

**request method**

post

Parameter  | required  | Type  | caption
------------- | ------------- | ------------- | -------------
type  | true  | string  | string
orderType  | true  | string  | Order type: 1 limit price, 2 market price
coinMarket  | true  | string  | trading pair name
amount  | true  | BigDecimal  | number of orders
type  | true  | string  | string
price  | true  | BigDecimal  | Order price
userId  | true  | int  | User ID
uid  | true  | int  | User ID

Return the sample

```markdown

{
code: 1,
data: {"78764432"},
message: "success",
success: true
}

```

Remark

data is the order number entrustNo

## 3.2. Batch order API

[TOC]

**A brief description**

Quantity - batch order API, now the quantity is within 15 each time < quantity

**request URL**

/order/add/market-user-entrusts

**request method**

Example of post request parameters


```markdown

{
    {
    ...,
entrustVos: [{ Single Order Parameter },{...}]
}

```

Parameters


Parameter  | required  | Type  | caption
------------- | ------------- | ------------- | -------------
type  | true  | string  | Order direction: 1 buy, 2 sell
orderType  | true  | string  | Order type: 1 limit price, 2 market price
coinMarket  | true  | string  | trading pair name
amount  | true  | BigDecimal  | number of orders
price  | true  | BigDecimal  | Order price
userId  | true  | int  | User ID
uid  | true  | int  | User ID


Return the sample

```markdown

{
    code: 1,
    data: {"78764432","78764431",...},
    message: "success",
    success: true
}

```

## 3.3. List of pending orders for users
[TOC]

**A brief description**

- User"s pending order list

**request URL**

/order/market-user-entrust-list

**request method**

- post

Parameter  | required  | Type  | caption
------------- | ------------- | ------------- | -------------
type  | true  | string  | Order direction: 1 buy, 2 sell
coinMarket  | true  | string  | trading pair name
userId  | true  | int  | User ID

Return the sample

```markdown

{
    code: 1,
    data: {78764432},
    message: "success",
    success: true
}

```

Return parameter description

Parameter  | Type  | caption
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


## 3.4、Paging query order transaction details
[TOC]

**A brief description**

- Paging query order transaction details

**request URL**

/order/market-entrust-detail-page

**request method**

post

Parameter  | required  | Type  | caption
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
Return parameter description

Parameter  | Type  | caption
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


## 3.5, long distance single interface
[TOC]

**A brief description**

- Batch cancellation interface, it is recommended to operate a single order

**request URL**

/order/add/market-user-entrusts

**request method**

```markdown

Example of post request parameters
{
...,
cancelEntrustList:[{entrustNo:"683948239"},...]
}
```


Parameter  | required  | Type  | caption
------------- | ------------- | ------------- | -------------
entrustNo  | true  | string  | Order number


Return the sample

```markdown

{
    code: 1,
    data: {},
    message: "success",
    success: true
}

```

Remark

## 3.6. Paging query user history orders
[TOC]

**Brief description**

- Paging query user history orders

**Request URL**

/order/entrust-history-pagination

**Request method**

post

**parameter**   


Parameter  | required  | Type  | caption
------------- | ------------- | ------------- | -------------
type  | true  | string  | 	Order direction: 1 buy, 2 sell
coinMarket  | true  | string  | trading pair name
userId  | true  | int  | User ID

Return the sample

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

Return parameter description

Parameter  | Type  | caption
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


# 4. Quote interface
## 4.1. Get Quotes

[TOC]

**Brief description**

Get Quotes

**Request URL**

/market/kLine

**Request method**

post

parameter

Parameter  | required  | Type  | caption
------------- | ------------- | ------------- | -------------
coinMarket  | true  | string  | Pair
type  | true  | string  | Dimension, market data type

dimension (lowercase automatically converts to uppercase)

Value  | Caption
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

Example of post request parameters

```markdown

{coinMarket: "BTC/USDT", dimension: "one_minute"}

```

Return the sample

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

Parameter  | Type  | caption
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