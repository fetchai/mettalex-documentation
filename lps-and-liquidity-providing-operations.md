# LPs and Liquidity Providing Operations

Liquidity is essential in Mettalex DEX. An adequate level of liquidity in the system guarantees the correct execution of operations and transactions. Each pool of liquidity is referenced by a specific asset (e.g. Silver, Steel Scrap, Bitcoin and others) and here LPs play a fundamental role thanks to liquidity provisioning operations. These actions are undertaken in the Liquidity Provisioning Layer of the Mettalex system. This layer enables the collection of stablecoin collateral from users which is then used by the Mettalex smart contract and converted into Long or Short position tokens made available on the Exchange Layer for trading and minting operations on the DEX itself. In exchange for locking up their collateral, LPs are rewarded with a further aggregated yield on the capital invested via transaction fees and trading spreads between prices, according to the amount and duration of liquidity supplied into the system. Liquidity providing operations are available to users in the Supply Liquidity section of the Mettalex DEX. There, Liquidity Providers can perform the following actions:&#x20;

* _**Deposit**_ collateral for the Autonomous Market Maker to use to create Position Tokens for the Trade functionality;&#x20;
* _**Withdraw**_ collateral to claim your share of the trading fees earned by the Autonomous Market Maker;&#x20;
* _**Stake**_ Liquidity Provider shares for Liquidity Mining rewards in the form of MTLX Governance tokens.&#x20;

Within the Mettalex ecosystem, we have 3 different liquidity pools of reference:

1. **Mettalex vault**: contains the liquidity coming from the collateral used to back a pair of L and S Position tokens when minting or trading operations occur.
2. **LPs pool**: LP supplies coin to earn a return return from trading fees (i.e. Liquidity Provision Layer). The liquidity supplied is at disposition of the Mettalex AMM so as to guarantee the correct execution of operations and transactions on the DEX.
3. **AMM pool**: AMM that contains a mix of stablecoin in addition to L and S tokens. The liquidity contained in the AMM pool is for traders to swap between each other (i.e. Exchange Layer).

Even if all of these liquidity pools are connected one to each other at the same time, these work separately and each one of them accumulate a different type of collateral tokens. The Mettalex AMM is a three token Balancer pool consisting of the stablecoin collateral token, long position token, and short position token.&#x20;

The position token prices are subject to the following constraints:

* 1L token + 1S token = Collateral Value, i.e.&#x20;

$$
L+S=C
$$

* The long token fair value varies linearly from 0 to C as the spot price varies between the floor and the cap of the trading band. Conversely, the short token varies linearly from C to 0 over the same range, i.e.

$$
L ∈ [0, C]
$$

$$
S ∈ [C, 0]
$$

* V represents the scaled price within the trading band. This means that a long token will have fair value vC and a short token (1- v)C in the absence of trade imbalance, where

$$
V= (Asset Spot Price - Floor value)/(Cap value - Floor value)
$$



Liquidity providers who wish to provide liquidity within the Mettalex DEX ecosystem will deposit their liquidity through the dedicated UI section by choosing the desired asset’s liquidity pool. Suppose you are a Liquidity Provider and you want to provide liquidity for $200.00 to the silver liquidity pool available on Mettalex DEX. By doing so, you will expose yourself to potential gains coming from trading fees and spreads but you could also face some potential risks that could lower the amount of liquidity you initially provided into the system, due to impermanent loss and slippage events. This is determined by the fact that your liquidity is being used by the AMM to deploy new position tokens on the market and so making it dependent on the movements and balances of these latter tokens. Let’s consider an example in which you decide to deposit liquidity into the Silver’s liquidity pool on Mettalex DEX so as to receive a proportionate amount of trading fees on your deposit through time. The Mettalex AMM converts your liquidity into L\S position tokens to be traded on the market. Let’s consider now the following information about this asset and pool of reference:

* Long Price: $50.00
* Short Price: $50.00
* Floor: $200.00
* Cap: $300.00
* Weighted Price (i.e. Spot Price): $250.00

The sum of weights applied to tokens inside the AMM pool is 1, i.e.

$$
Wc+Wl+Ws=1
$$

Given this and&#x20;

$$
Plong+Pshort=C
$$

&#x20;we can determine the weight of tokens in the pool according to the following constraints:

* **Long position tokens weight:**

** **

![](https://lh4.googleusercontent.com/DWsbuhVEoDCrbGObeeYqVh1qD8X73BiS99jpYHc79D6XhigFVhfjcg8rmz6q82QyllwVQZFknbfP7EyKuxIU4eDWLMPUVVc0R71q5UlfRiqriH4\_IUdGzZRGDg0bEIY\_uklrmefe)

* **Short position tokens weight:**

![](https://lh3.googleusercontent.com/yDO1De37svCYrVRnr0jUYCqshXJcM9jMrboFbM6qONLyMVITAuP2NsR8lfVVz07RCDYbPwbkfOsk62-huJy-X5JSzGyxXGaZifeoL2v9oTHZsaHuFcWX8SpQ1aT8\_J0bm--T63mX)

* **The spot price of a long (short) token in terms of a coin token is given by**:

$$
Pl=(Wl/Wc)(Xc/Xl)
$$

$$
Ps=(Ws/Wc)(Xc/Xs)
$$

Hence, If the silver the spot price fed by the oracle is equal to $250.00, on Mettalex the price of long and short position tokens need to be of $50.00 and $50.00 respectively (i.e. $50.00 + $50.00 = $100.00). At these prices, if a LP deposits $200.00, he will create 100 stablecoins, 1 long, 1 short tokens in the Mettalex AMM pool. We have the following composition inside this pool:

![](<.gitbook/assets/1 (3).png>)

If the copper the spot price fed by the oracle goes down to $220.00, the fair value at zero imbalance for Long and Short position token need to be of $20.00 and $80.00 respectively (i.e. $20.00 + $80.00 = $100.00). At these prices, we will have the following:

![](<.gitbook/assets/2 (3).png>)

As it is possible to see, the weights inside the pool are dynamically modified through time in accordance to the spot price fed by the oracles into the system and to the changing amounts of token balances into the pools occurring due to trades. If a trader comes inside Mettalex DEX and decides to perform a trade, then the risk to the LP is that the unbalanced short or long token value goes to zero and thus that the amount of liquidity provided into the system can decrease because of these events. If a trader decides to buy a long position token whose underlying asset is silver from the Mettalex AMM, then the amount of Long tokens inside the pool will decrease and demand and price will increase. Conversely, short position tokens value will reduce as a consequence of a higher demand for L position tokens and this can potentially erode the deposited amount the LP provided before. This means, the risk for the LP is that the unbalanced short token price goes to zero. However, this potential loss is offset by:

* The amount the trader pays to the Mettalex AMM for the long token he is buying on the market;
* The price increase of the long tokens. This is due to the higher demand for this token as more of these tokens are bought from the Mettalex AMM. The higher the demand, the higher the price for that token.

According to the law of demand, the higher the price the lower the demand for a good. This is, the more expensive L tokens become, the more the incentive to buy S tokens users have because they will be getting cheaper.

### Risks connected with liquidity provisioning

Mettalex DEX has been designed in order to minimize the risk exposure for LPs and these types of operations on the exchange. However, there is still a possibility that some problems and risks may arise in the normal course of operations. The nature of these problems is mainly related to the fact that Mettalex DEX is still in the experimental and deployment phase and most of the errors and risks that could be faced arise because:

* not all of the system components have been fully audited. Additionally, possible interactions between components inside the DEX system structure may be outside the scope of the normal purposes of these components which have been audited separately causing contract risks to eventually arise;
* errors in the contracts may cause contracts to settle unexpectedly and also cause potential data feed outages. This means that operational risks are still present for operations on the DEX;
* the initial implementation of the software still relies on privileged admin access for some type of operations on the DEX (this until full decentralisation is not being reached);
* market risks are still connected with the normal execution of operations on the DEX.

Mettalex DEX liquidity provisioning mechanism is based on the possibility for LPs to deposit their liquidity in stablecoin in a single token fashion rather than a ratio of multiple tokens. This latter scenario is very common in other decentralised exchanges available in the DeFi space (e.g. Uniswap). However, compared to these other protocols, Mettalex DEX offers to traders and LPs a lower volatility of the underlying assets thanks to the properties of position tokens. This, in addition to the single token (i.e. stablecoin) liquidity provisioning feature, reduces the impact of impermanent loss and slippage events which instead are controlled very efficiently. As previously mentioned, the stablecoin used as a collateral to issue position tokens has a combined value which is always equal to the collateral value. This means, on Mettalex each time liquidity is added to system or a tokens trade happens, the AMM rebalances the tokens in the pool by minting or redeeming position token pairs to keep the ratio of stablecoin to paired long and short tokens at around 1:1, in order to respect the aforementioned constraints about weights, prices and balances of tokens in each pool. If a trader comes in the market and buys Long tokens representing a specific underlying asset (e.g. Copper) thanks to the trade functionality, then the amount of Long tokens decreases, the weights are reapplied to guarantee balance and Long tokens price increases until it reaches the collateral value. This is balanced by Short position tokens value going to 0 as Long position tokens value increases. If trades keep happening in the same direction (i.e. high demand for Long tokens), then the imbalance between Long and Short value and amount increases and the cost of the token being highly demanded increases more and more.

Considering the previous example, the LP has one Long token and one Short token whose combined value is equal to the collateral amount deposited on the platform:

$$
1L + 1S = C => 1L = $50.00, 1S = $50.00, C = $100.00
$$

We are considering an increasing demand for Long tokens in time as more traders start to buy this type of token. The first trader comes in, buys 1L for $50.00 pushing the long tokens price up to $60.00 whereas the short tokens price falls down to $40.00. This event generates a reweighting and rebalancing of the tokens balances in the pool according to the previously introduced formulas, as follows:

![](<.gitbook/assets/3 (3).png>)

If a second trade happens and this trader buys 1L for $60.00, then L prices will go up to $70.00 whereas the short token price falls to $30.00. As it is possible to see, the AMM provides a balancing mechanism in order to guarantee an efficient trading and slippage controlling mechanism thus to guarantee the stability of the whole system. If a trader comes in and buys 1 Short tokens at the price of $40.00, then this will drive the Short tokens price back to $50,00 whereas the Long tokens one will fall from $60.00 back to $50.00 too. There may be an arbitrage opportunity here. Before the trader buys the Short token, you can redeem 1L and 1S at the price of $50.00 and $40.00 respectively on the market ($50.00 + 40.00 = $90.00) for the underlying collateral amount of $100.00. Hence, the potential arbitrage profit from this is equal to $100.00 - $90.00 = $10.00. However, the AMM counteracts this with slippage by reapplying the weight to L and S position tokens as previously explained, thus changing their prices accordingly.

In order to understand how LPs are influenced by trading operations let’s consider the previous LP. Let’s say t LP to be starting with 10 Long position tokens and 10 Short position tokens, for a total worth of $1’000.00 (i.e. 10 x $50.00 + 10 x $50.00), so $500.00 worth of long and $500.00 of short tokens respectively. If a trader comes in the market and buys a Long position token, the the amount of tokens belonging to the LP is going to be equal to:

* 9 Long tokens at the value of $60.00 each, so $540.00;
* 10 Short tokens at the value of $40.00 each, so $400.00.

So the total amount the LP has is going to be worth $540.00 + $400.00 + $50.00 coming from the Long token being bought by the trader on the market, so $990.00. Whenever a second trade takes place, with a trader buying a Short token exposure, then the amount of tokens belonging to the LP is going to be equal to:

* 9 Long tokens at the value of $50.00 each, so $450.00;
* 9 Short tokens at the value of $50.00, so $450.00.

So the total amount the LP has is going to be worth $450.00 + $450.00 + $50.00 coming from the Long token bought by the trader on the market + $40.00 coming from the Short token being bought on the open market, for a total worth of $990.00.

In both scenarios, we have an arbitrage opportunity for the LP. In fact, this latter one could redeem these tokens for the amount calculated at the specified prices and gain an arbitrage profit of $10.00. However, the Mettalex AMM slippage should counteract this. The term slippage counteracting represents the slippage in price value of tokens when trades happen through the AMM. In fact, the L token price is initially $50.00 for an infinitesimal trade. Whenever a full Long token is being bought, the cost increases so the average price gets higher reaching the price of $60.00. Conversely, whenever a full Short token is being bought on the market, the price for this token passes from $40.00 to $50.00 due to this AMM slippage that occurs to maintain balance.

_**E.g.**: Let’s consider another example in which the LP deposits $2’000.00 to the Mettalex AMM which then converts this into a mix of stablecoin, Long and Short tokens made available for traders._

_**Pool Balance after deposit: $2’000.00.**_

_The balance in the pool can be divided into 2 main components_:

1. _**Safe balance**: this is the amount of liquidity (i.e. coins and L/S tokens pair) the Liquidity Provider can consider as safe from events that could potentially erode the value of the deposit (e.g. Slippage, IL) into the system;_
2. _**Risk balance**: this is the imbalanced amount of liquidity the Liquidity Provider has to risk whenever operations occur on the DEX._

_At the very beginning we have the following balance breakdown:_

_**A.  Balance = $2’000.00 (safe) + $0.00 (risk)**, divided into:_

![](<.gitbook/assets/4 (2).png>)

_Let’s say a trader comes in and wants to trade 100.00 coins for 1.74 Long tokens at the initial spot price of $50.00. Once the trade operation is finalised, the AMM reweights the tokens in the pool and sets the new final spot price at $54.75._

_The new pool balance is $2’004.98 and the composition is given in the table below:_

_**B.  Balance = $1’926.45 (safe) + $78.53 (risk)**, divided into:_

![](<.gitbook/assets/5 (2).png>)

_Let’s now consider a second trader who comes in and wants to trade 100.00 coins for 1.91 Short tokens at the initial spot price of $45.25. Once the trade operation is finalized, the AMM reweights the tokens in the pool and sets the new final spot price at $50.52. The long spot price will be increasing due to a higher demand for these tokens in the pool, whereas the price of Short tokens will be decreasing._

_The new pool balance is $2’017.81 and the composition is given in the table below:_

_**C.  Balance = $2’009.35 (safe) + $8.46 (risk)**, divided into:_

![](<.gitbook/assets/6 (1).png>)

__

__
