--- 
title: On Polynomial Commitments 
draft: true 
katex: true 
---

# What is a Polynomial Commitment? 

# Why are they useful? 

# Merkle Trees (Random Oracle Model)

# KZG

# Hyrax 

1. square-root commitment scheme: gives $O(\sqrt{|w|})$ communication and verifier runtime, where $w = w_{1}, \dots, w_{\ell}$ is the witness. 
2. proof-of-dot-product ($4+n$ elements for vectors of length $n$) $\longrightarrow$ proof-log-of-dot-product ($4+2log n$ elements for vectors of
   length $n$).
    - Verifier's computational cost dominated by multi-exponentiation of length $n$ 
3. Matrix commitment of Groth (encodes polynomial as matrix of evaluations)
4. 


# SPARK 

**Def Dense Multilinear Polynomial**. 

**Def Sparse Multilinear Polynomial**. 

From Spartan, extended in Lasso. A cryptographic compiler that takes any polynomial commitment scheme for dense multilinear polynomials and transforms
it into an more efficient polynomial commitment for *sparse* polynomials. In particular, uses ZK-snark with sublinear verification for restricted
class of NP statements. SPARK uses Hyrax as a starting point.  

# FRI

# DARK 

# Lattice-Based

# Taxonomy 
