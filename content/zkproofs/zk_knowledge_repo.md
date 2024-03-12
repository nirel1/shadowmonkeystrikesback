--- 
title: Directory of Zero Knowledge Definitions, Notions, Tools  
draft: true 
katex: true 
--- 

# Introduction 

It's very difficult to keep track of all the various notions related to zero knowledge. Indeed there are many, making zero knowledge an extremely
nuanced topic and its academic literature difficult to navigate. There are canonical definitions that are commonplace, but developing an intuition for
more esoteric notions can be difficult. The goal of this page is to collect these various definitions under common notation in order to systematically
build intuition for what concepts these definitions aim to capture and how they are connected. 

# Fundamental Building Blocks 

**Def Interactive Argument of Knowledge:** $\mathsf{ARG} = (\bm{G}, \bm{P}, \bm{V})$ denotes an *interactive argument* of knowledge for relation
$\mathcal{R}$. The goal of $\mathsf{ARG}$ is for $\bm{P}$ to prove to $\bm{V}$ that he knows a witness $w$ with respect to statement $x$ that
satisfies $\mathcal{R}$. Following the setup algorithm $\bm{G}$, $\bm{P}$ and $\bm{V}$ will exchange messages until eventually $\bm{V}$ will either
accept or reject $\bm{P}$'s claim of knowledge. 

**Interactive Proof (IP)**. 

**Probabilistically Checkable Proof (PCP)**.

**Interactive Oracle Proof (IOP)**. 

**Interactive Oracle Proof of Proximity (IOPP)**. Essentiall a low-degree test for RS relation.  

**Reed-Solomon Encoded IOP (RS-IOP)**. 

**Tensor IOP**. An IOP where the verifier can make tensor queries to the proof strings sent by the prover, as oppsed to just point queries as in a
standard IOP. The verifier specifies a vector with a prescribed tensor structure and receives as answer the ineer product of the tensor vector and
proof string. Tensor IOPs are paramaterized by $(\mathbb{F}, k, t)$, which describes the tensor query structure. 

## The Basic Properties   

1. Completeness 
2. Soundness 
3. Zero Knowledge (full zero-knowledge)
4. Public Coin 

## Variations 

1. $n$-Special Soundness
2. Statistical Zero Knowedge 
3. Computational Soundness
4. Knowledge Soundness 
5. Honest Verifier Zero-Knowledge
6. Perfect Special Honest-Verifier Zero-Knowledge
7. Witness-Extended Emulation 
8. Computational Witness-Extended Emulation 

## Tools of the Trade 

1. Simulation-Extractable 
2. Transcript Trees 
3. Knowledge-Extractor 
4. **Multi-Proof Online Extractability**: Extractor does not need to rewinda malicious prover and instead, only needs a list of Random Oracle queries
   made by the adversary and the proof to extract a satisfying witness. 
5. Simulators vs Extractors vs Emulators 
6. Forking Lemma  
7. The Fiat-Shamir Heuristic 

## Some Building Blocks 

1. Interactive Argument of Knowledge
2. Succinct Non-Interactive Argument (SNARG)
3. Succinct Non-Interactive Argument of Knowledge (SNARK)
4. Designated Verifier SNARK 


