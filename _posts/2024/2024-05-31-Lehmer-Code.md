---
title: Lehmer Code
date: 2024-05-31 20:35:54 +0530
categories: [Mathematics, Permutation]
tags: [lehmer-code, permutation]     # TAG names should always be lowercase
description: Approach for encoding permutations
toc: true
math: true
# comments: false
---
The Lehmer Code, named in reference to [Derrick Henry Lehmer](https://en.wikipedia.org/wiki/D._H._Lehmer) is method of encoding permutations. The encoding is done in the form of an inversion table. The Lehmer Code is also known and used as the [Factorial Number System](https://en.wikipedia.org/wiki/Factorial_number_system).


## Description:
Lehmer Codes are examples of an inversion tables. That is to say, they can be defined as follows:  
Let $\sigma$ be a permutation: $\sigma = (\sigma_1, \sigma_2, \ldots, \sigma_n)$, where $\sigma_i \in [1,n]\; \forall i \in [1,n]$  
The **Lehmer Code**, $L(\sigma) = (L{\small(\sigma)_1,L(\sigma)_2,\ldots,L(\sigma)_n})$ where $L(\sigma)_i = $ $\\#\\{j>i:\sigma_j < \sigma_i \\}$  


### Properties:
- Trivially, $\sum_{i=1}^nL(\sigma)_i =$ number of inversions in the permutation.
    - Side note, number of inversions is equal to the minimum number of adjacent swaps required to sort an array [(link TBA)](https://vrangr1.github.io/posts/Lehmer-Code/).
- Lexicographic ordering of Lehmer codes corresponds with the lexicographic ordering of the corresponding permutations. That is to say a permutation that is lexicographically larger than another will have its lehmer code be lexicographically larger than the lehmer code of the other permutation.
    <details> <summary> Proof</summary>
    Let the comparison operators correspond to lexicographic ordering. <br>
    Let $\sigma_1$ and $\sigma_2$ be permutations of length $n$ and $L\left(\sigma_1\right)$ and $L\left(\sigma_2\right)$ be their lehmer codes respectively. <br>
    Claim: $\sigma_1 > \sigma_2 \iff L\left(\sigma_1\right) > L\left(\sigma_2\right)$ <br>
    Proof:<br>
    Suppose $\sigma_1 > \sigma_2$
    $$
    \begin{eqnarray}
    \implies \exists i\in[1,n]\text{ s.t. } {\sigma_1}_j &=& {\sigma_2}_j \forall j < i \text{ and } {\sigma_1}_i > {\sigma_2}_i \\
    \implies \{ {\sigma_1}_j : j \geq i \} &=& \{ {\sigma_2}_j : j \geq i\} \\
    \text{Let } S_1 &:=& \{ {\sigma_1}_j:j\geq i \text{ and } {\sigma_1}_j < {\sigma_1}_i \}\nonumber \\
    \text{and let } S_2 &:=& \{ {\sigma_2}_j:j\geq i \text{ and } {\sigma_2}_j < {\sigma_2}_i \} \nonumber \\
    \text{Since } {\sigma_1}_i > {\sigma_2}_i &\text{ and }& (2) \nonumber \\
    \implies \forall p\in S_2,\text{ } &p\in& S_1  \nonumber \\
    \implies S_2 &\subsetneq& S_1 \because {\sigma_2}_i \in S_1 \land {\sigma_2}_i \not\in S_2 \nonumber \\
    \implies \left(L\left({\sigma_1}\right)_i = \vert S_1 \vert\right) &>& \left(L\left({\sigma_2}\right)_i = \vert S_2\vert\right) \\
    \text{By (1) and (3),} &&\text{we can conclude:} \nonumber \\
    L\left({\sigma_1}\right)_j = L\left({\sigma_2}\right)_j \forall j < i &\text{ and }& L\left({\sigma_1}\right)_i > L\left({\sigma_2}\right)_i \nonumber \\
    \implies L\left({\sigma_1}\right) &>& L\left({\sigma_2}\right) \nonumber
    \end{eqnarray}
    $$
    Since $\sigma_1$ and $\sigma_2$ are arbitrary permutations and the contrapositive of the converse is immediate, the proof is complete.
    </details>
- The Lehmer Code also coincides with the [Factorial Number System](https://en.wikipedia.org/wiki/Factorial_number_system) and, as such, for more properties please refer to my post on the Factorial Number System.

## See Also:
