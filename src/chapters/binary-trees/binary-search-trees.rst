===================
Binary Search Trees
===================

.. relevant objectives
- Understand the conceptual structure of a binary search tree
- Understand the concept of a depth of a BST
- Explain what it means for a BST to be balanced
- Explain how a BST might become unbalanced (including worst-case scenarios),
  and how an unbalanced tree affects the efficiency of a binary search
- Understand how to balance a BST (segue to operations)

.. relevant notes from paul
- Binary Search Tree
- Depth with regards to a BST
- Balance with regards to a BST
- Unbalanced BST (including worst-case scenarios for an unbalanced BST)
- Balancing an unbalanced BST
- Difference between a Binary Tree (structure) and a Binary Search Tree
  (ordered structure)

Binary Search Tree
------------------
A Binary Search Tree, is a Binary Tree that is sorted. Like the Binary Tree
each node can have no more than two child nodes. But in the case of ordering
the tree there is an additional rule: The left child most be a smaller value
than the parent node, and the right child most be a greater value than the parent
node. Ordering our data this way makes performing Binary searches easy to
visualize.
Taking the example we saw for Binary Search let's turn it into a Binary Tree.
Collection: (1, 2, 3, 4, 8, 9, 10, 14, 18, 20, 30)
               9
       3               18
  2        4       14      30
1            8   10      20
In this example we most know what our middle most value is and it becomes our
root node: 9. From here we need to know what is the middle of the values that
are greater than 9 in our collection: 18. We also need to know what is the
middle of the values that are less than 9 in our collection: 3.
Now from both of those nodes we need to keep going. From 18 for the left child
node we need to know what is the middle of the reamining nodes between 9 and
18? In this case it would be 14. From 18 for the right child onde we need to
know what is the middle of the remaining nodes between 18 and the last element
of the array (rounding up): 30.
We would need to keep this up to fill out the rest of the 

Depth
^^^^^

.. what is the concept of depth? How does it pertain to BSTs?

Balance
^^^^^^^

.. what do we mean when we say the BST is balanced?

.. what would happen if the tree were to become unbalanced?

.. logically (conceptually) what would you need to do to balance, and unbalanced tree?


Concept Checks
--------------