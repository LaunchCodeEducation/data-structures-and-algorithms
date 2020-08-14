.. _insertion-sort:

Insertion Sort
==============

Sorting
-------

.. index:: ! sorting

**Sorting** is the act of taking a collection of data and rearranging it into a specific order. The order can be numerical ascending, numerical descending, alphabetical, by time, and so on.

Some of the most famous algorithms are sorting algorithms. Sorting algorithms are important for many reasons, but for the purposes of this class they are primarily important because searching through *unsorted* data *always* takes *O(n)* time. 

To search for a value in unsorted data, the worst-case scenario is that the value in question is last and we have to check every single item in the collection. However, if the data is sorted you can implement different searching algorithms that are more performant than *O(n)*. We will see some of these searching algorithms in future lessons.

That being said, not all sorting algorithms are equal. A sorting algorithm comes with it's own big-O notation, making some sorting algorithms better depending on the incoming data.

Throughout this book, we will introduce a number of various sorting algorithms. We will provide information about each sort which will be helpful in deciding when it provides the best solution. Some sorting algorithms are more efficient for small sets of data, others for large sets of data. Most programming languages already have these sorting algorithms built-in as a part of their standard libraries. However, it is valuable to know how they work, and how to implement them if you need to write your own custom sorting algorithm.

Insertion Sort
--------------

.. index:: ! insertion sort

The first sorting algorithm we will be looking at is **insertion sort**. This sort can be implemented in a couple of different ways, but we will be showing examples that sort a collection of numbers in ascending order. That is to say, the smallest number will be the first element in the array, and the largest number will be the last element in the array.

.. admonition:: Example

   Given the input
   
   ::
   
      [4, 3, 8, 7, 2, 10]
      
   insertion sort will return
   
   ::
   
      [2, 3, 4, 7, 8, 10]

Insertion sort works as follows:

#. Create a new, empty array. This will eventually contain the sorted items.
#. Add the first item from the unsorted array to the new array.
#. For each other item in the unsorted array, insert the item in the new array so that the new array remains sorted.

Here is the algorithm in pseudocode:

::

   // create a new array with the first item
   sorted = [unsorted[0]]

   for i in 1..unsorted.length-1:
      for j in 0..sorted.length:

         item = unsorted[i]

         // we've reached the end of the array, so the new element 
         // is larger than all elements in sorted
         if j == sorted.length:
            append item to sorted
            break

         if item < sorted[j]:
            insert item at position j, and shift elements to the right 
            break

We see that the algorithm requires a loop nested inside of another loop, making it's big-O value |On^2|.

Let's manually step through an array to see how the insertion sort works. We will start with the example array above ``[4, 3, 8, 7, 2, 10]``, and end up with ``[2, 3, 4, 7, 8, 10]``.

::

   [4, 3, 8, 7, 2, 10] // original unsorted array

   // -- pass 1 --
   // sorted elements: [4]
   // new element: 3
   //   -- pass a --
   //   new element (3) is smaller than sorted elements [0] (4)
   //   insert new element (3) into sorted elements at sorted elements [0] (4)
   //   break out of inner loop
   
   // -- pass 2 --
   // sorted elements: [3, 4]
   // new element: 8
   //   -- pass a --
   //   new element (8) is not smaller than sorted elements[0] (3)
   //   -- pass b --
   //   new element (8) is not smaller than sorted elements[1] (4)
   //   -- end of inner loop --
   //   new element (8) was not smaller than any sorted elements so insert it at the end of sorted elements

   // -- pass 3 --
   // sorted elements: [3, 4, 8]
   // new element: 7
   //   -- pass a --
   //   new element (7) is not smaller than sorted elements[0] (3)
   //   -- pass b --
   //   new element (7) is not smaller than sorted elements[1] (4)
   //   -- pass c --
   //   new element (7) is smaller than sorted elements[2] (8)
   //   insert new element (7) into sorted elements at sorted elements[2] (8)
   //   break out of inner loop
   
   // -- pass 4 --
   // sorted elements: [3, 4, 7, 8]
   // new element: 2
   //   -- pass a --
   //   new element (2) is smaller than sorted elements[0] (3)
   //   insert new element (2) into sorted elements at sorted elements[0]
   //   break out of inner loop

   // -- pass 5 --
   // sorted elements: [2, 3, 4, 7, 8]
   // new element: 10
   //   -- pass a --
   //   new element (10) is not smaller than sorted elements[0] (2)
   //   -- pass b --
   //   new element (10) is not smaller than sorted elements[1] (3)
   //   -- pass c --
   //   new element (10) is not smaller than sorted elements[2] (4)
   //   -- pass d --
   //   new element (10) is not smaller than sorted elements[3] (7)
   //   -- pass e --
   //   new element (10) is not smaller than sorted elements[4] (8)
   //   -- end of inner loop --
   //   new element (10) was not smaller than any sorted elements so insert it at the end of sorted elements
   
   // all loops have completed
   // sorted elements: [2, 3, 4, 7, 8, 10]

We will now look at two implementations of insertion sort in code. The examples here are in C#, but you should be able to follow even if you're unfamiliar with the language.

Non-Recursive Solution
^^^^^^^^^^^^^^^^^^^^^^

.. sourcecode:: csharp

   using System;
   using System.Collections.Generic;

   class MainClass {

     public static List<int> insertionSort(List<int> arr) {
       Console.WriteLine("Original Array:");
       arr.ForEach(Console.WriteLine);
       var sortedArray = new List<int>();
       sortedArray.Add(arr[0]);
       for(int i = 1; i < arr.Count; i++) {
         int new_element = arr[i];
         bool inserted = false;
         int count = sortedArray.Count;
         for(int j = 0; j < count; j++) {
           if(new_element < sortedArray[j]) {
             sortedArray.Insert(j, new_element);
             inserted = true;
             break;
           }
         }
         if(!inserted) {
           sortedArray.Add(new_element);
         }
       }
       return sortedArray;
     }

     public static void Main (string[] args) {
       var arr = new List<int>() {4, 3, 8, 7, 2, 10};
       var sortedArray = insertionSort(arr);
       Console.WriteLine("---------");
       Console.WriteLine("Sorted Array:");
       sortedArray.ForEach(Console.WriteLine);
     }
   }

Recursive Solution
^^^^^^^^^^^^^^^^^^

.. sourcecode:: csharp

   using System;

   class MainClass {

     public static void recursiveInsertionSort(int[] arr, int n) {
       if(n == 1) {
         return;
       }
       recursiveInsertionSort(arr, n - 1);

       int last = arr[n - 1]; 
       int j = n - 2;

       while (j >= 0 && arr[j] > last) 
         { 
             arr[j + 1] = arr[j]; 
             j--; 
         } 
         arr[j + 1] = last; 
     }

     public static void Main (string[] args) {
       int []arr = {4, 3, 8, 7, 2, 10}; 
        
       recursiveInsertionSort(arr, arr.Length); 
      
       for(int i = 0; i < arr.Length; i++) {
         Console.Write(arr[i] + " ");
       }
     }
   }

Check Your Understanding
------------------------

.. admonition:: Question

   **True/False:** Searching for a value in a collection has the same big-O value regardless of whether or not the collection is sorted.

.. admonition:: Question

   **True/False:** All sorting algorithms have the same big-O value.

.. admonition:: Question

   What is the big-O value of insertion sort?

.. |On^2| raw:: html

   <em>O(n<sup>2</sup>)</em>
