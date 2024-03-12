--- 
title: Heterogeneous Utility Belt 
draft: true 
katex: true 
--- 

# Introduction 

Here is a collection of theorems and concepts that are useful. They will roughly be sorted by subject. I will attempt to give explanations or examples 
of why they are useful, at least in the contexts that I've encountered them. Some will be incredibly basic, while others will be slightly more invovled. 


# Number Theory 

**Fermat's Little Theorem**. Let $p$ be a prime. Then $\forall a \in \mathbb{Z}$, $a^{p} \equiv a \pmod{p}$. The more useful special case of this is
when $\mathsf{gcd}(a, p) = 1$. Then, $a^{p-1} \equiv 1 \pmod{p}$. 

# Combinatorics 

**Binomial Theorem**:  $(x + y)^{n} = \displaystyle{\sum_{k = 0}^{n} \binom{n}{k} x^{k}y^{n-k}}$

# Probability 

**Central Limit Theorem**: 

**Chebyshev Bound**: 

**Chernoff Bound**:  

**Birthday Paradox**: 

**

# Algebra 

**Konecker's Theorem**: Let $\mathbb{F}$ be a field and $f \in \mathbb{F}[X]$ be a non-constant polynomial. Then there exists an extension field
$\mathbb{E}$ of $\mathbb{F}$ containng a zero of $f$. 

# Complexity Theory 






## IP Theorems

1. **IP** = **PSPACE**. 

> Any set in **PSPACE** has an interactive proof. This theorem is fundamental to our understanding of both interactive proofs and polynomial space
> computations. In addition, it has important applications, such as the existence of program checkers for **PSPACE**-complete sets, and the existence
> of zero knowledge proofs for every set in **PSPACE**. Known proofs go roughly along the following lines: Suppose that we are given a claim that can
> be verified in polynomial space, and we are required to design an interactive protocol for verifying the claim. We begin by expressing the claim as
> a quantified Boolean formula, using the **PSPACE**-completeness of the **TQBF** problem. Then, we *arithmetize* the formula, transforming it into a
> claim about the value of a particular arithmetic expression. Finally, we use the celebrated sum-check protocol in order to verify the value of the
> arithmetic expression One key point is that the sum-check protocol employs the fact that certain restrictions of the arithmetic expression are
> low-degree polynomials. [From Or Meir IP = PSPACE from Error Correcting Codes]. 

2. **coNP $\subseteq$ IP**. 

3. **#P $\subseteq$ IP**. 
