# Stellar API #

Stellar-REST API 提供基于Stellar的API封装。

## API Routes ##

#### 账户 ####

* [生成 - `GET /v1/account/new`](#生成账户)
* [注销 - `POST /v1/account/delete`](#get-account-balances)
* [开户 - `POST /v1/account/prepare`](#get-account-settings)
* [查询 - `GET  /v1/account/{:address}/info`](#update-account-settings)


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


