--- 
title: One Methods of Arithmetization 
draft: true 
katex: true 
---

# What Is a Circuit? 

## Arithmetic Circuit Satisfiability 

## Uniform vs Non-Uniform Computation 

# Quadratic Arithemtic Programs (QAP) 

**QSP Precursor**: Quadratic Span Programs as a custom encoding for Boolean circuits. Superficially similar to QAPs, but only support boolean wire
values and therefore only use two sets of polynomials. 

> Quadratic arithmetic programs are a means to batch together a set of quadratic equations with a single multiplication each into a polynomial
> equation. While QAPs have mainly been used to construct pairing-based SNARKs, we find that they can also be used in interactive proofs. 

**Def Regular QAP**: A QAP $Q$ over field $\mathbb{F}$ contains three sets of $m+1$ polynomials $\mathcal{V} = \lbrace v_{k}(x) \rbrace, \mathcal{W} 
= \lbrace w_{k}(x)\rbrace, \mathcal{Y} = \lbrace y_{k}(x) \rbrace$ for $k \in \lbrace 0,m \rbrace$, and a target polynomial $t(x)$. Suppose $F$ is a 
function that takes as input $n$ elements of $\mathbb{F}$ and outputs $n'$ elements, for a total of $N = n + n'$ I/O elements. Then we say that $Q$ 
computes $F$ if: $(c_{1}, \dots, c_{N}) \in \mathbb{F}^{N}$ is a valid assignment of $F$'s inputs and outputs, if and only if there exists coefficients 
$(c_{N+1}, \dots, c_{m})$ such that $t(x)$ divides $p(x)$, where: 

$$ p(x) = \left(v_{0}(x) + \sum_{k=1}^{m}c_{k} \cdot v_{k}(x) \right) \cdot \left(w_{0}(x) + \sum_{k=1}^{m}c_{k} \cdot w_{k}(x) \right) -  \left(y_{0}(x) + \sum_{k=1}^{m}c_{k} \cdot y_{k}(x) \right) $$    

> Recall that [2] shows how to transform a regular QAP into a strong QAP, but the transformation more than *tripples* the degree of the QAP
> Consequently, when they plug their strong QAP into their VC construction, the strengthening step more than triples the key generation time,
> evaluation key size, and worker computation. 

**QAP Batching**: 

**Groth's Lower Bound**: *A pairing-based non-interactive argument with generic group algorithms as described must have at least two group elements in
the proof.*

*Proof Sketch*: 


1. [Pinocchio: Nearly Practical Verifiable Computation](https://eprint.iacr.org/2013/279.pdf)
2. [Square Span Programs with Applications to Succinct NIZK Arguments](https://eprint.iacr.org/2014/718.pdf)
3. [Arya](https://eprint.iacr.org/2018/380.pdf) 
4. []() 

# Rank 1 Constraint Systmes (R1CS) 

**Generic R1CS Relation**: Let $\mathbb{F}$ be a finite field. Then, given coefficient matrices $A, B, C \in \mathbb{F}^{n \times n}$, $z$ is a witness for
$\mathcal{R}\_{\mathsf{R1CS}}$ if and only if $z \in \mathbb{F}^{n}$ such that  

$$Az \circ Bz = Cz.$$

{{< details "**Remark.** *Nuanced Witnesses*" >}}
> Here, $z$ is treated as a monolithic R1CS witness. However, in pratice, $z = (\mathsf{wit}, \mathsf{pub})$ is often split into private and a public 
> parts. The private part, $\mathsf{wit}$ is considered the witness, and is committed to in order to achieve zero knowledge. Intuitively, such a distinction 
> makes sense on two counts. The first is that the costs of zero knowledge proof systems are dominated by cryptographic operations. Therefore one wishes 
> only to commit to the minimum necessary amount of information. Secondly, many computations we care about do indeed have both public and private input. Or, 
> more precisely, input that corresponds to the witness known by the prover and input that the verifier can and should know. For example, one might 
> wish to prove that he knows a valid signature with respect to a particular public key. The verification algorithm takes as input a message, signature, 
> and public key, where the signature is private, the public key is not, and the status of the message is context dependent. 
{{< /details >}}

A $\mathsf{R1CS}$ relation can be decomposed into two subrelations often referred to as (1) $\mathsf{Rowcheck}$ and (2) $\mathsf{LinCheck}$.
Proof systems that work over a $\mathsf{R1CS}$ instance often decompose the instance into these two relations, propose separate protocols for each,
and finally combine them into a single IOP, reasoning about security in an appropriately modular way. As there are many $\mathsf{R1CS}$ variants, we
will be slightly more careful moving forward about specifying the setting for different relations. 

**Classic $\mathsf{R1CS}$**. We refer to a classic $\mathsf{R1CS}$ relation as $\mathcal{R}\_{\mathsf{C-R1CS}} = ((\mathbb{F}, n, m, A, B, C), z)$, where
$\mathbb{F}$ is a finite field, $A, B, C \in \mathbb{F}^{n \times n}$ are public coefficient matrices with at most $m$ non-zero entries, and $z \in
\mathbb{F}^{n}$ serves as witness such that $Az \circ Bz = Cz$. 

**Classic $\mathsf{RowCheck}$**. We refer to a classic $\mathsf{RowCheck}$ relation as $\mathcal{R}\_{\mathsf{C-RC}} = ((\mathbb{F}, w, y), x)$
where $\mathbb{F}$ is a finite field and $x, y \in \mathbb{F}^{n}$ are public vectors and $x \in \mathbb{F}^{n}$ serves as a witness such that 
$w \circ x = y$. 

**Classic $\mathsf{LinCheck}$**. We refer to a classic $\mathsf{LinCheck}$ relation as $\mathcal{R}\_{\mathsf{C-LC}} = ((\mathbb{F}, n, M, y), x)$
where $\mathbb{F}$ is a finite field, $M \in \mathbb{F}^{n \times n}$ is a public matrix, $y \in \mathbb{F}^{n}$ is a public target vector, and $x \in
\mathbb{F}^{n}$ serves as a witness such that $Mx = y$. 

**Composing $\mathsf{RowCheck}$ and $\mathsf{LinCheck}$**. 

**Indexed Relations**. 

**Holographic $\mathsf{R1CS}$**.

**Holographic $\mathsf{RowCheck}$**.

**Holographic $\mathsf{LinCheck}$**.

**Twisted Tensor Relations**. 

**Arithmetic Circuit $\rightarrow \mathcal{R}\_{\mathsf{R1CS}}$** 

1. [SNARKS for C: Verifying Program Executions Succinctly and in Zero Knowledge](https://eprint.iacr.org/2013/507.pdf)
2. [Aurora: Transparent Succinct Arguments for R1CS](https://eprint.iacr.org/2018/828.pdf)

# Algebraic Intermediary Representation (AIR)

Most modern SNARK constructions represent computations as R1CS instances, derived from arithmetic circuits. STARK, however, uniquely requires a
computation be expressed in its Algebraic Intermediary Representation (AIR), an execution trace subject to polynomial constraints that enforce
conditions at key points and transition between each adjacent pair of the trace's rows. Informally, an execution trace is a table of field elements,
where each row represents a machine state at a sequenced step of the computation. These states are composed of registers holding finite field elements
that over time build the trace's columns. This allows much flexibility in AIR design, which affects both prover and verifier efficiency in interesting
ways. Most relevant here is the degree of constraint polynomials, which coalesce during the prover's protocol in a manner that make his work
essentially proportional to their multiplicative degree. Strategies such as decomposing high degree polynomial constraints into multiple low degree
constraints therefore weighs decreased multiplicative degree against execution trace length. 

Formally, a computation $\mathfrak{c}$ whose state is encoded by $w$ registers of elements in finite field $\mathbb{F}\_{p}$ corresponds to an
execution trace over $\mathbb{F}\_{p}$ with $|\mathfrak{c}|$ rows denoted $s_{0}, \dots, s_{|\mathfrak{c}|-1}$ and $w$ columns denoted $f_{0}, \dots,
f_{w-1}$. There are two fundamental constraint types that enforce a computation.

**Boundary Constraints**. A boundary constraint $\mathfrak{b}$ is characterized by tuple $i,j, \alpha$ as the equality relation
$f_{i}\left[j\right] = \alpha$, where $i \in [0, |\mathfrak{c}|-1]$, $j \in [0,t-1]$, $\alpha \in \mathbb{F}\_{p}$. That is, the value of register $i$
at step $j$ of $\mathfrak{c}$ is $\alpha$. Generalizing a boundary constraint for the entire state of $\mathfrak{c}$ at a particular moment, column
index and value pair $(i, \vec{\alpha}) \in [0, |\mathfrak{c}| - 1] \times \mathbb{F}\_{p}^{w}$ defines equality relation $s_{i} = \vec{\alpha}$.
Boundary relations are useful for asserting values at key points in the computation, input and output for example.  \\

**Transition Constraints**. A transition constraint $\mathfrak{t}$ defines a relation for a consecutive pair of trace rows by polynomial $p
\in \mathbb{F}\_{p}[\vec{X}]$, where $|\vec{X}| = 2w$ such that for some $j\in[0, t-1], \: \vec{X} = \{f_{1}[j] \dots, f_{w}[j], f_{1}[j+1], \dots,
f_{w}[j+1]\}$. More succinctly, $\forall i \in [0, |\mathfrak{c}|-1], \exists \: p \in \mathbb{F}\_{p}^{w}$ such that $s_{i+1} = p(s_{i})$. 

1. [ethStark Documentation - Version 1.1](https://eprint.iacr.org/2021/582.pdf)

# Plonkish Representation  

1. [gnark PLONK explainer blog](https://hackmd.io/@gnark/plonk)
2. [Recursive Proof Composition without a Trusted Setup](https://eprint.iacr.org/2019/1021.pdf)
3. [From AIRs to RAPs - How PLONK-style Arithmetization Works](https://hackmd.io/@aztec-network/plonk-arithmetiization-air) 

# Customizable Constraint Systems (CCS) 

1. [Customizable Constraint Systems for Succinct Arguments](https://eprint.iacr.org/2023/552.pdf)


