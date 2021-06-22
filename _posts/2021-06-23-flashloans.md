---
layout: post
title: Flash Loans, Mempools, and MEV
date: 2021-06-23
---
<br/>
<h1 style="font-weight: bold; text-align: center;">Flash Loans, Mempools, and MEV</h1>
<br/>
<br/>

### **Intro**
Imagine you want $1 million to perform some action right now. Maybe it’s profiting off an arbitrage opportunity, getting out of a bad loan, or, if you just want to watch the world burn, taking advantage of an exploit in a financial system to steal money. Obviously you’d have to pay the $1 million back, but think of how long the process to obtain the loan in the first place would take you. Plus, there’s no guarantee that your use case for the loan won’t go haywire and leave you in debt. What if there was a permissionless way to get this loan, execute whatever strategy you wanted to (so long as it can be done instantaneously), and have 0 risk of going into debt because, if you fail to pay it back, it’s as if you never even got the loan in the first place. In decentralized finance (DeFi), you can with a flash loan.
<br/>
<br/>

### **What is a flash loan**
Before defining what a flash loan is, let me clarify that, in this article, we will be discussing flash loans in the context of the Ethereum blockchain. The same concepts apply elsewhere, but most flash loans occur on Ethereum given the amount of DeFi activity and the broader accessibility to these loans.
<br/>
<br/>
