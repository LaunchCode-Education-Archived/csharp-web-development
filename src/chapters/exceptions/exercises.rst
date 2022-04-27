Exercises: Exceptions
=====================

To get started, fork and clone this `repo <https://github.com/LaunchCodeEducation/csharp-web-dev-exceptions>`_ from Github. 

Divide By Zero!
---------------

.. _exercise-1:

The professor you TA for, Professor Jackson, shared with you the code she uses to auto-grade students' work.
She and the other TAs have encountered some problems with the code in the past when they enter the total possible point value for an assignment.
Occasionally, they accidentally enter ``0`` for the total number of possible points and the program encounters a fatal error when trying to divide by 0.

To help out with this issue, complete a function called ``Divide()`` in ``Program.cs``.

* The ``Divide()`` method takes in two parameters: ``x`` and ``y``.
* Your function should return the result of ``x/y``.
* However, if ``y`` is zero, you should throw an exception, such as ``ArgumentOutOfRangeException``. 

:ref:`Check your solutions<divide-by-zero>`

* Put your ``try/catch`` block in ``Main()`` to test out your error-handling skills.  If an exception is caught, make sure to print out the error message.


:ref:`Check your solutions<try-catch>`

.. _exercise-2:

Test Student Labs
-----------------

After mentioning to Professor Jackson that you would like to get some more practice with exceptions, she offered to let you write some grading software!
Before she gives you full control over auto-grading students' work, she asked if you could write a function called ``CheckFileExtension()``.

The ``CheckFileExtension()`` function should do the following:

* Take in one parameter: ``fileName``.
* Return an integer representing the number of points a student receives for properly submitting a file in C#.
* If a student's submitted file ends in ``.cs``, they get 1 point.
* If a student's submitted file doesn't end in ``.cs``, they get 0 points.
* If the file submitted is ``null`` or an empty string, an exception should be thrown. What kind of exception is up to you!

:ref:`Check your solution<test-student-labs>`

In ``Main()``, Professor Jackson has provided a dictionary of students and the names of their submitted files for you to test out your work.
If an exception is caught, make sure to print out the error message.
