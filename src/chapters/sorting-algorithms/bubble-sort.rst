Bubble Sort
===========

.. index:: ! bubble sort

.. index::
   :single: sort;in place


**Bubble sort** works by swapping adjacent elements in a list whenever they are in the wrong order. It sorts a list **in place**, which means that it works by moving elements within the unsorted list. This is in contrast to insertion sort, which creates a new list to hold the sorted elements. For this reason, bubble sort is more memory-efficient than insertion sort and other sorts that result in a new list being created.

The Algorithm
-------------

Here is the bubble sort algorithm:

#. Loop through the list

   #. Moving from left to right, compare adjacent items in the list. Swap the pair if they are out of order.
   #. Continue this process---starting at the beginning of the list and comparing pairs---until a full pass of the list occurs without any swaps.

In psuedocode, bubble sort can be written as follows.

::

   is_sorted = false
   while not is_sorted

      for i in 0..list.length-1

         // assume the list is sorted until we find a pair that's out of order
         is_sorted = true

         // if items are out of order, swap them
         if list[i] > list[i+1]
            temp = list[i+1]
            list[i+1] = list[i]
            list[i] = temp
            is_sorted = false

At the end of each iteration of the ``while`` loop, at least one additional element is in its correct, sorted location. For example, after the first iteration, the largest element in the list will be in the last position. After the second iteration, the second-largest element will be in the next-to-last position. This observation is how bubble sort got its name: With each iteration, an additional element "bubbles up" to its correct position.

An Example
----------

Let's look at an example. We will sort the following list using bubble sort:

::

   (7, 5, 1, 3, 8)

We'll break down the process step-by-step. At each step, the two items being compared are bolded.

**Pass 1**

(**7**, **5**, 1, 3, 8) -> (5, 7, 1, 3, 8) swap, since 7 > 5

(5, **7**, **1**, 3, 8) -> (5, 1, 7, 3, 8) swap, since 7 > 1

(5, 1, **7**, **3**, 8) -> (5, 1, 3, 7, 8) swap, since 7 > 3

(5, 1, 3, **7**, **8**) -> (5, 1, 3, 7, 8) no swap, since 7 < 8

**Pass 2**

(**5**, **1**, 3, 7, 8) -> (1, 5, 3, 7, 8) swap, since 5 > 1

(1, **5**, **3**, 7, 8) -> (1, 3, 5, 7, 8) swap, since 5 > 3

(1, 3, **5**, **7**, 8) -> (1, 3, 5, 7, 8) no swap, since 5 < 7

(1, 3, 5, **7**, **8**) -> (1, 3, 5, 7, 8) no swap, since 7 < 8

**Pass 3**

(**1**, **3**, 5, 7, 8) -> (1, 3, 5, 7, 8) no swap

(1, **3**, **5**, 7, 8) -> (1, 3, 5, 7, 8) no swap

(1, 3, **5**, **7**, 8) -> (1, 3, 5, 7, 8) no swap

(1, 3, 5, **7**, **8**) -> (1, 3, 5, 7, 8) no swap

After the third pass, the list is in order. Note that the list was actually in order after the *second* pass. However, the algorithm doesn't know this. It needs an additional pass to confirm the correct ordering of the elements.

Big-O Analysis
--------------

To determine the worst-case runtime, let's first look at the inner ``for`` loop. This loop always goes through the entire list, carrying out *n-1* comparisons for a list of length *n*. 

The number of iterations of the outer, ``while`` loop can vary depending on the initial ordering of elements. So what's the worst case? We noted above that after each iteration of the ``while`` loop *at least* one more element is in its correct location. So the worst-case scenario occurs when *only* one additional element is correctly placed after each iteration. This occurs with a list that is in reverse order:

::

   (n, n-1, ... 2, 1)

In this situation, the ``while`` loop executes *n-1* times also. So the worst-case number of comparisons is |n-1^2|. Due to big-O reduction rules, we see that bubble sort is |On^2|.

Bubble sort is NOT an efficient sorting algorithm. It is, however, one of the more intuitive sorting algorithms to understand. For this reason, it is frequently taught in courses on algorithms. In the next section, we will learn about an *efficient* sorting algorithm, merge sort.


.. |n-1^2| raw:: html

   <em>(n-1)<sup>2</sup> = n<sup>2</sup> - 2n + 1</em>

.. |On^2| raw:: html

   <em>O(n<sup>2</sup>)</em>