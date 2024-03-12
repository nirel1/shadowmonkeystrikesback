--- 
title: On Polynomials 
draft: true 
katex: true
--- 

# What are Polynomials and Why are they Useful? 

Here we will usually on provide statements. Ocassionally, if I'm feeling inspired, I'll give proofs as well. Polynomials are the bread and butter of
modern proof systems. 

# Settings 

## General Polynomial Objects 

<span style="color:red">Notation is important here. In particular, need to make sure number of variablesand degree have consistent variables. Then we
need a way to refer to different descriptions of polynomial (evaluation vs coefficient form).</span>

**Def Univariate Polynomial:** A univariate polynomial $p$ of degree $d$ has coefficient vector $\vec{c}$ = $\langle c_{0}, \dots, c_{d}\rangle$ and 
degree $d$ is expressed as

$$ \sum_{i = 0}^{n} c_{i}X^{i}$$

Let $\vec{X_{i}} = $ 

**Def Multivariate Polynomial:** *Here, we have to go a bit deeper, since we probably have to specify many things -- max degree vs total degree,
various, orderings etc. The most general way to go is defining multisets of coefficients, exponents, and variables in order to generalize the notion
of a ``term"* 

# Polynomial Representations

## Density and Sparsity 

## Coefficient Form (CF)

## Evaluation Form (EF)

## CF $\Longleftrightarrow$ EF (Love Lagrange)

# Facts about Polynomials

**Vanishing Polynomials**.Let $\mathbb{F}$ be an extension field of a prime field $\mathbb{F}\_{p}$ and $H \subseteq \mathbb{F}$. $\mathbb{Z}\_{H}$ is
the unique monic polynomial such that $\mathsf{deg}(\mathbb{Z}\_{H}) \le |H|$ and $\mathbb{Z}\_{H}(a) = 0 \: \forall a \in H$. $\mathbb{Z}\_{H}$ is
called an *affine subspace polynomial*.   

{{< details "**Remark.** *Computational Advantages of Working with Linear Subspaces of Finite Fields*" >}}
> [Short PCPs Verifiable in Polylogarithmic Time](http://people.csail.mit.edu/madhu/papers/2005/bghsv2-full.pdf) 
> If $\mathbb{F}$ has small characteristic (e.g, 2) and $S$ is a linear subspace of $\mathbb{F}$ (where $\mathbb{F}$ is treates as a vector space),
> then the polynomial $\mathbb{Z}\_{S}$ is $log|S|$-sparse (that is, has only $\mathsf{log}|S|$ terms), and thus $\mathbb{Z}\_{S}$ can be evaluated in 
> $\mathsf{polylog}(|S|)$ field operations. This gives clear computational advantages of working with linear subspaces of finite fields. 
{{< /details >}}

**Shwartz-Zippel Lemma.**

*Proof*. 

**Multilinear Extension Lemma.** Let $f: \lbrace 0,1\rbrace^{n} \rightarrow \mathbb{F}$. Then there is a unique multilinear polynomial $\tilde{f}$ over
$\mathbb{F}$ such that $\tilde{f}(x) = f(x) \: \forall x \in \lbrac0,1\rbrace^{n}$. $\tilde{f}$ is called the *multilinear extension* (MLE) of $f$. Given
as input a list of all $2^{n}$ evaluations of $f$, and an arbitrary point $r \in \mathbb{F}^{n}$, there is an algorithm that can evaluate $\tilde{f}(r)$ in
$O(2^{n})$ time. 

*Proof*.

**Polynomial Remainder Theorem.** Let $p(x)$ be a univariate polynomial. $p(x)$ can be written as $p(x) = q(x)(x-r) + p(r)$, where 
$\mathsf{deg}(q) < \mathsf{deg}(p)$. Another way of phrasing this is that the remainder of $p(x)$ when divided by $(x - r)$ for some number $r$ 
is $p(r)$. 

{{< details "**Proof and Relevance**" >}}
> *Proof*. 
> Let $p(x)$ be a degree $d$ univariate polynomial. By Euclidean division, given divisor polynomial $f(x)$, $p(x) = q(x)f(x) + s(x)$, where
> $q(x)$ and $s(x)$, referred to respectively as the quotient and remainder polynomials, are unique. Letting $f(x) = (x-r)$ for some $r$, we observe
> that $s(x)$ is constant. Either $s(x) = 0$ if $f(x)$ perfectly divides $p(x)$ or otherwise some non-zero constant since $\mathsf{deg}(s) < \mathsf{deg}(f)$ 
> and $(x-r)$ is of degree $1$. We therfore write 
> $$p(x) =  q(x)f(x) + S$$
> Now, is it clear that $p(r) = S$
> 
> *Relevance*. 
> The PRT shows up everywhere, especially in efficient evaluation of polynomials. See Horner's Method. 
{{< /details >}}

## Polynomial Sum Lemmas 

**Lemma 1**. Let $H$ be an affine subspace of $\mathbb{F}$ and let $\hat{g}(x)$ be a univariate polynomial over $\mathbb{F}$ of degree strictly less
that $|H| -1$. Then 

$$\sum_{a \in H}\hat{g}(a) = 0$$

*Proof*. 

**Lemma 2** If $H$ is an affine subspace of $\mathbb{F}$ and $l(x)$ is the linear term of $\mathbb{Z}\_{H}$, then 

$$ \sum_{a \in H} a^{|H|-1} = l(X) $$

*Proof*.

**Lemma 3** Let $H$ be a multiplicative subgroup of a finite field $\mathbb{F}$ and let $p(X_{1}, \dots, X_{l}) \in \mathbb{F}[X_{1}, \dots, X_{l}]$.
If we denote by $p_{i_{1}, \dots, i_{l}} \in \mathbb{F}$ the coefficient of $X_{1}^{i_{1}} \dots X_{l}^{i_{l}}$ in the polynomial $p(X_{1}, \dots,
X_{l})$, then 

$$\sum_{\vec{w} \in H^{l}} p(\vec{w}) = \left(\sum_{\vec{i} \equiv \vec{0} \pmod |H|} p_{\vec{i}} \right) \cdot |H|^{l}$$

*Proof*. By induction of $l$. 

**Lemma 4**. Ket $H$, $\mathbb{F}$, and $p$ be as in **Lemma 3**. Then for every integer vector $\vec{j} = (j_{1}, \dots, j_{l}) \in \mathbb{N}^{l}$,
and writing $\vec{w}^{\vec{j}}$ for the product $w_{1}^{j_{1}} \cdots w_{l}^{j_{l}}$, 

$$\sum_{\vec{w}\in H^{l}}p(\vec{w})\cdot \vec{w}^{\vec{j}} = \left(\sum_{\vec{i} + \vec{j} \equiv \vec{0} \pmod |H|} p_{\vec{i}} \right) \cdot |H|^{l}$$

*Proof*

**Remark**. Analogue exists for case of additive subgroups. 

**Lemma 5**. Let $H$ be a cyclic subgroup of finite order of the multiplicative group of a ring $R$, such that $1-h$ is not a zero-divisor for any $h
\in H\text{\textbackslash}\lbrace 1 \rbrace$. Let $M$ be an $R$-module and let $p(X_{1}, \dots, X_{l}) \in M[X_{1}, \dots, X_{l}]$ be a polynomila. If
we denote $p_{i_{1}, \dots, p_{l}} \in M$ the coefficient of $X_{1}^{i_{1}} \cdots X_{l}^{i_{l}}$ in the polynomial $p(X_{1},\dots,X_{l})$ then, 

$$\sum_{\vec{w} \in H^{l}}p(\vec{w}) = \left(\sum_{\vec{i} \equiv \vec{0} \pmod |H| p_{\vec{i}}}\right) \cdot |H|^{l}$$

*Proof*. 

**Lemma 6**. Let $H$ be an additive subgroup of $\mathbb{F}$. Let $a_{0}$ be the formal linear term of the subspace polynomial $\prod_{h \in H}(X -
h)$. Then, 

$$\sum_{\vec{w} \in H^{l}}p(\vec{w}) = \left(\sum_{\vec{i} \equiv -1 \pmod |H|}p_{\vec{i}} \right) \cdot |a_{0}|^{l}$$

*Proof*. 

**Remark**. 

**Summation Domains**: 
1. Affine subspace of $\mathbb{F}$ 
2. Multiplicative subgroup of $\mathbb{F}$ 
3. Cyclic subgroup of finite order of multiplicative group of a ring 
4. Additive subgroup of $\mathbb{F}$ 


# Resources 
1. [Polynomials Tristin Shin](https://www.mit.edu/~shint/handouts/Polynomials.pdf)
2. Lemmas 1 and 2 [Aurora](https://eprint.iacr.org/2018/828.pdf)
3. Lemmas 3 and 4 [Linear Time Arguments with Sublinear Verification from Tensor Codes](https://eprint.iacr.org/2020/1426.pdf)
4. Lemmas 5 and 6 [Sumcheck Arguments and their Applications](https://eprint.iacr.org/2021/333.pdf)





