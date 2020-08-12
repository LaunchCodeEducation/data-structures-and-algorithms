Binary Search Tree Operations
=============================

BST Operations
--------------

There are three basic operations for a BST:

- Searching for a value
- Inserting a new value
- Deleting an existing value

Inserting or deleting requires a change to the binary search tree, which are destructive actions. In other words, they alter the underlying structure of the tree. Over the course of several insertions and deletions, a balanced tree can become unbalanced. As we have learned, this will degrade performance of the tree. 

There are techniques to keep a BST balanced even after a destructive operation, but those are beyond the scope of this course. Going forward, we will typically assume that a BST is balanced when talking about runtime efficiency.

Search
^^^^^^

We have seen binary search already in this chapter multiple times, but let's go through one final example.

Let's search for 13 in the following tree:

::

           ____10____
          /          \
       __6__         19
      /     \       /  \
     3       9     13   25
    / \     /     /  \    \
   2   5   7     11  14    30

#. Check the first node, 10. 13 is greater than 10 so go to its right child, 19.
#. 13 is less than 19, so go to the left child of 19, which is 13.
#. 13 is the element we are searching for, so the algorithm terminates here.

The search operation on a BST will involve at most *h* comparisons, where *h* is the height of the tree. For a balanced tree, this means that search is *O(log n)*.

Insert
^^^^^^

Let's take the example from above and add a couple of new values to it.

::

           ____10____
          /          \
       __6__         19
      /     \       /  \
     3       9     13   25
    / \     /     /  \    \
   2   5   7     11  14    30

First lets add a new largest value: 31. In order to maintain the ordering structure of a BST, we must be careful where we insert this new value. 

The insertion algorithm is as follows:

#. Compare the new value to the root node. If it is larger, move to the right subtree. If it is small, move to the left subtree.
#. Carry out step 1 on the root of the subtree until we reach a node with no left/right child. Add the new value to the left or right of this node, based on how it compares.

To insert 31 into the tree, we start at the root element, 10. 31 > 10 so we move to the right subtree, with 19 as the root. We continue this process until we reach 30. Since 31 > 30 and 30 does NOT have a right child, we insert 31 here.

::

           ____10____
          /          \
       __6__         19
      /     \       /  \
     3       9     13   25
    / \     /     /  \    \
   2   5   7     11  14    30
                             \
                              31

Lets see another example. Lets add the value 4 to our new BST.

::

           ____10____
          /          \
       __6__         19
      /     \       /  \
     3       9     13   25
    / \     /     /  \    \
   2   5   7     11  14    30
      /                      \
     4                        31

Carry out the algorithm step-by-step for yourself to verify our work. It is also easy to verify that our new tree is still BST, based on the algorithm that we used.

Like search, insertion will take at most *h* operations, where *h* is the height of the tree. For a balanced tree, this means that insertion is *O(log n)*.

Remove
^^^^^^

Remove is similar to search it that first must find the element in the tree, and then remove it. 

Let's remove 11 from the final tree in the previous section. This gives us:

::

           ____10____
          /          \
       __6__         19
      /     \       /  \
     3       9     13   25
    / \     /        \    \
   2   5   7         14    30
      /                      \
     4                        31

This was fairly simple. We first had to find 11, which took 4 steps. Then we simply removed it. Note that 11 was a **leaf** node. In other words, it had no children. Removing a node with children takes a bit more work.

Let's try removing 5, which has a child node.

::

           ____10____
          /          \
       __6__         19
      /     \       /  \
     2       9     13   25
      \     /        \    \
       4   7         14    30
   
Something interested happened. 5's left child took the place of 5. When deleting a node that has only one child, replacing it with its child is an easy way to keep the BST property.

To remove a node that has two children, it becomes more complicated. 

Let's consider the case of removing 19, which has two children. The rule for this scenario is:

- Replace the node with its **in-order successor**, or
- Replace the node with its **in-order predecessor**.

The in-order successor of a node is the smallest node in the entire tree that is still larger than the node in question. In other words, if all of the elements were in an ordered list, the in-order successor is the element that would *immediately* follow the element in question. A similar definition applies to in-order predecessor.

Replace 19 with it's in-order successor, 25, gives us this tree:

::

           ____10____
          /          \
       __6__         25
      /     \       /  \
     2       9     13   30
      \     /     /  \    
       5   7     11  14   
      /         /    /       
     4         10   13  

As with insert, remove is a *destructive* operation. This means it can result in an unbalanced tree. An actual implementation of a BST would include logic to re-balance a tree after each insertion or removal.
