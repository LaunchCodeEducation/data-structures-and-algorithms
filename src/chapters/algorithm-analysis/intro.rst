Introduction
============

What Is Algorithm Analysis?
---------------------------

What Is An Algorithm?
^^^^^^^^^^^^^^^^^^^^^

.. index:: ! algorithm

An **algorithm** is an ordered sequence of steps that carry out an action or solve a problem. Many everyday tasks can be described as an algorithm. For example, here is one way to describe the process of brushing your teeth. 

#. Grab the toothbrush
#. Apply toothpaste to the brush
#. Wet the brush
#. Move the brush in a circular motion over a tooth
#. Repeat step 4 for each tooth in your mouth
#. Rinse your mouth with water
#. Rinse the toothbrush

The algorithm has a few notable characteristics:

- The steps have a specific order
- Some steps take a fixed amount of time (steps: 1, 2, 3, 4, 6, 7)
- Some steps are dependent on the number of teeth you have (step 5)
- The number of times step 4 is repeated is controlled by step 5

How long would it take one person to brush their teeth? To determine this, We need to know how long each step will take.

#. Grab the toothbrush - 3 seconds
#. Apply toothpaste to the brush - 3 seconds
#. Wet the brush - 3 seconds
#. Move the brush in a circular motion over a tooth - 4 seconds
#. Repeat step 4 for each tooth in your mouth - 32 teeth at 4 seconds (32 x 4)
#. Rinse your mouth with water - 5 seconds
#. Rinse the toothbrush - 3 seconds

Calculating the total time gives us 3 + 3 + 3 + (32 x 4) + 5 + 3 = 145 seconds. Our algorithm takes almost 2 and a half minutes!

What we have just done is a basic `analysis` of an algorithm. We have a list of steps, and have defined which steps are dependant on the input size---in this case the number of teeth. 

Algorithm Analysis
^^^^^^^^^^^^^^^^^^

.. index:: ! algorithm analysis
.. index:: ! complexity

**Algorithm analysis** is the process of inspecting an algorithm in order to determine how a performance characteristic changes based on the size of the algorithm's input. We call each characteristic measure the **complexity** of an algorithm. In essence, algorithm analysis tells us how long an algorithm will take to run.

We write algorithms to solve problems, however there are typically many different ways to solve a given problem. We perform algorithm analysis to determine *which* algorithm performs the best. To assist with comparing algorithms, programmers have developed a notation that describes the complexity of an algorithm.

Big-O Notation
^^^^^^^^^^^^^^

.. index:: ! big-o notation
.. index:: ! time complexity
.. index:: ! space complexity

**Big-O notation** is a means of describing the complexity of a function in relation to the size of its input. It focuses on the amount of time or space (that is, run time or memory usage) required for an algorithm to complete its steps. We refer to these performance characteristics as the algorithm's **time complexity** and **space complexity**, respectively. More specifically, big-O notation expresses the *upper bound* on run time for an algorithm. 

In software development, space complexity often takes a back seat to time complexity. Time complexity is a `software limitation`. It can only be improved by implementing a faster algorithm, which can take a considerable amount of effort. Space complexity, however, is a `hardware limitation`. It can be resolved by provisioning more memory and only involves changes to the operating budget. 

Unless otherwise specified, we will use big-O to measure time complexity. This common language will allow us to compare two very different algorithms, and determine which one will perform better with regards to time complexity. The next section introduces the formal definition of big-O notation.

Check Your Understanding
------------------------

.. admonition:: Question

  What is an algorithm?

  #. A way to determine the big-O value
  #. An ordered sequence of steps
  #. Another word for complexity
  #. A special type of loop

.. 2/B

.. admonition:: Question

  What does the time complexity of an algorithm refer to?

  #. How much processing power an algorithm requires relative to its input size
  #. How much memory an algorithm requires relative to its input size
  #. How long an algorithm takes to complete relative to its input size
  #. How long it takes for developers to write an algorithm

.. 3/C

.. admonition:: Question

  What does the space complexity of an algorithm refer to?

  #. How much processing power an algorithm requires relative to its input size
  #. How much memory an algorithm requires relative to its input size
  #. How long an algorithm takes to complete relative to its input size
  #. How long it takes for developers to write an algorithm

.. 2/B

.. admonition:: Question

  Which complexity of an algorithm is more important to optimize? Why?

  #. Time complexity, because space complexity can be solved by allocating more resources
  #. Space complexity, because an algorithm can be written faster by assigning more developers

.. 1/A

.. admonition:: Question

  What is big-O Notation?

  #. A way to describe the complexity of an algorithm relative to its input size
  #. The process of analyzing an algorithm's performance
  #. An analogous term for an algorithm

.. 1/A
  