--- 
title: "Cheating Single Slot Finality"
katex: true 
draft: true 
--- 

A catchy phrase that gets thrown around is ‘single slot finality’. If you’re not familiar, here are two links ordered by complexity, and an example protocol to go along: 
https://ethereum.org/en/roadmap/single-slot-finality/
https://notes.ethereum.org/@vbuterin/single\_slot\_finality 
https://ethresear.ch/t/a-simple-single-slot-finality-protocol/14920

The idea here being that on Ethereum we want a user’s transaction to be considered final as soon as the slot that their transaction is included in is complete. Each slot is 12 seconds. 32 slots make up an epoch, which is justified after 2/3rds of validators vote correctly on its chain head. An epoch is finalized once the following two epochs have been justified, so finality on Ethereum takes ~15 minutes on average. (https://hackmd.io/@prysmaticlabs/finality). 

I wonder if there are lessons to learn on how we can use information about risk to enable new tech, and I’m reminded of this:

    Add screenshot of instant transfer option vs 1-3 day bank transfer on paypal

You probably see where I’m going. If bank transfers take 1-3 days to complete, and that tech isn’t getting faster anytime soon, a counterparty can step in, underwrite the risk of default, and charge a fee to protect against that risk (although Venmo is a little different, pretend this is a generic expedited bank transfer). We should have that option on Ethereum, and I’ll go so far as to claim that there should be a completely decentralized option - where anyone can step in as a counterparty (probably via a pool). 

Since PoS, there have been very few reorgs of depth >3 (https://etherscan.io/blocks_forked), and one in May of last year of depth 7 that got a lot of attention. So, we can predict the likelihood of reorgs based on their depth, and p;lausibly charge a fee for faster fake finality. Perhaps that cheated finality can be served a couple slots sooner, an entire epoch sooner, or even better by looking at data on attestations. 

You might be thinking: not every counterparty will measure the risks of a reorg the same way, and there are so many risks. We must consider that options change the game theory, where there are new opportunities for arbitrage that might incentivize a greater incidence of reorgs (referred to as MEV reorgs in the first article I link). But this is actually great! Different counterparties can price risk differently, and anyone can participate on either side. They can pool funds as a counterparty and risk that risk is underestimated, causing the pool to get emptied. When transacting, they might choose the cheapest fee for their fast finality, risking that there’s a reorg and the pool is emptied before they get reimbursed. 

Vitalik actually discusses a similar concept for quick settlement of rollup transactions,

Screenshot of: This could be worked around with on-chain security deposits, aka "bonds", at the cost of high capital inefficiency, but such an approach is inherently imperfect because a malicious actor could trick an unlimited number of different people by sacrificing one deposit. https://vitalik.ca/general/2019/12/26/mvb.html

And highlights the challenge of deceptive counterparties. Which brings us to the point of reimbursal: perhaps we authorize the counterparty to spend from a wallet up front, or there’s some sort of contract that can automate reimbursal on the occasion of a reorg. This same point is true for settling rollup transactions. If there is a provable way to script the reimbursement, we can decentralize this process.

The first question should be: how do we make fee predictions from data in a verifiable way? If the system is decentralized no one should be able to change how data is interpreted / risk is predicted / fees are calculated. I think that all public, predictive, measurable data exists between Ethereum’s consensus client in attestations and the execution client where epochs are published. With each slot, the model should be making a prediction about how likely that set of transactions in the slot is to be finalized. This probably involves some sort of SNARKs. In fact, I imagine an army of provers constantly generating proofs for all sorts of computation about risk, feeding on-chain in order to trigger/inform smart contract actions. Initially, we’d probably start only with transfers, where we could pay a fee for faster finality, and the counterparty would send funds directly to the recipient, assuming that the slot containing the transaction would eventually be finalized. This could evolve to support something like a DEX, where the target asset for a trade is sent immediately, and the counterparty gains ownership of the trade if/when it completes. 
