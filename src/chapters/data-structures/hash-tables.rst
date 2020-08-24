Hash Tables
===========

You just learned about linked lists, which have similarities to and differences with fixed-length arrays and built-in variable-length list types. 

This section explores hash tables, which have similarities to built-in key/value data structures such as maps and dictionaries.

Abstract Structure
------------------

.. index::
   single: hash; table

A **hash table** (or hash map) is an associative array data structure, which means it maps keys to values. There are multiple approaches to building a hash table. We will explore one approach, and point you toward information on other approaches. All hash tables, however, use hash functions as a key part of their structure.

Hash Functions
^^^^^^^^^^^^^^

.. index::
   single: hash; function

Each hash table has a hash function. A **hash function** is a function that assigns a value, or index, to a value. This index determines which **bucket** the value should be stored in.

For a given value, ``x``, the index returned by the hash function is called its **hash value**. Ideally, hash values are unique. In other words, if ``x`` and ``y`` are not equal, then their hash values are different. In practice, however, this doesn't usually happen. We'll explore the ramifications of this below.

Here's how hash functions are used. To insert a value, ``x``, into a hash table with hash function ``h``, compute its hash value, ``h(x)``. Then put ``x`` into the bucket labelled ``h(x)``.

.. image:: figures/buckets.png

.. index::
   single: hash; value

Similarly, if we want to retrieve a value from a hash table, we compute ``h(x)`` and then use this hash value to determine which bucket to look in. In key/value language, the hash value is the key, and the element itself is the value.

The choice of hash function is typically left to the developer using the hash table, and is a *critical* component to ensure that the hash table is efficient, as we will see below.

.. admonition:: Example

   Suppose we wanted to store a bunch of student records in a hash table. We could set up 26 buckets, one for each letter of the alphabet. We could then have our hash function return the first letter of each student's last name. This would group students together into buckets based on their last name.

The abstract definition of a hash table can be hard to grasp, so let's look at one approach to implementing a hash table.

Array-Based Implementation
--------------------------

One common hash table approach uses fixed-length arrays. To demonstrate this approach, we'll consider storing student records, as in the example above.

A hash table can be set up to use a fixed-length array, where the hash function determines the index in the array where a given item should be stored. For our student records, let's use an array of length 26. Our hash function, ``h``, will return numeric index of a student's last initial.

.. admonition:: Example

   A student named Jane Adams would have hash value 0. A student named Tim Zane would have hash value 25.

Here's what our hash table looks like, with a few students stored in it:

.. image:: figures/student-hashing.png

To look up a student's record, we compute their hash value and look at that location in the array. 

This structure has one big problem though, which is that two different students can have the same hash value. Where would we put Johnny Appleseed in the above hash table? 

Collisions 
----------

.. index:: ! collision

When two different values have the same hash value, it is known as a **collision**. Ideally, our hash function would provide a unique hash value for every item in practice, however, this is very difficult to achieve. There are many approaches to dealing with collisions, and we'll look at one of them now.

Separate Chaining
^^^^^^^^^^^^^^^^^

.. index:: ! separate chaining

One technique for handling collisions is **separate chaining**. With this technique, instead of storing values in the array, we store linked lists. Then, each spot in the array corresponds to the collection of values that have the same hash value. And since linked lists can grow as needed, our hash table can store as many items as needed. 

A student hash table with several collisions and using separate chaining looks like this:

.. image:: figures/separate-chaining.png

To add a new student to the table, we compute their hash value, and then append them to the linked list at the given index. Similarly, to search for a student in the table, we compute their hash value and search for them in the given linked list. 

Operations
----------

Let's look at a few basic operations on hash tables using separate chaining, along with their big-O runtimes. In doing so, we will make two important assumptions:

#. Collisions are *very, very rare*
#. In addition to assumption 1, collisions are so rare that we can assume each linked list has no more than *N* items, where *N* is some fixed integer.

Given our simplistic student record example, this may seem like a big assumption. In practice, however, it isn't that difficult to achieve these requirements by carefully setting up the hash table. It's typically possible to choose the array length and hash function so that these assumptions hold. If you don't believe us, you can `read more on the topic <https://en.wikipedia.org/wiki/Hash_table>`_. Some very smart computer scientists have devised methods to achieve these assumptions in most cases. 

Okay, with these assumptions on collisions and the length of our chains, we can look at operations. In the following pseudocode examples, ``table`` will be our hash table and ``h`` will be the hash function. This means that ``table`` is an **array** and ``h`` is a function that takes values and returns values in the range 0...``array.length``.

.. admonition:: Note

   A common practice used to ensure that a hash function doesn't return a value past the end of the array is to use the modulo operator. So, for example, of ``f`` is a function that takes a value and returns an integer, possibly well outside of the array bounds, we can make a hash function:

   .. raw:: html

      <div style="text-align:center;">h(x) = f(x) % array.length</div>

   This ensures that all hash values will be within the array bounds.

Search, Insertion, and Deletion
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The algorithm to find a value in a hash table is:

::

   function search(table, h, val)

      hash_val = h(val)
      list = table[hash_val]
      return list_search(list, val)

Here, ``list_search`` is a function to search for a value in a linked list, as demonstrated in the last section.

What's the big-O runtime of this algorithm? The first two operations of this function run in *constant* time. The third operation, as we saw in the last section is *O(n)*, where *n* is the number of items in the linked list at the given spot in the hash table. However, due to our assumptions above, *this value is fixed*. In other words, we have *constant* big-O runtime! 

Searching a hash table is *O(1)*. Hash tables are very, very efficient for this operation. It's not hard to see that insertion and deletion will also be *O(1)*. If you're not convinced, we encourage you to write out the pseudocde for these operations and determine the big-O value yourself.

Given the assumptions above, 

.. admonition:: Note

   You will often see it stated that these operations are *O(1)*. Always remember that this is only the case if we have a carefully chosen hash function and array size. 

   With our simplistic student example above (with a simple has function and a small array), it's easy to see that these big-O values don't apply. We could have lots and lots of students with the same last initial, all stored in the same linked list.


Applications and Notes
----------------------

Hash tables are optimized for fast lookup/search. Thus, they are often used for things like caching data or database indexing. They are also often used as the underlying structure for built-in map/dictionary data structures.

The downside of hash tables is that to achieve *O(1)* efficiency, it is usually necessary to use very large arrays. This requires a large amount of memory. In fact, in most hash table implementations it is common for a large number (up to 25-50%) of the array slots to be empty! This means that such hash tables require a lot of unused memory in order to achieve such efficiency. 

As mentioned, there are many ways to set up a hash table. The main options involve the choice of hash function and the technique used to handle collisions. We encourage you to spend some time `reading more about these aspects of hash tables <https://en.wikipedia.org/wiki/Hash_table>`_.