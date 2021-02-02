# Economic model behind Mettalex DEX

Mettalex overall structure is composed of **four** different **layers**:

* **Tokenisation Layer**
* **Exchange Layer**
* **Liquidity Provision Layer**
* **Governance Layer**

Inside the Mettalex platform an important role is played by Position tokens. As mentioned, these tokens are minted in pairs by the Mettalex smart contract by locking up collateral into it \(i.e. ERC-20 stablecoin such as USDT\). This process takes place on the **Tokenisation Layer**. In the latter, the **Mettalex Vault** is fundamental as it contains the collateral that backs the pairs of L and S Position tokens.

The **Mettalex Exchange Layer** provides a reference price feed from an index or data-feed provider. The fairness of the information is guaranteed by the multiple sources providing different data \(e.g. QUANDL, Chainlink, REFINITIV or Davis\) and more data feeds will be added in the near future \(e.g. Platts and Fetch.ai agents\) thus providing a wide variety of possible oracles from which gather data. These multiple sources allow the communication between Mettalex and the real world. The price data gathered is thus processed by the Mettalex CloudSQL component in order to allow the implementation of new markets, the recovery of price feeds and to ensure the continuous updating of prices displayed to on-chain and off-chain components. Traders are presented with reliable indices providing valuation for the commodities listed which are denominated in either fiat currency or stablecoin. On this layer, Position tokens are used to track the change in the price of an underlying asset and users are free to open positions on the market. Position tokens can be divided into **Long tokens** \(i.e. **L tokens**\) and **Short tokens** \(i.e. **S tokens**\). These respectively track the positive and negative change in a given price. 

Traders can buy or sell using stablecoin \(e.g. USDT\) collateral by trading with other participants or an Mettalex AMM. In this case, the latter refers to the **AMM pool** which contains a mix of USDT, L and S tokens that can be swapped among traders, while it adjusts the price of the tokens depending on liquidity demand and data from outside oracles.

Position tokens are a disruptive technology equipped with _various properties_, such as:

* No need for further funding as these are always fully collateralised \(i.e. there are not any margin requirements\);
* These are ERC-20 tokens, so it is easy to store them in wallets \(e.g. MetaMask\);
* No fixed expiry date so holders do not need to rollover their positions as token expiry reaches;
* These allow holders to open a leveraged position \(i.e. in this case, the ratio between the price of L tokens and S tokens will differ from the spot price available on the market\).

  These tokens do not require the entire value of the collateral to be locked up in a smart contract: it means that contracts of much larger sizes can be traded with fewer collateral requirements on Mettalex. 

Let’s consider the following example:

> _**E.g.**: A trader wants to open a position on the market via buying an asset like Bitcoin \(i.e. BTC\). If the BTC price on the market is BTCUSD = $10’000,00, with Cap = $11’000,00 and Floor = $9’000,00 the collateral required on Mettalex DEX to mint a pair of L/S tokens would be equal to $2’000,00 rather than the market spot price equal to $10’000,00._

\_\_

As outlined in the example above, distinctly from conventional market, Mettalex leverage requirements refer to price movements: the trade happens in a range of price, called **Δ** \(i.e. **delta**\), until this one hits a pre-set price band of reference \(i.e. **floor** or **cap**\). The value of a L/S pair of tokens is equal to the Δ, so the pair can be minted just by depositing a collateral as worth as Δ**.** The underlying spot price moves inside this range of values and as it trades away from the centre price \(i.e. the central value of the band\), it will be cheaper to buy tokens representing the trend opposite to the price movements. If the spot price breaches the band, the L/S pair will be settled automatically and all of the backed collateral will be distributed back to the token holders. The new spot price will initialise the smart contract around the new price value with the same Δ. At this point new position tokens will be minted and trading starts again. The following example helps to visualise the idea:



> _**E.g.**: Table 1 depicts the historical price graph for the London Metal Exchange \(i.e. LME\) Steel Scrap: For commodity Position tokens we expect the spot price to usually trade inside Δ. If we consider the steel scrap this might range from $225 to $375 per tonne \(i.e. a delta of $150 centred around $300\). We can use this trading range to set the floor and cap prices for the token pair. The value of a long and short pair of tokens is equal to the delta, here $150,00, with floor set at $225,00 and cap at $375,00. That is, depositing a collateral worth $150,00 will allow the trader to mint a L/S pair. Assuming the spot price when the tokens are minted is $300, each token will have a value of $75,00, representing a leverage of $300,00/$75,00 = 4x._

![ Table 1: LME Steel Scrap historical price graph.](https://lh3.googleusercontent.com/v279Yho9C53TCYxmNvKDZ2DtTFfk7X1G3lQYQmAGj84H4dSr7BDx6OuvEG6G-L0dXBIh9ROoMY7dQpgVu3jOmb_ucjYOfh1x098-eWrISE8ocWD0e89TKFVW0JjmXAqlfmSzEmGW)



Choosing the floor and the cap basing on historical delta allow us to create a non-expiring perpetual token that can be held indefinitely as long as the spot remains within the historical range. This has the consequence that as the spot trades away from the centre price it becomes cheaper to buy exposure for the position opposite the movement.

> _Following the example above, if spot increases to $350,00 the value of a long token becomes $125,00 \(i.e. leverage of $350,00/$125,00 = 2.8x\) while the short token is now worth $25,00 \(i.e. leverage of $350,00/$25,00 = 14x\). This is an incentive for market participants to provide liquidity for the short position at low._

\_\_

Mettalex offers to **Liquidity Providers** \(i.e. **LPs**\) the chance to supply liquidity directly to Mettalex system through the **Liquidity Provision Layer**. The liquidity collected throughout this layer is stored into a decoupled liquidity pool. The AMM uses Mettalex smart contract to convert supplied collateral into position tokens for market making operations. In exchange for locking up their collateral, LPs are rewarded with a further aggregated yield on the capital invested via transaction fees and trading spreads between prices, according to the amount and duration of liquidity supplied into the system. Compared with other liquidity pools, like Uniswap or Balancer, Mettalex DEX allows LPs to deposit just a token in order to provide liquidity, as only one asset \(i.e. USDT\) is contained in the Liquidity Providers pool \(i.e. the LPs pool\). Other liquidity pools liquidity providers would need to supply a pair of tokens \(e.g. ETH/USDT\) in order to provide liquidity into them. The Mettalex decoupled LPs pool works as a decoupled liquidity pool whose role is to guarantee the provisioning of liquidity to the AMM so minimising the timing risk of any impermanent losses the AMM is exposed to. This liquidity will be then converted internally by the AMM pool \(i.e. it is a different Balancer-based pool\) into a mix of USDT, Long and Short tokens which will be supplied to the Exchange layer in order to be traded among traders on the market. This is, the latter pool contains a mix of tokens whereas LPs pool contains just stablecoin collateral \(i.e. **USDT**\). The mechanism is based on the fact that LPs take on the _timing risk_ in exchange for a return from the AMM. The contract is very simple as it focuses on only one variable: total liquidity provided \(i.e. deposits\). The objective is having always enough liquidity in the pool. So, the liquidity provision layer represents the component that funds autonomous market making processes.

Because of this, the **Governance Layer** rewards LPs with **governance tokens** \(i.e. **MTLX Tokens**\) via a liquidity mining process that rewards in proportion to the amount and duration of supplied liquidity in the system. These tokens were initially distributed among Fetch.ai stakeholders \(i.e. **FET token holders**\) in accordance to the quantity of FET owned. This layer enables decentralised governance of the platform itself: MTLX tokens enable stakeholders to take part in the decision making process regarding the platform. These allow them to govern on the policies and fees applied inside the platform itself, including:

* System parameters \(e.g. the choice of the AMM to back with liquidity from the liquidity pool\);
* Creation of new markets;   
* Usage of the collected exchange fees;
* Percentage of spread going into the liquidity pool;
* The buy-back and borrowing rates from the liquidity pool.



The following table offers an overview of the Mettalex Decentralised Exchange Platform \(Table 2\):



![Table 2: MTLX system diagram. Source: Mettalex Litepaper, September, 2020.](https://lh3.googleusercontent.com/bY9agOHMEMc0F1R3D1b2ApjARqT0RcZW3mY_CFHZJQ45amA9bVRQ4nzB1tYY2feuNJFFUzT4TLYsw9BxU3hOXLNSV53N12qh32xDStkcsjq2DHLyDqjuOH5QJAuPwzErWBX5BHUm)



As an additional part of the mechanism, Mettalex DEX uses a fraction of the exchange fees earned on the platform to algorithmically buy MTLX tokens back from the market. Governance tokens are minted at a linear rate to incentivise early liquidity providers in the system. However as the total liquidity in the pool increases, liquidity mining will become more difficult.

In conclusion, as we can see in Table 2, Mettalex DEX comprehends three different pools of liquidity. Even if all these liquidity pools are connected one to each other at the same time these work separately and each one of them accumulate a different type of collateral tokens. We can distinguish the following pools of tokens:

* **Mettalex vault**: contains the liquidity coming from the collateral used to back a pair of L and S Position tokens \(i.e. Tokenisation Layer\);
* **LPs pool**: LP supplies coin to earn a return return from trading fees \(i.e. Liquidity Provision Layer\);
* **AMM pool**: AMM that contains a mix of stablecoins in addition to  L and S tokens. The liquidity contained in the AMM pool is for traders to swap between each other \(i.e. Exchange Layer\).

