Binary Trees
============

You likely have used some form of ordered collection (such as an array or list) to meet the needs of our various data requirements. Lists are great. They allow us to collect data together and reference items by their index. The majority of lists are unsorted, but in many cases a language offers a sort method.

Lists are fantastic for collecting together data, but to search for a specific piece of data in an unordered list you typically would use a simple search, which is *O(n)*. Lists are less performant the larger they get.

Today we will be introducing a new data structure that will allow us to easily use a binary search easily with our new data structure the binary tree.

Binary Tree
-----------

Before we can learn about a binary search tree---which is the unique data
structure that works with binary search---we have to learn about the data
structure a binary search tree is based on, the binary tree.

.. index:: ! binary tree

A **binary tree** is a tree-like data structure in which any node can have up to
two branches connecting it to additional nodes. When visualized the data structure looks
like a tree.

::

       __A__
      /     \
     B       C
    / \     / \
   D   E   F   G

The root item, A, has two branches down to b and c. B has two branches down to D and E. C has
two branches to F and G. If we were to add more elements to this data
structure we would put them as new nodes connected by branches to either D, E,
F, or G.

.. index:: ! subtree

A **subtree** of a binary tree consists of one element and all of it's children. For example, the subtree in the above example with root node B is:

::

     B   
    / \  
   D   E 

Not every binary tree will look perfect, with every
node having two children nodes. To be a binary tree, it simply needs to be the case that no node has more than 2 children.

::

       _______A__
      /          \
     B_____       C__
    /      \     /   \
   D        E   F     G
           /         / \
          H         I   J
        /
       K

This is an example of a valid binary tree. None of the nodes have more than
two children, and not every node has the same number of children. Some nodes
have 2, 1, or even 0 children. 

The child's position from the parent node is important.
A has two children (B and C). We would call B the left child, and C the right
child. B has two children (D and E). We would call D the left child of B, and
E the right child of B.

Binary trees are almost always used in Computer Science when it comes to
sorting or searching. It is very rare you would need to code a binary tree
yourself, but knowing how they work is beneficial in understanding how certain
sorting and searching algorithms are performed.

One of the main ways lists and binary trees are different is in the indexing of values for arrays. With an array you can access the first value by accessing index 0. You can use the same practice to access any value in the array, you simply need to know it's position. In a binary tree, you cannot access a value by knowing it's position. You find values by looking at the children of a node, and keep checking children until you find the value you are looking for. So how the data structure is used is quite different. We will see examples of how this is used in future sections.

Since you cannot access an element by it's index, and you must search through child relationships, this makes a binary tree a recursive structure.

Root Node
^^^^^^^^^

.. index:: ! root node

In a binary tree the **root node** is the first element of our data structure.

In the example list ``[5, 19, 2, 4]`` our first element is 5.

In the example binary tree

::

       5
      / \
    19   2
   /
  4

5 is our root node. The element at the top of our tree is always considered the root node of the binary tree.

So what are the remaining nodes called?

Child Nodes
^^^^^^^^^^^

.. index:: ! child node

The next level down from our root node would be the child nodes of our root node.

So in the example above of

::

       5
      / \
    19   2
   /
  4

5 is our root node, and it has two children: 19 and 2.

.. index::
   :single: child;left
   :single: child;right

Even though both 19 and 2 are considered child nodes of 5, we may want to distinguish between the children so we have further classifications: **left child** and **right child**.

In the example above, 19 is the left child of 5, and 2 is the right child of 5.

Depth
^^^^^

.. index:: ! depth

The final term you should learn for binary tree is depth. **Depth** refers to the number of levels in a given binary tree.

::

       5
      / \
    19   2
   /
  4


With the example we have used throughout this section, we can see three levels to our tree. 5 is the first level, 19 and 2 are at the second level, and 4 is at the third level. The depth of this tree is 3.

Converting a List to a Binary Tree
----------------------------------

As a final example let's turn the list we saw from the last section into a binary tree.
Recall that the list is: (1, 2, 3, 4, 8, 9, 10, 14, 18, 20, 30).

Our algorithm to create a binary tree from this list will be:

#. Make the first element in the list the root.
#. Looping through the remaining items in the list, fill out the tree one level at a time, moving left to right.

This algorithm gives us the tree:

::


             ________1__
            /           \
        ___2___          3
       /       \        / \
      4         8      9   10
     / \       / \
    14  18    20  30

.. note::

   This is a basic algorithm for turning a list into a binary tree. In future sections, you will see slightly more complex algorithms for creating a balanced binary tree from a list.

The Importance of Order
-----------------------

Binary trees are powerful because they enable fast (*O(log n)*) search, insertion, and deletion. However, these efficient operations are only possible with an *ordered* tree. With an unordered binary tree you cannot achieve *O(log n)*.

Let's take an example of finding a specific value in the binary tree we created above.

::

       5
      / \
    19   2
   /
  4

What if we are looking for the value 2? We would first check the root node 5. Does 5 equal 2? No, we need to move on. Let's check the left node of the root node, 19. Does 19 equal 2? It does not. Let's check the left node of the 19, which is 4. Does 4 equal 2? Nope. Since we don't have any left nodes, let's move back up a level. 19 does not have any right nodes so, let's move up a level. 5 has a right node that is 2. Does 2 equal 2? Yes! We found our value in 4 checks, which happens to be the size of our data structure. 

From this example, we see that the worst case for search in an unordered binary tree is *O(n)*. This is nowhere near as good as a binary search *O(log n)*.

However, what if this binary tree was ordered? Let's impose an ordering condition:

#. For every element in the tree, its left subtree only contains elements less than or equal to it.
#. For every element in the tree, its right subtree only contains elements greater than or equal to it.

::

       5
      / \
    4    19
   /
  2


Now if we try to search through our binary tree, since it is ordered and follows the rule that every left child is smaller, and every right child is larger or equal to the parent node, we can easily do a binary search.

If we are looking for the value 2. We would first check the root node 5. Does 5 equal 2? No, but now we can make an informed decision. Since 2 is smaller than 5, we know that it must be to the left of 5, if it is in the tree. 

The left child of 5 is 4. Does 2 equal 4? No. Since 2 is smaller than 4, we need to check the left child again. Does 2 equal 2? Yes! We found the matching value in one less iteration than the previous check.

Imposing this order on a binary tree makes searching much easier.
