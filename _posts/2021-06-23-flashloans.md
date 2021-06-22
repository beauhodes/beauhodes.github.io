---
layout: post
title: Flash Loans, Mempools, and MEV
date: 2021-06-23
---
<br/>
<h1 style="font-weight: bold; text-align: center;">Flash Loans, Mempools, and MEV</h1>
<br/>
<br/>

<br/>
<p align="center">
  <img src="/resources/flash.jpg" width="350" title="Flash">
</p>
<br/>
<sub><a href="https://www.vecteezy.com/free-vector/3d">Source: Vecteezy</a></sub>
<br/>
<br/>

### **Intro**
Imagine you want $1 million to perform some action right now. Maybe it’s profiting off an arbitrage opportunity, getting out of a bad loan, or, if you just want to watch the world burn, taking advantage of an exploit in a financial system to steal money. Obviously you’d have to pay the $1 million back, but think of how long the process to obtain the loan in the first place would take you. Plus, there’s no guarantee that your use case for the loan won’t go haywire and leave you in debt. What if there was a permissionless way to get this loan, execute whatever strategy you wanted to (so long as it can be done instantaneously), and have 0 risk of going into debt because, if you fail to pay it back, it’s as if you never even got the loan in the first place. In decentralized finance (DeFi), you can with a flash loan.
<br/>
<br/>

### **What is a flash loan**
Before defining what a flash loan is, let me clarify that, in this article, we will be discussing flash loans in the context of the Ethereum blockchain. The same concepts apply elsewhere, but most flash loans occur on Ethereum given the amount of DeFi activity and the broader accessibility to these loans.

To understand what flash loans are and how they work on Ethereum, we need to know a few things about how Ethereum works at a basic level. The Ethereum blockchain consists of blocks (surprise). A new block is created roughly every 13 seconds, and each block is filled with transactions (about 2,000 per block recently). Further, each of these transactions can contain multiple operations, and the operations in a transaction are atomic. This means that, for a transaction containing multiple operations, they must all succeed or all fail. If even one operation fails, the entire transaction is invalidated. Think of operations inside a transaction as being “all or nothing”. 

Flash loans take advantage of this atomicity by allowing users to take out large, non-collateralized loans on the condition that the loan is paid back in the same transaction (plus, depending on where the loan comes from, a small fee). These loans can be non-collateralized because, if the user is unable to pay back the loan in the same transaction, the entire transaction is invalidated, and it is as if the loan was never given out in the first place. The user still pays the gas fees associated with the operations inside of the transaction, but, even if they took out a $100 million loan and lost it all, the loan would be invalidated. 

Since a flash loan must be taken out and paid back in the same transaction, how could they actually be useful? The most common use cases are: 
- Arbitrage: Taking advantage of the same asset being priced different in two different places. For instance, if ETH was trading for 2000 DAI on Uniswap and 2100 DAI on Sushiswap, you could use a flash loan to buy ETH on Uniswap and sell it on Sushiswap and pocket the difference after paying back the loan.
- Collateral swaps: Swapping the collateral on a loan to avoid liquidation. For instance, if you have a DeFi loan (not a flash loan!) that is collateralized by ETH and the ETH price starts dropping quickly, you could use a flash loan to swap the loan’s collateral for a stablecoin in order to avoid liquidation from the loan becoming under-collateralized and forcibly selling your collateral. 
- Debt swaps: Swapping the platform or asset of a loan to obtain a better rate. For instance, if you had a loan for DAI with an interest rate of 7% but the rate for USDT loans was 5%, you could use a flash loan to pay back your DAI loan, take out a new loan for USDC at the lower rate, swap the USDC for DAI, and pay back the flash loan all in one transaction. You could think of this as instant refinancing.
- Attacks: Flash loans are also used in attacks on DeFi platforms. Usually this involves using large amounts of capital to manipulate prices or taking advantage of systematic issues in protocols to steal tokens. Most attacks are complex, and these are requiring developers to be much more careful about protocol design and, for trading-related apps, where they get price data from. 

 

Anyone can get a flash loan through protocols that offer them and have sufficient reserves of capital to offer. Aave, dYdX, Uniswap, and Pancakeswap are some of the most common that offer smart contract support for flash loans. There are also some more user-friendly interfaces like Collateral Swap, Furucombo, and DeFi Saver. However, it’s easiest to understand flash loans by looking “under the hood” at the smart contracts.

Coding a flash loan
As an example, I’ve put together a short smart contract, shown below, that uses Aave to obtain a flash loan for 10 ether worth of DAI. If ETH was priced at $2000, we’d be getting a flash loan of about $200,000. Keep in mind that this code should not be used in production and it has not been error checked/audited. Also, for the non-coders, everything following a double slash (//) is a comment, not actual code. Let’s walk through how the contract works.

*insert code*
```javascript
pragma solidity 0.6.12;

import "@openzeppelin/contracts/math/SafeMath.sol";

//Assuming we have the following contracts in the same directory as this contract
import { FlashLoanReceiverBase } from "./FlashLoanReceiverBase.sol";
import { ILendingPool } from "./ILendingPool.sol";
import { ILendingPoolAddressesProvider } from "./ILendingPoolAddressesProvider.sol";

contract flashLoanContract is FlashLoanReceiverBase {
  using SafeMath for uint256;

  //Upon contract deployment, we specify which Aave lending pool to use for the loan
  constructor(ILendingPoolAddressesProvider _addressProvider) FlashLoanReceiverBase(_addressProvider) public {}

  //called after we have received the loan
  function executeOperation(
      address[] calldata assets,
      uint256[] calldata amounts,
      uint256[] calldata premiums,
      address initiator,
      bytes calldata params
      ) external override returns (bool) {

      //Input logic
      //Could be multiple swaps, providing collateral, etc

      //Check to ensure we can pay back. Even if we did not do this, Aave would revert the transaction
      //Since we are only calling this with one asset, we can do some simple math
      uint amountOwed = amounts[0].add(premiums[0]); //calculate loan repayment amount
      require(amountOwed <= getBalanceInternal(address(this), assets[0]); //ensure we can repay the loan

      //Send any profits wherever you want - do not keep them in this contract

      //Allow the lending pool to be able to take back the amount owed for the loan
      //Since we only used one asset, you could do this without a for loop, but I'll leave it as an example
      for (uint i = 0; i < assets.length; i++) {
        uint amountOwed = amounts[i].add(premiums[i]);
        IERC20(assets[i]).approve(address(LENDING_POOL), amountOwed);
      }

      return true;
  }

  function _initiateFlashLoan() internal {
    address receiver = address(this);

    address[] memory assets = new address[](1);
    assets[1] = address(0x6b175474e89094c44da98b954eedeac495271d0f); //DAI token address

    uint256[] memory amounts = new uint256[](1);
    amounts[0] = 100 ether; //specify loan amount: 100 ether worth of DAI tokens

    uint256[] memory modes = new uint256[](1);
    modes[0] = 0; //no debt - loan must all be paid back in the same transaction

    address onBehalfOf = address(this);
    bytes memory params = ""; //would need to encode if needed - for instance "abi.encode(address(this), 1234)"
    uint16 referralCode = 0;

    LENDING_POOL.flashLoan(receiver, assets, amounts, modes, onBehalfOf, params, referralCode); //initiate the flash loan
  }

  function initiateFlashLoan() public onlyOwner {
    _initiateFlashLoan();
  }

}
```
<br/>
<br/>
