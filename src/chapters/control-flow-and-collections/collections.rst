.. index:: ! data structure

Collections
===========

Data Structures
---------------

A **data structure** lets us hold on to lots of data in a single place. It 
is a programming construct to aggregate many values into one value. Many 
types of data structures exist in various languages. A few examples are 
lists, dictionaries, arrays, tuples, etc. 

.. index:: ! collections, ! C# Collections Namespace

C# Collections Namespace
------------------------

C# provides powerful and flexible structures to store data, known as
**collections**. The **C# collections namespace** refers to the various interfaces
the language provides for implementing collection types. 

Here, we'll discuss a collection called ``List`` and compare it to the 
``Array`` class. We'll then introduce a third collection type called ``Dictionary``. 
These three collection types will be sufficient for our basic C# needs. 
For more, refer to the official C# documentation on `collections <https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/concepts/collections>`__.

Gradebook, Three Ways
---------------------

We’ll explore collections in C# by looking at different versions of
the same program. The program functions as a gradebook, allowing a
user (a professor or teacher) to enter the class roster for a course,
along with each student’s grade. It then prints the class roster along
with the average grade. In each variation of this program, the grading
system could be anything numeric, such as a 0.0-4.0 point scale, or a
0-100 percentage scale.

A test run of the program might yield the following:

::

   Enter your students (or ENTER to finish):
   Chris
   Jesse
   Sally

   Grade for Chris: 3.0
   Grade for Jesse: 4.0
   Grade for Sally: 3.5

   Class roster:
   Chris (3.0)
   Jesse (4.0)
   Sally (3.5)

   Average grade: 3.5

We’ll look at the gradebook using a ``List`` first. 

