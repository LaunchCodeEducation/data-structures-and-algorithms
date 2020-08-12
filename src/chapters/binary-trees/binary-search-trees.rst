Binary Search Tree
===================

.. index:: ! binary search tree

A binary tree that follows the ordering rules explored at the end of the previous section is a **binary search tree**. 

To recall, a binary search tree (BST) has these properties:

#. For every element in the tree, its left subtree only contains elements less than or equal to it.
#. For every element in the tree, its right subtree only contains elements greater than or equal to it.

Here's an example of a BST:

::

       __7__
      /     \
     3       15
    / \     /  \
   1   3   8    17

Convert Ordered List to Binary Search Tree
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Let's convert the ordered list from the Binary Search section into a BST.

Recall that this list is: (1, 2, 3, 4, 8, 9, 10, 14, 18, 20, 30)

The algorithm to convert an ordered list to a BST is:

#. Set the middle element in the list to be the root node.
#. If there is more than 1 element in the list:
   #. Take the sublist of all elements smaller than (i.e. to the left of) the middle element and recursively build the root's left subtree.
   #. Take the sublist of all elements greater than (i.e. to the right of) the middle element and recursively build the root's right subtree.

This algorithm gives us the following BST:

::

         ____9______
        /           \
       3             18
      / \           /  \
     2   4         14   30
    /     \       /    /
   1       8     10   20

Balanced Trees
^^^^^^^^^^^^^^

.. index:: ! height

The **height** of a binary tree is the number of levels that it contains. A **balanced** binary tree has the additional property that its height is a small as possible. Conceptually, this means that its elements are evenly spread across the tree so as to create the fewest number of levels possible. 

It turns out that the height of a balanced tree is roughly *log n*, where *n* is the number of items in the tree. More specifically, the height will be the next largest integer to *log n*.  

.. admonition:: Note

   The rigorous definition of a balanced binary tree is much more complicated and very mathy. If you're into that kind of thing, we encourage you to `read up on it! <https://en.wikipedia.org/wiki/Self-balancing_binary_search_tree>`_

The tree we created in the section above is balanced due to the way in which we created it. However, not every BST will be balanced. Consider this example:

::

         4
        /
       3
      /
     2
    /
   1

This is certainly a BST by our definition. However, it is very unbalanced. A balanced version of this tree can be created by putting the elements in a sorted list, and applying the algorithm we learned above:

::

       3
      / \
     2   4
    /
   1

In this case, the difference is only 1 level. However, for trees with large numbers of elements, the difference in height between a balanced and unbalanced tree can be very large. 

Working with balanced binary search trees is important because most tree operations are *O(h)*, where *h* is the height of the tree. For a balanced tree, *h* is close to *log n*, but for an unbalanced tree *h* can be as big as *n*. This means that the runtime of various operations will be *much* faster for balanced trees.

In the next section of the chapter we will look at some binary search tree operations, such as search and insert.