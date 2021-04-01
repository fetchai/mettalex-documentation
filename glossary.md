# Glossary

#### **Autonomous Market Makers** 

Each commodity token pair has an associated autonomous market maker that allows market participants to exit a position at any point without having to find a counterparty on the exchange. The autonomous market maker uses a liquidity sensitive algorithm with bounded loss to manage market risk. Autonomous market maker liquidity providers receive pool tokens that entitle them to a fraction of the fees and spread earned by the market maker.



#### **Banded trading**

The Mettalex contract performs the settlement and clearing of the position tokens in the event that the reference price goes outside the specified trading band. The reference price feed comes in from an independent oracle specified at creation of the Mettalex contract and in the event of the price exceeding the cap or floor value, all position tokens are automatically redeemed for the collateral value of their position. The Mettalex contract then resets the floor and cap parameters automatically based on current market condition.



#### **Blockchain**

The blockchain is a digital ledger of all the transactions ever made in a particular cryptocurrency. It’s composed of individual blocks \(see definition above\) that are chained to each other through a cryptographic signature. Each time a block’s capacity is reached, a new block is added to the chain. The blockchain is repeatedly copied and saved onto thousands of computers all around the world, and it must always match each copy. As there is no master copy stored in one location, it’s considered decentralized.



#### **Circulating Supply**

This term refers to the number of cryptocurrency coins or tokens that are publicly available and circulating in a specific market. The circulating supply of a cryptocurrency can increase or decrease over time.



#### **Collateral**

A collateral is something of value given as a guarantee to obtain something else. For instance, a borrower may offer their car as a collateral to a lender when taking out a loan. The vehicle acts as a safeguard or warranty in case the borrower fails to pay their debts.  Usually, collateralized loans present much lower interest rates when compared to non-collateralized ones. Collateral can come in different forms. Some of the most common types include mortgage collaterals, invoice financing and margin trading collaterals.



#### **Decentralized Application \(DAPP\)**

A computer program that utilizes a blockchain for data storage, runs autonomously, is not controlled or operated from a single entity, is open source and has its use incentivized by the reward of fees or tokens.



#### **ERC-20**

The standard to which each Ethereum token complies. It defines the way that each token behaves so that transactions are predictable. Other cryptocurrencies also use the ERC-20 standard, piggybacking on the Ethereum network in the process.



#### Fiat

According with the Investopedia's definition:

> Fiat money is a government-issued currency that is not backed by a physical commodity, such as gold or silver, but rather by the government that issued it. It usually requires fiat exchanged at a CEX or through local means such as Bitcoin ATMs to be able to purchase cryptocurrency with fiat currency.



#### Gas Fees

Gas fees are rewards paid to Proof Of Work miners to incentivize them to support the network's transactions which become written to the blockchain. In Ethereum, this gas fee unit amount is expressed in gwei. Operations to or from CEXs, DEXs Liquidity Pools and wallets all require gas fees. The amount of this gas fee will vary in cost depending on current supply and demand: when demand on Ethereum or an ERC-20 network is at its highest, these gas fees are at also their highest.



#### **Governance Tokens** 

Governance tokens \(MTLX\) are used to vote on system parameters such as choice of autonomous market makers to back with liquidity from the liquidity pool, borrowing rates from the liquidity pool, usage of exchange fees, etc. Governance tokens are minted at an exponentially decreasing rate to incentivise early liquidity providers in the system. Minted tokens are distributed in proportion to the amount of liquidity supplied to the system at each block. Some fraction of the exchange fees and autonomous market maker spreads is used to buy back MTLX and burn.



#### **Liquidity Pool** 

A liquidity pool is a decoupled provider of collateral to the autonomous market maker. Liquidity providers receive an aggregated return from all commodity market maker fees and spreads in exchange for providing collateral that the market makers can use to mint position tokens. In addition liquidity providers receive a pro-rata distribution of MTLX governance tokens based on the amount and duration of their participation in the liquidity pool.



#### **Liquidity Provider**

A liquidity provider \(i.e. LP\) is a user who funds a liquidity pool with own crypto assets so as  to facilitate trading on the platform and earn passive income on the liquidity deposited.



#### **Mining**

Mining is the process through which cryptocurrency transactions are gathered, verified and recorded into a digital ledger known as blockchain. The work done by miners is essential for maintaining the integrity of the network and is also responsible for introducing new coins into the system.



**Mettalex Smart Contract** 

Each position token pair has an associated Mettalex smart contract that acts as a decentralized clearing house. Position tokens are minted in pairs of long and short tokens by locking up collateral in the Mettalex smart contract. Thereby,  position tokens are always fully collateralized, removing margin requirements and counterparty risk. At any stage a token holder can use the Mettalex smart contract to redeem the collateral backing a long and short token pair. The Mettalex smart contract is responsible for settling the position tokens if the underlying commodity index breaches the range \(i.e. Price Band\) specified at deployment of the Mettalex contract. 



**Oracle**

Within the blockchain context, an oracle is basically a data source that is used as a bridge between smart contracts and other external sources. More specifically, an oracle is an agent that not only communicates with external data sources but also verifies and authenticates that the data being provided is accurate. Thus, oracles are responsible for providing vital and reliable information to smart contracts, which in turn perform certain tasks.



**Position tokens**

Position tokens track the price change of an underlying asset \(i.e. long tokens\) or the negative of that change \(i.e. short tokens\). Leverage is achieved by the token price being a fraction of the asset price. This leverage enables hedgers to manage their risk exposure at minimal cost.



#### Spread

When an order is made on an exchange or market, the disagreement of the difference in price between potential buy and sell offers of an asset is called the spread. A wide spread in price can lead to higher slippage.



**Stablecoin**

A stablecoin is a type of cryptocurrency that is designed to maintain a stable market price. Recently, this type of digital currencies has grown in popularity, and we now have numerous stablecoin projects. Although the exact mechanisms vary from one coin to another, stablecoins are supposed to be somewhat resistant to market volatility, so they should not experience significant price changes.



**Volatility**

Volatility describes how quickly and how much the price of an asset changes. It is usually calculated in terms of standard deviations in the annual return of an asset over a set period of time. Because it is a measure of the rapidity and degree of price changes, volatility is often used as an effective measure of the investment risk associated with an asset.



**Yield Farming**

Yield farming is the practice of staking or lending crypto assets in order to generate high returns or rewards in the form of additional cryptocurrency. Yield farming protocols incentivize liquidity providers to stake or lock up their crypto assets in a smart contract-based liquidity pool. These incentives can be a percentage of transaction fees, interest from lenders or a governance token. These returns are expressed as an annual percentage yield \(APY\). As more investors add funds to the related liquidity pool, the value of the issued returns rise in value. 

