---
title: BlockMarkets API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - curl

toc_footers:
  - <a href='https://www.blockmarkets.io/'>BlockMarkets Website</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the BlockMarkets API.

BlockMarkets provides real-time and historical market data from the leading global cryptocurrency exchanges, along with USD spot prices for over 100 cryptoassets that can be used for price discovery, portfolio valuation, and backtesting. We are committed to building the fastest and most reliable API for cryptocurrency pricing applications.


## Authentication

> Request Syntax


```curl
curl "https://api.blockmarkets.io/v1"
  -H "x-api-key: <client-api-key>"
```

The base url for the API is: 

`https://api.blockmarkets.io/v1`

Clients must include an API key in the header of every request they make to the API. The format is as follows:

`x-api-key: <client-api-key>`

<aside class="notice">
You must replace <code>&lt;client-api-key&gt;</code> with your assigned API key.
</aside>


## Timestamps

All timestamps are in UTC and returned in the following ISO 8601 datetime format:

`YYYY-MM-DD`**T**`hh:mm:ss.sss`**Z**

For example:

`2017-12-17T13:35:24.351Z`

The "T" separates the date from the time. The “Z” at the end indicates that this is a UTC time.

Timestamp arguments must also be in this format.


## Market Open and Close

Digital asset exchanges operate 24x7x365. 

For USD spot prices and market pairs, the opening price is calculated as the first trade at or after 00:00:00 UTC. The closing price is calculated as the last trade prior to 00:00:00 UTC.

Benchmark rates are calculated at 4pm GMT, 4pm EST, and zero UTC.

## Envelope

> Response Example

```json
{
	"result": "success",
	"server_time": "2018-10-21T01:27:30.965Z",
	"data": [...]
}

```

All API responses are in JSON format. A **result** key, with a value of **success** or **error**, is returned with each request. Upon an **error**, a **message** key will provide an explanation of the error. The **server_time** key displays the datetime on the server at the time of the request. The **data** key contains the results of the request.


# Assets

## Index

> Request Example

```curl
curl "https://api.blockmarkets.io/v1/assets"
  -H "x-api-key: <client-api-key>"
```

> Response Example

```json
{
	"result": "success",
	"server_time": "2018-10-21T03:27:30.965Z",
	"data": [
		{
			"symbol": "BTC",
			"name": "Bitcoin",
			"is_fiat": false
		},
		{
			"symbol": "BCH",
			"name": "Bitcoin Cash",
			"is_fiat": false
		},
		...
	]
}
```

Returns a list of supported assets.

### HTTP Request

`GET https://api.blockmarkets.io/v1/assets`

### Parameters

Parameter | Required | Description
--------- | -------- | ---------
none	|


## Asset

> Request Example

```curl
curl "https://api.blockmarkets.io/v1/assets/BTC"
  -H "x-api-key: <client-api-key>"
```


> Response Example

```json
{
	"result": "success",
	"server_time": "2018-10-21T03:27:30.965Z",
	"data": [
		{
			"symbol": "BTC",
			"name": "Bitcoin",
			"is_fiat": false,
            "markets": {
                "base": [
                    {
                        "exchange": "BNCE",
                        "pair": "BTC-USDT"
                    },
                    {
                        "exchange": "BFNX",
                        "pair": "BTC-EUR"
                    },
                    ...
                ],
                "quote": [
                    {
                        "exchange": "BNCE",
                        "pair": "ADA-BTC"
                    },
                    {
                        "exchange": "BNCE",
                        "pair": "ADX-BTC"
                    },
                    ...
		}
	]
}
```

Returns a list of all markets (base and quote) for a specific asset.

### HTTP Request

`GET https://api.blockmarkets.io/v1/assets/{symbol}`

### Parameters

Parameter | Required | Description
--------- | -------- | ---------
symbol | Yes | See /v1/assets





# Pairs

## Index

> Request Example

```curl
curl "https://api.blockmarkets.io/v1/pairs"
  -H "x-api-key: <client-api-key>"
```


> Response Example

```json
{
    "result": "success",
    "server_time": "2018-10-21T09:29:31.959Z",
    "data": [
        {
            "pair": "ABT-BTC",
            "base": {
                "symbol": "ABT",
                "name": "Arcblock",
                "is_fiat": false
            },
            "quote": {
                "symbol": "BTC",
                "name": "Bitcoin",
                "is_fiat": false
            }
        },
        {
            "pair": "ABT-ETH",
            "base": {
                "symbol": "ABT",
                "name": "Arcblock",
                "is_fiat": false
            },
            "quote": {
                "symbol": "ETH",
                "name": "Ethereum",
                "is_fiat": false
            }
        },
        ...
	]
}
```

Returns a list of supported asset pairs.


### HTTP Request

`GET https://api.blockmarkets.io/v1/pairs`

### Parameters

Parameter | Required | Description
--------- | -------- | ---------
none	| |



## Pair

> Request Example

```curl
curl "https://api.blockmarkets.io/v1/pairs/BTC-USD"
  -H "x-api-key: <client-api-key>"
```


> Response Example

```json
{
    "result": "success",
    "server_time": "2018-10-21T09:32:38.832Z",
    "data": [
        {
            "pair": "BTC-USD",
            "base": {
                "symbol": "BTC",
                "name": "Bitcoin",
                "is_fiat": false
            },
            "quote": {
                "symbol": "USD",
                "name": "US Dollar",
                "is_fiat": true
            },
            "markets": [
                {
                    "exchange": "BFNX",
                    "pair": "BTC-USD",
                    "start_date": "2013-01-14"
                },
                {
                    "exchange": "BFLY",
                    "pair": "BTC-USD",
                    "start_date": "2017-09-06"
                },
                ...
			]
		}
	]
}				
```

Returns a list of markets for a specific asset pair.


### HTTP Request

`GET https://api.blockmarkets.io/v1/pairs/{pair}`

### Parameters

Parameter | Required | Description
--------- | -------- | ---------
pair | Yes | See /v1/pairs







# Exchanges


## Index

> Request Example

```curl
curl "https://api.blockmarkets.io/v1/exchanges"
  -H "x-api-key: <client-api-key>"
```

> Response Example

```json
{
    "result": "success",
    "server_time": "2018-10-21T09:36:58.347Z",
    "data": [
        {
            "exchange": "BNCE",
            "name": "Binance",
            "website": "https://www.binance.com/",
            "country": "Hong Kong",
            "country_iso": "HKG"
        },
        {
            "exchange": "BFNX",
            "name": "Bitfinex",
            "website": "https://www.bitfinex.com",
            "country": "Hong Kong",
            "country_iso": "HKG"
        },
        ...
	]
}
```

Returns a list of supported exchanges.


### HTTP Request

`GET https://api.blockmarkets.io/v1/exchanges`

### Parameters

Parameter | Required | Description
--------- | -------- | ---------
none	| |




## Exchange

> Request Example

```curl
curl "https://api.blockmarkets.io/v1/exchanges/CPRO"
  -H "x-api-key: <client-api-key>"
```


> Response Example

```json
{
    "result": "success",
    "server_time": "2018-10-21T09:37:57.070Z",
    "data": [
        {
            "exchange": "CPRO",
            "name": "Coinbase Pro",
            "website": "https://pro.coinbase.com/",
            "country": "United States",
            "country_iso": "USA",
            "markets": [
                {
                    "pair": "BCH-BTC",
                    "start_date": "2018-01-17"
                },
                {
                    "pair": "BCH-EUR",
                    "start_date": "2018-01-24"
                },
                ...
			]
		}
	]
}
```

Returns a list of markets for a specific exchange.

### HTTP Request

`GET https://api.blockmarkets.io/v1/exchanges/{exchange}`

### Parameters

Parameter | Required | Description
--------- | -------- | ---------
exchange | Yes | See /v1/exchanges








# Markets


## Index

> Request Example

```curl
curl "https://api.blockmarkets.io/v1/markets"
  -H "x-api-key: <client-api-key>"
```

> Response Example

```json
{
    "result": "success",
    "server_time": "2018-10-21T09:43:37.513Z",
    "data": [
        {
            "exchange": "BFLY",
            "pair": "ETH-BTC",
            "start_date": "2016-04-14"
        },
        {
            "exchange": "BFLY",
            "pair": "BCH-BTC",
            "start_date": "2017-08-02"
        },
        ...
	]
}
```

Returns a list of all supported markets.


### HTTP Request

`GET https://api.blockmarkets.io/v1/markets`

### Parameters

Parameter | Required | Description
--------- | -------- | ---------
none	| |




## Market

> Request Example

```curl
curl "https://api.blockmarkets.io/v1/markets/CPRO"
  -H "x-api-key: <client-api-key>"
```


> Response Example

```json
{
    "result": "success",
    "server_time": "2018-10-21T09:37:57.070Z",
    "data": [
        {
            "exchange": "CPRO",
            "name": "Coinbase Pro",
            "website": "https://pro.coinbase.com/",
            "country": "United States",
            "country_iso": "USA",
            "markets": [
                {
                    "pair": "BCH-BTC",
                    "start_date": "2018-01-17"
                },
                {
                    "pair": "BCH-EUR",
                    "start_date": "2018-01-24"
                },
                ...
			]
		}
	]
}
```

Returns a list of markets for a specific exchange.

### HTTP Request

`GET https://api.blockmarkets.io/v1/markets/{exchange}`

### Parameters

Parameter | Required | Description
--------- | -------- | ---------
exchange | Yes | See /v1/exchanges






## Ticker

> Request Example

```curl
curl "https://api.blockmarkets.io/v1/markets/CPRO/BTC-USD"
  -H "x-api-key: <client-api-key>"
```


> Response Example

```json
{
    "result": "success",
    "server_time": "2018-10-21T09:47:16.502Z",
    "data": [
        {
            "last": 6440,
            "amount": 0.00162387,
            "open_24h": 6406.23,
            "high_24h": 6452.87,
            "low_24h": 6390.1,
            "vol_24h": 2635.82,
            "time": "2018-10-21T09:47:13.455Z"
        }
    ]
}
```

Returns ticker for a market pair.


### HTTP Request

`GET https://api.blockmarkets.io/v1/exchanges/{exchange}/{pair}`

### Parameters

Parameter | Required | Description
--------- | -------- | ---------
exchange | Yes | See /v1/exchanges
pair | Yes | See /v1/pairs




## Trades

> Request Example

```curl
curl "https://api.blockmarkets.io/v1/markets/CPRO/BTC-USD/trades"
  -H "x-api-key: <client-api-key>"
```


> Response Example

```json
{
    "result": "success",
    "server_time": "2018-10-21T09:49:00.988Z",
    "data": [
        {
            "tid": 52743331,
            "price": 6439.99,
            "amount": 0.00225,
            "time": "2018-10-21T09:48:57.588Z",
            "side": "s",
            "created_at": "2018-10-21T09:48:58.563Z"
        },
        {
            "tid": 52743330,
            "price": 6440,
            "amount": 0.00525287,
            "time": "2018-10-21T09:48:42.619Z",
            "side": "b",
            "created_at": "2018-10-21T09:48:43.600Z"
        },
        ...
	]
}
```

Returns trades for a market pair. By default returns the 100 most recent trades. Use parameters to return historical trades.


### HTTP Request

`GET https://api.blockmarkets.io/v1/markets/{exchange}/{pair}/trades{?limit,start,end}`

### Parameters

Parameter | Required | Description
--------- | -------- | ---------
exchange | Yes | See /v1/exchanges
pair | Yes | See /v1/pairs
limit | No | Number of records to retrieve (default = 100, max = 1000)
start | No | Starting datetime in ISO 8601
end | No | Ending datetime in ISO 8601 (or when limit is reached)




## OHLCV

> Request Example

```curl
curl "https://api.blockmarkets.io/v1/markets/CPRO/BTC-USD/ohlcv"
  -H "x-api-key: <client-api-key>"
```


> Response Example

```json
{
    "result": "success",
    "server_time": "2018-11-02T19:56:47.424Z",
    "data": [
        {
            "time_start": "2018-11-01T00:00:00.000Z",
            "time_end": "2018-11-02T00:00:00.000Z",
            "open": 6304.18,
            "high": 6360,
            "low": 6293.44,
            "close": 6344,
            "volume": 4490.97798078,
            "vwap": 6313.475512761219,
            "ticks": 39448
        },
        {
            "time_start": "2018-10-31T00:00:00.000Z",
            "time_end": "2018-11-01T00:00:00.000Z",
            "open": 6267.63,
            "high": 6353.24,
            "low": 6201.67,
            "close": 6304.18,
            "volume": 5229.17300922,
            "vwap": 6279.573836439961,
            "ticks": 40903
        },
		...
	]
}
```

Returns OHLCV history for a market pair. By default returns the most recent daily OHLCV values. Use parameters to return historical OHLCV.


### HTTP Request

`GET https://api.blockmarkets.io/v1/exchanges/{exchange}/{pair}/ohlcv{?limit,interval,start,end}`

### Parameters

Parameter | Required | Description
--------- | -------- | ---------
exchange | Yes | See /v1/exchanges
pair | Yes | See /v1/pairs
limit | No | Number of records to retrieve (default = 100, max = 1000)
interval | No | Interval period in minutes. Supported: 1, 3, 5, 15, 30, 60, 1440 (default = 1440)
start | No | Starting datetime in ISO 8601
end | No | Ending datetime in ISO 8601 (or when limit is reached)





# Spot Rates

## Index

> Request Example

```curl
curl "https://api.blockmarkets.io/v1/rates/spot"
  -H "x-api-key: <client-api-key>"
```

> Response Example

```json
{
    "result": "success",
    "server_time": "2018-11-02T21:08:20.357Z",
    "data": [
        {
            "symbol": "ADA",
            "name": "Cardano"
        },
        {
            "symbol": "AE",
            "name": "Aeternity"
        },
        {
            "symbol": "AGI",
            "name": "SingularityNET"
        },
        {
            "symbol": "AION",
            "name": "Aion"
        },
		...
	]
}
```

Returns a list of available USD spot rates.


### HTTP Request

`GET https://api.blockmarkets.io/v1/rates/spot`

### Parameters

Parameter | Required | Description
--------- | -------- | ---------
none	| |




## Rate

> Request Example

```curl
curl "https://api.blockmarkets.io/v1/rates/spot/BTC"
  -H "x-api-key: <client-api-key>"
```


> Response Example

```json
{
    "result": "success",
    "server_time": "2018-11-02T15:42:57.358Z",
    "data": [
        {
            "last": 6391.0023,
            "open_24h": 6331.4993,
            "high_24h": 6422.0365,
            "low_24h": 6325.8124,
            "time": "2018-11-02T15:42:39.164Z"
        }
    ]
}
```

Returns the last USD spot rate for an asset.

### HTTP Request

`GET https://api.blockmarkets.io/v1/rates/spot/{symbol}`

### Parameters

Parameter | Required | Description
--------- | -------- | ---------
symbol | Yes | See /v1/assets





## History

> Request Example

```curl
curl "https://api.blockmarkets.io/v1/rates/spot/BTC/history"
  -H "x-api-key: <client-api-key>"
```


> Response Example

```json
{
    "result": "success",
    "server_time": "2018-11-02T15:43:48.482Z",
    "data": [
        {
            "time": "2018-11-02T15:43:47.869Z",
            "price": 6391.5528
        },
        {
            "time": "2018-11-02T15:43:42.354Z",
            "price": 6391.466
        },
        {
            "time": "2018-11-02T15:43:41.852Z",
            "price": 6393.0444
        },
		...
	]
}
```

Returns historical spot rates for an asset. By default returns the 100 most recent rates.

### HTTP Request

`GET https://api.blockmarkets.io/v1/rates/spot/{symbol}/history{?limit,start,end}`

### Parameters

Parameter | Required | Description
--------- | -------- | ---------
symbol | Yes | See /v1/assets
limit | No | Number of records to retrieve (default = 100, max = 1000)
start | No | Starting datetime in ISO 8601
end | No | Ending datetime in ISO 8601 (or when limit is reached)


## OHLCV

> Request Example

```curl
curl "https://api.blockmarkets.io/v1/rates/spot/BTC/ohlcv"
  -H "x-api-key: <client-api-key>"
```


> Response Example

```json
{
    "result": "success",
    "server_time": "2018-11-02T19:55:57.651Z",
    "data": [
        {
            "time_start": "2018-11-01T00:00:00.000Z",
            "time_end": "2018-11-02T00:00:00.000Z",
            "open": 197.8094,
            "high": 199.6458,
            "low": 196.881,
            "close": 198.8524,
            "ticks": 67950
        },
        {
            "time_start": "2018-10-31T00:00:00.000Z",
            "time_end": "2018-11-01T00:00:00.000Z",
            "open": 196.4452,
            "high": 199.9528,
            "low": 192.6163,
            "close": 197.9165,
            "ticks": 70366
        },
		...
	]
}
```

Returns the OHLCV history for a spot rate. By default returns the latest daily history.

### HTTP Request

`GET https://api.blockmarkets.io/v1/rates/spot/{symbol}/ohlcv{?limit,interval,start,end}`

### Parameters

Parameter | Required | Description
--------- | -------- | ---------
symbol | Yes | See /v1/assets
limit | No | Number of records to retrieve (default = 100, max = 1000)
interval | No | Interval period in minutes. Supported: 1, 3, 5, 15, 30, 60, 1440 (default = 1440)
start | No | Starting datetime in ISO 8601
end | No | Ending datetime in ISO 8601 (or when limit is reached)


# Websocket

The BlockMarkets websocket delivers real-time streaming data to your application. A premium subscription is required for this service. See our <a href='https://www.blockmarkets.io/api'>API Plans</a> for details.

## Authentication

> Respone Example


```json
{
	"result": "success",
	"action": "authenticate",
	"data": "Authentication Succeeded."
}
```

The websocket feed is located at: 

`wss://ws.blockmarkets.io`

Clients must authenticate using their assigned API key:

`{ "action": "authenticate", "token": "<client-api-key>" }`


## Subscribe

> Response Example (Spot Rate)

```json
{
	"result": "success",
	"action": "subscribe",
	"data": {
		"type": "spot",
		"symbol": "BTC",
		"price": 6381.3241,
		"time": "2018-11-02T22:43:42.513Z"	
	}
}
```

> Response Example (Market Pair)

```json
{
	"result": "success",
	"action": "subscribe",
	"data": {
		"type": "market",
		"pair": "BTC-USD",
		"exchange": "CPRO",
		"price": 6350.01,
		"amount": 0.00438907,
		"time": "2018-11-02T22:44:31.555Z"	
	}
}
```


Clients can subscribe to receive real-time spot rates, and real-time trades from exchanges. Please note that each subscribe request overwrites the previous subscribe request. Here are some examples.

**USD Spot Rates**

`{ "action": "subscribe", "channels": ["BTC", "XLM", "ETH" ] }`

**Market trades from all exchanges**

`{ "action": "subscribe", "channels": ["BTC-USD", "XLM-BTC" ] }`

**Market pair trades**

`{ "action": "subscribe", "channels": ["CPRO:BTC-USD", "KRKN:ZEC-USD" ] }`

**Multiple channels**

`{ "action": "subscribe", "channels": ["BTC-USD", "XLM", "CPRO:ETH-USD" ] }`




## Unsubscribe

To unsubscribe from a product, send a new subscribe request excluding the product you wish to unsubscribe from. 





