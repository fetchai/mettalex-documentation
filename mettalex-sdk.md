# Mettalex SDK

[**Website**](https://mettalex.com/)

Access the world’s first DEX focused on token based commodities trading using this SDK. Accessible 24/7 with tight trading spreads, low margin requirements and unique hedge instruments that ensure you don’t get liquidated prior to settlement dates.

### Prerequisites

This package is designed for python 3. While using pip, pip should be configured for python3.

### Installation

Mettalex for python can be installed directly from github using the following command:

`pip install -e git+https://github.com/fetchai/mettalex-sdk.git@master#egg=mettalex-sdk`

### Usage

#### **Importing**

`from mettalex import apiSDK`

#### **Connecting to a network**

Mettalex provides 3 networks for connecting to Metallex exchange, namely, `'bsc-testnet'`, `'kovan'` and `'bsc-mainnet'`. You will need to connect to one of these to be able to access Mettalex. You will require your `key` while connecting to any network. `Infura project ID` and `Infura API Secret` are required only when connecting to `kovan`.

```text
apiSDK.connect([network], [userkey], [infuraSecret ? Optional], [infuraProjectId ? Optional])
```

You can pass credentials as a json file **\(**e.g. trade\_sdk\_creds.json\).

```text
{
  "kovan": {
    "infura": {
      "project_id": "...",
      "secret": "..."
    },
    "user": {
      "address": "0x...",
      "key": "14a..."
    }
  },
  "bsc-mainnet": {
    "user": {
      "address": "", 
      "key": ""
    }
  },
  "bsc-testnet": {
    "user": {
      "address": "", 
      "key": ""
    }
  }
}
```

then connect with:

```text
apiSDK.connect('kovan', filename=os.path.expanduser('~/trader_sdk_creds.json'))
```

#### **Getting Commodities**

`apiSDK.getCommodities(network_id=optional, coin_id='default')` This function returns a pandas DataFrame with details of all the commodities in the connected network.  
Use this function typically while getting the list of all commodities available on a network.

The optional `network_id` argument allows the user to examine commodities present on different networks. If unspecified the connected network is used.

The optional `coin_id` argument specifies the underlying collateral.

**Note: on bsc-mainnet BUSD is "real money":** please exercise caution and understand the risks involved.

```text
commodities = apiSDK.getCommodities(coin='BUSD')
commodities.loc[:, ['category', 'commodity_symbol', 'id']]
Out[27]: 
  category commodity_symbol   id
0   Spread          BTCTSLA  338
1   Crypto              BTC  336
```

#### **Creating a commodity instance to trade**

`commodity = apiSDK.Commodity([commodity symbol or commodity ID])` 

A Commodity instance can be created using the commodity symbol. This initializes a class instance of the particular commodity. An instance of a commodity needs to be created to be able to execute trades and getting expected prices. We can get commodity symbols available by calling `getCommodities()` and looking at the `commodity_symbol` column. If there are multiple commodities with the same symbol, e.g. settled and active commodities, then it is better to use the `commodity_id` to access a market.

#### **Expected trading prices**

Two functions `ask` and `bid` can be used to retrieve trading prices. These functions can be called on commodity instances created, taking two arguments of token and amount to be traded.

```text
commodity.ask(token, amount) - amount of coin required to buy token amount

commodity.bid(token, amount) - amount of coin received from sell token amount
```

Token is provided as a string and can be either `"long"` or `"short"`.  
Amount is provided by default as a `float` using token amounts taking token decimals into account.  
If the `unitless` parameter is set to True the amount values are in `int`

#### **Trading**

Trading in a commodity is quite simple. We have to call trade function on a commodity instance providing in token, out token and the amount we want to trade. `In token` and `Out Token` can take `"long"`,`"short"`, or `"coin"` as values.  
Amount is provided as a `float or` `int` as for `bid` and `ask` methods. `commodity.trade([In Token], [Out Token], [amount In], [minimum amount Out])`

### 

