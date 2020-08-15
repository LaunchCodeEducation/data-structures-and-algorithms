Linked Lists
============

.. index:: ! linked list

A **linked list** is an ordered data structure built out of units called nodes. Unlike the ordered data structures we are used to, such as lists and arrays, linked lists are NOT indexed. In other words, you can not look up an item at a specific place in the structure using its index.

Nodes
-----

.. index:: ! node

A **node** is an object that has two fields:

- A value
- A pointer to the next node in the list

This book is primarily language agnostic, but we will refer to a node as an object. This makes sense for most languages, but for languages without objects (e.g. C) you can substitute any similar structure. 

We visualize a node like this:

.. image:: figures/node.png
   :alt: a node with a value and next pointer
   :width: 500px

If a node is not linked to a next node, it's ``next`` field is ``null``.

And we visualize a chain of connected nodes like this:

.. image:: figures/nodes.png
   :alt: A chain of nodes

.. index:: 
   single:linked list; head

More formally, a linked list value is a reference, or pointer, to the first node in the list. This first node is the **head** of the list. From the head, we may access all other nodes by following the chain of nodes, using the ``next`` references.

.. index::
   single: linked list;traversal

.. admonition:: Example

   Here's what it looks like, in pseudocode, to print out all of the values in a linked list, ``list``. Recall that the ``list`` variable is just a pointer to the head node.

   ::

      current_node = list

      while current_node is not null
         print current_node.value
         current_node = current_node.next

   The loop terminates when we reach a node with ``next`` value that is ``null``. The process of iterating across an entire linked list is called **traversal**. 

Operations
----------

Let's look at some basic operations on linked lists, as well as their big-O runtimes.

Search
^^^^^^

Consider the operation of searching for a specific value in a linked list. Similarly to built-in list types, we must traverse the entire data structure in order, checking each item in the linked list to see if it matches.

::

   function search(list, val)

      current_node = list

      while current_node is not null

         // the value was found
         if current_node.value == val
            return current_node
         
         current_node = current_node.next

      // the value was not found
      return null

In the worst-case scenario, this algorithm looks at every node in the list. Therefore, search for linked lists is *O(n)*.

Insertion at End of List
^^^^^^^^^^^^^^^^^^^^^^^^

.. _linked-list-append:

The algorithm for appending a new value to the end of a linked list is:

::

   function append(list, val)

      current_node = list

      // walk through the list to find the last node
      while current_node.next is not null
         current_node = current_node.next

      // create a new node
      new_node = node()
      new_node.value = val

      // attach the node to the end of the list
      current_node.next = new_node

This operation is *O(n)* since we must traverse the entire list.

Notice that this is much less efficient than appending an item to a regular list type, where we have access to properties like indexes and list length.

Deletion
^^^^^^^^

Deletion can be approached in a few different ways. We could think about deleting a *value* from the list, or we could look at deleting a given *node* from the list. Either approach is valid, but we will look at the algorithm for deleting a given node.

.. _linked-list-delete:

::

   function delete(list, node)

      current_node = list

      // walk through the list until we get to the given node
      while current_node.next is not node
         current_node = current_node.next

      // now, current_node.next is the node to delete
      current_node.next = node.next

To remove the node, we have its predecessor point to the node following it. This detaches it from the list. As with the other operations we have looked at, this is *O(n)*.

Applications and Notes
----------------------

Linked list operations are slower than operations for fixed-length arrays since they don't allow for indexing. In addition, they take up more memory, since each node must store a pointer to it's next node. The *advantage* of linked lists over fixed-length arrays is that they have variable length. For languages like C, this can be very useful. And for applications where the length of the linked list is expected to be small, the slower runtime of its operations turns out not to be a big deal, as we'll see in the next section.

Compared to built-in list types in high-level languages, linked lists are much more memory efficient. Built-in list types dedicate a lot of time and memory to managing the list state and providing indexing. 

The linked list structure outlined in this section is only one approach to building a linked list. It is referred to as a **singly linked list**, because each node has only one pointer, connecting it to its successor. There is also a widely used **doubly linked list** approach, in which each node has a pointer to its next *and* previous nodes. You can `read more about doubly linked lists <https://en.wikipedia.org/wiki/Linked_list#Doubly_linked_list>`_ if you're curious. 

.. admonition:: Fun Fact

   The linked list implementations provide by `Java <https://docs.oracle.com/javase/7/docs/api/java/util/LinkedList.html>`_ and `C# <https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic.linkedlist-1?view=netcore-3.1>`_ are both doubly linked lists.

You are unlikely to ever need to write your own linked list implementation; most high-level languages provide one for you. However, a basic understanding of how linked lists work will help you work with code that uses this particular data type, and to understand how its operations may affect the runtime of an application.

Check Your Understanding
------------------------

.. admonition:: Question

   big-O of:

   - insertion at beginning
   - insertion in the middle 

.. admonition:: Question

   Write the algorithm to delete a given value from a linked list, in pseudocode. You can assume that the value exists only once in the linked list.