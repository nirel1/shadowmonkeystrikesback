--- 
title: notes3
draft: on 
katex: on 
---

Note 3 - enshrine

Many rollups discuss the concept of enshrining logic. The idea is that if rules are baked into the protocol, the rollup benefits from better safety guarantees. Some of the tradeoffs are discussed here: https://ethresear.ch/t/why-enshrine-proposer-builder-separation-a-viable-path-to-epbs/15710

In the context of a proving marketplace, this idea has also been discussed (https://discourse.aztec.network/t/ideas-on-a-proving-network/724/3 ) . Here, it seems like the minimal requirement for a rollup is to ‘enshrine’ a delegation mechanism - we interpret this to mean that a method to request proofs from a 3rd party is baked into the protocol. 

While rollups have a unique design space, because they get to build the protocol from scratch and are not limited to ordinary constraints (like that of an application building on Ethereum), it seems like applications also benefit from the ability to ‘enshrine’ proving logic. In other words, an application might want to automate the generation of proofs that allow it to migrate computation off-chain while minimizing trust assumptions.
