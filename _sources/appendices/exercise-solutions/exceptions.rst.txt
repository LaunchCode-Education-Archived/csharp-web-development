Exercise Solutions: Exceptions
==============================

Line numbers are for reference. They may not match your code exactly.

Divide by Zero
--------------

.. _divide-by-zero:

* Complete a function called ``Divide()`` in ``Program.cs``. ``The Divide()`` method takes in two parameters: ``x`` and ``y``.
* Your function should return the result of ``x/y``.
* However, if ``y`` is zero, you should throw an exception.

.. sourcecode:: csharp
   :linenos:

      static double Divide(double x, double y)
      {
         if (y == 0.0)
         {
            throw new ArgumentOutOfRangeException("y", "You cannot divide by zero!");
         }
         else
         {
            return x / y;
         }
      }

.. _try-catch:

* Put your ``try/catch`` block in ``Main()`` to test out your error-handling skills. If an exception is caught, make sure to print out the error message.

.. sourcecode:: csharp
   :linenos:

      try
      {
         Divide(num1, num2);
      }
      catch (ArgumentOutOfRangeException e)
      {
         Console.WriteLine(e.Message);
      }

:ref:`Back to the exercises<exercise-1>`

.. _test-student-labs:

Student Test Labs
-----------------

The ``CheckFileExtension()`` function should do the following:

* Take in one parameter: ``fileName``.
* Return an integer representing the number of points a student receives for properly submitting a file in C#.
* If a student's submitted file ends in ``.cs``, they get 1 point.
* If a student's submitted file doesn't end in ``.cs``, they get 0 points.
* If the file submitted is ``null`` or an empty string, an exception should be thrown. What kind of exception is up to you!

.. sourcecode:: csharp
   :linenos:

      static int CheckFileExtension(string fileName)
      {
         if (fileName == null || fileName == "")
         {
            throw new ArgumentNullException("fileName","Student did not submit any work!");
         }
         else
         {
            if (fileName.Substring(fileName.Length - 3, 3) == ".cs")
            {
               return 1;
            }
            else
            {
               return 0;
            }
         }
      }

:ref:`Back to the exercises<exercise-2>`
