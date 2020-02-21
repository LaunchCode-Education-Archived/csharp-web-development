Array
=====

We learned about arrays in C# in :ref:`a previous lesson <array>`, 
so let’s spend a moment comparing them to ``Lists``. ``Lists``  
are generally easier to use than C#'s ``Array``. Let's see why this is.

Why does C# have both ``Arrays`` and ``Lists``? The answer is
historical, at least in part. C# is a C-style language, and arrays are
the most basic data structure in C. Using an ``Array`` over a
``List`` might be preferred in some circumstances, primarily for
performance reasons (array operations are generally faster than ``List``
operations). Also note that *Arrays are of fixed size*. You cannot
expand or contract an ``Array`` after it is created, so you must know
exactly how many elements it will need to hold when you create it. This
fact is reason enough to use ``Lists`` in most scenarios.

To illustrate ``Array`` usage, here is a version of the Gradebook program
using ``Arrays`` instead of ``Lists``:

.. sourcecode:: csharp
   :lineno-start: 9

   // Allow for at most 30 students
   int maxStudents = 30;

   string[] students = new string[maxStudents];
   double[] grades = new double[maxStudents];

   string input;
   string newStudent;
   int numStudents = 0;

   Console.WriteLine("Enter your students (or ENTER to finish):");

   // Get student names
   do {
      input = Console.ReadLine();
      newStudent = input

      if (!Equals(newStudent, "")) {
         students[numStudents] = newStudent;
         numStudents++;
      }

   } while(!Equals(newStudent, ""));

   // Get student grades
   for (int i = 0; i < numStudents; i++) {
      Console.WriteLine("Grade for " + students[i] + ": ");
      input = Console.ReadLine();
      double grade = double.Parse(input);
      grades[i] = grade;
   }

   // Print class roster
   Console.WriteLine("\nClass roster:");
   double sum = 0.0;

   for (int i = 0; i < numStudents; i++) {
      Console.WriteLine(students[i] + " (" + grades[i] + ")");
      sum += grades[i];
   }

   double avg = sum / numStudents;
   Console.WriteLine("Average grade: " + avg);

We suggest you try running this version of the gradebook program called ``ArrayGradebook`` in Visual Studio.
This program lives in the `csharp-web-dev-lsn2controlflowandcollections <https://github.com/LaunchCodeEducation/csharp-web-dev-lsn2controlflowandcollections>`_ repository.
If you haven't forked and cloned the repository, you should do so now.

.. index:: ! bracket notation

Note that we have to decide up front how large our arrays, ``students``
and ``grades``, are going to be. Thus, this program sets an arbitrary maximum amount
of students, likely larger than any user will enter. It may seem obvious, then, 
that ``Array`` has no equivalent :ref:`Add() method <list-methods>`. The only 
way to access and alter an element in an ``Array`` is with **bracket notation**, 
using an explicit index. For example, gradebook defines a counter variable, ``numStudents``.
When the first student is entered by the user, the value is stored in ``newStudent``.
If the value is not the empty string, then the value in ``students`` at position 0 is assigned the ``newStudent`` value. 
The next time the ``do-while`` loop executes, the value of ``students`` at position 1
will be assigned. This process continues until the user enters an empty string for ``newStudent``.
Because we must always access and assign ``Array`` elements using an
explicit index, our code can seem littered with ``Array``
counter variables (like our friends ``i`` and ``j``), making it more difficult to
read (not to mention more error-prone).

Like ``Lists``, however, we can loop through an ``Array`` using a ``foreach``
loop as long as we don’t need to use the index of the current item. If
we only wanted to print each student’s name, and not their grade, at the
end of our program, we could do the following:

.. sourcecode:: csharp
   :linenos:

   foreach (string student in students) {
      Console.WriteLine(student);
   }

We’ll use ``Arrays`` in C# from time-to-time, but for the most part you should
rely on ``Lists`` to store collections of values, or ordered data.

Check Your Understanding
-------------------------

.. admonition:: Question

   ``Array`` size and element values cannot be changed once defined.

   #. True
   #. False

.. ans - false. array values can be changed

.. admonition:: Question

   Given the ``Array`` below, which of the following options is a valid action?

   .. sourcecode:: csharp

      int[] randomNumbers = new int[5];

   #. ``randomNumbers.Add(3);``
   
   #. ``randomNumbers.Add("one");``

   #. ``randomNumbers[0] = "three";``

   #. ``randomNumbers[0] = 1;``

.. ans - ``randomNumbers[0] = 1;``

  