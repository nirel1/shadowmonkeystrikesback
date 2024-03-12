--- 
title: On Cryptographic Security Models 
draft: on 
katex: on 
---

# Random Oracle Model (ROM)

Models cryptographic hash functions as random oracles. 

## Random Beacons vs Random Oracles 

> The difference between random beacons and the much more well-known random oracles, is that their values are not available until certain time slots.
> That means we can assume a given random beacon value is independent of values output by an adversary in previous time slots. (Or in the case of the
> adversary having influence on the beacon, beacon values have lots oentropy conditioned on previous values output by the adversary.) This is
> completely different from a random oracle value, that can have entropy zero conditioned on adversary messages (e.g, if the adversary simply queries
> and outputs the RO value). 

1. [Scalable Multi-party Computation for zk-SNARK Parameters in the Random Beacon Model](https://eprint.iacr.org/2017/1050.pdf)

# Generic Group Model (GGM)

> At the highest level, generic group algorithms are algorithms that do not exploit any special structrue of the representation of the group elements
> and can thus be applied in any cyclic group. More concretely, a generic algorithm may use only the abstract group operation and test whether two
> group elements are equal. This property makes it possible to prove information-theoretic lower bounds on the running time for generic algorithms.  
> 
> The class of algorithms encompasses many important algorithms such as the baby-step giant-step algorithm and its generalization for composite-order
> groups (also known as Pohlig-Hellman) as well as Pollard's rho algorithm. 


# Algebraic Group Model (AGM)

1. [The Algebraic Group Model and its Applications](https://eprint.iacr.org/2017/620.pdf)

## Hidden Order Groups 

# Standard Model 

# Linear Code Random Oracle Model (LCROM) 

[On Succinct Non-Interactive Arguments in Relativized Worlds](https://eprint.iacr.org/2022/383.pdf)

