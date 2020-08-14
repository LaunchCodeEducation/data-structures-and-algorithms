Binary Search
=============

Sort Revisited
--------------

In the last chapter you learned about the insertion sort algorithm. Sorting algorithms are very popular
algorithms for applying algorithm analysis. One reason is that for sorted lists, some sorting algorithms have *O(log n)* runtime, which is one of the most performant big-O values. 

There are several sorting algorithms that are best-suited for different applications. We'll explore these in more detail in the next chapter. In most examples, we will work with lists of integers. However, *any* data type can be sorted given a way to compare elements of the give type. We will learn about this in detail in the next chapter.

For now, you can think of list of integers when we discuss sorted lists. And when we refer to a sorted collection, you can assume it has been sorted using something like insertion sort. 

Simple Search
-------------

In the previous chapter, we discussed **simple search**, though we didn't give it that label. Simple search is a *naive* search algorithm:

#. Loop through a list.
#. For each element, compare it to the element we are searching for. If they are equal, we found it and can return. Otherwise, continue to the next element.
#. If we reach the end of the list without finding a match, the search term is not in the list.

This algorithm is *O(n)*, because in the worst case we have to look at every element in the list. It also works whether or not the list is sorted. 

Binary Search
-------------

.. index:: ! binary search

We can achieve *O(log n)* search time with **binary search**. Since *log n < n* for large values of *n*, this will be a much more efficient alternative to simple search.

So how does it work?

Binary Search Algorithm
^^^^^^^^^^^^^^^^^^^^^^^

Binary search employs a split-the-middle approach. The basic outline of the algorithm is this:

#. Start with a sorted list of items
#. Compare the search value with the item in the *middle* of the list

   #. If the two values are equal, we've found it! 
   #. If the list has only 1 item, and the values are not equal, then the search value is not in the list
   #. Else...

      #. If the search value is *less* than the middle value, apply the algorithm to the *left* half of the sorted list
      #. If the search value is *greater* than the middle value, apply the algorithm to the *right* half of the sorted list

In less rigorous language, this algorithm can be described this way:

#. Compare the search value to the middle item in the list

   #. If they're equal, you've found it!
   #. If they're not equal, and there's only one item in the list, then the search value is not in the list
   #. Otherwise, look in the left or right half of the list, depending on whether the search value is less or greater than the middle value

Notice how this algorithm depends on the list being sorted: If the list is NOT sorted, we can't reliably make the decision to search to the right or left of the middle item.

Binary Search Examples
^^^^^^^^^^^^^^^^^^^^^^

Let's see how binary search works by exploring a specific example. We will apply the algorithm to find a couple of different values in the list:

::

   (1, 2, 3, 4, 8, 9, 10, 14, 18, 20, 30)

Search Value: 18
################

**Step 1:** The list has 11 items, so the middle item is at index 5 (i.e. the 6th item). So the middle value is 9. Since 9 < 18, we cut the list down to:

::

   (10, 14, 18, 20, 30)

**Step 2:** This new, smaller list has 5 items, and the middle value is 18. This is our search value, so we are done. It took us 2 steps to find the search value in the list.

Search Value: 1
###############

**Step 1:** As before, the middle item is 9. Since 1 < 9, we cut the list down to:

::

   (1, 2, 3, 4, 8)

**Step 2:** The middle value of the new list is 3. Since 1 < 3, we cut the list down to:

::

   (1, 2)

**Step 3:**. In this case, the list has an even number of elements, so it's not clear what the middle element is. Typically, we use *length / 2* to calculate the middle index. In this case, this gives us a middle index of 1. The item at index 1 is 2. Since 1 < 2, we cut the list down to:

::

   (1)

**Step 4:** There is only one element left in the list, and it's our search value. So we are done! We found 1 in the list in 4 steps.

This is an example of the worst-case scenario for a collection of size 11. Let's discuss the performance of binary search in more detail.

Binary Search Performance
^^^^^^^^^^^^^^^^^^^^^^^^^

.. _binary-search-perf:

So for a collection with a length of 11, the best-case performance is 1
operation, and the worst-case performance is 4 operations. That's certainly
more better than *O(n)* (where the best case would be 1, and the worst case
would be 11).

A binary search gives us a much more performant way of finding a value in a
collection. Let's figure out the big-O value for binary search. To do this, we observe that for a list of size *n*, the worst-case scenario is that the item either isn't in the list, or that we follow the algorithm long enough to get down to a list of size 1. So the question becomes, how many times do we have to cut a list of size *n* in half to get down to a list of size 1? 

To answer this question, it's a bit easier to think of it this way: How many times do we have to *double* the size of a list of size 1 to get up to size 9? If you think about it for a moment, you'll see that is equivalent to the first question. In other words, we need to figure out the value *x* such that:

.. raw:: html

   <div style="text-align:center;"><em>2<sup>x</sup> = n</em></div>

Taking the base-2 logarithm of both sides gives us |log_2 n|. Therefore, binary search is *O(log n)*.

Let's apply this to our example above. There, the length of the list was 11, and |log_2 11| is 3.4594. It
took 4 steps in the worst case scenario!

So now we have a handy equation for estimating how many operations a binary
search would take on any size collection in the worst-case.

- Collection length of 10 -> |log_2 10| -> 3.3219
- Collection length of 100 -> |log_2 100| -> 6.6428
- Collection length of 10000000 -> |log_2 10000000| -> 26.5754

You can see how increasing the size even drastically doesn't increase the
number of operations. Binary search works so well because you can *double* the size of a list
while only increasing the worst-case runtime for search by 1 operation. A
binary search's worst-case performance will always be better than a simple
search's worst-case performance when the collection size is the same.

Since binary search is so powerful a unique data structure has been created
for it. It's essentially a data structure that is structured around splitting
segments of data in half. We will explore this new structure further in the
next section.

Check Your Understanding
------------------------

.. admonition:: Question

   **True/False:** Binary search only works in conjunction with insertion sort.

.. and: False, any sort is fine

.. admonition:: Question

   Suppose you have a list of size *n*, which then grows to size *4n*. How many more operations will binary search take now, in the worst case?

.. ans: 2

.. |log_2 11| raw:: html

   <em>log<sub>2</sub> 11</em>

.. |log_2 10| raw:: html

   <em>log<sub>2</sub> 10</em>

.. |log_2 100| raw:: html

   <em>log<sub>2</sub> 100</em>

.. |log_2 10000000| raw:: html

   <em>log<sub>2</sub> 10000000</em>

.. |log_2 n| raw:: html

   <em>x = log<sub>2</sub> n</em>