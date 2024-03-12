--- 
title: notes1
draft: on 
katex: on 
---

Note 1 - EVM

Trust + stickiness

Why the EVM sticks

In blockchains people talk a lot about trust, and especially about minimizing trust. Truthfully, trust can only migrate, and it is a subjective measure. Many of us in the space happen to believe that humans are often the least trustworthy part of a system, and by minimizing their involvement we maximize the trustworthiness of the system (all other things equal).  

This is all well and good for a system like Bitcoin - there’s no clear authority and the community is allergic to most upgrades. But, out of simplicity evolves complexity, and complexity needs upgrades. New data structures, programs, virtual machines, consensus mechanisms - they can all be buggy. And when a system is financialized, these bugs lead to exploits. After you’ve seen these systems get hacked, you’ll actually start to trust them more when they have the proper fallback mechanisms, which almost always require human involvement. 

Trust in Ethereum seems to be two-fold: it is trust in the battle-tested, careful to change system (EVM and recently, PoS), and trust in Ethereum’s brand, community, and vision. I’ve found from asking around that the majority of people (in my small sample) believe that if there were to be another large exploit, Ethereum would fork again to protect the majority of its users. 

Trust points to why the EVM has become so prominent. It is the most trusted way to build and use decentralized applications. Entire businesses have emerged out of optimizing the gas costs, studying each opcode, and writing in assembly for this VM. So too with Solidity tooling. And so, despite many other competing consensus mechanisms, VMs, and designs for blockchains emerging, both developers and users have continued to choose Ethereum more than any other chain. 

But, Ethereum is changing. It was once a vision of executing smart contract logic, distributed across many miners. A rollup-centric future points to a world where Ethereum is the base layer for other decentralized and permissionless systems to build atop. 

That means the purposes that EVM serves must change, right?

In my opinion, kinda. 

I think there is a certain set of EVM users (perhaps institutions, large applications) that will always rely on the EVM for its initial purpose: to execute smart contracts. These users will not want to venture beyond the boundaries of smart contract risk. The EVM is tried and tested, and operating within its bounds will always pose less risk than operating both inside and outside its bounds. 

On the other hand, the vision seems to be that a growing set of users will rely on Ethereum (and the EVM) for operations that provide guarantees for stuff outside of Ethereum. Two examples of these future operations are precompiles for KZG commitments and precompiles for new(ish) elliptic curves.  

Precompiles for KZG commitments will make it cheaper to use Ethereum for data availability (DA). 
Precompiles for elliptic curves will make it cheaper to verify SNARKS and ZK-SNARKs on-chain. 

In PBS, block builders are appointed to perform t

For proving, it’s unclear who does that work


This is especially useful for rollups, which rely on Ethereum to have data temporarily available to guarantee that 



I would argue that in the long term, more complexity evolves around these features, and many smart contracts will emerge that get very good at providing guarantees for stuff off-chain. 













Each of these is an addition to the EVM that 

, where rollups and potentially other applications can store commitments to data at a much lower cost. 

Both will likely become common operations .

provide economic security to 

And restaking, which I won’t get into here. 

two key features will become increasingly important in the EVM: data availability and proving. 

Rollups



The EVM will become particularly useful for verifying off-chain computation, because it is inherently cheaper to verify than it is to re-run computation across a network of 1M+ validators. This might take some time, especially as bugs in proving off-chain computation emerge and we experience many exploits. Eventually, though, the tradeoffs will evidence that for most applications, it will make more sense to compute off-chain and verify on-chain. At early onset, this is why zkEVMs make sense. They can port the computation environment that applications and builders are familiar with, so that all it takes (hopefully) is redeploying up the stack, and ta-da! Your application is much cheaper, but still settles to Ethereum - through verification of a proof of the execution of transactions on that application along with all the others in a rollup. But, I think zkEVM rollups make less sense for some of these applications. Rollups bundle verification of proofs altogether, so if the rollup defaults, all its applications break. This will probably happen to at least one, if not multiple rollups - what I mean is there will be some transaction that is bundled into a proof and verified on chain when it in fact shouldn’t be, and the rollup might become undercollateralized. Also, a rollup fragments an application’s identity (this might not always be the case), as they likely associate with the complete decentralization of Ethereum and don’t want to become a rollup’s kiddie project. 



This begs the question: if a lot of trust is due to the engineering soundness of the EVM, where does that trust go when Ethereum serves different functions?

Part 2: proofs

Migrate to trusting da, circuits, 
