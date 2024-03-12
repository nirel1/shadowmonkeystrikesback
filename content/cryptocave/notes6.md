--- 
title: notes6
draft: on 
katex: on 
---

Note 6 - Off-chain incentivization (with crypto economic security)

It seems that incentivizing off-chain activity has been a topic of discussion. Eigenlayer brought more attention to the value of crypto economic security, building a framework for others to design slashing conditions. Cowswap was able to design a mechanism where solvers operate from an off-chain orderbook to match ‘coincidence of wants’ that relies on slashing, so that solvers stake and they can be economically enforced to act correctly. However, one criticism of Ethereum’s merge (tim from risc0) has been that there are less constraints - in the PoW model, the rules of Ethereum were enforced such that a block had to contain valid smart contracts. However, after the merge, these rules are now arbitrary - a ⅔ majority of validators could vote on a different state of the chain. As such, the security of cowswap is also limited - solvers can act maliciously, but they’ll be slashed. 

By adding a constraint, these systems can be more effective - especially for off-chain computation. On Cowswap, the computation that solvers perform can be verified. Given a specific set of orders, they should be matched according to a specific algorithm. This way, the worst that a solver can do is stall instead of providing the result of its computation along with proof that the computation was done correctly. Another thing to investigate is how multiple solvers are rewarded in cowswap. 

Flashbots looked into this, but chose TEE computation for now because privacy is important for their computations in SUAVE, and because distributing zk proofs is currently too slow. In the future what we’re building will likely be of interest to them.  



More notes

What is blockspace
Opportunity to have computation work done on many machines
Markets emerge

Can stake for this opportunity

Rollups are just off chain computation until sufficiently decentralized

Some applications on ethereum won’t migrate to rollups because it’s not in line with their ethos
