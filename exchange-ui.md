# Exchange UI

Interactions with Mettalex DEX will require the ability to call some Mettalex contract events, \(e.g. Mint L/S Position tokens from coin tokens \(USDT\), redeem L/S token pair for coin tokens or redeem single Position token for coin tokens if contract is settled\). This means that each user needs to call different methods accordingly to the liquidity pool they want to interact with \(i.e. Mettalex Vault, LPs pool or AMM pool\).

## **Possible Events: Mettalex Vault**

The possible scenarios a user can face when operating with position tokens in the Mettalex Vault are the following:

**Allowance**

`allowance(address owner, address spender)`

This method returns the remaining number of tokens the spender address is allowed to spend on behalf of the owner address through the method `transferFrom`. This value is zero by default. This value changes when `approve` or `transferFrom` are called.

**Approve**

`approve(address spender, uint256 amount)`

This method sets an amount `uint256` of tokens as the allowance of the spender address over the caller's tokens. It returns a boolean value indicating whether the operation succeeded or not.

### **BalanceOf**

`balanceOf(address account)`

Returns the amount of tokens owned by the account.

### **IncreaseAllowance**

`increaseAllowance(address spender, uint256 addedValue)`

This method is called when the user wants to increase the allowance related to his address. `uint256` indicates the value added to the existing allowance.

### **DecreaseAllowance**

`decreaseAllowance(address spender, uint256 subtractedValue)`

This method is called when the user wants to decrease the allowance related to his address. `uint256` indicates the value subtracted to the existing allowance.

### **MintPositions**

`mintPositions(uint256 _quantityToMint)`

This method is called to mint new position tokens where `uint256` indicates the amount of positions to be minted and transferred to the user’s account.

### **MintFromCollateralAmount**

`mintFromCollateralAmount(uint256 _collateralAmount)`

This method is called to mint new position tokens depending on the amount of collateral deposited. The amount of collateral to be deposited is given by `uint256`.

### **RedeemPositions**

`redeemPositions(address _to, uint256 _redeemQuantity)`

This method allows the user to redeem the collateral to send to the sender address.

The method is called to redeem the given amount of positions held by the user. The address the user wants to use to transfer the collateral redeemed is indicated by `address _to`. The amount of positions to redeem is given by `uint256`.

**SettlePosition**

`settlePositions()`

This method allows the users to settle by returning collateral and burning position tokens.

### **BulkSettlePositions**

`bulkSettlePositions(address[] calldata _settlers)`

This method allows the users to settle multiple accounts by returning collateral and burning position tokens. The parameter `address[]` indicates the array of user accounts to be settled.

### **TotalSupply**

`totalSupply()`

Returns the amount of tokens in existence.

### **Transfer**

`transfer(address recipient, uint256 amount)`

This method is called when a user wants to move an amount `uint256` of tokens from the caller's account to the recipient address. This method returns a boolean value indicating whether the operation succeeded or not.

### **TransferFrom**

`transferFrom(address sender, address recipient, uint256 amount)`

When this method is called it generates a transfer event in which the user wants to move an amount `uint256` of tokens from the sender address to recipient address using the allowance mechanism. The amount transferred will be deducted from the caller's allowance. This method returns a boolean value indicating if the operation succeeded.

## **Possible Events: LPs pool**

The scenarios a liquidity provider can face when operating with the the LPs pool can be the following:

### **Deposit**

`deposit(uint _amount)`

This method allows users who want to provide liquidity to deposit the quantity of liquidity desired into the pool. `uint _amount` indicates the amount of liquidity to be deposited.

### **Withdraw**

`withdraw(uint _shares)`

With this method users who want to withdraw their liquidity from the LPs pool. `uint _shares` indicates the amount of liquidity the user wants to withdraw.

### **WithdrawAll**

`withdrawAll()`

With this method the user can withdraw all of their liquidity from the LPs pool.

### **Earn**

`earn()`

This method transfers money from the vault to the autonomous market maker contract in order to earn trading fees from the supplied funds.

### **GetPricePerFullSare**

`getPricePerFullShare()`

This method is called when the user wants to get the price for the entire amount of liquidity he owns in the liquidity pool.

## **Possible Events: Autonomous Market Maker**

### **ClaimFees**

`claimFee(address _to)`

This method is called to claim the fee accumulated by the vault. The parameter `address _to` indicates the address to transfer the fees accrued.

### **GetExpectedOutAmount**

`getExpectedOutAmount (address fromToken, address toToken, uint256 fromTokenAmount)`

`returns (uint256 tokensReturned, uint256 priceImpact)`

This method is called to get the expected amount of tokens \(i.e. `uint256 fromTokemAmount`\) given out in a swap operation from the `fromToken` address to the `toToken` address.

This method returns the amount of tokens returned to the user’s account \(i.e. `uint256` `tokensReturned`\) and the price impact due to the operation \(i.e. `uint256 priceImpact`\).

### **GetExpectedInAmount**

`getExpectedInAmount (address fromToken, address toToken, uint256 toTokenAmount)`

`returns (uint256 tokensReturned, uint256 priceImpact)`

This method is called to get the expected amount of tokens \(i.e. `uint256 toTokemAmount`\) received in a swap operation from the `fromToken` address to the `toToken` address.

This method returns the amount of tokens returned to the account \(i.e. `uint256 tokensReturned`\) and the price impact due to the operation \(i.e. `uint256 priceImpact`\).

### **GetSwapFee**

`getSwapFee()`

It shows the fee related to the swap operation.

### **GetBalance**

`getBalance(address token)`

It is used in order to get the balance of tokens owned by the address

### **HandleBreach**

`handleBreach()`

Settle all Long and Short tokens held by the contract in case of Commodity breach.

### **SwapExactAmountIn**

`swapExactAmountIn (address tokenIn, uint256 tokenAmountIn, address tokenOut, uint256 minAmountOut, uint256 maxPrice)`

`returns (uint256 tokenAmountOut, uint256 spotPriceAfter)`

This method is called when the user wants to trade an amount `uint256 tokenAmountIn` of `tokenIn` taken by the pool, in exchange for an amount `uint256 minAmountOut` of `tokenOut` given to the user from the pool, with a maximum marginal price equal to `uint 256 maxPrice`.

This method returns the amount of tokens taken out from the user’s account \(i.e. `uint256 tokenAmountOut`\) and the new spot price after the swap operation \(i.e. `uint256 spotPriceAfter`\).

### **UpdateOracle**

`updateOracle(address _newOracle)`

This method changes the address of the Oracle contract. address is the new Oracle address.

### **UpdateSpot**

`updateSpot(uint256 _price)`

This method updates the spot price of an asset. `uint256` is the new updated price. The update can take place only if the arbitration price is within the contract bounds otherwise the contract settles.

### **UpdateCommodityAfterBreach**

`updateCommodityAfterBreach(address _vault, address _ltk, address _stk)`

This method is called to update the contract addresses after a band breach occurs. `address _vault` is the vault address whereas `address _ltk` and `address _stk` are respectively the Long and Short token addresses.

