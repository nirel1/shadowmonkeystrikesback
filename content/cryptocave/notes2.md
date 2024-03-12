--- 
title: notes1
draft: on 
katex: on 
---

Note 2 - more direct economic security

In Bitcoin, the cost to mine a block maps to the cost of electricity. The price of Bitcoin isn’t really correlated to electricity costs, which means that the cost to mine a block has very little to do with the value of that block. 

Ethereum, start with 32 stake and protocol can upgrade (as have been proposed) to adjust in the future

In Ethereum, the cost to attack the network is based on the staking and slashing rates. This is an improvement, because generally, the better that ETH is performing, the more valuable the blocks, and the more valuable the capital that miners have staked. So there is some correlation. However, it’s still not perfect - staking and slashing are fixed in the protocol, and there is a fluctuating delta between the penalty to attack the network and the value in the latest block. This leads to occasions like https://www.coindesk.com/business/2023/04/03/ethereum-mev-bot-gets-attacked-for-20m-as-validator-strikes-back/, 
Where it is profitable for a validator to act dishonestly despite getting slashed. The response is to consider increase the staking limit and slashing rates, but don’t address the root of the problem - the crypto-economic security doesn’t map directly.



In a system where we rely on proofs to collect the value in the block, it is possible to make the cost of proofs variable based on the amount at risk. The proof generated for a valuable zkEVM block should be worth more, and the amount a prover has to stake can be programmably higher. In this world, the two costs collide, meaning we can map risk and reward well, which opens up the design space for more cool stuff like bonding and underwriting. 

Update this idea: not to do with proving, but more to do with parameterizing slashing conditions