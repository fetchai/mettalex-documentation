# Mettalex DEX - FAQs

#### **What type of instruments are position tokens: combination of CFD and Spread betting?**

Position tokens allow linear exposure to the underlying asset price movements, with capped exposure.  They are similar to futures contracts but with fixed margin requirements.



#### **What does Floor and Cap mean?**

Floor and cap define the trading range for position tokens.  If the trading range is breached the tokens automatically settle.  



#### **What happens if you breach the floor or cap?**

If the spot price breaches the band, Long/Short token pairs will be settled automatically and the collateral will be distributed back to the token holders. Mettalex smart contract performs settlement and clearing of the position tokens, with one of the L or S tokens having the full value of the underlying collateral and the other being worthless. The new weighted spot price will initialise the smart contract around the new price value with the new trading band and trading resumes as normal.



#### **What is a DEX?**

A DEX is a Decentralized Exchange where there is no central organization holding user funds.  Trades are handled automatically by blockchain smart contracts and user wallets.  In the Mettalex system the DEX uses an on-chain Autonomous Market Maker to handle trades. There is no counterparty and/or counterparty risk.



#### **Is it like OTC?**

It is like OTC in that a participant can always go to the Autonomous Market Maker to get the desired exposure for a fair price. It differs from OTC in that the position tokens are tradeable independently, and not fixed contractual obligations with an OTC desk.



#### **How does the price of long and short position tokens change?**

Within the trading range the long token price varies linearly from 0 at the floor to the full collateral value at the cap, and conversely for the short token.



#### **What is Mint function?**

The Mint function takes collateral tokens and creates a pair of Long and Short position tokens backed by that collateral.  The collateral is deposited in an on-chain Vault contract.



#### **What is Redeem?**

The Redeem function takes a pair of Long and Short position tokens and redeems them for the collateral backing the pair of tokens.  The collateral is retrieved from the Vault contract and the pair of tokens burnt.



#### **Why do you need Mint and Redeem?**

Mint and Redeem guarantees that liquidity can always be supplied to the system, by minting new long and short pairs, and that a pair of long and short tokens has a known value. They provide a mechanism for arbitrageurs to generate profits in times when the total price of a pair of long and short position tokens is either below or above the reference price provided by the oracle. Through these incentivised actions, the arbitrageurs perform valuable liquidity balancing services for the Mettalex DEX platform.



#### **How can Market Makers get involved?**

Market makers can use the Mettalex system in a number of ways:

* as a hedging mechanism for trades outside Mettalex e.g. sell an exposure to a trader then buy a hedging exposure from Mettalex AMM;
* Mint pairs of Long and Short tokens then make markets on a central limit order book exchange;
* Buy and sell position tokens against the Mettalex Autonomous Market Maker to reduce slippage**.**

\*\*\*\*

#### **What is the role of arbitrageurs?**

Arbitrageurs keep the weighted price of the commodity as perceived by the Mettalex Autonomous Market Maker in line with the price on reference exchanges.



#### **What is liquidity provision?**

Liquidity providing represents a very important and necessary operation. The liquidity collected supports Mettalex throughout all market making processes that need to take place. 



#### **Why do we need liquidity?**

The Mettalex decoupled LPs pool works as a decoupled liquidity pool whose role is to guarantee the provisioning of liquidity to the Mettalex Autonomous Market Maker so minimizing the timing risk of any impermanent losses it is exposed to.



#### **How do I provide liquidity to different markets?**

Traders are able to provide liquidity by using the Mettalex smart contract to mint L/S token pairs or use it to redeem a paired position in long and short tokens to reclaim the backing collateral.



#### **How can I earn from providing liquidity?**

Sources who provide the system with liquidity receive an aggregate return on maker fees and market spreads. Liquidity Providers are rewarded with a further aggregated yield on the capital invested via transaction fees and trading spreads between prices according to the amount and duration of liquidity supplied into the system.



#### **What APY from trading fees can I earn by providing liquidity?**

This depends on the market and the demand of trading on a particular market.The AMM spread and fees range from 0.25%-3% of transaction value based on demand. Average APY would vary from 5-25%.



#### **What are the risks of providing liquidity?**

Liquidity providers expose themselves to timing risk when providing liquidity to the Autonomous Market Maker. In regular circumstances, liquidity suppliers have the opportunity to exit the system in times of high demand. This provides them with an opportunity to recoup capital before re-engaging with the system. However, in periods where need for liquidity is high, they may be required to wait a short period in order for a baseline level of liquidity to be reached. This is not only to make sure the system remains afloat, but also to protect the investment they have made into the exchange. 



#### **Am I subject to impermanent loss when providing liquidity?**

The LPs in Mettalex work differently to other crypto based LPs like Uniswap. In Mettalex liquidity is provided in a single token and not as a ratio of multiple tokens. Also, the liquidity is provided using stable coins \(e.g.  USDT, BUSD\) which reduces the risk of volatility. The stable coins are then used as a collateral to issue position tokens whose combined value is always equal to the collateral value. Whereas there is always a risk of loss in supplying liquidity to pools, in Mettalex LPs due to lower volatility of the underlying assets and provision of liquidity in stablecoins, the risk of impermanent loss is very low.



#### **Why is Mettalex better/different than other decentralized derivatives markets in crypto?**

Unlike other decentralized derivatives platforms, Mettalex is mainly focused on token-based commodities derivatives and spreads. As such, speculators in the crypto space can get exposure to trading pairs unavailable on other decentralized markets. Other noteworthy Mettalex DEX advantages include:

* Mettalex lowers market-entry barriers for physical asset holders and provides them with cost-efficient hedging tools;
* Trading on Mettalex is less risky since trades are capped in fixed trading ranges per commodity;
* Position tokens are fully backed by collateral when they are created so there is no need for margin calls or provision of additional capital as commodity prices change;
* Open positions have no expiry dates and are settled automatically once the upper/lower limit of the band is reached;
* Since the prices of position tokens are just fractions of the asset’s market price, leverage is achieved at minimal cost;
* Since system collateral is mainly composed of USDT and other stable coins, Mettalex is much more capital-efficient than other solutions that rely on highly volatile assets;
* Yields for stablecoin liquidity providers are very competitive in comparison to those available in other markets without the impermanent loss. Yield is composed of trading fees and governance tokens \(MTLX\) distribution.



**How is the current price of a commodity determined in Mettalex?**

Commodity price is acquired by multiple methods which include oracles \(e.g. chainlink\), direct integration with index providers \(e.g. S&P\) and aggregator services like Refinitiv \(e.g. Reuters\).



#### **How are AMM spreads \(between a short and long position\) calculated?**

Spreads take into account the price of the reference asset within the trading range, combined with an offset based on trade imbalance between long and short tokens.



#### **How is the APY for each Vault calculated?**

The APY is reported as the trailing one week annualized return of current vault balance relative to supplied liquidity. 



#### **How are trading fees calculated?**

The overall trading spread is a combination of the trading fees calculated as a commodity-dependent percentage of the trade value plus slippage dependent on the amount of available liquidity in the autonomous market maker. 



#### **What are trading fees used for?**

Trading fees are used to pay data providers and buy back MTLX governance tokens and FET tokens.



#### **How does the Mettalex Autonomous Market Maker differ from other AMMs such as Uniswap or Balancer?**

The Mettalex AMM is a pluggable component of the system that can be upgraded as new algorithms or blockchain capabilities become available.  The roadmap has the AMM moving to the Fetch.ai blockchain to take advantage of on-chain machine learning capabilities.

The initial Ethereum implementation of the AMM is based around each commodity having a private Balancer pool containing a mix of USDT, Long and Short tokens. This pool is controlled by a separate strategy smart contract that responds to trading activity and price updates.



#### **Do liquidity providers have to supply a mix of tokens?**

No, liquidity providers only need to supply stablecoin \(e.g. USDT, BUSD, MUSD**\)** collateral to the Mettalex system \(the stablecoin collateral will depend on the type of network the user decides to use to connect to the platform\) in accordance with the network they use to connect to the DEX.  The strategy uses the Mettalex vault to convert a portion of the supplied stablecoin into position token pairs.



#### **How is slippage controlled?**

Each time liquidity is added the AMM rebalances by minting or redeeming position token pairs to keep the ratio of USDT  to paired long and short tokens at around 1:1.



#### **How do the position token prices respond to trading activity?**

Each time a position token is bought from or sold to the AMM the weights are updated to keep the sum of the long and short token prices equal to the value of the collateral backing a token pair.  For example if a long token is bought from the AMM, the relative amount of long tokens to short tokens held by the AMM will decrease.  This results in the long token price increasing and the short token price decreasing, which incentivizes traders to buy short tokens and equalize the long and short token balances held by the AMM.

![](https://lh3.googleusercontent.com/6Chykpk-z9gGlF9cOrdTrzTkIp5Wyz1e0Ss-uvzPwfwUtlKxD2p_KBgFcwgah6rEcSSuNCs-T_55X_v2uS3lc773skC8raIYmRDNDNKjjaf75LQj7mQc8ogogluiVfw0C9-rcoAi)

_**Left Table**_: ****AMM balance after trade of varying size for coin buying long tokens.

_**Right Table**_: ****Resulting prices of position tokens after trade, their sum \(stays equal to underlying collateral price\), and average price per token paid by trader.



#### **How do the position token prices respond to the reference price?**

Each time the underlying commodity or spread price updates from the parent exchange\(s\) the AMM reweights to set the spot price for position tokens to be equal to their fair value based on the reference price location within the trading range.  This provides commodity traders with a guarantee that they can hedge their exposure using position tokens as the tokens will track the price movement in the reference asset.  


![](https://lh5.googleusercontent.com/u2ENb_2moc6OOCSiOS5psYnvn2_c90A8fcu_j8ha-vSrKs02yMQSuryY1uTUkujM1gw86joRMqMGBhslJuBxofo7CLQoY9yya2mzSlS8fztUWIFOh-ls9TFxJ9yhw67Go81zp49H)

