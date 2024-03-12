--- 
title: Blockchain 108 (Rollups)
draft: off 
katex: on 
---

## Problem
Gas is expensive on Ethereum. 
or
I want more control over my application but I still want to rely on Ethereum security. 

## Solution
Rollups - very unfinished

## Context
Rollups are a clever workaround to circumvent the high gas costs of transacting on Ethereum. By compressing many transactions into calldata, a rollup can effectively run hundreds of transactions on Ethereum for the price of one. To do this, however, requires another layer (a Layer 2) where these transactions are derived to. Another way to think about an L2 is as a translator for what’s happening on its base layer. In order to maintain the canonical history of the rollup, the base layer is relied upon as a data availability layer. Users can send transactions to a rollup, experience fast speed and low costs, and every couple of hours, the rollup will compress all the most recent transactions and post them on the base layer, where they are considered final. The user experiences a soft confirmation that is almost instantaneous, and hard confirmation when they can see their transaction published on Ethereum. 

Rollups either have their own set of validators (operators) that batch transactions, or run a sequencer. With a sequencer, the rollup is in charge of ordering transactions before they are published, giving them the power to front run and manipulate users. The tradeoff here is increased scalability bears centralization. There are many efforts to decentralize sequencing, either by sharing sequencing as a service among multiple rollups, or by voting [20]. The other risk is censorship - rollups can choose to exclude specific user transactions and prevent them from participating. This is combatted with forced inclusion, where a smart contract is published on the base layer that any user can interact with to ‘force’ their transaction - for a predictably higher gas cost. Despite these tradeoffs, rollups are a useful technology to scale transactions and improve experience for users. However, rollups take on increased risk.

Successful rollups experience huge volumes of user transactions to their operator/sequencer. The rollup is responsible for implementing the logic that batches and compresses these transactions to post as calldata, and the logic to interpret that calldata later. Furthermore, should the rollup use a validator model, anyone is able to run an operator and propose batches. Should any of the derivation logic be flawed, or an operator attempts to include a malicious transaction, the rollup is exposed to financial risk whereby an attacker could manipulate the state of the chain and run away with funds. For example, if an operator were to find a bug where they could include an invalid transaction to mint the rollup token, they could add this transaction to a batch, and as soon as the transaction reached finality on the base layer, they would be able to withdraw their minted tokens, leading to an undercollateralized market for other participants and huge systemic risk. To combat this risk, rollups generally take two approaches to validate transactions. 

The first approach is known as optimistic proving: because the history of the chain is public and published in calldata on Ethereum, anyone can run a validator to replay the history of state transitions for the rollup. If any differences emerge between the state recorded on Ethereum and that of the rollup, one can submit a fraud proof of these differences, and the malicious operator will be slashed. In order for this to work, there is a withdrawal period (aka dispute resolution period) that users must wait before withdrawing funds from the rollup. This method is considered optimistic because it relies on the assumption that there exists one honest and attentive node that would submit a fault proof. 

