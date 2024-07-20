---
title: Order Statistics Tree
date: 2024-07-18 14:40:28 +0530
categories: [Data Structures]
tags: [data-structure, gnu-pbds, ordered-set, cartesian-tree, treap]     # TAG names should always be lowercase
description: Approach for encoding permutations
toc: true
math: true
# mermaid: true
# comments: false
---

The Order Statistics Tree is a variant of the well known Binary Search Trees that allow for the following operations with optimal efficiency (depending on the method of construction of the binary search tree):
* select(k) : get the $k^{th}$ smallest element
* rank(v): get the rank (in sorted order) of the value v among the value of the BST.

The above two operations are linearly dependent on the height, H, of the binary search tree. That is, both of the operations take $O(H)$ operations in the worst case.

## Construction:
The construction of an order statistics tree requires nothing other than an addition variable to be associated with every node in the binary search tree that stores the size of the subtree of the node in that variable. It's simple enough to intuit why that is sufficient to perform the additional two operations mentioned above. For that reason, I'll be skipping the proof for the same.

## C++ STL Implementation:
While the above section metions the simple modification needed to make a binary search tree into an order statistics tree, making that tree optimal is a different question altogether. While there are popular ways of making a balanced binary search trees (using Red-Black trees or AVL trees), they can be quite troublesome to implement. Too troublesome to regularly implement in any competitive programming contest. Thankfully, there exists an extension of C++ STL that contains within itself an implementation for an order statistics tree. For more details on the C++ STL extension: GNU Policy Based Data Structures (PBDS), please refer [this](https://www.geeksforgeeks.org/policy-based-data-structures-g/).

Note that the PBDS extention to STL is only included implicitly with GNU C++ compilers. For     people on Apple computers and using CLang complilers, you'll need to either install GNU C++ compilers on your computer or, setup CLang to use PBDS. There are various blogs online (especially on [codeforces.com](https://codeforces.com)) that mention how to accomplish this.

Here's how one can import and use an order statistics tree.
```c++
#include <bits/stdc++.h>
#include <ext/pb_ds/assoc_container.hpp>
#include <ext/pb_ds/tree_policy.hpp>

using namespace std;
using namespace __gnu_pbds;
template <typename type>
using ordered_set = tree<type, null_type, std::less<type>, rb_tree_tag, tree_order_statistics_node_update>;

int main() {
    ordered_set<int> ost;
    ost.insert(1);
    ost.insert(2);
    ost.insert(3);
    cout << ost.order_of_key(2) << endl;
    cout << ost.find_by_order(1) << endl;
}
```
As might be apparent by the above code block, the PBDS implementation of the order statistics tree is quite more complicated than just a modified balanced binary search tree. In actuality, what we have here is a treap, a variant of a cartesian tree. It can also be customized in some ways. I will not be diving deeply into that here. For the purposes of an order statistics tree, we can treat the aliased data structure `ordered_set` as essentially a C++ set with the two additional methods `order_of_key` and `find_by_order` that are exactly the `select` and `rank` methods described above. The time complexitities of these two new methods in `ordered_set` is $O\left(\log n\right)$

<!-- ## Variants

## Uses

## Competitive Programming Problems: -->