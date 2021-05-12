---
layout: post
title: The Future of Ethereum Scaling: No More $300 Gas Fees
date: 2021-03-31
---
<br/>
<h1 style="font-weight: bold; text-align: center;">The Future of Ethereum Scaling: No More $300 Gas Fees</h1>
<br/>
<br/>

### **What’s the Ethereum gas issue?**
Lately, Ethereum (ETH) gas fees have skyrocketed, cutting into the pockets of transactors and completely blocking out some low-capital participants. For those who aren’t familiar, gas fees are fees paid to process a transaction on Ethereum, and they go up as network congestion grows. As an example, let’s say you wanted to swap .005 ETH (at the time of this writing, worth about $20) for USDT, which is equal to $1, through Uniswap. Uniswap is a DeFi application that allows you to, among other things, swap two Ethereum-based tokens. When I attempt to do this swap today, May 12th, 2021, this happens:
<br/>
<p align="center">
  <img src="ETHSwap.jpg" width="350" title="ETH for USDT Swap">
</p>
<br/>
That’ll be a $350 gas fee - insane. I would be at a net loss of about ~330 just to swap one token to another. Let’s also take a look at the Ethereum gas and daily transaction charts from 2018 to today:
<br/>
<br/>
<p align="center">
  <img src="ETHGas.png" width="900" title="ETH for USDT Swap">
</p>
<br/>
<p align="center">
  <img src="ETHTransactions.png" width="900" title="ETH for USDT Swap">
</p>
<br/>
<sub>Charts courtesy of https://etherscan.io</sub>
<br/>
<br/>
To clarify, gas prices on the first chart are denominated in Gwei; one Gwei is equal to 0.000000001 ETH. As we can see, daily transactions are trending upwards. So, as the network has to process more of these transactions, it must charge more Gwei as a gas fee to compensate miners, and each Gwei becomes more and more expensive in terms of dollars as the price of ETH continues to move up. So, when you want to swap tokens through Uniswap, which takes 10+ individual transactions, the gas fees start piling up.
<br/>
<br/>
Not only do current Ethereum scalability issues affect gas prices, they also affect transaction speed. This is clearly a problem, as Ethereum is home to many decentralized applications, NFTs, users, and developers. That’s where scaling solutions come in. 
<br/>
<br/>

### **Scaling solutions**
There are many proposed solutions to the Ethereum scaling issue. Some are already deployed, while others are still in development. Let’s go over a few prominent ones:
<br/>
- Layer 2 solutions such as zero-knowledge rollups. These seek to minimize on-chain transactions
- Sidechains. These are separate blockchains that run in parallel to the main Ethereum chain, come with cheaper transaction costs, and allow assets to be moved on and off of them. They do, however, come with security risks because attacks on these, unlike layer 2 solutions, could result in stolen assets. Polygon provides an interesting side-chain-like solution that allows various deployed Ethereum-compatible chains to process cheaper transactions and still communicate with the Ethereum main chain. They also offer other scaling solutions.
- EIP1559. This releases in a couple month’s time and features a new fee structure for gas.
- ETH 2.0. This actually involves changes made to the Ethereum chain itself. Among the changes are a beacon chain (already active), proof of stake, and sharding. 

Now, let’s dive deeper into some of these.

### **ZK-rollups with ZK-STARKS**
Zero-knowledge rollups offer over 100x improved scalability by batching many transactions into one and sending it to the main Ethereum blockchain. Two popular zero-knowledge proofs used in these rollups are ZK-SNARKs (discussed in an EARLIER ARTICLE) and ZK-STARKs. There are also other types of rollups such as optimistic rollups. In this article, I will focus on ZK-STARK based ZK-rollups. 

<br/>
<br/>
