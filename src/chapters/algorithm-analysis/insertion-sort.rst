Insertion Sort
==============

.. IDEA:
  case studies:
    in main doc: pseudocode
    link to: directory of implementations in various languages
      c# for this first draft

.. TODO:: Link back to the recursion lesson in LC101.

Sorting
-------

``Sorting`` is the act of taking a collection of data and rearranging it into a specific order. The order can be numerical ascending, numerical descending, alphabetical, by time, etc,.

Some of the most famous algorithms are sorting algorithms. Sorting algorithms are important for many reasons, but for the purposes of this class they are primarly important because searching through unsorted data always takes *O(n)* time. You have to check against every single value every time you search for something. However, if your data is sorted you can implement different searching algorithms that are more performant than *O(n)*. We will see some of these searching algorithms in future lessons.

That being said not all sorting algorithms are equal. A sorting algorithm comes with it's own big-O Notation, making some sorting algorithms better depending on the incoming data.

Throughout this book we will introduce a number of various sorting algorithms. We will provide information about each sort which will be helpful in deciding which sort is better for which dataset. Some are more efficient for small sets of data, or for large sets of data. Most programming languages already have these sorting algorithms as a part of their standard library when working with data structures. However, it is valuable to know how they work, and how to implement them if you need to write your own custom sorting algorithm.

Insertion Sort
--------------

The first sorting algorithm we will be looking at is ``Insertion Sort``. This sort can be implemented in a couple of different ways, but we will be showing examples that sort a collection of numbers in ascending order. That is to say the smallest number will be the first element in the array, and the largest number will be the last element in the array.

An Insertion sort is a sorting algorithm that puts a collection of data into ascending numerical order. It would take an array like this ``[4, 3, 8, 7, 2, 10]`` and return an array like this ``[2, 3, 4, 7, 8, 10]``

An Insertion sort is an algorithm that loops through all the elements of an array and compares that value to all the previously sorted elements of the array. If it finds that the currently selected value is smaller than the value it is comparing to, it will insert that value into the position of the value it is being compared to. When an insert happens the nested loop breaks, and the outer loop moves to the next value in the remaining unsorted values of the array.

The insertion sort achieves this order by looping through all the elements of an array, starting with the second element, and compares that element to every element that comes before it. If it finds that the element is smaller than any of the previous comparison elements it will move the element into the position of the comparison element. After it has this element in place, it moves to the next element in the array. In essence the code requires a loop nested inside of another loop making it's big-O notation |On^2|.

Let's manually step through an array to see how the Insertion Sort works. We will start with the array above ``[4, 3, 8, 7, 2, 10]``, and end up with ``[2, 3, 4, 7, 8, 10]``.

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

Again we have a nested loop the big-O notation for an Insertion Sort algorithm would be |On^2|.

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

- What is sorting?
- Why is sorting valuable?
- What is the big-O Notation of Insertion Sort?

.. |On^2| raw:: html

   <em>O(n<sup>2</sup>)</em>
