--- 
title: Blockchain 101
draft: off 
katex: on 
---

## Problem
I want to send money over the internet but I don't trust financial intermediaries. 

## Solution
Instead of giving a financial intermediary control over the recordbook, distribute the recordbook across a network of participants.

## Naive Approach
How does one distribute a recordbook across a network of participants?
<br>
<br>
Well, not unlike the internet itself, we can create a network of nodes (participants) that can transmit messages to one another. Each participant in the network can can store its own version of the recordbook. When the system first starts (genesis), all participants in the network will have an empty recordbook. When a particpant wants to add a record, they add it to their local version. Then, they can broadcast it to other participants, and once a sufficient number of participants agree on the new record, it is considered the latest addition to the correct recordbook. 

You might be asking: 
- How do we determine the correct recordbook?
- What if the participant or record is malicious? 
- What if other participants' machines go down? 
- What is the sufficient number of participants for agreement? 
- So on and so forth

Here lie some of the many challenges of distributed consensus. 

## Distributed Consensus
This problem is formally addressed in 1972 in a research paper titled 'The Byzantine Generals Problem': 
>*Several divisions of the Byzantine army are camped outside an enemy city, each division commanded by its own general. The generals can communicate with one another only by messenger. After observing the enemy, they must decide upon a common plan of action. However, some of the generals may be traitors, trying to prevent the loyal generals from reaching agreement. The generals must be able to guarantee that:*
 >- All honest generals decide on the same plan of action
 >- A small number of traitors cannot cause the honest generals to adopt a malicious plan
 ><br>
 ><br>
 >![byzantine](/byzantine.png "Byzantine Generals Problem")
 ><br>
 ><br>
 >[Original Research Paper](https://www.microsoft.com/en-us/research/uploads/prod/2016/12/The-Byzantine-Generals-Problem.pdf)

In this paper, we are prescribed a set of algorithms that relay unforgeable, signed messages between parties until a threshold is met to reach agreement. Lamport’s paper forecasts many of the challenges with transmitting messages in a distributed network of nodes. include leader election, mention oversimplification

The summary above is oversimplified, and Elaine Shi covers everything to know of Byzantine Broadcast, Distributed Consensus, and how they relate to blockchains here:
<br>
[Foundations of Distributed Consensus and Blockchains](http://elaineshi.com/docs/blockchain-book.pdf)

## Byzantine Fault Tolerance (BFT)
In computer systems, ‘[Byzantine Fault Tolerance](https://en.wikipedia.org/wiki/Byzantine_fault)’ refers to the resiliency of a system with unreliable components - like unloyal generals. To stay secure, the distributed recordbook needs a BFT Consensus mechanism so that honest participants in the network can reach agreement in spite of attacks from dishonest participants. A consensus mechanism refers to a collection of protocols that ensure participants reach agreement, which can include incentivization, punishment, and random selection. More on this in the next article. (link)

## Bitcoin
In 2008, a BFT consensus mechanism was applied to financial transactions in the [Bitcoin whitepaper](https://bitcoin.org/bitcoin.pdf). The paper invents a record keeping system that is resilient against traitors who would insert false records. Bitcoin uses a ledger, also known as a blockchain, to record transactions between accounts. Using Bitcoin, participants can transact without relying on a financial institution. 

### Append-Only Ledger
The recordbook we refer to above is formalized in Bitcoin as an append-only public ledger. Once a record is added to the ledger, it cannot be removed - this protects transactions from change or reversal once they are finalized. 

### Blocks as Records
However, it is time-intensive for nodes in a network to reach agreement on adding a record to the ledger. 
Rather than agreeing on one transaction at a time, many transactions are bundled into a record (block). After nodes reach agreement on a block, it is linked to the chain of previously approved blocks (ledger), thus extending a 'blockchain'.

![hashing2](/hashing2.png "Chaining Blocks") Credit voynich

### Block Headers
The image above depicts headers at the top of each block. Each header is an 80-byte chunk of data summarizing its respective block, which is allows nodes with less storage capacity (light nodes, link) to keep up with the network. Each header contains:

- A hash of the previous header
- A timestamp
- A mining difficulty value
- A proof of work nonce
- A root hash for the Merkle tree containing the transactions for that block.

The mining difficulty value and proof of work nonce will make more sense after reading the next article. 

### Merkling

In order to efficiently bundle transactions into a block header, Bitcoin uses a data structure called a 'Merkle Tree'. 

>*A Merkle tree, in the most general sense, is a way of hashing a large number of "chunks" of data together which relies on splitting the chunks into buckets, where each bucket contains only a few chunks, then taking the hash of each bucket and repeating the same process, continuing to do so until the total number of hashes remaining becomes only one: the root hash.*
><br>
><br>
>The root hash provides a simple way for light nodes to verify that a transaction is contained inside of a block - by requesting a merkle proof. This method is known as Simplified Payment Verification (SPV).
><br>
><br>
>![merkling](/merkling.jpeg "Merkling")
>Vitalik's elaboration here: https://blog.ethereum.org/2015/11/15/merkling-in-ethereum

### State
A system is described as stateful if it is configured to remember preceding events or user interactions. In Bitcoin, state transitions occur when a block is added to the chain, and many account balances are updated. * collection of many state transitions This is where the term 'globally replicated state machine' comes from: consensus on the entire state of the blockchain and validity of all of its transactions is distributed to thousands of nodes across the world that continually connect and disconnect from the network. This logic will be explored in the third article.  

### Unspent Transaction Output Model vs. Account Model 
There are different ways that the state of all accounts and balances can be stored. Bitcoin uses the Unspent Transaction Output (UTXO) model, where the entire graph of transaction outputs, spent and unspent, represents the global state. In the account model, only the current set of accounts and their balances represents the global state.

![utxo](/utxo.jpeg "UTXO")

https://www.horizen.io/academy/utxo-vs-account-model/

### Blockchain Protocol Guarantees
#### Consistency
Consistency requires that all
nodes have the same view of the linearly ordered log — but since their
network speeds may differ, we shall allow some nodes’ logs to potentially
grow a little faster than others.

#### Liveness
Liveness requires that if some honest node receives some
transaction tx in some round r, then tx will appear in every honest node’s
“finalized log” by the end of round r + Tconf where Tconf is often called the
“confirmation time”.

#### Immutability
Immutability requires that once data is final, it is permanent and cannot be changed or removed. 

#### Censorship Resistance
Censorship resistance requires that a minority of nodes cannot censor users or their transactions. 

## Summary
Using a blockchain like Bitcoin, we can send money over the internet by trusting nodes in a distributed network instead of a financial intermediary.