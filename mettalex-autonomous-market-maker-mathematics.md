# Mettalex Autonomous Market Maker Mathematics

**Mettalex introduces improvements to its Autonomous Market Maker to improve risk management, control slippage, & modify fees dynamically.**

![](.gitbook/assets/image%20%287%29.png)

Currently, the [Mettalex system](https://www.mettalex.com/read) is running on the Ethereum blockchain which has the benefit of allowing reuse of existing DeFi protocols at the expense of some limitations in the allowed efficient mathematical operations. **The Mettalex system roadmap plans to transition the autonomous market making functionality to the Fetch.ai network to make use of more advanced optimization techniques.** As such the functionality described here should be regarded as an initial version of the autonomous market maker \(AMM\) that will be extended as more network capabilities become available.

The Mettalex AMM makes use of a private [Balancer Smart Pool](https://bankless.substack.com/p/the-ultimate-guide-to-balancer-smart) to provide the functionality of swapping between a US Dollar-based coin \(stablecoin\) and long or short position tokens. It determines the cost for opening a short or long position on each Mettalex market based on market demand and several constraints that we have put in place.

### AMM Reweighting

The [Balancer whitepaper](https://balancer.finance/whitepaper/) describes the mathematics underlying the internal Balancer pool used for swaps between a stablecoin and long or short position token. The Mettalex AMM is a three token Balancer pool consisting of the stablecoin collateral token \(currently USDT, more options in the future\), long position token, and short position token. The position token prices are subject to the following constraints:

* A pair of long and short tokens is equal in value to the underlying coin backing the pair i.e. 1L + 1S = C.
* The long token fair value varies linearly from 0 to C as the spot price varies between the floor and the cap of the trading band. The short token varies linearly from C to 0 over the same range.

We use _v_ to represent the scaled price within the trading band i.e. long token will have fair value _vC_ and short token _\(1- v\)C_ in the absence of trade imbalance, where _v_ = \(asset spot price -floor\)/\(cap-floor\).

To meet these constraints the weights of the pool are updated to set the desired prices.

The spot price of each token is dependent on the token balances and weights as shown below

```text
calc_spot_price(bI, wI, bO, wO, sF=0)
    calcSpotPrice                                                   
     sP = spotPrice                                                 
     bI = tokenBalanceIn            ( bI / wI )         1       
     bO = tokenBalanceOut     sP =  -----------  *  ----------  
     wI = tokenWeightIn             ( bO / wO )     ( 1 - sF )  
     wO = tokenWeightOut                                            
     sF = swapFee
```

Constraints on the pool weights:

_**Constraint 1**_: the sum of weights is 1

![Image for post](https://miro.medium.com/max/331/0*5LhNtKvYsFaPW87K.png)



_**Constraint 2**_: sum of prices is C

![Image for post](https://miro.medium.com/max/228/0*fEhP6o-1gWPDP6T7.png)



_**Constraint 3**_: the relationship between long token weight and long price

![Image for post](https://miro.medium.com/max/417/0*jdgUn3Tbwv3MQmjR.png)



_**Constraint 4**_: the relationship between short token weight and short price

![Image for post](https://miro.medium.com/max/422/0*v6qnEQXbhWcezbbU.png)



_**Constraint 5**_: long/short price ratio when equal amounts of long and short tokens in the pool

![Image for post](https://miro.medium.com/max/224/0*6VK7mycJ9njWrYJG.png)

Given the above constraints and a spot price that is a fraction of _v_ from the floor of the trading range, we can solve for the pool weights for arbitrary token balances in the pool.

**\[Stable\]coin weight**:

![Image for post](https://miro.medium.com/max/721/1*xIdK-SZCEnYyE_p7fZhs6g.png)

**Long token weight**:

![Image for post](https://miro.medium.com/max/644/1*b97mOenYk9klt7DTBCoSOQ.png)

**Short token weight**:

![Image for post](https://miro.medium.com/max/649/1*RFnDdPdG-njeW_dQJv9XjQ.png)



### Spot Price for Balanced

For a Balancer pool, the spot price of a long token in terms of a coin token is given by:

![Image for post](https://miro.medium.com/max/328/0*L6nnknhn7LNEMSid)

as shown in the Spot Price section, equation 2 of the [Balancer whitepaper](https://balancer.finance/whitepaper/).

The AMM checks that the spot prices for long and short tokens at zero imbalance are as expected \(below\).

**Long token price**:

![Image for post](https://miro.medium.com/max/597/1*MxkC9Qg0p4kSR1qUc0VUwA.png)

**Short token price**:

![Image for post](https://miro.medium.com/max/708/1*PLrNGkF6kq9kkuStrkLVeA.png)



### Spot Price for Highly Imbalanced Positions

The Mettalex AMM also checks the limiting behavior of the spot price as the imbalance increases. Here we show the long token price only.

We see that as the amount of short tokens in the pool approaches 0, i.e. prevailing sentiment is for the price of the asset to decrease, the long token price also approaches 0. **This incentivizes traders to take the opposite side of the prevailing sentiment and buy the cheaper long tokens.**

![Image for post](https://miro.medium.com/max/561/1*kKEGrwHXeE34610vE9d3ew.png)

Conversely, if the prevailing sentiment is that the underlying asset price will increase then the amount of long token in the pool will approach 0 and the long token price will rise. **This serves to damp out the purchase of new long tokens and incentivises existing long token holders to sell back to the pool**.

![Image for post](https://miro.medium.com/max/569/1*tWukGn1VpEHvUACyTSLQMA.png)

### Summary

In this short article, we described how we have used dynamic Balancer pool weights to achieve the desired imbalance-sensitive prices in the Mettalex Autonomous Market Maker. A key constraint here is that when the AMM contains an equal balance of long and short position tokens, the spot price tracks the underlying asset linearly within the trading band.

We have not yet considered some of the additional degrees of freedom that are available in the Mettalex AMM. The **trading fees can be adjusted dynamically** in response to trade volumes in a manner similar to the [Kyber 3.0](https://blog.kyber.network/kyber-3-0-architecture-revamp-dynamic-mm-and-knc-migration-proposal-acae41046513) Dynamic Market Maker. Furthermore, the Mettalex AMM has the additional flexibility of minting or redeeming position token pairs for coins within the AMM to **control slippage as individual trade size increases without changing the fee**. These topics will be covered in later articles.



