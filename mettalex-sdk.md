# Mettalex SDK

[**Website**](https://mettalex.com/)

Access the world’s first DEX focused on token based commodities trading using this SDK. Accessible 24/7 with tight trading spreads, low margin requirements and unique hedge instruments that ensure you don’t get liquidated prior to settlement dates.



### Pre requisites

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

You can pass credentials as a json file \(e.g. trade\_sdk\_creds.json\).

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



### Example

1. Setup and imports in ipython console;

```text
%load_ext autoreload
%autoreload 2
import pandas as pd
import os
from mettalex import apiSDK
pd.set_option('display.width', 1000)
pd.set_option('display.max_columns', None)
```

  2. Connect to blockchain and list commodities;

```text
apiSDK.connect('kovan', filename=os.path.expanduser('~/trader_sdk_creds.json'))
commodities = apiSDK.getCommodities('kovan', output='dataframe')
Connected to network ID 42
commodities.groupby('category')['id'].count()
Out[6]: 
category
Agricultural    1
Crypto          3
Ferrous         5
Forex           1
Indices         1
Industrial      5
Other           1
Spread          5
Test QA         2
Name: id, dtype: int64
commodities.loc[commodities.category == 'Spread', ['id', 'commodity_symbol', 'commodity_name']]
Out[7]: 
     id commodity_symbol            commodity_name
5   303         LINKBAND          Link Band Spread
12  286           BTCETH   Bitcoin Ethereum Spread
17  299          BTCTSLA      Bitcoin Tesla Spread
18  307        SDEFISCEX         sDEFI sCEX spread
19  211          SRSCSPR  Steel Rebar Scrap Spread
```

  3. Connect to specific market and trade.

```text
commodity = apiSDK.Commodity('BTCTSLA')
connection established sucessfully
commodity
Out[11]: 
BTCTSLA: Bitcoin Tesla Spread
Mettalex Vault: 0x37eeDc79D22980Bd60652751072ac252C300959a
  Prices - Floor: 50.0 Spot: 79.2 Cap: 100.0
  Coin : 0xe551960F80e5f855bB75d36016Ca92c981314b3E  568937.305831
  Short: 0x6aE1854843e5AD57e103E68C6E1A455530336750  11374.34611
  Long : 0x924D2bf052538F4DF696450214A827D0575127b6  11374.34611
Mettalex Liquidity Pool: 0x071826Eb1FD5bCC1a2219CC8F9ae99a1A6eC9AFE
  Coin : 0xe551960F80e5f855bB75d36016Ca92c981314b3E  {'y_vault': 330.505877, 'vault_controller': 0.0, 'strategy': 0.0, 'balancer': 594117.125268}
  Short: 0x6aE1854843e5AD57e103E68C6E1A455530336750  {'y_vault': 0.0, 'vault_controller': 0.0, 'strategy': 0.0, 'balancer': 7776.0527}
  Long : 0x924D2bf052538F4DF696450214A827D0575127b6  {'y_vault': 0.0, 'vault_controller': 0.0, 'strategy': 0.0, 'balancer': 9659.39263}
Short spot price: 23.953781  Long spot price : 27.070647
commodity.getUserBalance()
Out[12]: (35752.557059, 0.0, 0.0)
commodity.ask('long', 100)
Out[13]: 2727.088497
commodity.ask('long', 10)
Out[14]: 270.887126
commodity.bid('long', 10)
Out[15]: 259.778631
commodity.bid('long', 100)
Out[16]: 2580.950892
commodity.trade('coin', 'long', 3000)
Swapped 3000.000 coin to 109.926 long
Out[17]: (3000.0, 109.92576)
commodity.getUserBalance()
Out[18]: (32752.557059, 0.0, 109.92576)
```

### 

### Example Showing Mint and Redeem Operations

```text
commodity = apiSDK.commodity_from_symbol('BTCTSLA')
connection established sucessfully
commodity
Out[7]: 
BTCTSLA: Bitcoin Tesla Spread
Mettalex Vault: 0xdd458CDBbEAEE04C010C721E50fD4C4BEA02507c
  Prices - Floor: 50.0 Spot: 83.0 Cap: 100.0
  Coin : 0x6e71C530bAdEB04b95C64a8ca61fe0b946A94525  475250.192
  Short: 0xe17d1431D2f13044e660fa25Fea2009316F8Bf2c  9504.96
  Long : 0xbf97902FfEB9520DbB0014DF36961B59cfB1875a  9504.96
Mettalex Liquidity Pool: 0x5629f27EBF0921605c99269f92F537F1eDCb860a
  Coin : 0x6e71C530bAdEB04b95C64a8ca61fe0b946A94525  {'y_vault': 279605.588519, 'vault_controller': 0.0, 'strategy': 0.0, 'balancer': 746369.04679}
  Short: 0xe17d1431D2f13044e660fa25Fea2009316F8Bf2c  {'y_vault': 0.0, 'vault_controller': 0.0, 'strategy': 0.0, 'balancer': 6038.29334}
  Long : 0xbf97902FfEB9520DbB0014DF36961B59cfB1875a  {'y_vault': 0.0, 'vault_controller': 0.0, 'strategy': 0.0, 'balancer': 4064.57865}
Short spot price: 13.137957  Long spot price : 37.889255
commodity.getUserBalance()  # See our coin, short, long account balance
Out[8]: (99979707.333966, 0.0, 0.0)
paid_trade, received_trade = commodity.trade('coin', 'long', 100)
Swapped 100.000 coin to 2.639 long
commodity.getUserBalance()  # See our coin, short, long account balance
Out[10]: (99979607.333966, 0.0, 2.63863)
paid_mint, received_mint = commodity.mint(200)  # Mint $200 worth of long and short tokens
Paid 200.000 coin to mint 3.984 long and short
commodity.getUserBalance()  # See our coin, short, long account balance
Out[12]: (99979407.333966, 3.98406, 6.62269)
paid_trade_2, received_trade_2 = commodity.trade('coin', 'short', 100)  # Buy $100 worth of short tokens
Swapped 100.000 coin to 7.611 short
commodity.getUserBalance()  # See our coin, short, long account balance
Out[14]: (99979307.333966, 11.59466, 6.62269)
paid_redeem, received_redeem = commodity.redeem(5)  # Redeem 5 long and short token pairs for coin
Redeemed 5.000 long and short for 250.000 coin
commodity.getUserBalance()  # See our coin, short, long account balance
Out[16]: (99979557.333966, 6.59466, 1.62269)
# Close position either by swapping long to coin, short to coin
# or redeeming max number of pairs and then trading the remaining position tokens for coin
```

