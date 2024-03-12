--- 
title: "Revisiting Rollup Centrism"
katex: true 
draft: true 
--- 

## Introduction

It’s been 3 years since Vitalik’s post on [A rollup-centric Ethereum roadmap](https://ethereum-magicians.org/t/a-rollup-centric-ethereum-roadmap/4698). In it, he described the long-term future for eth2 as: *a single high-security execution shard that everyone processes, plus a scalable data availability layer*. This roadmap laid out an evolution of functionality from Ethereum as a platform for smart contracts ([Prehistory](https://vitalik.ca/general/2017/09/14/prehistory.html)) to a base layer that would scale blockchains for the next billion users. It was a great culmination of his thinking on base layers from a year prior ([Base Layers and Functional Escape Velocity](https://vitalik.ca/general/2019/12/26/mvb.html)), which extended ideas about the roles of layer 1s and layer 2s another year earlier ([Layer 1s should be innovative in the short term but less in the long term](https://vitalik.ca/general/2018/08/26/layer_1.html)). To understand this envisioned future, it’s important to read the first, third, and fourth links above. 

## Thesis

The general belief about the long-term future was that users and applications would live on rollups, the EVM would live on rollups, and Ethereum would specialize in consensus (high-security) and data availability. Since the time of Vitalik’s writing we’ve gotten to observe the first cohort of rollups launch, narratives evolve (RaaS, shared sequencing, cross-rollup communication, and proving), and user/application preferences emerge. It seems likely to me that in the long-term users and applications will originate on Ethereum, the EVM will live on Ethereum, and Ethereum will have a dual identity (preserving execution and consensus, while improving DA). What gives me this belief?

- Rollups are straying from EVM standardization
- Trust doesn’t scale
- Smart contracts are sticky

By the way, all of this only matters in a world of [contract completeness](https://jessewalden.com/incomplete-contracts-and-scaling-crypto/), where systems minimize the need for human interpretation or external decision-making. Otherwise, a PoA bridge will do perfectly well, as Haseeb points out in ‘[I’m worried nobody will care about rollups](https://medium.com/dragonfly-research/im-worried-nobody-will-care-about-rollups-554bc743d4f1)’. 

### On EVM Standardization

Many would say that EVM standardization is succeeding. There are more than 100 EVM chains. The EVM is beloved, and there are entire companies built around optimizing gas fees for this VM (s/o Gaslite). As the first blockchain VM, it is the most tried, trusted, and tooling-compatible ([Immutable Ground Up Guide](https://www.immutable.com/blog/ground-up-guide-zkevm-evm-compatibility-rollups)). 

To me, an EVM chain without Ethereum’s community, leadership, and decentralization is immaterial. Yes, it’s convenient to be highly compatible with existing tools, and you can be pretty confident that code will execute as expected - but, is there a significant difference in code security from using the cosmos-sdk? Ethereum stands out for its economic security, as a global consensus layer that is irreplaceable. Therefore, the EVM matters most on eth2 and (maybe) on the protocols that sought out to increase blockspace for Ethereum. 

In the context of rollups, EVM standardization is failing. One of the short-term goals in that roadmap is: “More explicitly standardize on Yul or something similar as an intermediate compiling language”. This point is vital, because these standards are what can guide rollups on how they execute smart contracts, how they upgrade, and how they might interoperate. Without these standards, users are taking a gamble on each rollup based on how they choose to process EVM-ish instructions.

Unfortunately, it seems that most rollups fell short of this goal. Many made modifications to the EVM, and built their own frameworks to have their own Ethereum vision of interoperable rollups, but only on their stack. As time goes on, these changes will likely diverge more and more from a single standard. This is pertinent for both optimistic rollups and [the different types of zk-EVMs](https://vitalik.ca/general/2022/08/04/zkevm.html). 

In a type 1 zkEVM, we get the best guarantees that a rollup has executed its state transition function by the intended design. It is also the most expensive, time exhaustive, least flexible (same gas costs, state tree, hash functions, precompiles, etc.), and least scalable design, requiring a team to hand-write circuits that mimic the EVM. As we inch across the x-axis, most every modification opens a box of worms for new vulnerabilities, because the only guarantee a validity rollup gets from Ethereum security is that the proof of execution is valid. We are left to believe that the proof is generated with a system that considers every possible constraint, lest it is not proving what we think it is. 

With all these factors, I’m left to think that a validity rollup is best served by a type 1 zkEVM, or a different execution engine altogether. If the choice is a type 1 zkEVM, it begs the question: what about danksharding and the other planned upgrades to Ethereum? Do we have to upgrade the circuit or let it become outdated? 

In fact, Vitalik hints at this conflict all that time ago in the [Layer 1s](https://vitalik.ca/general/2018/08/26/layer_1.html) article from above. It is paradoxical - how can layer 2 execution engines both track the EVM standard and be designed in different shapes and sizes? At some point, many rollups will have modified the EVM enough that it makes more sense to operate in any other VM environment - we get similar security guarantees, and significantly lower cost, less time, higher flexibility, and better scaling. 

In the long-term, I believe smart contract development will stray from the EVM (whether or not rollups win). There will be less good reasons for devs to be writing in Yul or fidgeting with integer sizes. We will have frameworks to write smart contracts in Solidity, Javascript, Rust, Go, Move, and many other languages, where the compiler is completely abstracted from the developer. After all, this is largely the devX that’s evolved from building internet applications. It’s all possible when tens of thousands of consensus-critical EVM execution code collapse to a few hundred lines of SNARK verification code. The key to scaling Ethereum lies in the succinctness (S) of SNARKs, not the EVM.

### On Trust

It’s not possible to trust execution on a rollup the way we do on Ethereum. This is how I interpret ‘extending blockspace’ - if the guarantees are significantly changed, it’s not Ethereum anymore. Anytime you hear the term ‘trustless’, think ‘risk-free rates’ (Toghrul is rightfully strict about using the term trust-minimized).

Security has been a massive pain point for rollups, and a point of contention for a community that sets high expectations on decentralization (ex: sequencing). However, most of this discussion revolves around economic security - the cost to corrupt the sequencer(s) or prover(s). Aside from the liveness and censorship resistance risks, there is a huge correctness risk to how proving is designed. 

By ‘proving’ I’m referring to the mechanism that a rollup uses to check that posted data matches execution, whether it be with fault proofs (that anyone can submit to initiate a dispute) or validity proofs (that are verified autonomously by a contract on Ethereum). 

As Tarun has pointed out, an optimistic rollup fork is uncharted territory. If one were to prove faulty execution and the rollup were to halt, it is not clear how operations would resume, nor whether executed but unfinalized transactions would be fulfilled or abandoned. If the rollup is designed to resume based on its own interpretation of state, it can hardly be considered Ethereum dependent.

In order to trust validity proofs, we need to know that proof systems are sound, circuits are well-constrained, and verifiers are bug-free. However, there are no ways to guarantee these properties, just like there are no ways to guarantee that smart contracts do what they say. Audits provide better certainty, but there are always risks. As time goes on, quality of audits, security tooling, and even formal verification can all provide better certainty, but in a validity rollup we are always introducing some level of trust to these factors. 

Bugs in these environments will be victim to many exploits and hacks like we’ve seen in the past, and TVL on rollups is already shaping up to fund generous bounties. It will be many years before rollups approach the level of trust and decentralization that Ethereum has today. Despite the philosophy in [Base Layers…](https://vitalik.ca/general/2019/12/26/mvb.html), the site of ongoing innovation comes at the cost of trustworthiness (if we trust the [code is law](https://www.harvardmagazine.com/2000/01/code-is-law-html) ‘regulators’ more than the human regulators). 

In fact, this term ‘layers’ is misleading. When I think of the components of a decentralized system, I think of an application that dedicates trust to IPFS, The Graph, Chainlink (wearily), a frontend provider, and Ethereum’s validators. I don’t think of an application that sits in a cloud of shared validiums which all settle to a single validium that settles to Ethereum. Web3 ‘layers’ sit in stark contrast to the elements of the frontend, backend, and/or the database layer in Web2.

Whether we execute contracts with a sequencer that publishes data to Ethereum to get voted on, or whether the execution is voted on directly, feels more like an implementation detail. Maybe the real layers in Web3 are applications, not rollups (s/o [David’s proto-app thesis](https://davidphelps.substack.com/p/the-proto-app-thesis)). 

Not to mention, the fact that we can verify the execution of arbitrary code on an untrusted device completely changes the dynamics of blockchains. In this world, less stuff needs to be published on a layer at all to give the satisfaction that a system can’t be corrupted by a minority of participants (using ‘minority’ loosely here). 

### On Contract Stickiness

In other short-term goals for rollup infrastructure, Vitalik points out that we’d need to adapt to a world where users have their primary accounts, balances, assets, etc. entirely inside an L2. One key change is the ability for users to register and transfer their ENS names to L2s. 

This was the beginning of a string of discussions and proposals for ENS on how to do this, which has led to a clever off-chain resolver that allows ENS names to be bridged to an L2 and managed there. Nonetheless, what hasn’t changed is that ENS names must ultimately be read from the mainnet contract. While new subdomains can exist for L2s, the canonical truth persists on Ethereum. 

A counter-example of Ethereum’s first-mover advantage is account abstraction, which has centered around rollups ([Six Degree AA Report](https://sixdegree.xyz/research/Half-Year-Data-Report-of-ERC4337-by-Sixdegree.pdf)). If the nature of account management is at the cross-section of security and convenience, I’m tempted to think that breakthroughs in account logic/UX will also settle to Ethereum.

In the roadmap, Vitalik concedes:

- "users and applications still need it [the base layer] to eg. move between rollups, submit fraud proofs, submit ZK proofs in ZK rollups, publish root ERC20 token contracts (sure, most users will live in rollups, but the base contract has to live somewhere…), etc."

However, I think these base contracts extend to a lot more - they include accounts, ENS, governance, treasuries, and many other pieces of fundamental logic for decentralized systems. As time goes on, the contracts that have already been deployed to mainnet will have more dependencies. They will be composed across applications, manage more users, and secure more capital. To duplicate these contracts on rollups will surely happen, but to migrate where DAOs, funds, and accounts live? Hm.

Ethereum’s ability to execute the EVM will be increasingly important as time goes on. The more dependencies, the more core stuff, the more difficult it is to ever move away from execution on Ethereum. The more it makes sense for Ethereum to be where users, applications, protocols, and rollups all establish and communicate with one another.  

## Conclusion

Rollups are a foreshadow of decentralized systems of the future. They incorporate innovative ways to scale Ethereum, and (hopefully) extend blockspace. 

But, they certainly aren’t the end state. 

Decentralized system architecture is something that spans across different platforms, with some stuff on-chain and some stuff off-chain, as there are different tradeoffs for each piece of an application.

I expect the EVM will continue to be incredibly powerful, and persist as a global standard - on Ethereum. 

Danksharding will help pave the way for a new era of blockchain applications that weren’t possible before. Between cheaper space to post cryptographic proofs, and a precompile that will make it cheaper to verify statements about those proofs ([Danksharding Precompiles](https://notes.ethereum.org/@vbuterin/proto_danksharding_faq#What-are-the-two-precompiles-introduced-in-proto-danksharding)), we are venturing into a new design space where the limitations of blockspace can be reconciled with off-chain work that can be made expressive, reasoned about, and secured at the smart contract level. 

Maybe, just maybe - we can extend blockspace without another bridge or more airdrop farmers. 

Thanks for reading. Some existential questions that I can’t escape: 

Do blockchains really scale trust, or are we still capped at Dunbar’s number?

What happens to all of these ‘web3’ companies that rely on centralization for profit?

Has anything changed about Vitalik’s DAS claim here?

Where do I find the ‘price of anarchy’ dashboard for all this stuff?
