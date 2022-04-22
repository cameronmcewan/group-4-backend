# PortFolio

This repository contains the backend code for the PortFolio project, written in Solidity. 

## Motivation

A PortFolio is an [ERC20 token](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/token/ERC20/ERC20.sol) representing a pre-defined 'basket of goods' (a portfolio) of crypto assets. These assets are themselves other ERC20 tokens on the Ethereum blockchain. 

What are the benefits of PortFolio?

1. Easily buy and hold a diversified set of crypto assets.
2. Redeem for the underlying assets at any time.
3. Sell the underlying assets for the open-market Eth value at any time.
4. Create custom PortFolios according to your risk preferences.

## Development

### Hardhat

We use the [Hardhat framework](https://hardhat.org/getting-started/) to compile and test the contracts. 

When you clone the repo, you will need to run `npm install` to get all of the smart contract, Hardhat and testing dependencies.

You will also need to create a .env file and replace the following variables with your own:

```
RINKEBY_API_KEY="https://rinkeby.infura.io/v3/<rinkeby_infura_api>"
KOVAN_API_KEY="https://kovan.infura.io/v3/<kovan_infura_api>"
PRIVATE_KEY="<wallet_private_key>"
```

To run HardHat tests, use:

+ npx hardhat test

Testing:
1. test/integration_test_portfolio_factory.js
    - Verifies that the portfolio factory is functioning as expected.  Deploys two portfolio instances and verifies that these are working.
2. test/integration_test_portfolio.js
    - Monitors the minting, and burning of the portfolio ERC20 token, and ensures that assets are bought, sold, and transferred correctly.
    - Tests key functionality of the portfolio contract, including:
        - Initial dployment
        - function: initialisePortfolio()
        - function: buy()
        - function: redeemAssets()
        - function: sellAssets()

### Smart contracts

The contracts folder contains three smart contracts:

1. Portfolio.sol - an ERC20 token representing a portfolio of crypto assets/
    + Allows users to buy into the portfolio
    + Swaps WETH to allocated proportions of portfolio assets
    + Stores all assets held by the portfolio (e.g., 50 LINK, 1000 DAI)
    + Allows users to redeem their share of assets directly 
    + Alternatively: allows users to sell their assets and receieve ETH

3. PortfolioFactory.sol - a contract used to create new Portfolios and track existing Portfolios

### Test Portfolios

**Kovan**

We have deployed an example Portfolio on Kovan at the following address:

*0x6CB8336581f0B99B225b14F3AfE7E2AC3f876C4F* 

This PortFolio is made up of the following assets:

| Asset           | Holding (%) |
| --------------- | ----------- |
| Wrapped Ether   | 20          |
| Dai Stablecoin  | 40          |
| ChainLink Token | 40          |

**Rinkeby**

We have deployed an example Portfolio on Kovan at the following address: 

*0x7157Ea1F87Cc4CbeE63137D3CB5ecBd44eE1960a*

ERC20 : NAME = "Portfolio", TICKER = "FOLO"

It's super simple, containing only Weth.

## Core Functionality

### 1. Creating a portfolio

Use the constructor of PortfolioFactory.sol to create a portfolio containing *k* tokens:

### 2. Buy into an existing portfolio

First, you need the contract (portfolio) address. 

Send a transaction to the *buy* function, with Ether in msg.value. 

### 3. Sell position in existing portfolio

First, you need the contract (portfolio) address.

Send a transaction to the *sell* function, and pass as argument the number of PortFolio tokens to sell. 

The function will sell the appropriate share of the underlying assets and transfer the Ether to your address. 

### 3. Redeem assets from existing portfolio

First, you need the contract (portfolio) address.

Send a transaction to the *redeem* function, and pass as argument the number of PortFolio tokens to sell. 

The function will transfer the appropriate share of the underlying assets to your address. 

## Contributors

[Luke Kirwan](https://github.com/thelk22)

[Alex Straw](https://github.com/alex-straw)


