--- 
title: "Some Paper Notes"
katex: true 
draft: true 
--- 

# Lattices 

## [Practical Exact Proofs from Lattices: New Techniques to Exploit Fully-Splitting Rings](https://eprint.iacr.org/2020/518.pdf)

*Motivation/Overview*

- Goal: prove knowledge of secret vector $s$ that satisfies $As = t$, where $A$ and $t$ are public. $A \in \mathbb{Z}^{m \times n}$, $t \in
  \mathbb{Z}^{m}$, $s \in \langle-1, 0, 1\rangle^{n}$.  
- What we will really mean is that $A$ is a matrix of polynomials in $\mathcal{R}\_{q}$ over some basis in $\mathbb{Z}\_{q}$. $t$ is a polynomial
  vector and $s$ is a short polynomial vector -- that is, its coefficients are themselves ternary polynomials.  
- More efficient to prove knowledge for relaxation $\hat{s}$ where $A\hat{s} = ct$. The coefficients of $\hat{s}$ come from a wider range and $c$ is
  some short polynomial.
- Based on rejection sampling of Lyubashevsky, used in some important standard signature schemes and also for more exotic lattice-based signatures
  such as group and ring signatures. Work over polynomial rings.  
- Most efficient at time of writing because they achieve security after only a single run as opposed to Stern-type protocols which require repeated
  runs for the purpose of soundnness amplification. 
- But (1) not compatible with standardized encryption schemes and (2) not sufficiently expressive -- cannot support integer range proofs or proofs of
  integer relations. Such proofs have applications in blockchain protocols. **Exact proof systems -- that prove knowledge of $s$ rather than $\hat{s}$
  -- make these more expressive proofs possible**. 
- Exact proof systems are made possible by BDLOP commitments. 
- Fastest lattice-based KEM encapsulation and decapsulation times are on the **order of a few microsections**, which is **one magnitude faster than a
  single elliptic curve multiplication**. Speed comes from the fact that (1) modulus $q$ is usually not more than 32 bits, so not multi-precision
  arithmetic is necessary as it is for EC crypto and (2) required arithmetic favors parallelism - NTTs. 
- 47KB   

*Approach*

# Crypto Ecosystem 

## [Extractable Value](https://medium.com/amber-group/extractable-value-7b0d4356a843)

*Motivation* 
- Rothschild superior trans-European information network was primary competitive advantage. Nathan Rothschild learns of Napolean's defeat at Waterloo
  36 hours ahead of London official messenger. 
- MEV = **Maximum Extractable Value** $\longrightarrow$ impact on protocol transparency, sustainability, decentralization, security, censorship
  resistance, valuation, etc. 
- **MEV contributed to $\ge 5.8% $ of total miner revenue since 2020**. MEV opportunities: arbitrage, liquidations, sandwich attacks.

### *Lifecycle of Ethereium Transaction* 
1. Connect MetaMask wallet to Uniswap front end. 
2. Specify and sign trade, which is sent through MetaMask default RPC endpoint to Infura 
3. Infura propagates to other nodes throughout Ethereium network, which themselves propogate to nodes they are connected to. 

**def mempool**. database of pending transactions that every validator maintains. Each validator builds blocks of transactions based on its own
mempool. Transactions are typically ordered by gas price, though they could be ordered according to custom validator logic.  

4. Every 12 seconds, validator is randomly selected to build and propose a block of transactions. Validator broadcasts proposed block to network. The
   proposed block is checked by a randomly selected committee of validators, who create attestations for it. 
5. If the proposed block is validated, then the transactions it contains are considered *submitted*, and are removed from a node's mempool. 

### *MEV Opportunities*

- The mempool is public, and because transactions are submitted publicly, they produce some interesting opportunities for profit. The main point is that
validators are in a privelaged position to take advantage of these opportunities. 

> Ethereum's consensus protocol only enforces agreement at the block level, **allowing validators to choose what happens within each block. Therefore,
> validators can decide what transactions to include and in what order these transactions are executed.** Because the mempool is visible to all,
> transactions that take advantage of MEV opportunities can be observed and copied, leading to a "pile-on" effect. This incentivizes users to collude
> with validators/miners to guarantee that their transactions will be included or that transactions will be ordered in a particular way.
> Validators/miners can also submit and prioritize their own transactions. 

- Parties in MEV Supply Chain: User expresses intent to change state of blockchain, Wallet/App translates user intent to transaction, Searcher
  monitors mempool and submits transactions to extract MEV, Builder aggregates transactions into blocks, Validator proposes and attests to blocks. 

**Def PoS MEV**. The total value a validator can extract across a block (or series of blocks) given the state of its environment and all the actions
available to it. 
- Here, the validator's environment is usually fixed outside of the validator's control as the blockchain's rules, smart contract code,
      the mempool, etc. 
- Validator actions: reordering, censoring, inserting transactions, modifying block timestamps, randomness manipulation, DOS of other validators,
      etc. 

**Sandwich**. Has to do with frontrunning, but still not entirely sure I understand ... Takes advantage of delay in transaction confirmation and
slippage. Essentially a timing attack that tunes state to maximum slippage, then takes advantage of state change after transaction executes to extract
value. 

**Arbitrage**.

**Liquidation**. Users deposit collateral and in exchange are given a borrowing budget. As value of collateral fluctuates, so does user borrowing pwoer.
Market participants are responsible for liquidating borrowers if they exceed their budget. Protocols charge borrowers a liquidation fee, which is then
awarded to liquidators, who compete to be the first to liquidate borrowers with underwater positions. During market downturn, competition to liquidate
leads to surge in gas fees. Liquidators who can optimize their code can bide more effectively for liquidations.   

**Long-Tail MEV**. 

**Cross-Chain MEV** 

### *Why MEV Matters*

**Def Priority Gas Auction (PGA)**. Searchers and bots compete to have their transactions included included in a particular order by strategically
setting their gas fees. Leads to 
- Network congestions, causing other transactions to get stuck or dropped 
- Spiking and volatility in gas prices, pricing out other crypto users 
- Failed bids that waste block space 
- Arms race between searchers to win latency war, since searcher with lowest latency has advantage in placing the winning bid. 

**Remark.** PGAs occur less frequently on Ethereum, but are still prevalent on high-throughput, low-fee chains like BNB Chain, Polygon side-chain,
Aurora, etc. Would be interesting to see on which chains they occur most frequently, then analyze how the environment of each chain affects PGA
behavior. 

**Decentralization**. MEV is a centralizing influence. There are two cases. 
    1. Builders/Validators can extract MEV: 
    2. Builders/Validators 

**Censorship Resistance**. 

### *Capturing MEV* 

- Validator income = issuance rewards + base transaction fee + MEV/priority fee. Issuance rewards = redistribution of ownership from passive holders
  to stakers. Base transaction fee $\longrightarrow 0$. Validator income in the long run is therefore rooted in MEV. 
- MEV opportunity $\longrightarrow$ blockspace demand 

**Remark**. If the solution to MEV is capturing, internalizing, then redistributing, is it possible to use MEV as a form of UBI? MEV is a consequence
of user and there market activity. As market activity grows and complexifies, so does the total available MEV which can be captured and then
redistributed amongst stakers. This yeilds something like a *zero waste market* in which value which would have been lost is captured and used to
incentivize market activity/growth. 

- MEV internalization examples: Optimism, Aurora, Osmosis, Cosmos 

### *Tradeoffs* 

**Virtual Machine**. The more complex the VM, the more opportunity for MEV. 

**Consensus Mechanism**. 
- Encrypting the mempool seems like one of the more promising solutions to reducing toxic MEV, but how to do it is still up for grabs. One
  possibility is threshold encryption: encrypt transactions when they enter the mempool, share private key with validators, and only decrypt block
  once it is finalized. (Osmosis, Shutter Network)
- Might be able to use trusted hardware instead of cryptography for similar effects (Flashbots)
- Both proposalsintroduce additional latency into the system 
- Single secret leader election for preventing MEV-incentivized DOS attacks 
- Single-slot finality vs medium time to finality vs probabilistic finality 
- Enshrinig proposer-builder separation into the protocol 

**Blockspace Market**. 
- Markets that lack an efficient auction mechanism incentivize transaction spamming the chain. If placing a winning bid is decided on a
  first-come-first serve basis, then searchers will spam validators with transactions to maximize their chances of success. 
- Auction mechanism examples: Transparent batch auction, sealed bid batch auction, transparent batch auction with low fees/low latency, FCFS
  (Arbitrum), transparent batch auction with randomized fair ordering 

**Flashbots MEV Markets**. 
- MEV-geth for PoW 
- MEV-boots for PoS 


### *Open Questions*

1. How does vertical integration (institutions that manage multiple parties in MEV supply chain) affect MEV? Binance-Coinbase (centralized exchange +
   on-chaine operations) for example 
2. Can bridges with multi-chain liquidity capture MEV themselves? 
3. Affect of centralized chains on decentralization of other chains. 
4. Shift to PoS allows multi-block MEV. Now, proposers for next 32 blocks of an epoch are public. What are the possible attack vectors for multi-block
   MEV? How can they be mitigated? 
    - 445K+ active validators, but many are under institutional control. Coinbase controlls 13% of active validators $\longrightarrow \approx 39%$ of 
      proposing $\ge 2$ blocks in a row. **Five consecuitve blocks = control of block production for 1 minute** 
    - Manipulation of TWAP price oracles in order to exploit money market protocols.  
5. Auction mechanisms that mitigate block builder centralization and searchers with exclusive order flow. 

**Terms to Define**: 
- Frontrun 
- Arbitrage 
- Builder
- Validator 
- Long-Tail Strategy  

## [Flash Boys 2.0](https://arxiv.org/pdf/1904.05234.pdf)


## [Blockspace: An Introduction with Chris Dixon](https://www.generalist.com/briefing/blockspace)

**Def Blockspace**. Space on blockchain to store data and run code. 

This compute-space is software rather than hardware subordinate. This means that stronger guarantees can be made about the code being run or the data 
being stored -- namely, that it cannot be arbitrarily manipulated by the hardware owners. This is because the state of the blockchain virtual computer
is determined by consensus (guaranteed by consensus mechnaism). 

**Remark**. The exact properties of blockspace as a unite of compute/storage depends on the blockchain in which it lives. The main considerations here
are: 
1. Security: how trustworthy is the architecture of the underlying blockchain?  
2. Performance: Is it possible to improve efficiency and thus lower transaction fees? 
3. Community: Is there a healthy developer community around the blockchain? 

**Question:** It's unclear from Dixon's explanation how these features of the underlying blockchain impact blockspace. In particular, I am interested
in concretely understanding how the value of blockspace is determined. Clearly, a robust developer community increases blockspace demand, but given
discussions of scalability, it isn't yet clear what determines blockspace supply. 

**Scalability**. There are three primary ways in which blockspace supply can grow: 
1. Layer 2s: L2s (Optimism, Arbitrum, zkSync, Aztec, Starkware) sit on top of the L1 blockchain (Ethereum), inherit their security properties, and
   provide additional blockspace where applications can run with lower gas fees. *Still need to understand the exact relationship between L1 and L2.
   Why are gas costs lower? What allows additional blockspace?*
2. System Design: Solana mentioned, but exact considerations are not given. *Note to look into what Solana does to increase blockspace supply* 
3. More L1s: More L1 blockchains under development, along with bridges that allow interoperability. 

**Remark**. Mentions "gas auction systems that finanicalize blockspace", but only within single blockchains like like Ethereum. If blockspace is truly
a commodity, then it must be possible to bundle (meaningfully, using bridges) blockspace accross different L1s. In this case, what would an auction
system look like? *First, should understand how gas auction systems work on Ethereum and how they financialize blockspace*. 

**Def Induced Demand**. Improved infrastructure $\longrightarrow$ new applications $\longrightarrow$ increased demaned $\longrightarrow$ improved
infrastructure. This feedback loop is common to many computing waves and will likely characterize the rise of blockchains as well. Induced demand
usually means exponential growth. 

**Question**. Dixon makes it clear that at the head of an induced demand boom, it is good to be selling a high-quality product. He gives examples of
mobile phones, personal computers, and broadband in the 1990s and 2000s. He then claims "high quality blockspace" will be such a product in the 2020s,
but it still isn't clear what characterizes "high quality" blockspace. Would be nice to get clarity here. 

## [Consensus Capital Markets](https://openalchemy.substack.com/p/consensus-capital-markets)

**Def Commodity**. Raw material that serve as the basis for production of everyday goods and services. Examples: rice, metals, spices, oil. 

**Blockspace Supply-Demand**. Miners + staking validators supply blockspace and transactions consume blockspace. Increase in on-chain activity
$\longrightarrow$ increase in network fees $\longrightarrow$ increase in value of block subsidy $\longrightarrow$ increased dcompetition to append
next block. 

**Blockspace as a commodity**. Can be used to hedge against production or enhance returns. *This is what is meant by "financialization of blockspace",
but it still isn't clear to me exactly how blockspace is used as the basis for financial instruments. Would be nice to get clarity on exactly what
financial instruments can be built (and how) from blockspace.* 

**Commodity Markets**. 
1. Dojima Rice Exchange (1697): One of the first formal commodity exchanges. Merchants trade "rice tickets", which are claims to rice in their
   warehourse. Rice tickets gave rise to derivative contracts such as short sales, forwards, and options.   
2. Chicago Board of Trade: Becomes global leader in grain/agro futures + options markets. Volume of financial contracts >> volume of physical
   commodities. 
3. P1: "financial abstractions in commodity markets let commodity producers and consumers better manage their risks, and
   therefore allow them to effectively scale their operations". 
4. P2: Robust commodity markets (with diverse financial instruments that help manage risk) stabilize the consumption and production of commodities.
   Stable commodity production is not guaranteed, since it is affected by a wide range of factors. 

**Remark**. Software is "procedural epistomology" -- infinite medium for human expression. Interested in this term from Abelson and Sussman, but also 
in the assumption made here about the volume of the portentially avaialble digital real estate and the potential volume of human content production.  

**Blockspace for the Future**. The thesis that blockspace will become the "most sought-after commodity of the new cryptoeconomic era relies on the
assumption that the metaversal infrastructure will rely heavily on cryptonetworks -- mainly for compute, interoperability, and payments. 

1. The thesis can deconstructed as follows: The metaverse is the future $\longrightarrow$ the infrastructure of the metaverse will rely on
cryptonetworks $\longrightarrow$ the primary cryptoeconomic commodity is blockspace $\longrightarrow$ blockspace will be the primary digital commodity
of the metaversal future. 
2. Blockspace has implicit time value, since only so many transactions can be included in a single block at a time. Excluded transactions have to way.
   Therefore, blockspace in the future is inherently less valuable than blockspace now. Time value has historically been quantified by network fees,
   with block producers defaulting to including transactions with the highest fees.   

**Def Metaverse (from Matthew Ball)** A massively scaled and interoperable network of real-time rendered 3D virtual worlds which can be experienced
synchronously and persistently by an effectively unlimited number of users with an individual sense of presence and with continuity of data, such as
identity, history, entitlements, objects, communications, and payments $\longrightarrow$ users incentivized to pay larger fees for more urgent
transactions $\longrightarrow$ MEV. 

**Remark**. Interesting question raised here about the volatility of node operator rewards. Recall node operator rewards = consensus incentivization -
node operation costs. This is a function of spot price, transaction fees, probability of finding the block, network-specific incentivization
mechanisms. Node operation costs also differ -- PoW (mining hardware, electricity costs) vs PoS (minimal electricity consumption, staking capital).  

**Blockspace-based Financial Instruments**. The nature of blockspace production/consumption indicates a need for blockspace commodity markets to
create financial instruments that isolate and manage underlying risks. *Still unclear exactly what these underlying risks are.*  Simple instruments
already exist today: 
- Hashrate indices:  
- Gas tokens: 
- Staking derivatives:  


**Terms to Define**. 
1. Futures contract: contract to buy/sell something at a predetermined price (**forward price**) for delivery at a specified time (**delivery date**) 
   in the future. 
    - Parties not known when contract is created. 
    - Transacted asset usually a commodity or financial instrument 
    - Example of a "derivative" since value is derived from value of underlying asset 
    - Traded at "futures exchanges" where **buyer = long position holder**, **seller = short position holder**. The buyer and seller are at odds with
      one another, since whomever the price trends against may reneg. If forward price << actual price, the buyer gets a good deal but the seller
      might not want to sell anymore since he is getting shortchanged. If forward price >> actual price, then the buyer might not want to buy anymore,
      since he is overspending. The signal for the actual price is given by the "spot market" where commodities/financial instruments are traded for
      immediate deliver. To prevent parties from reneging, the parties may store some margin of the contract's value with a third party, where the
      margin is determined by the volitility of the spot market. 
    - On the one hand, creates opportunity to hedge against unfavorable events (currency movements for example) prior to delivery date but, on the
      other hand, creates opportunity for speculation since sellers can set futures prices based on predictions regarding assets in order to yield
      profit. 
2. Mortgage 
3. Derivative contracts
4. Short sales
5. Forwards
6. Options
7. Rent extraction 
8. User-owned protocols 
9. On-chain money market 
10. Network fees
11. Spot price 
12. CapEx vs OpEx
13. Network consensus cash flows 
14. Swap contract 
15. Staked asset vs base network asset 
16. Future network fee accrual of asset 
17. Covered calls 

## [Settlement Assurances](https://medium.com/@nic__carter/its-the-settlement-assurances-stupid-5dcd1c3f4e41)



## [LatticeFold](https://eprint.iacr.org/2024/257.pdf)









