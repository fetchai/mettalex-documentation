# Fetch.ai’s Stop-Loss agent for DeFi Liquidity Providers

Everybody now knows DeFi will be a crucial element of the decentralized world to come. At Fetch.ai, we want to provide you with a friendly _DeFi Toolkit_ to build your own DeFi applications, whether to market them, or for your own private use. The Fetch.ai team is releasing the _first version_ of this kit, in the form of **Stop-Loss Agents**. Without requiring any technical knowledge, liquidity providers on Uniswap and Pancake Swap can now define stop-loss instructions that will reduce the risks associated with impermanent loss. The long term vision for this year is that we plan to add more features and to easily define more agents: arbitrary sets of automated instructions, acting on your behalf in virtually any field of the decentralized ecosystem.

The idea here is to provide liquidity to a pool and to define a certain threshold, beyond which the agent will automatically remove your liquidity from that pool. Simple as that. Whether there is a sudden price pump or dump, Fetch.ai's stop-loss agent will automatically withdraw your liquidity and help you avoid impermanent loss. You will give all the instructions on the Fetch.ai platform, where the UI guides you through the whole process to make it perfectly straightforward. The platform also takes care of security under the hood, via a proxy contract: this ensures that your funds will be returned directly to you and only your agent has the permission to trigger the liquidity withdrawal. This way, you don’t need to worry about any liquidity loss. Besides, the agent doesn’t have access to your funds but only to the trigger that will withdraw them: other than you, no one and nothing has access to the tokens or funds you own.

The only thing you will need to know through the process, is the Ethereum address of the pool you wish to add a trigger for. If you don’t know how to get this information, here is how it works:

1. Visit [Uniswap](https://info.uniswap.org/home). Go on the left column, and click on Pairs. A certain pool is the pool for a certain pair: (e.g. the ETH/USDC pair is traded through the ETH/USDC pool. If the pair you are looking for does not appear right away in the top pairs, click on the loop icon on the top right of the page, and use the search field to find the pair and pool you’re looking for);
2. Once you see it, click on it. For instance, click on “ETH/USDC”. On the bottom of the page, you have the _Pair Information_, and it includes the _Pair Address_;
3. &#x20;This is the address of the pool you are looking for, so just click on the _Copy_ icon, and you are good to go.

### **How it works**

1. Register for the service on [http://agents.fetch.ai/](http://agents.fetch.ai). You will need to provide an email address, a password;
2. Remember to check your inbox mails as a confirmation will be email sent to the email provided;
3. Once registered, you will be prompted to deposit FET into your account as a fee (this is a paid service): 5 FET per agent and per month;
4. Create an agent;
5. Create a _**Stop Loss trigger,**_ and assign this task to one of your free agents (**note**: 1 agent will be mapped to 1 trigger). When creating the trigger, you must register your address with the proxy contract. Do not worry, the platform will guide you through this process. The interaction will happen through MetaMask, so it is necessary you own a [MetaMask](https://metamask.io) account;
6. At this point send some ETH to your agent. This fund will be needed and used for gas fees;\
   This process is not possible on Mainnet 2.0 at the moment, and it is available only on our original Ethereum contract, since we are targeting DeFi pools on ETH. In the future, we will offer discounts for paying with Mainnet 2.0 native FET;
7. You will be charged based on your number of active agents;
8. When a trigger is tripped, the following actions will be performed:
9. you agent sends a transaction to the proxy contract;
10. The proxy contract withdraws your liquidity from the pool, and returns it to you.

