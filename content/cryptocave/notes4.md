--- 
title: notes4
draft: on 
katex: on 
---

Note 4 - Shared Sequencers

At SBC this year, there was a lot of interesting discussion about shared sequencers. Because the idea of rollups is relatively untested, there are still a lot of experimental formats for attempting to decentralize rollups such that they resemble Ethereum. On Ethereum, anyone can post a transaction request to the public mempool - this results in communication overhead to network this mempool of pending transaction requests to one another. While it introduces latency, it also provides the guarantees that anyone can operate on Ethereum. On rollups, however, most designs have started with a single sequencer, meaning the rollup operator runs a server that collects and orders transaction requests. To affirm censorship resistance, there are deployed contracts that allow one to ‘force’ transactions by transacting on Ethereum. While they’re better than nothing, they still don’t provide the same guarantees that users will need in the future, making shared sequencers a hot topic of discussion. 

This is a little too explanatory, and it should be more about expressing ideas than explainers. 

One solution that a couple of teams have been working on is shared sequencing. It provides a collaborative way for rollups to decentralize sequencing and protect their users. I don’t think it’ll succeed with rollups that have already deployed, because rollups inherently capture value through sequencing. Unlike Ethereum and other L1s that capture value (to redistribute to validators) through gas fees, L2s compete on low gas fees and tend to collect in ETH. So, shared sequencing might work for RaaS’s, where rollups are focused on deploying quickly and operate more like cloud businesses, but for fully decentralized rollups on Ethereum, they will likely design their own decentralization mechanisms for sequencing. 

idea: why shared sequencing might not work, and why the same logic does/doesn't apply for proving