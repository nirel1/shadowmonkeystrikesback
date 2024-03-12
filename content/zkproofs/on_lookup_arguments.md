--- 
title: Lookup Arguments 
draft: true 
katex: true 
--- 

# What are Lookup Arguments Good For 

The main goal of a lookup argument is to prove that a particular value $x$ is contained in a given table $T$. Lookup tables are useful for a number of
reasons, but should be principly thought of as a way to express high-degree algebraic functions. 

# Arya and the Lookup Proposal 

> To enable decomposition proofs into odd and even-position bits, we develop a new lookup proof that makes it possible to check that a field element
> belongs to a table of permitted values. By creating a lookup table of all words with even-position bits, we make it possible to verify such
> decompositions. Lookup proofs not only enable decomposition into odd and even-position bits but also turn out to have many other uses such as
> demonstrating that field element represents a correct program instruction, or that a field element represents a valid word within the range $\lbrace 0,1
> 2^{w}\rbrace$. 

1. [Nearly Linear-Time Zoer-Knowledge PRoofs for Correct Program Execution](https://eprint.iacr.org/2018/380.pdf)

# Plookup, Plonkup, Halo2  

1. [Plookup: A Simplified Polynomial Protocol for Lookup Tables](https://eprint.iacr.org/2020/315.pdf)
2. [Plonkup: Reconciling Plonk with Plookup](https://eprint.iacr.org/2022/086.pdf)

# The Caulk Geneology

1. [Caulk: Lookup Arguments in Sublinear Time](https://eprint.iacr.org/2022/621.pdf)
2. [Caulk+: Table-Independent Lookup Arguments](https://eprint.iacr.org/2022/957.pdf)
3. [Flookup: Fractional Decomposition-Based Lookups in Quasi-Linear Time Independent of Table Size](https://eprint.iacr.org/2022/1447.pdf)
4. [Baloo: Nearly Optimal Lookup Arguments](https://eprint.iacr.org/2022/1565.pdf)

## Caulk $\rightarrow$ Caulk+ 

## Flookup 

## Baloo 

# nlookup  

1. [HyperNova: Recursive Arguments for Customizable Constraint Systems](https://eprint.iacr.org/2023/573.pdf)
