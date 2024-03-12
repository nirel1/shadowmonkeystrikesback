--- 
title: Blockchain 102 (Consensus)
draft: off 
katex: on 
---

## Problem
I want to send money over the internet using a distributed network but I don't trust malicious nodes.

## Solution
Combine consensus protocols to create a Byzantine Fault Tolerant consensus mechanism. 

## Consensus
can probably delete this paragraph
In order to add to the ledger, transactions undergo a process to check that they’re legitimate. But, it’d be inefficient to try to process every transaction one-by-one; instead, the transactions are bundled together into blocks. Each block goes through the process before being added to the chain of all previous blocks. This process is known as a consensus mechanism, and these processes must have byzantine fault tolerance to be secure.
[Consensus Mechanisms](https://ethereum.org/en/developers/docs/consensus-mechanisms/)

### Nakamoto Consensus
In Bitcoin, Nakamoto Consensus combines consensus protcols in order to incentivize nodes to act honestly.
https://bitcoinmagazine.com/guides/what-is-nakamoto-consensus-bitcoin

#### Proof of Work
In Proof of Work (PoW), miners compete to solve complex cryptographic puzzles in order to add a new block to the blockchain ([hashing](https://medium.com/certik/how-bitcoin-works-hashing-e897157f7940)). Solving the puzzle relies on incrementing a nonce (arbitrary number) in the block until the correct value that represents the block’s hash and required zero bits for the beginning of the nonce is reached. 

The difficulty of these puzzles adjusts to ensure that the time taken to solve them remains approximately constant, thereby securing a steady addition of new blocks. These puzzles are also stochastic, meaning there is no way to forecast which miner will crack a given puzzle. This replaces the need for the leader election required in other protocols like Proof of Stake (PoS). 

The more computational (hashing) power that a miner has dedicated to the network, the more likely that they are to crack the puzzle. A miner proves that they have provided computational power by providing a solution to the puzzle, and because electricity is a real cost, a malicious miner will have to pay to play. 

Once the puzzle is solved and a miner proposes a block, the network validates the block (checking that no transactions are double-spent). Successful miners are rewarded with new bitcoin and transaction fees, providing an economic incentive for maintaining the integrity and security of the network. Watch this video for more detail: [But How Does Bitcoin Actually Work?](https://www.youtube.com/watch?v=bBC-nXj3Ng4&vl=en)

#### Longest Chain Rule
In Nakamoto Consensus, the longest chain is considered the canoncial (valid) chain because it has had the largest amount of computational power dedicated. This allows new nodes to accept the longest chain as proof of Bitcoin's state history and circumvents the need for a central authority to keep track of the valid chain. 

#### Attacks
51% of the miners are required to force a malicious block, continue to produce new blocks after it, and attack the network. Due to the Bitcoin network’s current size, the economic cost of accruing over 51% of the hashing power is extremely high.

#### Finality
In Bitcoin the validity of blocks is always probablistic. Even in the longest chain, there is no guarantee that the most recent block is valid. There is always a small chance that another chain is the canonical one, and it will eventually outgrow what is the longest chain at (assuming the majority of nodes are still honest). When the longest chain changes to a new longest chain, this is known as a reorganization (reorg). Reorgs happen less than twice a year. https://learnmeabitcoin.com/technical/chain-reorganisation

However, as a block gets buried by new blocks it is increasingly unlikely that it is part of an incorrect longest chain. As a rule of thumb, most of the industry follows a 6 block maturation, meaning a block is considered final after 5 blocks have been added after it.

### Ethereum Consensus
In Ethereum (a blockchain launched in 2015) the consensus mechanism consists of Proof of Stake (PoS), Random Leader Election, and a Fork Choice Rule. Ethereum used to rely on PoW consensus but switched to PoS in September 2022 in an event known as 'The Merge'. 
https://ethereum.org/en/roadmap/merge/
https://ethereum.org/en/developers/docs/consensus-mechanisms/

#### Proof of Stake
Ethereum's Proof of Stake (PoS) is a consensus mechanism where validators (like miners) are selected to propose and vote on blocks of transactions, based on the amount of ETH (token native to Ethereum) they willingly 'stake' as collateral to earn rewards. The selection process is probabilistic, with higher-staked nodes having a higher chance of being chosen. The staked ETH then acts as collateral that can be destroyed if the validator behaves dishonestly or lazily.

#### Random Leader Election
In Ethereum, time is divided up into twelve second units called 'slots'. In each slot a single validator is selected to propose a block. In order to protect the network, the validator for each slot is chosen pseudo-randomly using a protocol called RANDAO. 
https://eth2book.info/capella/part2/building_blocks/randomness/

#### Fork Choice Rule
When a validator must choose between two seemingly correct blocks at the head of a chain, they rely on an algorithm that favors the fork with the most attestations (votes in favor from other validators).
https://ethereum.org/en/developers/docs/consensus-mechanisms/pos/#fork-choice

#### Attacks
⅔ of the validators must vote to approve a block. Still a 51% attack.
https://ethereum.org/en/developers/docs/consensus-mechanisms/pos/#pos-and-security

#### Finality
The first block in each epoch is a checkpoint. Validators vote for pairs of checkpoints that it considers to be valid. If a pair of checkpoints attracts votes representing at least two-thirds of the total staked ETH, the checkpoints are upgraded.
https://ethereum.org/en/developers/docs/consensus-mechanisms/pos/#finality

#### Delegated Proof of Stake
Remember BFT? Practical Byzantine Fault Tolerance (pBFT) is a variant of BFT consensus, where there is a limited membership list of nodes that are elected as leaders. This variant takes advantage of the tradeoff between decentralization and scalability in the trilemma - by limiting the number of nodes that the network decentralizes voting across, communication between nodes is reduced and the network is less latent. Delegated proof of stake takes advantage of a similar function, whereby stakers delegate their stake to a limited membership list that validate on their behalf.
https://academy.binance.com/en/articles/delegated-proof-of-stake-explained

### Proof of Authority
Proof of Authority (PoA) is a reputation-based consensus algorithm that leverages the value of identities. Block validators stake their reputations instead of their money. Therefore, PoA blockchains are secured by the validating nodes that are arbitrarily selected as trustworthy entities.
https://academy.binance.com/en/articles/proof-of-authority-explained

### Proof of History
Proof of History is a sequence of computation that can provide a way to cryptographically verify passage of time between two events. Solana (a blockchain launched in 2020) uses Proof of History to prove that transactions are added to a block at specific points in time. Ultimately, this allows nodes to verify transactions in parallel. 
https://tokens-economy.gitbook.io/consensus/chain-based-proof-of-capacity-space/proof-of-history

## Proof of Storage 

### Proof of Replication 

### Proof of Spacetime
Filecoin is a decentralized and permissionless storage provider. It functions similarly to DropBox, but the idea is that any node can participate in the network by providing storage space, such that Filecoin can never delete a user's data. Proof of Spacetime is a way that nodes in the network prove that they are continuously providing storage space in order to be rewarded. 
https://spec.filecoin.io/algorithms/pos/post/

Why is this important?
Dunbar's number

## Summary
Using a blockchain coupled with a robust consensus mechanism, we can send money over the internet without trusting malicious nodes. 

Now we've discussed the different data structures, consensus mechanisms, tradeoffs between scalability, security, and decentralization, and variance in storage size, latency, and throughput. As you might imagine, many different blockchains have emerged with their own native token, each weighing these tradeoffs uniquely. 
