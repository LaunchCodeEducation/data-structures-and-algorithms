========================
Big-O Notation In Detail
========================

In the introduction, we discussed big-O notation as a generalized way of describing and comparing an algorithm's time complexity relative to its input size. 

.. index:: big-o
.. index:: growth rate

More specifically, big-O is a notation for describing the **growth rate** of a time complexity function as its input size is increased. The time complexity function serves as an approximate model for the behavior of the actual algorithm classified by it. 

In mathematical terms it is used to describe an algorithm as a function, ``f(n)``, which will never grow faster than at the upper bound its representative complexity function, ``g(n)``.
      
That is to say ``f(n) < O(g(n))`` with respect to their growth rates.

There is a lot to unpack here. And if your head is spinning don't worry. In this section we will dissect the confusing parts of the definition and introduce the three elementary big-O Values. This will prepare you for the more practical section to follow where you will learn the arithmetic used to calculate the big-O of steps and algorithms along with some other common big-O Values.

.. index:: growth rate
.. index:: upper bound

Growth Rates & Bounds
^^^^^^^^^^^^^^^^^^^^^

At its core big-O Notation is concerned with the **growth rates** of algorithms as a function of their input size. The growth rate of a function is its incremental change in output as the value of its input is continuously increased. The most important part of big-O notation is *n* the size of the input of the algorithm. 

It stands to reason searching through 5 records doesn't take very long no matter what algorithm you use. But searching through 500,000,000 records can take a relatively short amount of time, or an almost infinite amount of time depending on which algorithm you use. This is why we need to perform algorithm analysis and be able to determine the big-O Notation for our algorithms. Having an understanding of how well various algorithms perform allow us to make informed decisions in choosing the best fit for the problem at hand.

.. index:: upper bound
.. index:: lower bound

In terms of big-O the x-axis represents increasing input sizes, *n*, from a **lower bound** of 0 through an **upper bound** value of infinity. The y-axis then represents the behavior of a complexity function at each increasing value of *n*. 

.. todo:: generic graph with x (input size, n) and y as a generic complexity(n). no lines plotted just these labels of the axes as boundless arrows in the x and y

.. index:: curve

By representing algorithms as mathematical functions we are able to visualize their behavior on a graph. Each big-O value will have a characteristic behavior that is either a straight or curved line.

Big-O As The Worst Case
-----------------------

Big-O Notation is to be able to compare the `upper bound` time complexity of candidate algorithms. When we visualize the limit of each algorithm's big-O growth rate we are able to compare them to each other. 

Algorithms that quickly slope are said to be less performant. Because their growth rate is limited at smaller input sizes relative to other candidates. 

Big-O Notation determines the ``worst case`` performance of a given algorithm. It is possible and even likely that an algorithm will perform better than the worst case, however to compare one algorithm to another we always want to consider the worst case of each algorithm.

Below is a graph of the common big-O Values you are likely to encounter. We will cover how each Value relates in a practical sense to an algorithm in the coming section. For now just consider how the complexity function of *n* controls the limiting behavior of these Big-O Values.

.. todo:: preview of all the common values on a graph (operations vs input size). something like this https://s14-eu5.startpage.com/cgi-bin/serveimage?url=https%3A%2F%2Fwww.cdn.geeksforgeeks.org%2Fwp-content%2Fuploads%2Fmypic.png&sp=b82f0f2b0994a01b2ddadf6679f37c21&anticache=340636


The Elementary Big-O Values

Check Your Understanding
========================

.. admonition:: Question

  Time complexity refers to the runtime in standard units of time (seconds, minutes, etc.)

  - true
  - false

.. false

.. admonition:: Question

  The limit of a complexity function is the point where its curve becomes vertical

  - true
  - false

.. true

.. admonition:: Question

  The big-O of an algorithm is the upper bound representation of its behavior

  - true
  - false

.. true

.. admonition:: Question

  An algorithm's actual growth rate at will always be less than the upper bound of the Big-O Value that classifies it

  - true
  - false

.. true
