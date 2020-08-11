Studio: Analyzing Algorithms
============================

This studio consists of several practice exercises.

#. Given the un-reduced big-O value, calculate the reduced value.

   a. 10
   b. 10n
   c. 5n\ :sup:`2` + 2n
   d. 3 log\ :sub:`2`\ n + 2

#. For each of the following algorithms, calculate the big-O value. Be sure to specify which value *n* refers to.

   a. **Reversing a string**

      ::

         reversed = ''

         for c in str:
            reversed = c + reversed

   b. **Printing out a matrix**

      ::

         for row_idx in matrix.length:
            row = matrix[row_idx]
            for col_idx in row:
               print row[col_idx]
               print " " 
            print "\n"

   c. **Reversing each string in an array**

      *Note:* For this exercise, assume that each string has at most 10 characters.

      ::

         reversed_strings = []

         for str in strings:

            reversed = ''

            for c in str:
               reversed = c + reversed

            reversed_strings.append(reversed)

#. Suppose you have an array of ``Customer`` objects, sorted in alphabetical order by last name. For each of the following tasks, determine the run time in terms of big-O. 

   a. Print the names of all of the customers. 

   b. Print the names of only the customers with last name starting with "A".

   c. Find all customers with last name beginning with "A".

   d. Find all customers with first name beginning with "A".

#. Now supposed that you have a dictionary (or hash map) of customer objects, where the keys are letters and the values are arrays storing all customers with last name beginning with that letter. For example, of our dictionary is ``customers`` then ``customers["A"]`` is an array of all customers with last name ending with "A". Within each array, the customer objects are not sorted in any way. 

   a. Print the names of all of the customers.

   b. Print the names of only the customers with last name starting with "A".

   c. Find all customers with last name beginning with "A".

   d. Find all customers with first name beginning with "A".