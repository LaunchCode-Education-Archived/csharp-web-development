.. _area-of-a-circle-studio:

Studio: Area of a Circle
========================

To get started, create a new console application in Visual Studio for the studio.

Calculate the Area of a Circle
------------------------------

Write a program that prompts the user for the radius of a circle.
Calculate the area of the user's circle and print the result.

.. admonition:: Tip

   Recall that the area of a circle is ``A = pi * r * r`` where ``pi`` is
   3.14 and ``r`` is the radius.

Here’s an example of how your program should work:

::

   Enter a radius: 2.5
   The area of a circle of radius 2.5 is: 19.625

Some questions to ask yourself:

#. What data type should the radius be?
#. What is the best way to get user input into a variable ``radius`` of
   that type?

.. admonition:: Note

   Use the ``Math`` class in C# to get the value of pi and square the radius. 
   The `documentation <https://docs.microsoft.com/en-us/dotnet/api/system.math?view=netframework-4.8>`_ has guidance on how to use the ``PI`` field and the ``Pow`` method.

Add a Little Validation
-----------------------

Extend your program further by using a `while or do-while loop <https://www.w3schools.com/cs/cs_while_loop.asp>`__, so that when the user enters a negative number they are re-prompted for a radius.

Bonus Mission
-------------

Add additional validation to your program.
If the user enters a non-numeric character or a empty string?
Print an error message and quit. You’ll need to peek ahead to learn about `conditional syntax in C# <https://www.w3schools.com/cs/cs_conditions.asp>`__.