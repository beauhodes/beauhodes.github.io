---
layout: post
title: A Metaverse Investment Thesis
date: 2022-04-25
---
<br/>
<h1 style="font-weight: bold; text-align: center;">A Metaverse Investment Thesis</h1>
<br/>
<br/>

### **Intro**
Prevailing sentiment is that current crypto games are subpar compared to their centralized alternatives because of issues surrounding developer talent and, though less so, regulations. “Just wait until the big gaming studios come into crypto”, “No major game developer will incorporate crypto without regulatory clarity”, and “No one is really playing these play-to-earn games for fun” are all phrases that have been echoed in recent months. There *is* some truth to these; powerhouse game studios can usually out-engineer small teams of developers, a lack of regulatory clarity can deter traditional developers from incorporating crypto into their games, and a not-insignificant portion of gamers would enjoy Halo over Axie Infinity. That being said, the reality is that lower developer firepower and unclear regulations are only part of the reason why current crypto games can’t hold a candle, gameplay-wise, to traditional games.

Surface-level, what might a utopian version of play-to-earn look like? Imagine Rocket League, but with the addition of “cars as tradable NFTs” and tournaments where you can pay tokens to enter and earn tokens if you win. Maybe you can even bet on teams as tournaments are on-going and livestream the games. Imagine Borderlands, but with a marketplace for selling items and allowing high-powered players to take lower-leveled players on boss raids for loot. Imagine Fortnite or any other game you enjoy with similar mechanics, or an MMO with a bustling crypto-based economy. To top it off, imagine all of this is decentralized (players custody their own items) and provably fair (impossible to cheat). I’m sure many gamers would be chomping at the bit to participate in this hypothetical future of gaming.

**This future of decentralized gaming (or, “the metaverse”) is currently constrained more by technology than by regulatory issues or a relative lack of developer talent.**
<br/>
<br/>

### **Why Decentralization?**
Centralized game creators own everything. Players’ data, items, and freedom to participate can be determined by the game creators. The game’s IP and profits are typically the sole property of the creators. Creators can change any of this at any time, which allows them to alter game mechanics, ban players without a reasonable cause, take away items that players have rightfully earned, or shut the game down completely. There may also be unintended side effects as a result of centralization such as high traffic shutting down servers, easy methods of cheating, or bugs that harm players’ experiences.

These lead us to some reasons why we would want decentralization in games:
- **Censorship Resistance:** No central party can determine who can play.
- **24/7 Uptime:** Users and developers are assured that the game will always be there. Scalability is not limited by cloud service costs; games scale with demand.
- **Open Infrastructure:** Many typical costs for infrastructure (databases, servers, etc.) can be cut down by outsourcing them to existing, open technologies, which saves time and money.
- **Ownership:** Users can take full custody of their own items.
- **Interoperability:** Games can incorporate items from other games, and users can use their assets in any ecosystem that supports them.
- **Anti-cheat:** Rules are written directly in code and can be verified.
<br/>
<br/>


### **How Do We Get Decentralized Games?**
Let’s think about this from first principles. At a high level, a game takes a series of inputs from players, who are utilizing some sort of interface, and produces some outputs. You shoot at an opponent, and the opponent takes damage. The goal then is to be able to *implement* and *enforce* these “transition functions” - mappings from inputs to outputs - in a decentralized fashion.

Centralized games typically build most of this from the ground up, though some aspects like game engines, servers, and platforms may be provided through integrations. Creating scalable, enjoyable games in a decentralized fashion is arguably harder, but, thanks to the openness and high level of composability offered by decentralized solutions, even more parts of the tech stack can be outsourced. Some technologies that are available to build such experiences include:
- **Cheap/programmable asset ledgers:** Solana, Polygon, Avalanche, etc.
- **Cross-chain communication:** Layer Zero, IBC, Synapse, Wormhole, etc.
- **Oracles:** Chainlink, Pyth, Band, etc.
- **Decentralized storage:** IPFS, Arweave, Ceramic, Filecoin, etc.
- **Decentralized/scalable compute:** Akash, Fluence, Aleph.im, ZK-rollups<sup>1</sup>, etc.
- **Interfaces/rendering:** Render Network, The Graph<sup>2</sup>, Livepeer, etc.
- **Connections:** Wallets, Pocket Network, Helium, etc.
<br/>
<sub><i>1 Mainly referring to recursive proofs; high scalability</i></sub>
<sub>2 Referring to using subgraphs to scale queries</sub>

Different “dGames” (decentralized games) and dApps will require different combinations of these. We already have some layers of the stack needed to make the aforementioned scalable, decentralized gaming vision happen, though there are some holes to be filled that will be addressed later.
<br/>
<br/>

### **Current Crypto Games**
One approach is to encode the entire game, aside from the interface (usually run on centralized cloud servers, but sometimes hosted using a decentralized service such as IPFS), into smart contracts. Current crypto games including Axie Infinity, DeFi Kingdoms, and Crabada operate this way. Often, they’ll use NFT metadata, randomness, and user inputs (“use this specific attack move”) as inputs to their smart contracts to produce some output. Although most crypto games don’t publish these contracts on block explorers or Github in order to keep their “secret sauce” safe and to make things harder on botters, this is really all that’s going on. This approach, when transition functions are not *highly* computationally-burdened or time-dependent, works great for more basic games such as turn-based strategy games. It also works great for DeFi applications and primitives, prediction markets, and the like as transition functions/rules are easier to program for financial assets that only require number manipulation.


<br/>
<p align="center">
  <img src="/resources/basicflow.png" width="600" title="BasicFlow">
</p>
<br/>
<sub><a href="https://www.vecteezy.com/free-vector/3d">Figure 1: Simple dApp transaction flow</a></sub>
<br/>
<br/>
