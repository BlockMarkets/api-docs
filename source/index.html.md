---
title: BlockMarkets.io API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - curl

toc_footers:
  - <a href='https://www.blockmarkets.io/'>BlockMarkets.io Homepage</a>
  - <a href='https://www.blockmarkets.io/#contact-section'>Contact us</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the BlockMarkets API.

BlockMarkets provides real-time, institutional quality price indexes for the leading digital assets. Our system retrieves and validates millions of trades each day from the world's leading cryptocurrency exchanges to deliver robust and reliable price indexes and market data to financial firms globally.


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

For price indexes and exchange data, the opening price is calculated as the first trade at or after 00:00:00 UTC. The closing price is calculated as the last trade prior to 00:00:00 UTC.

We also offer reference rates at 4pm GMT, 4pm EST, and zero UTC. <a href='https://www.blockmarkets.io/#contact-section'>Contact us</a> for details.

## Envelope

> Response Example

```json
{
	"result": "success",
	"server_time": "2017-12-22T03:27:30.965Z",
	"data": [...]
}

```

All API responses are in JSON format. A **result** key, with a value of **success** or **error**, is returned with each request. Upon an **error**, a **message** key will provide an explanation of the error. The **server_time** key displays the datetime on the server at the time of the request. The **data** key contains the results of the request.



# Market Data

## Assets

> Request Example

```curl
curl "https://api.blockmarkets.io/v1/assets"
  -H "x-api-key: <client-api-key>"
```

> Response Example

```json
{
	"result": "success",
	"server_time": "2017-12-22T03:27:30.965Z",
	"data": [
		{
			"asset_id": "BTC",
			"name": "Bitcoin",
			"type": "crypto",
			"website": "https://bitcoin.org/en/",
			"start_date": "2009-01-03",
			"max_supply": 21000000,
			"current_supply": 16751825.5
		},
		{
			"asset_id": "BCH",
			"name": "Bitcoin Cash",
			"type": "crypto",
			"website": "https://www.bitcoincash.org/",
			"start_date": "2017-08-01",
			"max_supply": 21000000,
			"current_supply": 16817156.75
		}
	]
}
```

This endpoint retrieves a list of supported assets.

### HTTP Request

`GET https://api.blockmarkets.io/v1/assets`

### Parameters

Parameter | Required | Description
--------- | -------- | ---------
none	|




## Asset Pairs

> Request Example

```curl
curl "https://api.blockmarkets.io/v1/pairs"
  -H "x-api-key: <client-api-key>"
```


> Response Example

```json
{
	"result": "success",
	"server_time": "2017-12-22T03:27:30.965Z",
	"data": [
		{
			"pair_id": "BTCUSD",
			"name": "BTC/USD",
			"base_id": "BTC",
			"base_name": "Bitcoin",
			"quote_id": "USD",
			"quote_name": "US Dollar"
		},
		{
			"pair_id": "ETHUSD",
			"name": "ETH/USD",
			"base_id": "ETH",
			"base_name": "Ethereum",
			"quote_id": "USD",
			"quote_name": "US Dollar"
		}
	]
}
```

This endpoint retrieves a list of supported asset pairs.


### HTTP Request

`GET https://api.blockmarkets.io/v1/pairs`

### Parameters

Parameter | Required | Description
--------- | -------- | ---------
none	| |



## Exchanges

> Request Example

```curl
curl "https://api.blockmarkets.io/v1/exchanges"
  -H "x-api-key: <client-api-key>"
```

> Response Example

```json
{
	"result": "success",
	"server_time": "2017-12-22T03:27:30.965Z",
	"data": [
		{
			"exchange_id": "BFNX",
			"name": "Bitfinex",
			"website": "https://www.bitfinex.com",
			"country": "Hong Kong",
			"country_iso": "HKG"
		},
		{
			"exchange_id": "BFLY",
			"name": "bitFlyer",
			"website": "https://www.bitflyer.com/",
			"country": "Japan",
			"country_iso": "JPN"
		}
	]
}
```

This endpoint retrieves a list of supported exchanges.


### HTTP Request

`GET https://api.blockmarkets.io/v1/exchanges`

### Parameters

Parameter | Required | Description
--------- | -------- | ---------
none	| |




## Exchange Pairs

> Request Example

```curl
curl "https://api.blockmarkets.io/v1/exchanges/GDAX"
  -H "x-api-key: <client-api-key>"
```


> Response Example

```json
{
	"result": "success",
	"server_time": "2017-12-22T03:27:30.965Z",
	"data": [
		{
			"pair_id": "BTCUSD",
			"name": "BTC/USD"
		},
		{
			"pair_id": "ETHBTC",
			"name": "ETH/BTC"
		}
	]
}
```

This endpoint retrieves a list of asset pairs for a specific exchange.

### HTTP Request

`GET https://api.blockmarkets.io/v1/exchanges/{exchange_id}`

### Parameters

Parameter | Required | Description
--------- | -------- | ---------
exchange_id | Yes | Valid exchange_id from /v1/exchanges.




## Exchange Ticker

> Request Example

```curl
curl "https://api.blockmarkets.io/v1/exchanges/GDAX/BTCUSD"
  -H "x-api-key: <client-api-key>"
```


> Response Example

```json
{
	"result": "success",
	"server_time": "2018-01-07T14:24:23.982Z",
	"data": [
		{
			"last": 16549.99,
			"amount": 0.008899,
			"open_24h": 16420.01,
			"high_24h": 17174,
			"low_24h": 16355,
			"vol_24h": 11631.64,
			"time": "2018-01-07T14:24:15.553Z"
		}
	]
}
```

This endpoint retrieves the ticker data for an asset pair on a specific exchange.


### HTTP Request

`GET https://api.blockmarkets.io/v1/exchanges/{exchange_id}/{pair_id}`

### Parameters

Parameter | Required | Description
--------- | -------- | ---------
exchange_id | Yes | Valid exchange_id from /v1/exchanges.
pair_id | Yes | Valid pair_id from /v1/pairs.






## Exchange Trades

> Request Example

```curl
curl "https://api.blockmarkets.io/v1/exchanges/GDAX/BTCUSD/trades"
  -H "x-api-key: <client-api-key>"
```


> Response Example

```json
{
	"result": "success",
	"server_time": "2018-01-07T14:27:38.171Z",
	"data": [
		{
			"price": 16565.79,
			"amount": 0.05140238,
			"time": "2018-01-07T14:27:32.329Z"
		},
		{
			"price": 16565.79,
			"amount": 0.03612889,
			"time": "2018-01-07T14:27:23.138Z"
		},
		{
			"price": 16565.78,
			"amount": 0.1352,
			"time": "2018-01-07T14:27:14.149Z"
		}
	]
}
```

This endpoint retrieves trades for an asset pair on a specific exchange. By default returns the 100 most recent trades.


### HTTP Request

`GET https://api.blockmarkets.io/v1/exchanges/{exchange_id}/{pair_id}/trades{?since,limit}`

### Parameters

Parameter | Required | Description
--------- | -------- | ---------
exchange_id | Yes | Valid exchange_id from /v1/exchanges.
pair_id | Yes | Valid pair_id from /v1/pairs.
since | No | Retrieves trades at or after the provided timestamp. Required format: 'YYYY-MM-DDThh:mm:ss.sssZ'
limit | No | Number of records to retrieve. The default is 100. Maximum of 1000.




## Exchange Candles

> Request Example

```curl
curl "https://api.blockmarkets.io/v1/exchanges/GDAX/BTCUSD/candles"
  -H "x-api-key: <client-api-key>"
```


> Response Example

```json
{
	"result": "success",
	"server_time": "2018-01-07T14:29:07.592Z",
	"data": [
		{
			"time": "2018-01-07T14:28:00.000Z",
			"open": 16565.79,
			"high": 16565.79,
			"low": 16565.78,
			"close": 16565.78,
			"volume": 3.87739761,
			"ticks": 15
		},
		{
			"time": "2018-01-07T14:27:00.000Z",
			"open": 16565.79,
			"high": 16565.79,
			"low": 16565.78,
			"close": 16565.78,
			"volume": 0.92360209,
			"ticks": 9
		},
		{
			"time": "2018-01-07T14:26:00.000Z",
			"open": 16565.79,
			"high": 16565.79,
			"low": 16565.78,
			"close": 16565.78,
			"volume": 0.44495095,
			"ticks": 7
		}
	]
}
```

This endpoint retrieves OHLCV history for an asset pair on a specific exchange. By default returns the most recent OHLCV values.


### HTTP Request

`GET https://api.blockmarkets.io/v1/exchanges/{exchange_id}/{pair_id}/candles{?since,limit,interval}`

### Parameters

Parameter | Required | Description
--------- | -------- | ---------
exchange_id | Yes | Valid exchange_id from /v1/exchanges.
pair_id | Yes | Valid pair_id from /v1/pairs.
since | No | Retrieves trades at or after the provided timestamp. Required format: 'YYYY-MM-DDThh:mm:ss.sssZ'
limit | No | Number of records to retrieve. The default is 100. Maximum of 1000.
interval | No | Interval period in minutes. Maximum of 1440 (1 day).



## Products

> Request Example

```curl
curl "https://api.blockmarkets.io/v1/products"
  -H "x-api-key: <client-api-key>"
```

> Response Example

```json
{
	"result": "success",
	"server_time": "2018-01-07T14:31:59.592Z",
	"data": [
		{
			"product_id": "XBTC",
			"name": "X-Series Bitcoin",
			"base_id": "BTC",
			"quote_id": "USD",
			"quote_precision": 2,
			"components": [
				{
					"exchange_id": "STMP",
					"pair_id": "BTCUSD"
				},
				{
					"exchange_id": "GDAX",
					"pair_id": "BTCUSD"
				},
				{
					"exchange_id": "GMNI",
					"pair_id": "BTCUSD"
				},
				{
					"exchange_id": "ITBT",
					"pair_id": "BTCUSD"
				}
			]
		}
	]
}
```

This endpoint retrieves a list of supported price index products.


### HTTP Request

`GET https://api.blockmarkets.io/v1/products`

### Parameters

Parameter | Required | Description
--------- | -------- | ---------
none	| |




## Product Ticker

> Request Example

```curl
curl "https://api.blockmarkets.io/v1/products/XXLM"
  -H "x-api-key: <client-api-key>"
```


> Response Example

```json
{
	"result": "success",
	"server_time": "2018-01-07T14:38:11.737Z",
	"data": [
		{
			"last": 0.720939,
			"open_24h": 0.750739,
			"high_24h": 0.781798,
			"low_24h": 0.681831,
			"time": "2018-01-07T14:38:05.265Z"
		}
	]
}
```

This endpoint retrieves the ticker data for a specific product.

### HTTP Request

`GET https://api.blockmarkets.io/v1/products/{product_id}`

### Parameters

Parameter | Required | Description
--------- | -------- | ---------
product_id | Yes | Valid product_id from /v1/products.




## Product Ticker Detail

> Request Example

```curl
curl "https://api.blockmarkets.io/v1/products/XBTC/detail"
  -H "x-api-key: <client-api-key>"
```


> Response Example

```json
{
	"result": "success",
	"server_time": "2018-01-07T14:42:09.472Z",
	"data": [
		{
			"time": "2018-01-07T14:42:07.257Z",
			"last": 16560.95,
			"open_24h": 16512.19,
			"high_24h": 17199.45,
			"low_24h": 16367.98,
			"trades": [
				{
					"exchange_id": "GDAX",
					"pair_id": "BTCUSD",
					"price": 16567.86,
					"time": "2018-01-07T14:42:03.000Z"
				},
				{
					"exchange_id": "GMNI",
					"pair_id": "BTCUSD",
					"price": 16529.99,
					"time": "2018-01-07T14:41:57.000Z"
				},
				{
					"exchange_id": "ITBT",
					"pair_id": "BTCUSD",
					"price": 16574.5,
					"time": "2018-01-07T14:39:45.000Z"
				},
				{
					"exchange_id": "STMP",
					"pair_id": "BTCUSD",
					"price": 16572.31,
					"time": "2018-01-07T14:42:05.000Z"
				}
			]
		}
	]
}
```

This endpoint retrieves the ticker along with underlying exchange data for a specific product.

### HTTP Request

`GET https://api.blockmarkets.io/v1/products/{product_id}/detail`

### Parameters

Parameter | Required | Description
--------- | -------- | ---------
product_id | Yes | Valid product_id from /v1/products.



## Product Price History

> Request Example

```curl
curl "https://api.blockmarkets.io/v1/products/XETH/history"
  -H "x-api-key: <client-api-key>"
```


> Response Example

```json
{
	"result": "success",
	"server_time": "2018-01-07T14:43:11.152Z",
	"data": [
		{
			"time": "2018-01-07T14:43:10.885Z",
			"price": 1073.5383
		},
		{
			"time": "2018-01-07T14:43:09.883Z",
			"price": 1073.4713
		},
		{
			"time": "2018-01-07T14:43:06.877Z",
			"price": 1073.4586
		}
	]
}
```

This endpoint retrieves spot prices for a specific product. By default returns the 100 most recent prices.

### HTTP Request

`GET https://api.blockmarkets.io/v1/products/{product_id}/history{?since,limit}`

### Parameters

Parameter | Required | Description
--------- | -------- | ---------
product_id | Yes | Valid product_id from /v1/products.
since | No | Retrieves trades at or after the provided timestamp. Required format: 'YYYY-MM-DDThh:mm:ss.sssZ'
limit | No | Number of records to retrieve. The default is 100. Maximum of 1000.



## Product Candles

> Request Example

```curl
curl "https://api.blockmarkets.io/v1/products/XXMR/candles"
  -H "x-api-key: <client-api-key>"
```


> Response Example

```json
{
	"result": "success",
	"server_time": "2018-01-07T14:44:17.711Z",
	"data": [
		{
			"time": "2018-01-07T14:43:00.000Z",
			"open": 413.5381,
			"high": 414.3311,
			"low": 413.4792,
			"close": 414.3311,
			"ticks": 15
		},
		{
			"time": "2018-01-07T14:42:00.000Z",
			"open": 413.7621,
			"high": 413.9561,
			"low": 413.244,
			"close": 413.244,
			"ticks": 13
		},
		{
			"time": "2018-01-07T14:41:00.000Z",
			"open": 414.2931,
			"high": 414.2931,
			"low": 413.5548,
			"close": 413.8697,
			"ticks": 12
		}
	]
}
```

This endpoint retrieves the OHLC history for a specific product. By default returns the latest OHLC values.

### HTTP Request

`GET https://api.blockmarkets.io/v1/products/{product_id}/candles{?since,limit,interval}`

### Parameters

Parameter | Required | Description
--------- | -------- | ---------
product_id | Yes | Valid product_id from /v1/products.
since | No | Retrieves prices at or after the provided timestamp.
limit | No | Number of records to retrieve. The default is 100. Maximum of 1000.
interval | No | Interval period in minutes. Maximum of 1440 (1 day).




# Websocket

BlockMarkets uses <a target="_blank" href='https://www.pubnub.com/'>PubNub</a> to deliver real-time spot rates for our price index products. A premium subscription is required for this service. <a href='https://www.blockmarkets.io/#contact-section'>Contact us</a> for details.

PubNub subscribe key: `sub-c-468f918e-e108-11e7-b7e7-02872c090099`

You must include your `<client-api-key>` to authenticate.



## Subscribe

> Node.js Example

```javascript
var PubNub = require('pubnub');
var pubnub = new PubNub({
    subscribeKey: 'sub-c-468f918e-e108-11e7-b7e7-02872c090099',
	authKey: <client-api-key>
});
pubnub.addListener({
    message: function(data) {
        console.log(data.channel, data.message);
    }
});
pubnub.subscribe({
    channels: ['XBTC','XETH']
});
```

To subscribe to a price index, simply insert one or more product ids as channels. See the Node.js example to the right.

See <a target="_blank" href='https://www.pubnub.com/docs'>PubNub Documentation</a> for other languages.


## Unsubscribe

> Node.js Example

```javascript
pubnub.unsubscribe({
    channels: ['XETH']
})
```

To stop receiving updates for a product, simply unsubscribe from the channel.




