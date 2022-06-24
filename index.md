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