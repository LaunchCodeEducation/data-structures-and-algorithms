Analyzing Algorithms With Big-O Notation
========================================

Now that we have a conceptual foundation of big-O Notation let's explore it from a practical perspective. Analysis with big-O is about *comparing the classifications* of algorithms, not the algorithms themselves. Think of using big-O as a way of performing a surface-level analysis of how an algorithm will behave based on the `class of algorithms` it belongs to.

Why do we look at the classifications rather than the algorithms themselves? Simply put, because it's the fastest way of comparing performance. We perform analysis to determine what is worth pursuing. If at a high level one algorithm has a big-O that is more performant than another then we can immediately rule out the poorer candidate. We do not need to waste time implementing each algorithm to compare them in great detail. The classifications define their upper bound potential which, by definition, can never be exceeded.

In this section we will learn about the most common big-O values and how each of their relative performance to one another. Along the way we will cover how to evaluate the big-O values of steps and the algorithm's they belong to. 

Before we begin let's take a look at a visual representation of the big-O values you are likely to encounter. We will soon explore each of these in more detail. For now use this graph to form a mental model of each of their upper bound behaviors.

.. figure:: figures/function-examples.png
   :alt: Various functions of n
   :width: 600px

   Some functions of the variable *n* that commonly arise in algorithm analysis. (Image by `Cmglee <https://commons.wikimedia.org/wiki/User:Cmglee>`_, licensed under the Creative Commons Attribution-Share Alike 4.0 International license.) 


Linear Big-O Values
-------------------

From the graph above you likely noticed the two linear big-O values, *O(1)* and *O(n)*. Before getting into the more complex non-linear values let's explore these basic notations first.

.. admonition:: Tip

  Remember that the big-O of an algorithm is evaluated using the big-O `of the steps within it`. 

.. index:: ! pseudocode

When discussing big-O it is common to write **pseudocode** to represent the concepts associated with an algorithm. Pseudocode is an abstract way of writing code that is a mixture of plain English and generic syntax common to most programming languages. It allows us to describe programs and statements, such as the steps of an algorithm, while remaining agnostic to any specific programming language.

.. index:: O(1)

*O(1)*: Constant Time
-----------------------

.. index::
   :single: runtime;constant

A big-O of ``1`` means the time complexity is *independent of the size of the input* *n*. No matter how large the input size is the growth rate will always remain constant. In other words, its growth rate is constant and represented graphically as a horizontal line. 

- A step classified as of *O(1)* means it is an operation that runs in constant time.
- By extension, an algorithm classified as *O(1)* means the execution of its steps will run constant time. 

::

   # a simple print statement
   print "I am a simple print statement"

   # indexing into an element of a list of size n
   second_element = list_of_size_n[1]

   # finding the smallest value of a list of n numbers that are sorted in ascending order
   smallest_element = sorted_list_of_size_n[0]

   # comparing two elements in a list of size n
   if list_of_size_n[0] equals list_of_size_n[5]:
      # do some sub-step(s)

.. index:: O(n)

*O(n)*: Linear Time
--------------------

.. index::
   :single: runtime;linear

A big-O of *n* means the time complexity *is directly proportional to the size of the input* *n*. As the input size is increased, it will grow at a constant rate. It is represented graphically as a positively sloped line. 

It is associated programmatically with a finite loop, such as a ``for`` loop.

- An *O(n)* step is a loop that will repeat its sub-step operations at *most* *n* number of times
- An algorithm classified as *O(n)* will take *at most* *n* number of operations to complete its steps

::

   # a loop iterating n number of times
   # notice that n can be a number itself rather than a structure of size n
   repeat from 0 to n:
      # do some sub-step(s)

   # a loop iterating over each element in a list of size n
   for each element in list_of_size_n:
      # do some sub-step(s)

   # a while loop that eventually reaches a stop condition is also applicable
   count = 0
   while count < n:
      # do some sub-step(s)
      # one sub-step must increment the counter to ensure the loop will eventually end
      count++ 

Why do we say that *O(n)* will take `at most` *n* number of operations? Because this classification tells us the `upper bound` of what is possible, but the actual number of operations will depend on how the algorithm is used in practice. 

For example, if we are searching for a value in a list of size *n*, we would perform a comparison operation `up to` *n* times. We may find the match in the beginning (1 iteration) or at the end (*n* iterations) depending on where it is located. We can see that the practical number of iterations depends on the goal of the algorithm and its steps.

Evaluating the Big-O of an Algorithm
------------------------------------

As discussed previously, time complexity is referenced in units of operations. Some operations take a constant amount of time while others are dependent on the size of the input *n*. Algorithms are comprised of a series of steps, each of which can be thought of as an operation. Steps can also have sub-steps within them, such as an operation taken within a loop.

Our end goal is to `evaluate` the big-O value of an algorithm. In order to do so, we have to evaluate the big-O of the steps and sub-steps `within` it. We group and evaluate steps according to their **scope**.

In the pseudocode below, we use indentation to visualize the scope of each step and any sub-step within it. 

::

   function algorithm(n):
      # outermost scope, print and loop operations

      print "let's learn how evaluation works!"

      repeat from 0 to n:
         # loop scope, nested print operations
         
         print "I am in the loop scope" # O(1)

         print n 

After evaluating this algorithm, we classify it as *O(n)*. But how did we arrive at this classification?

When classifying an algorithm's big-O value, we need to evaluate each scope within it as a group. We start from the innermost scope and move outwards to the final scope of the algorithm itself.

#. **Count**: classify and **sum** the big-O of each operation of the inner scope
#. **Reduce**: take the **product** of the sum of the inner scope with the big-O of its outer operation
#. Repeat these steps for each scope in the algorithm
#. **Cancel**: as a final step we discard terms that have a negligible effect on the growth rate

The result written in big-O notation is the classification of the algorithm.

.. admonition:: Note

  Keep in mind that the use of `addition` and `multiplication` are used conceptually. You can not `actually` add or multiply a big-O value because it is just a notation not a value. We evaluate using the value inside the notation. For example, *O(1)* and *O(n)* are treated as the number *1* and variable *n* respectively.

Sum Rule: Count Within a Scope
------------------------------

When evaluating operations in the same scope we classify each operation and add them together.

Let's begin with the innermost scope---the loop scope---from our example above. It contains two print operations, both of which run in constant time.

::

   repeat from 0 to n:
      # loop scope, nested print operations
      
      print "I am in the loop scope" # O(1)

      print n # O(1)

The sum of the loop scope, containing two *O(1)* operations, is evaluated as:

.. raw:: html
   
   <div style="text-align:center;">1 + 1 = 2</div>

Product Rule: Reducing a Scope
------------------------------

A scope is reduced by taking the **product** of its sum and its outer operation. In other words we take the sum of the inner scope and multiply it by the operation it is contained in.

The loop operation may repeat up to the input size, *n*, number of times so we say it runs in *O(n)* time.

::

   repeat from 0 to n: # O(n)
      # loop scope, nested print operations

      print "I am in the loop scope" # O(1)
      print n # O(1)

Using the loop scope sum of *2* we evaluate the product with the loop operation as:

.. raw:: html
   
   <div style="text-align:center;">2 * n = 2n</div> 

The outermost scope now contains the reduced loop operation, *2n*, and a print operation, *1*. 

::

   function algorithm(n):
      # outermost scope, print and loop operations

      print "let's learn how evaluation works!" # O(1)

      repeat from 0 to n: # loop scope, reduced to 2n

We take the sum of these operations as they are both in the same scope: 

.. raw:: html
   
   <div style="text-align:center;">2n + 1</div>

At this point, we may be tempted classify our algorithm as *O(2n + 1)*. But we saw the algorithm's actual classification is *O(n)*. Why do we get rid of, or `cancel` the coefficient *2* and the constant term *1*? 

Cancel Rule: Discarding Negligible Terms
----------------------------------------

Recall that big-O represents the upper bound of an algorithm's runtime. 

When we consider the behavior at *very large* values of *n*, we see that the following can be discarded: 

- **Constant terms**: any number that doesn't change
- **Coefficients**: any number that is multiplied with a variable
- **Lower-order terms**: variables at a power less than the highest found in a polynomial 

To avoid getting bogged down in the mathematical details that supports cancellation let's think about constants and coefficients in a practical sense. We will defer the discussion on lower order terms until later in this section when they have a relevant context.

Essentially there is no number that can be multiplied (coefficient) or added (constant term) to the factor of *n* that will have any effect on the growth rate. For this reason, we consider coefficients and constants as `negligible` relative to the *n* term itself and can discard them.

From our pseudocode example that was reduced to ``2n + 1``, we can see that ``2`` is a coefficient of *n* and ``1`` is a constant term, so both can be cancelled. After cancelling we are left with *n*. Writing this value in big-O Notation we finally classify the algorithm as *O(n)*.

This example used linear big-O values to illustrate the process of evaluation simply. We will explore some common non-linear big-O values next. While they may appear more complex on the surface, they are evaluated in the same methodical way---from the inside out using sums, products, and cancelling negligible terms.

Non-Linear Big-O Values
-----------------------

Unlike the linear big-O values, the non-linear classifications are bounded at varying input sizes that cause their performance to degrade rapidly. At their respective upper bounds the number of operations they take to process larger inputs becomes impractical.  

|On^2|: Quadratic Time
^^^^^^^^^^^^^^^^^^^^^^

.. index::
   :single: runtime;quadratic

A big-O of |n^2| means the time complexity is *quadratic with respect to the size of the input* *n*. In other words, the number of operations required increases with the square of *n*. It is represented graphically as the positive half of a parabola, a U-shaped curve.

.. index:: nested loops
.. index:: recursive function

In practice, |On^2| is often related to two nested loops, where each may iterate `at most` *n* times. 

Recall that a loop behaves similarly to a *recursive* function call. Therefor, |On^2| often describes the runtime of a recursive call nested within a traditional finite loop.  

- A step classified as |On^2| is a reduction of a loop operation within another loop operation.
- An algorithm classified as |On^2| means the execution of its steps will take `at most` a number of operations equal to the square of the input size.

::

   # a nested loop step driven by a numeric input of size n
   repeat from 0 to n times:
      # some other sub-step(s)
      repeat from 0 to n times:
         # some sub-step(s)

   # an algorithm with recursion in a loop
   function recursing(list_of_size_n):
      for each element in list_of_size_n:
         # some other sub-step(s)

         # the breakout condition to ensure finite recursion
         if a breakout condition is not met:
            # where ...n represents some recursive usage of n
            return recursing(...n)

Let's consider an example to see how an algorithm is evaluated to a classification |On^2|:

::

   function nested_loops(n):
      # algorithm scope

      outer_count = 0
      inner_count = 0

      repeat from 0 to n times:
         # outer loop scope

         print outer_count
         repeat from 0 to n times:
            # inner loop scope

            print inner_count
            inner_count++

         outer_count++

Begin at the innermost scope:

::

      repeat from 0 to n times: # O(n)
         # inner loop scope

         print inner_count # O(1)
         inner_count++ # O(1)

inner loop scope is evaluated as:

.. raw:: html
   
   <div style="text-align:center;">n * (1 + 1) = 2n</div>

The outer loop scope is then considered:

::

   repeat from 0 to n times: # O(n)
      # outer loop scope

      print outer_count # O(1)
      
      repeat from 0 to n times: # inner loop reduced to 2n

      outer_count++ # O(1)

Substituting the reduced inner loop scope value of 2n the outer loop scope is evaluated as 

.. raw:: html
   
   <div style="text-align:center;">n * (1 + 2n + 1) = n * (2n + 2) = 2n<sup>2</sup> + 2n</div>

At the outermost algorithm scope:

::

   function nested_loops(n):
   # algorithm scope

   outer_count = 0 # O(1)
   inner_count = 0 # O(1)

   repeat from 0 to n times: # outer loop reduced to 2n^2 + 2n

The algorithm itself is evaluated as:

.. raw:: html
   
   <div style="text-align:center;">2n<sup>2</sup> + 2n + 1 + 1 = 2n<sup>2</sup> + 2n + 2</div>

If we factor out the common coefficient of 2 we can simplify this equation as:

.. raw:: html
   
   <div style="text-align:center;">2 * (n<sup>2</sup> + n + 1)</div>

We have already learned about cancelling negligible coefficients and constants which leaves us with:

.. raw:: html
   
   <div style="text-align:center;">n<sup>2</sup> + n</div>

But why do we drop the *n* term to arrive at the big-O Notation |On^2|?

Cancel Rule: Lower Order Terms
------------------------------

.. index:: polynomial function

Our algorithm reduction of |n^2+n| is known as a second-order polynomial, or quadratic function. We refer to it as `second order` because the highest power of *n* is *2*. 

.. index::
   :single: runtime;polynomial

We can see how each degree of nesting loops corresponds to the order of the polynomial. For example:

::

   repeat from 0 to n:
      repeat from 0 to n:
         repeat from 0 to n:

This algorithm contains 3 degrees of nesting loops and would be reduced to a third-order polynomial, |n^3|. Generally speaking, we classify algorithms running in **polynomial time** as |On^c| where *c* is the highest order, or number of degrees of nested loops. 

Earlier we mentioned that `lower order terms in a polynomial` can also be cancelled. The justification for this is similar to that of cancelling coefficients and constants. Take |n^2+n| for example. If both are taken at increasing values of *n* approaching infinity which will have a `greater effect` on growth rate? The highest order term will always *dominate* the growth rate relative to lower order terms. 

For this reason we can safely *cancel all but the highest order term*, leaving us with |n^2|. In big-O Notation we arrive at the classification |On^2|.


*O(log n)*: Logarithmic Time
-------------------------------

.. index::
   :single: runtime;logarithmic

In later sections, we will encounter an algorithm that has **logarithmic runtime**. This means that the algorithm will be |Olog2n|.

.. admonition:: Tip

   Recall that *x =* |log2n| means that *n =* |2^x|. In other words, |log2n| is the exponent that you must raise *2* to in order to get *n*. Taking a logarithm is the *inverse* (or reverse operation) of exponentiating.

Logarithmic runtime is another common nonlinear runtime. We won't provide an example of an algorithm with logarithmic time here, but we'll see one soon enough.

.. admonition:: Note

   In this book, we will usually write |Ologn| instead of |Olog2n|, dropping the base *2*. We will only ever use the base-2 logarithm, so this shouldn't present any confusion.

Comparing Big-O Values
----------------------

Now that we have covered some common big-O, values let's take another look at our graph:

.. figure:: figures/function-examples.png
   :alt: Various functions of n
   :width: 600px


We can see that when ordered from most to least performant, we get the following order:

#. *O(1)*: constant time
#. *O(log n)*: logarithmic time
#. *O(n)*: linear time
#. |On^2|: quadratic time
#. |On^c|: polynomial time

We will explore *O(log n)* in more detail within the context of binary searches. For now, keep this order in mind as a quick way of comparing the classifications of algorithms and ruling out less performant candidates. 

Check Your Understanding
------------------------

.. admonition:: Question

   Classify the following algorithm in big-O notation.

   ::

      function is_too_big(list_of_size_n, maximum_size):
         if list_of_size_n is smaller or equal to maximum_size:
            return true
         return false

   #. *O(1)*
   #. *O(n)*
   #. |On^2|
   #. *O(log n)*

.. admonition:: Question

   Classify the following algorithm in big-O notation.

   ::

      function has_the_number(numbers, target_number):
         for number in numbers:
            if number is equal to target_number:
            return true
         return false

   #. *O(1)*
   #. *O(n)*
   #. |On^2|
   #. *O(log n)*

.. admonition:: Question

   Classify the following algorithm in big-O notation.

   ::

      function is_in_sublist(lists, target):

         # lists is a two dimensional list (a list containing list elements)
         for each list in lists:
            for each element in sublist:
            if element is equal to target:
               return true
         return false

   #. *O(1)*
   #. *O(n)*
   #. |On^2|
   #. *O(log n)*

.. admonition:: Question

   Classify the following algorithm using big-O notation.

   ::

      function is_in_sublist(lists, target):

        # lists is a two dimensional list (a list containing list elements)
        for each list in lists:
          for each element in sublist:
            if element is equal to target:
              return true
        return false

   #. *O(1)*
   #. *O(n)*
   #. |On^2|
   #. *O(log n)*


.. |On^2| raw:: html

   <em>O(n<sup>2</sup>)</em>

.. |On^c| raw:: html

   <em>O(n<sup>c</sup>)</em>

.. |n^2| raw:: html

   <em>n<sup>2</sup></em>

.. |n^2+n| raw:: html

   <em>n<sup>2</sup> + n</em>

.. |n^3| raw:: html

   <em>n<sup>3</sup></em>

.. |Olog2n| raw:: html

   <em>O(log<sub>2</sub> n)</em>

.. |Ologn| raw:: html

   <em>O(log n)</em>

.. |log2n| raw:: html

   log<sub>2</sub> n

.. |2^x| raw:: html

   <em>2<sup>x</sup></em>