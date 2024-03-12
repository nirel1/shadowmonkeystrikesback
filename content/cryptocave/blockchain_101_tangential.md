--- 
title: 101 Tangential Topics
draft: off 
katex: on 
---

## Tangential Topics

### Peer-to-Peer
In order to avoid centralization, Bitcoin uses a peer-to-peer architecture. Unlike in a client-server architecture, nodes in this network act both as a server that can download files and as a client that can process data and message other nodes. This does not mean that the nodes must be identical, but only that there is no hierarchy among them.

### Nodes
In Bitcoin there are three types of nodes: full nodes, mining nodes, and light nodes. While other networks have varying types of nodes, it is common to have roles dedicated to heavy work, light work, and storing history.

#### Full Nodes
Full nodes store the entire blockchain and verify both individual transactions and blocks of transactions.

If a transaction is valid, the full node broadcasts it to other nodes. Once a sufficient number of full nodes agree the transaction is valid, it’s added to a pool of valid transactions.

#### Mining Nodes (Miners)
Miners pick up transactions from this pool and bundle them into blocks. Once a miner believes it has created a valid block, it broadcasts the proposed block back to the full nodes. When the block reaches consensus among full nodes: the block is added to the chain, the block's transactions are processed, and work begins on the next block. 

#### Light Nodes
Light nodes download the block headers from full nodes and permit lightweight devices (like mobile phones) to verify transactions.  

#### Pruning
Pruning refers to traversing the tree of transactions that represent Bitcoin history and removing the children that were visited  least recently. The entire Bitcoin state is hundreds of gigabytes, but pruning can reduce the storage cost of a node down to 2 GB while maintaining a majority of useful information. The only disadvantage here is that pruned nodes are unable to validate the transactions that have been removed.  

Storage costs have prompted many ideas of reducing the size of state and even eliminating the need for nodes to store state:
https://notes.ethereum.org/@vbuterin/verkle_and_state_expiry_proposal

#### Archive Nodes
On Bitcoin, archive nodes and full nodes are equivalent. However, other networks have state expiry where full nodes do not have to store the entire state history, and instead archive nodes take on that responsibility. 

#### Node Centralization
Large Data Centers have commercialized node provision, as it can be difficult and expensive to run your own node, but highly scalable. This warrants centralization concerns, as increasingly concentrated business (Alchemy) run a significant portion of total nodes on select networks.  

## Permissioned vs Permissionless
Bitcoin is designed as a permissionless protocol. Anyone is able to create a wallet and send or receive Bitcoin. Other protocols, like USDC, are permissioned: user wallets can be blacklisted and frozen by Circle. 

## Trilemma
The Blockchain Trilemma describes the tradeoff between scalibility, security, and decentralization in blockchain design. Maximizing any two of these factors will undermine the third. Ethereum's diagram describes each tradeoff in detail:
https://ethereum.org/en/roadmap/vision/

## Throughput vs. Latency
Scalability is often measured by speed, which has two factors. Throughput describes how many transactions can be processed simultaneously. Latency describes how long it takes for a transaction to be processed. For example, a latent system with high throughput could process 100,000 transactions per second, where each transaction takes 5 seconds to process. 

## Forking
### Soft Fork
### Hard Fork

## Bitcoin Stats
Block Time: A block is added on Bitcoin ~ every 10 minutes. 
Block Size: Each block is an average of 3 megabytes and contains an average of 2,500 transactions. The maximum block size is 4 megabytes. Itt used to be 2 megabytes before the controversial SegWit upgrade that resulted in a hard fork. 
https://en.wikipedia.org/wiki/SegWit
Size of Blockchain: As of August 2023, Bitcoin Blockchain size is ~ 500 gigabytes. It is ~ 20% larger than it was last year.
https://ycharts.com/indicators/bitcoin_blockchain_size
Time to Sync: Bitcoin Core requires updating the database with all UTXOs, so time is highly dependent on database access. With sufficient RAM and a download speed of 100 mbps, it takes about 12 hours to sync. 
https://www.doubloin.com/learn/bitcoin-core-sync#:~:text=Bitcoin%20Node%20Average%20Syncing%20Times&text=You%20would%20be%20done%20in,that%20big%20of%20a%20problem.

Number of Bitcoin nodes: ~50,000
https://bitnodes.io/nodes/all/#global-bitcoin-nodes
Number of Bitcoin miners: ~1,000,000

not your keys, not your coins - talk about wallets

NFTs