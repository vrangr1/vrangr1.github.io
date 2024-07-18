---
title: Factorial Number System
date: 2024-05-31 13:25:08 +0530
categories: [Mathematics, Permutation]
tags: [permutation, lehmer-code]     # TAG names should always be lowercase
description: Factorial Number System for indexing permutations in lexicographic order.
toc: true
math: true
mermaid: true
# comments: false
---
The Factorial Number System, also known as the factoradic, is [mixed radix numeral system](https://en.wikipedia.org/wiki/Mixed_radix) for efficiently indexing permutations in lexicographic ordering. It's also known as the [Lehmer Code](https://vrangr1.github.io/posts/Lehmer-Code).

## Motivation:
While the set of natural numbers can also be used to index permutations in their lexicographic ordering, the indexes can naturally increase far beyond values that can be easily handled by a computer (by say `integer` or larger similar data types in programming languages). As such, in cases when indexing and ordering of the permutations is required, the factorial number system might be used. Furthermore, there's no intuitive relation between a permutation's lexicographic index in the set of natural numbers and the permutation itself. That is to say, given an index or a permutation, it's not easy to get the other without utilizing something like the factorial number system itself.

## Description:
<details> 
<summary> Note </summary>
While this post has been written to be self contained to a certain extent, it might be better for the reader to first perhaps read the post on the [Lehmer Code](https://vrangr1.github.io/posts/Lehmer-Code) for an introduction into the Factorial Number System.
</details>
The factorial number system is a mixed radix numeral system that has the following properties:  

|   **Radix / Base**   |    n   |   n-1  |   n-2  |   $\ldots$   |  3  |  2  |  1  |
|   **Place Value**    | (n-1)! | (n-2)! | (n-3)! |   $\ldots$   |  2! |  1! |  0! | 
|**Highest Digit Allowed**| n-1 |   n-2  |   n-3  |   $\ldots$   |  2  |  1  |  0  |

The construction of a factoradic for a permutation goes as follows:  

Let the permutation be represented as follows $\sigma = \left(\sigma_1, \sigma_2, \ldots, \sigma_{n-1}, \sigma_n\right)$ where $\sigma_i \in [1,n]\;\;\forall i$ and $\sigma_i \neq \sigma_j,\;\forall i \neq j$  
Then the factoradic of that permutation is as follows:  
$L\left(\sigma\right) = \left(L\left(\sigma\right)_1,L\left(\sigma\right)_2,\ldots,L\left(\sigma\right)\_{n-1},L\left(\sigma\right)_n\right)$  
$L\left(\sigma\right)_i := $ the 0-indexed rank of $\sigma_i$ sorted order of $\\{1,2,\ldots,n\\}\setminus \\{\sigma_j: j < i\\}$  
That is to say, $L\left(\sigma\right)_i = \\# \\{j > i: L\left(\sigma\right)_j < L\left(\sigma\right)_i\\}$  

The above simplification of the definition of the factoradic is, in fact, the definition of the lehmer code of a permutation. As such, lehmer code and factorial number system refer to the same indexing/encoding system of permutations.

### Properties:
- The factoradic of a permutation is the lehmer code of that permutation. As such, the factoradic also has the same properties as that of the lehmer code, the most important of which is as follows:
    - Lexicographic ordering of the lehmer codes correspond with the lexicographic ordering of the permutations. That is to say, a factoradic is lexicographically bigger than a other factoradic if and only if their corresponding permutations also have the same lexicographic ordering. The proof for this, if required, can be found [here](https://vrangr1.github.io/posts/Lehmer-Code).

- Based on the definition and the table in the above section, it can be observed that for a fixed length $n$, there are $n!$ many different factoradics possible. Therefore, based on that fact and the last property, it can be trivially proved that $r^{th}$ (in 0-based indexing) lexicographically smallest permutation's factoradic is also the $r^{th}$ smallest factoradic possible. Furthermore, there's a simple way to get this $r$ from if the factoradic is provided/computed for a permutation:  
$$
r = \sum_{i=1}^n\left[\left(n-i\right)!\cdot L\left(\sigma\right)_i\right]
$$
    <details><summary>Proof:</summary>
    This can be proven via induction.<br>
    <b>Base Case:</b><br> It is trivial to note that the factoradic/lehmer code for the lexicographically smallest permutation i.e. $\sigma = \left(1,2,\ldots,n-1,n\right)$ is $L\left(\sigma\right) = \left(0,0,\ldots,0,0\right)$<br>
    As such, $r = \sum_{i=1}^n\left[(n-i)!\cdot L\left(\sigma\right)\right] = 0$<br>
    <b>Inductive Assumption:</b><br>
    Assume 
    </details>

## Relevant Competitive Programming Problems:
