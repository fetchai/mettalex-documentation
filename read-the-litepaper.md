# Mettalex Litepaper

{% file src=".gitbook/assets/mettalex-litepaper (1).pdf" %}
Mettalex Litepaper
{% endfile %}

Version: v1.0 (September 2020)

[www.mettalex.c](http://www.mettalex.com)[om](http://www.mettalex.com)

## Abstract

The Mettalex team is creating a commodities exchange to enable market participants to gain economic exposure to the spot price and derivatives of commodities and other instruments. This will allow hedging of risk for physical holders of the commodity or leveraged positions for speculators. Positions are taken using specially designed ‘position tokens’.

This document is a high level litepaper describing the goals and system components.

## Overview

### System diagram

![](<.gitbook/assets/0 (1).png>)

The Mettalex system diagram shows the core components:

* An exchange layer where traders can take long and short positions against a range of reference assets or related derivatives
* A tokenisation layer that provides tokens representing the long and short positions, together with autonomous market makers linked to the reference assets
* A liquidity provision layer where lenders can supply liquidity to the autonomous market makers in return for a proportion of the market making spreads
* A governance layer that rewards liquidity providers with governance tokens in proportion to the amount and duration of liquidity they supply to the system

### Users

#### Physical Asset Holders

Key Benefit: Risk Management

The main objective is to provide access to risk management tools to a large audience of physical commodity userse.g. Crypto Mining companies, steel mills. These users currently only have access to risk management tools via financial market intermediaries who charge high spreads and have limited liquidity

#### Speculators

Key Benefit: Access to Markets

The risk management tools provided to the main user group of physical traders will offer the opportunity for financial speculators to take a view on an otherwise inaccessible market.

#### Liquidity Providers

Key Benefit: Returns on Investment

There will be a role for liquidity providers (LPs) and market makers in the system to increase trading volumes and reduce cost of trading. LPs will receive yield on capital invested via transaction fees and/or trading spreads.

Liquidity providers supplying liquidity to system controlled autonomous market makers will additionally earn governance tokens via a liquidity mining process that rewards in proportion to the amount and duration of supplied liquidity.

### Components

We have created position tokens representing leveraged cash settled exposures to movements in commodity prices. These tokens are issued and traded on an exchange that provides a consortium of commodity producers and cryptocurrency investors to act as liquidity providers.

#### Position Tokens

The position tokens track the price change of an underlying asset (long tokens), or the negative of that change (short tokens). Leverage is achieved by the token price being a fraction of the asset price. This leverage enables hedgers to manage their risk exposure at minimal cost.

#### Exchange Interface

The exchange interface integrates a reference price feed for settlement and pricing of commodity tokens. Traders in the commodity tokens will be able to open and close positions using stablecoin collateral by trading against other participants or autonomous market makers. They will also be able to provide liquidity by using the Mettalex contract to mint token pairs, or use it to redeem a paired position in long and short tokens to reclaim the backing collateral.

#### Mettalex Contracts - Smart Contracts

Each position token pair has an associated Mettalex smart contract that acts as a decentralized clearing house. Position tokens are minted in pairs of long and short tokens by locking up collateral in the Mettalex smart contract. This means that the position tokens are always fully collateralised, removing margin requirements and counterparty risk. At any stage a token holder can use the Mettalex smart contract to redeem the collateral backing a long and short token pair.

The Mettalex smart contract also has the responsibility of settling the position tokens if the underlying commodity index breaches the range specified at deployment of the Mettalex contract.

#### Autonomous Market Makers

Each commodity token pair has an associated autonomous market maker that allows market participants to exit a position at any point without having to find a counterparty on the exchange. The autonomous market maker uses a liquidity sensitive algorithm with bounded loss to manage market risk. Autonomous market maker liquidity providers receive pool tokens that entitle them to a fraction of the fees and spread earned by the market maker.

#### Liquidity Pool

The liquidity pool is a decoupled provider of collateral to the autonomous market makers. Liquidity providers receive an aggregated return from all commodity market maker fees and spreads in exchange for providing collateral that the market makers can use to mint position tokens. In addition liquidity providers receive a pro-rata distribution of MTLX governance tokens based on the amount and duration of their participation in the liquidity pool.

#### Governance Tokens

Governance tokens (MTLX) are used to vote on system parameters such as choice of autonomous market makers to back with liquidity from the liquidity pool, borrowing rates from the liquidity pool, usage of exchange fees. Governance tokens are minted at an exponentially decreasing rate to incentivise early liquidity providers in the system. Minted tokens are distributed in proportion to the amount of liquidity supplied to the system at each block. Some fraction of the exchange fees and autonomous market maker spreads is used to buy back MTLX and burn.

## Explaining Position Tokens

Given a commodity, tokens are created that track the reference price in a long (L) or short (S) exposure:

* Long token: increase of spot price of $1.00 results in the long token price increasing by $1.00.
* Short token: increase of spot price of $1.00 results in the short token price decreasing by $1.00.

These tokens have the following properties:

* A leveraged exposure is achieved if the L/S token price differs from the spot price.
* The tokens do not require further funding once purchased i.e. the system has no margin requirements.
* The tokens do not have a fixed expiry date so that holders don’t need to roll their positions into a new series of tokens as token expiry is reached.
* Liquidity is concentrated into a small number of tokens for each reference asset.
* The exchange does not rely on external liquidity providers e.g. hedging spot exposure by buying futures contracts on LME, although market participants are free to use this capability should they have access to it.
* The tokens are ERC-20 compatible tokens so can be stored in wallets.

### Underlying Asset Price Feed

The reference asset price is periodically fed into the system from multiple reference exchanges such as the London Metals Exchange (LME), Chicago Mercantile Exchange(CME), Intercontinental Exchange (ICE). Using the derived multiple price feeds over the decentralised oracle network provides a fair pricing mechanism and is used to determine whether a band breach occurs i.e. when the price is out of the allowed range for the token. In the event of a band breach the position tokens change state to settled, with one of the token L/S pair having the full value of the underlying collateral and the other being worthless.

In normal circumstances outside of breach conditions an autonomous market maker provides a price for position tokens based on the current reference asset index and market sentiment expressed by demand for the different positions. This acts as a proxy for the futures curve for the asset.

### Commodity Derived Position Tokens

For commodity derived position tokens we expect the spot price to usually trade over a bounded range, called the delta. For example for steel scrap this might range from $225.00 to $375.00 per tonne, i.e. a delta of $150.00 centred around $300.00.

We can use this trading range to set the floor and cap prices for the token pair. Continuing the example above the value of a long and short pair of tokens is equal to the delta, here $150.00, with floor set at $225.00 and cap at $375.00. That is, depositing $150.00 worth of collateral will mint a L\&S pair. Assuming the spot price when the tokens are minted is $300.00, each token will have a value of $75.00, representing a leverage of $300.00/$75.00 = 4x. Choosing the floor and cap based on historical delta allows us to create a non-expiring perpetual token that can be held indefinitely as long as the spot remains within the historical range.

This has the consequence that as the spot trades away from the centre price it becomes cheaper to buy exposure for the position opposite the movement. For example if spot increases to $350.00 the value of a long token becomes $125.00 (leverage = $350.00/$125.00 = 2.8x) while the short token is now worth $25.00 (leverage = $350.00/$25.00 = 14x). This is an incentive for market participants to provide liquidity for the short position at low cost if they believe a top in the spot price has been reached.

If the spot price breaches the historical range the long and short tokens settle in an autonomous process:

* If cap is reached then long price = collateral value, short price = 0
* If floor is reached then long price = 0, short price = collateral value

At this point the current token pair would be settled and all collateral backed by the tokens distributed to the token holders. The position tokens would all be burnt. The Mettalex contract would be reinitialised with parameters centered around the current spot price with the same price range. New position tokens could then be minted using the reset Mettalex contract and trading resumes as normal.

Note that there is a trade off between leverage and the probability of breaching a floor or cap. In the limit of the case where we have leverage of 1 the floor is set at 0 and the cap at twice the spot price ($600.00 here), which should have a low probability of breaching either floor or cap.

In contrast a floor-cap range of $270.00-$330.00 would give initially 10x leverage but at the expense of multiple settlement and token reissuance cycles.

### Spread Position Tokens

A unique capability of the system is the ability to tokenize spreads between commodities simply by using the difference between asset indexes as the reference value. For example a steel mill is long the spread between steel scrap and steel rebar. To hedge their position using commodity futures would require opening positions in both commodities, while in the Mettalex system a single position token is sufficient.

## Market dynamics

### Settlement and Clearing of Position Tokens

Each position token pair is backed by a corresponding Mettalex contract that acts as a central clearing house for that pair. Any market participant can supply collateral to the Mettalex contract to mint a pair of long and short position tokens. Conversely, redeeming an equal quantity of long and short position tokens unlocks the collateral that backed their position. A small fee is charged for minting operations, this can either be paid in units of collateral or at a reduced rate in MTLX governance tokens.

### Arbitrage opportunities

This mechanism results in an arbitrage opportunity if a market participant can purchase a long and short token pair on the open market for less than the collateral value of the pair, as they can then redeem the pair for a higher value. The opposite arbitrage exists if a long and short position token pair can be sold for more than the underlying collateral.

### Banded trading

As well as removing counterparty risk, the other market regulation activity the Mettalex contract performs is settlement and clearing of the position tokens in the event that the reference price goes outside the specified trading band. The reference price feed comes in from an independent oracle specified at creation of the Mettalex contract and in the event of the price exceeding the cap or floor value all position tokens are automatically redeemed for the collateral value of their position as described above. The Mettalex contract then resets the floor and cap parameters automatically based on current market conditions.

## Autonomous Market Maker

Each position token pair has an associated autonomous market maker that allows market participants to exit a position by buying the other side of the position token pair. Market participants can only buy from the autonomous market maker, which adjusts the price of each token in response to liquidity demands and the reference index. This leads to the autonomous market maker being a proxy for the futures curve for the commodity or spread.

To remove risk the autonomous market maker will sell a long and short token pair at a price slightly higher than the backing collateral for the pair. This spread can be controlled using the decentralized governance mechanism.

The autonomous market maker uses the Mettalex contract to convert supplied collateral into position tokens for market making operations. Liquidity providers lock up collateral for use by the autonomous market maker in exchange for pool tokens that return a fraction of the market making spreads and fees.

The autonomous market maker is pluggable component of the system that can be upgraded as improved networks and algorithms become available. In the initial implementation on the Ethereum network a protocol is used to create a pool containing a mix of collateral and long and short position tokens for each commodity.

The interaction between the Mettalex contract and the Mettalex pool provides a fair price to the commodity trader by dynamically adjusting the token weights in response to price movements of the reference asset.

The Fetch.ai network implementation of the autonomous market maker will offer the opportunity to use more advanced AI agent driven market making algorithms to provide liquidity to a full supply chain at once. This could be achieved by having position tokens from multiple commodities (up to 12 currently but could be more) and spreads in the same autonomous market maker pool.

## Liquidity Pool

The Mettalex system supports a wide range of commodity and spread tokens. Liquidity providers can contribute collateral to a central pool that backs all autonomous market makers rather than supplying liquidity to a specific commodity token. In return the liquidity providers receive aggregate transaction fees from market making operations for the position tokens.

Additionally liquidity providers receive rewards in the form of MTLX governance tokens based on the fraction of the overall system liquidity they provide.

From a functional perspective the liquidity providers are locking up collateral for use by the Mettalex system as a whole, in return for a basket of autonomous market maker pool tokens and the accrual of governance tokens. Liquidity providers are free to reclaim their collateral at any point there is sufficient liquidity in the system. In normal operating conditions liquidity providers can freely exit the system however in times of high liquidity demand they may need to wait a short period of time until sufficient liquidity has been accrued through transaction fees.

## Governance Tokens

The purpose of the MTLX token is to enable stakeholders in the Mettalex decentralized platform to govern the policies and fees in operation on the platform.

In the ordinary course of business on Mettalex, MTLX tokens will be distributed to providers of liquidity to the liquidity pools that enable position tokens to be created.

In turn, MTLX then enable the platform stakeholders to vote on policy, including:

* to vote on system parameters such as choice of autonomous market makers to back with liquidity from the liquidity pool
* vote on the creation of new markets
* the usage of exchange fees
* the percentage of the spread going to the pool
* the buyback and borrowing rates from the liquidity pool

MTLX governance tokens are minted at linear rate and distributed to liquidity providers in proportion to the amount of liquidity they supply to the central pool. A proportion of market making fees is used to buy back and ultimately burn MTLX tokens, decreasing supply.

The demand for MTLX tokens comes from:

* Ability to vote on system parameters such as autonomous market maker spreads
* Use of MTLX tokens to pay for minting position token pairs
* Distribution of other income in the system.

## Roadmap

The initial release of the Mettalex exchange uses existing DeFi building blocks from the Ethereum ecosystem and some centralized components. This provides an entry point for commodity and crypto market participants to the system to allow iteration on requirements.

Initial users for the commodities platform have been recruited and have been participating in closed platform testing. Initial trading pairs will be experimented with, based on user demand, but are anticipated to include:

1. Steel Supply chain based commodity spreads
2. Gold and Silver spreads with BTC and USD
3. Lithium and Oil Spreads with BTC and ETH
4. Stock Market indices spreads with BTC and ETH
5. Data Storage, Compute cycle and Utilization spreads with USD/BTC/ETH

The roadmap for increasing use of Fetch.ai technology in the system includes:

* Replacing the centralized exchange with a decentralized exchange using the Fetch.ai ledger for high transaction rates (c.f. ETH level 2 scaling).
* Fetch.ai agents and collective learning acting as index providers e.g. monitoring process** **metrics throughout supply chains to create spread tokens for supply chain optimization.
* Autonomous market makers running on Fetch.ai ledger for increased capability

Fetch.ai interoperability technology will enable these use cases e.g. stablecoin pegging with the Ethereum network to enable the transactions in DEX and AMM use cases.
