# Stellar API #

Stellar-REST API 提供基于Stellar的API封装。

## API Routes ##

#### 账户 ####

* [生成 - `GET /v1/account/new`](#生成账户)
* [注销 - `POST /v1/account/delete`](#注销账户)
* [开户 - `POST /v1/account/prepare`](#开户)
* [查询 - `GET  /v1/account/{:address}/info`](#账户查询)

# 账户 #

账户是恒星中最基本的元素，每个账户都需要一定量的原生资产才能存在于账本之中。每个账户的交易都需要其私钥进行签名才能执行。

## 生成账户 ##

随机生成一个账号地址。注意：此操作未对区块链产生改变，账号需经激活后方可使用。*私钥请用安全的方法保管。*

```
GET /v1/account/new
```
#### 响应 ####

```js
{
    "success": true,
    "account": {
        "address": "GAYELCLJDXHTQIY6XF2I6SW3H6W74Z5XNM2M7APMIHO3CKXAO56OSWSG",
        "secret": "SCOQEJIF2LP2QHG6XBBW4XY63NEMQTA4CWDSIMHSAK6MQHQ77GO4HGQK"
    }
}
```

| 参数 | 类型 | 描述 |
|-------|-------|-------------|
| success | boolean | 只能是true |
| account | object | 由address,secret两个string组成 |


## 注销账户 ##

注销账户，原有账户的资产将转移到一个特殊的回收账户中。

```
POST /v1/account/delete
{
    "address": "GAYELCLJDXHTQIY6XF2I6SW3H6W74Z5XNM2M7APMIHO3CKXAO56OSWSG",
    "secret": "SCOQEJIF2LP2QHG6XBBW4XY63NEMQTA4CWDSIMHSAK6MQHQ77GO4HGQK"
}
```
#### 响应 ####

```js
{
    "success": true,
    "hash": "88bad5ec60f9516afbbd216ff64df296db81dc246b8d0037b506c1a7a636a75d"
}
```

| 参数 | 类型 | 描述 |
|-------|-------|-------------|
| success | boolean | true/false |
| error_code | string | 出错代码 |
| error_detail | string | 出错的描述和补充信息 |
| hash | string | 成功时返回的交易id |


## 开户 ##

多个动作的交易。第一步是特殊的激活，往需开户的账号发送200个原生资产。第二步是账号开展授信。

```
POST /v1/account/prepare
{
    "address": "GAYELCLJDXHTQIY6XF2I6SW3H6W74Z5XNM2M7APMIHO3CKXAO56OSWSG",
    "secret": "SCOQEJIF2LP2QHG6XBBW4XY63NEMQTA4CWDSIMHSAK6MQHQ77GO4HGQK"
}
```
#### 响应 ####

```js
{
    "success": true,
    "hash": "88bad5ec60f9516afbbd216ff64df296db81dc246b8d0037b506c1a7a636a75d"
}
```

| 参数 | 类型 | 描述 |
|-------|-------|-------------|
| success | boolean | true/false |
| error_code | string | 出错代码 |
| error_detail | string | 出错的描述和补充信息 |
| hash | string | 成功时返回的交易id |


## 账户查询 ##

查询账户信息。

```
GET /v1/account/{:address}/info
```
#### 响应 ####

```js
{
    "success": true,
    "address": "GAYELCLJDXHTQIY6XF2I6SW3H6W74Z5XNM2M7APMIHO3CKXAO56OSWSG",
    "balances": [
    {
      "balance": "126.8107491",
      "asset_type": "credit_alphanum4",
      "asset_code": "DDL",
      "asset_issuer": "GBAUUA74H4XOQYRSOW2RZUA4QL5PB37U3JS5NE3RTB2ELJVMIF5RLMAG"
    },
    {
      "balance": "294.0000000",
      "asset_type": "credit_alphanum4",
      "asset_code": "DDN",
      "asset_issuer": "GBAUUA74H4XOQYRSOW2RZUA4QL5PB37U3JS5NE3RTB2ELJVMIF5RLMAG"
    },
    {
      "balance": "9997.6802725",
      "asset_type": "native"
    }
  ],
  "data": {
    "datakey": "datavalue"
  }
}
```

| 参数 | 类型 | 描述 |
|-------|-------|-------------|
| success | boolean | true/false |
| error_code | string | 出错代码 |
| error_detail | string | 出错的描述和补充信息 |
| address | string | 账号ID |
| balances | array | 资产数组 |
| data | object | 键值对，用于存储一些关键短小的信息 |


