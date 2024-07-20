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
The factorial number system is a [mixed radix numeral system](https://en.wikipedia.org/wiki/Mixed_radix) that has the following properties:  

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

- Based on the definition and the table in the above section, it can be observed that for a fixed length $n$, there are $n!$ many different factoradics possible. Therefore, based on that fact and the last property, it can be trivially proved that $r^{th}$ (in 0-based indexing) lexicographically smallest permutation's factoradic is also the $r^{th}$ smallest (lexicographically speaking, in 0-based indexing) factoradic possible. Furthermore, there's a simple way to get this $r$ from if the factoradic is provided/computed for a permutation:  
$$
r = \sum_{i=1}^n\left[\left(n-i\right)!\cdot L\left(\sigma\right)_i\right]
$$
    <details><summary>Proof:</summary>
    This can be proven via induction.<br>
    <b>Base Case:</b><br> It is trivial to note that the factoradic/lehmer code for the lexicographically smallest permutation i.e. $\sigma_{(0)} = \left(1,2,\ldots,n-1,n\right)$ is $L\left(\sigma_{(0)}\right) = \left(0,0,\ldots,0,0\right)$<br>
    As such, $r_0 = \sum_{i=1}^n\left[(n-i)!\cdot L\left(\sigma_{(0)}\right)_i\right] = 0$<br>
    <b>Inductive Assumption:</b><br>
    Let the factoradic for the $n^{th}$ lexicographically smallest permutation, $\sigma_{(n)}$ be $L\left(\sigma_{(n)}\right) = \left(l_1,l_2,\ldots,l_{n-1},l_n\right)$<br>
    And, since we are going in the lexicographic ordering of both the permutations and the factoradics (which belong to a mixed radix numeral system described above), we can say that $L\left(\sigma_{(n)}\right)$ will be of the form $\left(l_1,l_2,\ldots,l_k,n-(k+1),n-(k+2),\ldots,1,0\right)$ for some $k\in[1,n-1]$ and $l_k \neq n-k$. Therefore, $l_i = 0$ $\forall i\in[k+1,n]$.<br>
    <b>Assume</b> that $r_n = \sum_{i=1}^n\left[(n-i)!\cdot l_i\right] = \sum_{i=1}^k\left[(n-i)!\cdot l_i\right] = n$<br>
    <b>Inductive Step:</b><br>
    Let's consider the factoradic, $L\left(\sigma_{(n+1)}\right)$, of the $(n+1)^{th}$ lexicographically smallest permutation $\sigma_{(n+1)}$. Now, we know that $L\left(\sigma_{(n+1)}\right)$ must be the next lexicographically bigger mixed radix number of $L\left(\sigma_{(n)}\right)$. Therefore, $L\left(\sigma_{(n+1)}\right)$ must be of the following form:
    $$
    \begin{eqnarray}
        L\left(\sigma_{(n+1)}\right) &=& \left(l_1,\ldots,l_k+1,0,0,\ldots,0,0\right)\nonumber\\
        \therefore r_{n+1} &=& \sum_{i=1}^{k-1}\left[(n-i)!\cdot l_i\right] + (n-k)! \cdot (l_k+1) \nonumber\\
        &=& \sum_{i=1}^{n}\left[(n-i)!\cdot l_i\right] + (n-k)! \cdot (l_k+1) - (n-k)! \cdot l_k - \sum_{i=k+1}^n\left[(n-i)!\cdot (n-i)\right] \nonumber\\
        &=& n + (n-k)! - \sum_{i=k+1}^n\left[(n-i)!\cdot (n-i)\right] \nonumber\\
        \text{It's } &\text{easily}& \text{ proven that } \sum_{i=1}^t\left(i!\cdot i\right) = (t+1)! - 1\nonumber\\
        \therefore r_{n+1} &=& n + (n-k)! - \left\{\left(n-(k+1)+1\right)! - 1\right\} \nonumber\\
        \implies r_{n+1} &=& n + (n-k)! - (n-k)! + 1 \nonumber\\
        \implies r_{n+1} &=& n+1 \nonumber
    \end{eqnarray}
    $$
    Thus, by the principle of weak mathematical induction, our proof is complete.
    <div style="text-align: right">
    $\square$
    </div>
    </details>

<!-- ## Conversion:
Now that we have defined the factoradic and some of its properties, we can go over the ways to convert the factoradic into the permutation and vice versa and, how to get either the factoradic or the permutation from the rank (in 0-indexed decimal number system) of the permutation in lexicographic order.
### Permutation -> Factorial Number System: -->

## Relevant Competitive Programming Problems:
-> [Codeforces Round 285 Div 2: Problem D: Misha and Permutation Summation](https://codeforces.com/contest/501/problem/D)