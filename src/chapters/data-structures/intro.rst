Introduction to Data Structures
===============================

You are likely familiar with several data structures already. Here are some common data structures in various languages, categorized by type.

.. list-table:: Common Data Structures
   :header-rows: 1
   :stub-columns: 1

   * - 
     - Ordered (variable-length)
     - Ordered (fixed-length)
     - Key/Value
   * - C#
     - ``List``
     - array
     - ``Map``
   * - Java
     - ``ArrayList``
     - array
     - ``HashMap``
   * - JavaScript
     - ``array``
     - n/a
     - ``object``
   * - Python
     - ``List``
     - n/a
     - ``Dictionary``
   * - C
     - n/a
     - ``array``
     - ``struct``

These are all built-in data structures in their respective languages. 

Ordered collection types are optimized for data that has a specific order, or can be sorted. Some examples of such data are numeric data or student records (where record are sorted by name). Key/value collection types are optimized for fast lookup. Where searching operations for ordered collections are *O(log n)* at best (using binary search), search for key/value collections is *O(1)*. 

You have likely become used to determining which data structure is best for a given application. Beyond these basic, built-in data structures, there are a large number of additional data structures that are optimized for specific uses. In some languages, these are provided in a package or library (e.g. the ``javax.collections`` package contains a large number of useful data structures). In others, you may have to code the data structure yourself. 

In this chapter, we explore some of the most common data structures, along with their use cases and performance for common operations.

Before we jump in, however, we need to review a couple of fundamental concepts.

Low-Level Programming Languages
-------------------------------

.. index::
   single: programming language;high-level
   single: programming language;low-level

While modern programming languages are often **high-level**, abstracting away tasks like memory management, the study of data structures and their design utilizes concepts more common in **low-level programming languages**. Low-level languages provide direct access to memory allocation, which allows them to be faster and more efficient. Thus, data structure design utilizes some of the more rigid components of low-level languages like C.

Fixed-Length Arrays
^^^^^^^^^^^^^^^^^^^

.. index::
   single: array;fixed-length

Low-level languages typically only provide fixed-length arrays. The programmer must specify the size of an array when declaring it, and the size may NOT be changed. While high-level languages like C# and Java have fixed-length arrays, most developers use them only for very specific purposes, relying more often on their variable-length counterparts. 

In this chapter, when we refer to an array, we will *always* be talking about a fixed-length array.

Pointers
^^^^^^^^

.. index:: ! pointer, ! reference type

In low-level languages, non-primitive types utilize **pointers**. A pointer is literally the memory address of the location that non-primitive value is stored. Since such types *reference* another location in memory, they are often called **reference types**. 

We typically visualize a pointer value as an arrow *pointing* at a non-primitive value.

.. image:: figures/pointer.png
   :alt: A pointer that refers to an object

With these tools in-hand, let's proceed to leaning about our first new data structure.