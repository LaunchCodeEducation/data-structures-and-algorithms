Merge Sort
==========

In the last section, we learned about bubble sort. That algorithm has worst-case runtime |On^2|, which is very slow for large data sets. 

We will now introduce merge sort, which is an **efficient sort**. An efficient sort is one that has *O(n log n)* runtime. Since *log n* is much smaller than *n* for large values of *n*, this is much more efficient than |On^2|.

The Algorithm
-------------

**Merge sort** uses a divide-and-conquer approach. The basic process is:

#. Break the list into *n* lists of size 1. A list of size 1 is automatically sorted.
#. *Merge* pairs of smaller lists so that the resulting merged lists are sorted.
#. Continue step 2 until there is only 1 list. This list is sorted.

To write this in code, or pseudocode, it is easier to think of this algorithm `recursively <https://education.launchcode.org/intro-to-professional-web-dev/chapters/more-on-functions/recursion.html>`_. 

#. Break the list into two halves.
#. Sort the two halves.
#. Merge the halves together.

Step 2 here is the recursive step. It results in a nested process of halving of lists until lists of length 1 are created. These lists are sorted automatically, so then the recursive process begins returning up the call stack, merging lists as it does so. 

To write merge sort in pseudocode, it will be helpful to have a ``merge`` function that takes two sorted lists and returns a single sorted list, the result of combining the two.

::

   function merge(a, b)

      merged = []
      i, j = 0

      while i < a.length and j < b.length
         if a[i] < b[j]
            merged[i+j] = a[i]
            i++
         else
            merged[i+j] = b[j]
            j++

      // a has been fully merged, but there are still elements of b to merge
      if i == a.length
         merged.append(b[j..b.length-1])
      // b has been fully merged, but there are still elements of a to merge
      else
         merged.append(a[i..a.length-1])


With this helper function in-hand, merge sort looks like this:

::

   function merge_sort(list)

      // base case for recursion
      if list.length == 1
         return list

      middle_idx = floor(list.length/2)
      a = list[0..middle_idx-1]
      b = list[middle_idx..list.length-1]
      left = merge_sort(a)
      right = merge_sort(b)

      return merge(left, right)

Note that ``floor`` is a function that returns the integer part of a positive float value. Most languages have such a function built-in, and if not, one can easily be written.

An Example
----------

The figure below shows how recursive merge sort works, step-by-step. The red arrows signify recursive calls to ``merge_sort`` on the halved lists. The green arrows signify calls to ``merge`` on sorted lists.

.. figure:: figures/merge-sort-example.png
   :alt: A tree-like diagram showing a recursive merge sort example
   :width: 600px

   Image via Wikipedia is in the public domain

Notice how at each step in the top half of the diagram, a list is broken down to smaller lists. This breaking-down process continues until we arrive at lists of size 1. From there, we start merging the pairs of sorted lists, one level at a time. 

Big-O Analysis
--------------

To understand the worst-case runtime for merge sort, we need to consider the big-O values of the ``merge`` and ``merge_sort`` recursive calls separately.

In the algorithm above, ``merge(a, b)`` has *a.length + b.length* operations. Looking at a single level in the lower-half of the example diagram above, we see that adding up all of these operations for each of the calls to ``merge`` at a given level results in *n* operations. For example, the second merge step combines the following pairs:

- ``(27, 38)`` and ``(3, 43)`` -> 4 operations to merge
- ``(9, 82)`` and ``(10)`` -> 3 operations to merge

So the total number of operations to carry out *both* merges is 7, which is the size of our original list. The same is true at every other level.

The overall number of operations will then be *n* times the number of recursive calls to ``merge_sort``, since each recursive call results in ``n`` operations to merge smaller lists. Since each recursive call *halves* a list, we need to figure out how many times we must carry out this halving operation before reaching lists of length 1. This is the *exact same* situation that we encountered when :ref:`calculating the big-O value for binary search <binary-search-perf>`!

Therefore, we see that there will be *log n* recursive steps, and so overall merge sort is *O(n log n)*.

.. |On^2| raw:: html

   <em>O(n<sup>2</sup>)</em>