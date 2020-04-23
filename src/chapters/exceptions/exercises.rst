Exercises
=========

To get started, fork and clone this `repo <https://github.com/LaunchCodeEducation/csharp-web-dev-lsn9exceptions>`_ from Github. 

Divide By Zero!
---------------

Complete a function called ``Divide()`` in ``Program.cs``.
``Divide()`` takes in two parameters: ``x`` and ``y``.

Your function should return the result of ``x/y``.

However, if ``y`` is zero you should throw an appropriate error message.
Try to use an ``ArgumentOutOfRangeException`` and put your ``try/catch`` block in ``Main()`` to test out your error-handling skills!

Test Student Labs
-----------------

After mentioning to Professor Jackson that you would like to get some more practice with exceptions, she offered to let you write some grading software!
Before she gives you full control over auto-grading students' work, she asked if you could write a function called ``CheckFileExtension()``.
``CheckFileExtension()`` takes in one parameter: ``fileName``.

``CheckFileExtension()`` should return an integer representing the number of points a student receives for properly submitting a file in C#.
If a student's submitted file ends in ``.cs``, they get 1 point.
If a student's submitted file doesn't end in ``.cs``, they get 0 points.
If the file submitted is ``null`` or an empty string, an exception should be thrown. What kind of exception is up to you!

In ``Main()``, Professor Jackson has provided a dictionary of students and the names of their submitted files for you to test out your work!
