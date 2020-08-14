Introduction to Sorting Algorithms
==================================

In the first chapter of this book we learned about :ref:`insertion sort <insertion-sort>`, which has |On^2| runtime. The algorithm works by creating a new, empty array and adding elements from the unsorted array one at a time so that the new array is always sorted. The implementation requires nested loops, each of which may execute *n* times, where *n* is the number of elements being sorted.

This chapter introduces two additional sorting algorithms: merge sort and bubble sort. The are `many, many sorting algorithms <https://en.wikipedia.org/wiki/Sorting_algorithm>`_ out there. Bubble sort and merge sort are two of the most commonly learned sorts. Each sorting algorithm has its own advantages, and often there will be a preferred choice given the application and characteristics of the data being sorted.

Once you gain a feel for a few sorting algorithms, it is straightforward to pick up others. This chapter is intended to lead you to this level of comfort and understanding.

Comparisons
-----------

.. index:: ! comparison

So far, we have only provided sorting examples for lists of integers. However, *any* data type can be sorted, given a way to compare two elements of the given type. More formally, we can think of this comparison as a ``compareTo`` function that takes two arguments and returns a number, such that:

- If ``compareTo(a, b)`` equals 0, then ``a`` and ``b`` are considered *equal*
- If ``compareTo(a, b)`` is less than 0 if ``a`` is considered to be *less than* ``b``
- If ``compareTo(a, b)`` is greater than 0 if ``a`` is considered to be *greater than* ``b``

This definition of ``compareTo`` is abstract, and can be difficult to grasp at first. However, consider the example where ``compareTo`` takes integer arguments, and is defined to be:

::

   function compareTo(a, b)
      return a - b

This function satisfies all three of the conditions stated above. It also aligns with our regular notions of numeric comparisons:

- If ``a`` and ``b`` are the same, then ``compareTo(a, b)`` is 0
- If ``a`` is less than ``b``, then ``compareTo(a, b)`` is less than 0
- If ``a`` is greater than ``b``, then ``compareTo(a, b)`` is greater than 0

In practice, when needing to sort non-numeric data types---such as strings or objects---you will need to implement a comparison function for that type. 

.. admonition:: Example

   A common approach to sorting strings alphabetically is to use the `ASCII values <https://www.asciitable.com/>`_ of the characters in the string. These values provide a numeric analog for each letter that corresponds to the natural ordering of the alphabet. 

   Note that to compare two letters by comparing their ASCII values, you'll typically want to first convert them to lowercase, since the lower and uppercase versions of a letter have different ASCII values.

For the sake of simplicity, we will continue to use integers in our sorting examples. But keep in mind that sorting has much broader applicability in practice.

.. |On^2| raw:: html

   <em>O(n<sup>2</sup>)</em>