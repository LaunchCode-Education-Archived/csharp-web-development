.. _List:

.. index:: ! List

Lists
=====

To write a **List** version of the program, we will have to introduce
several new C# concepts, including the class ``List``. We will also
review different kinds of ``for`` loops used in C#.

Before going any further, we suggest you run the ``ListGradebook``
program in Visual Studio Code. You can view this program in `csharp-web-dev-lsn2controlflowandcollections <https://github.com/LaunchCodeEducation/csharp-web-dev-lsn2controlflowandcollections>`_.
Once you’ve done that, let’s look at what is happening in the C#
source code.

.. sourcecode:: csharp
   :linenos:

   List<string> students = new List<string>();
   List<double> grades = new List<double>();
   string newStudent;
   string input;

   Console.WriteLine("Enter your students (or ENTER to finish):");

   // Get student names
   do {
      input = Console.ReadLine();
      newStudent = input;

      if (!newStudent.equals("")) {
         students.Add(newStudent);
      }

   } while(!newStudent.equals(""));

   // Get student grades
   foreach (string student in students) {
      Console.WriteLine("Grade for " + student + ": ");
      input = Console.ReadLine();
      double grade = Double.Parse(input);
      grades.Add(grade);
   }

   // Print class roster
   Console.WriteLine("\nClass roster:");
   double sum = 0.0;

   for (int i = 0; i < students.Count; i++) {
      Console.WriteLine(students[i] + " (" + grades[i] + ")");
      sum += grades[i];
   }

   double avg = sum / students.Count;
   Console.WriteLine("Average grade: " + avg);

Here we declare and initialize two objects, ``students`` and ``grades``,
which appear to be of type ``List<string>`` and
``List<double>``, respectively. An ``List`` in C# is very
similar to an Array. Like an ``Array``, we must let
the compiler know what kind of objects our ``List`` is going to
contain. In the case of ``students``, the ``List`` will contain
values of type
``string`` (representing the names of the students), so we use the
``List<string>`` syntax to inform the compiler that we intend to
fill our List with strings. Similarly, ``grades`` will hold exclusively
values of type ``double`` and is declared to be of type
``List<double>``.

In lines 10 and 11, we also initialize each List by creating a new, empty
List.

.. index:: ! generic class, generic type

.. admonition:: Note

   You will sometimes see the ``List`` class written as List<T>,
   where ``T`` represents a placeholder for the type that a programmer will
   declare a given List to hold. This is especially true in documentation.
   You can think of ``T`` as representing an arbitrary type.

   Classes like ``List<T>`` that take another type or class as a parameter
   are referred to as **generic classes** or **generic types**.

``List`` Iteration
-----------------------

``do-while``
^^^^^^^^^^^^

We then use a ``do-while`` loop to collect the names of each of the students
in the class.

.. sourcecode:: csharp
   :lineno-start: 18

   // Get student names
   do {
      newStudent = Console.ReadLine();

      if (!newStudent.equals("")) {
         students.Add(newStudent);
      }

   } while(!newStudent.equals(""));

Recall that a ``do-while`` loop is very similar to a ``while`` loop, but the
execution condition is checked at the end of the loop block. This has the net
effect that the code block will always run at least once. In this example, we
prompt the user for a name, which C# processes via ``Console.ReadLine()`` when
the user hits the enter key. To finish entering names, the user enters a blank
line.

.. index:: ! List.Add()

For each student that is entered (that is, each non-empty line), we add
the new ``string`` to the end of our List with ``students.Add(newStudent)``.
The ``.Add()`` method is provided by the ``List`` Class.
There are lots of other List methods to get familiar with, some of which
we will discuss in more detail below.

``foreach``
^^^^^^^^^^^

Below the ``do-while`` loop are two different loops that demonstrate two ways
you can loop through a List in C#. Here’s the first, which collects the
numeric grade for each student:

.. sourcecode:: csharp
   :lineno-start: 27

   // Get student grades
   foreach (string student in students) {
      Console.WriteLine("Grade for " + student + ": ");
      string input = Console.ReadLine();
      double grade = Double.Parse(input);
      grades.add(grade);
   }

This, you may recall, is C#'s ``foreach`` loop syntax. You may read this
in your head, or even aloud, as: ``for each student in students``. As you might
expect at this point, we must declare the iterator variable ``student``
with its data type.

``for``
^^^^^^^
The next loop on display prints out each student’s name and grade:

.. sourcecode:: csharp
   :lineno-start: 34

   // Print class roster
   Console.WriteLine("\nClass roster:");
   double sum = 0.0;

   for (int i = 0; i < students.Count; i++) {
      Console.WriteLine(students[i] + " (" + grades[i] + ")");
      sum += grades[i];
   }

.. index:: ! List.Count

Here, we introduce the syntax ``students.Count`` which utilizes the ``Count``
property of ``List``. This property holds the integer representing the
number of items in the List. This is similar to string's ``.length()`` method.

In this ``for`` loop, we use a *loop index* to define the starting point,
ending point, and increment for iteration. It may be helpful for you to
consider this kind of construction as something like,  ``for integer i in the
range of the number of items in students...``. The first statement inside the
parenthesis declares and initializes a loop index variable ``i``. The second
statement is a Boolean expression that is our exit condition. In other words,
we will keep looping as long as this expression evaluates to ``true``. The
third statement is used to increment the value of the loop index variable at
the end of iteration through the loop.

Again, the syntax ``i++`` is C# shorthand for ``i = i + 1``. C# also
supports the shorthand ``i--`` to decrement the value of ``i``.
We can also write ``i += 2`` as shorthand for ``i = i + 2``.

In the final lines of the program, we compute the average grade for all
students:

.. sourcecode:: csharp
   :lineno-start: 43

   double avg = sum / students.Count;
   Console.WriteLine("Average grade: " + avg);

List Methods
-----------------

Let’s gather up a few of the ``List`` methods that we’ve encountered so
far, along with a few new ones. While these will be the most common methods and
properties that you use with this class, they by no means represent a complete
List. Refer to the `official documentation on the List
class <https://docs.microsoft.com/en-us/dotnet/api/system.collections.List?view=netframework-4.8>`__
for such a List, and for more details.

To demonstrate the use of these methods, we'll create a new ``List``
called ``planets``.

.. sourcecode:: csharp

   List<string> planets = new List<string>();

Ok, we've got an empty List. We need to use the class's ``.Add()`` method
to populate this collection with items.

.. admonition:: Note

   There are other means to declare and initialize an List in fewer lines.
   These require knowledge of other collections types, so we'll stick with ``.Add()``
   for the time being.

Using ``.Add()`` to populate ``planets``:

.. sourcecode:: C#
   :linenos:

   planets.Add("Mercury");
   planets.Add("Venus");
   planets.Add("Earth");
   planets.Add("Mars");
   planets.Add("Jupiter");
   planets.Add("Saturn");
   planets.Add("Uranus");
   planets.Add("Neptune");

Thus, the first item in this table:

.. _list-methods:

.. list-table:: List methods in C#
   :header-rows: 1

   * - C# Syntax
     - Description
     - Example
   * - ``Add()``
     - Adds an item to the List
     - ``planets.Add("Pluto")`` adds ``Pluto`` to ``planets``
   * - ``Count``
     - Returns the number of items in an List, as an ``int``
     - ``planets.Count`` returns ``9``
   * - ``Contains()``
     - Checks to see if the List contains a given item, returning a Boolean
     - ``planets.Contains("Earth")`` returns ``true``
   * - ``IndexOf()``
     - Looks for an item in an List, returns the index of the first occurrence of the item if it exists, returns -1 otherwise
     - ``planets.IndexOf("Jupiter")`` returns ``4``

Here's a couple more methods that require slightly longer descriptions:

.. _listsort:

.. list-table:: List.Sort()
   :header-rows: 1

   * - C# Syntax
     - Description
     - Example
   * - ``.Sort()``
     - Rearranges the elements of an ``List`` into ascending order.
     - ``planets.Sort()`` produces ``["Earth", "Jupiter", "Mars", "Mercury", "Neptune", "Pluto", "Saturn", "Uranus", "Venus"]``

.. list-table:: ToArray()
   :header-rows: 1

   * - C# Syntax
     - Description
     - Example
   * - ``ToArray()``
     - Returns an Array containing the elements of the List
     - ``planets.ToArray()`` returns
       ``{"Earth", "Jupiter", "Mars", "Mercury", "Neptune", "Pluto", "Saturn", "Uranus", "Venus"}``

Perhaps you recall that in C#, you must know the size of the Array when you
create it. So we'll need to first define the new Array before we can use
``toArray()``.

.. sourcecode:: csharp
   :linenos:

   string[] planetsArray = new string[planets.Count];
   planetsArray = planets.ToArray();

Speaking of Arrays, let's see the Array version of Gradebook next.

Check Your Understanding
-------------------------

.. admonition:: Question

   The number of entries in an ``List`` may not be modified.

   #. True
   #. False

.. ans: False

.. admonition:: Question

   Create an ``List`` called ``charStars`` containing ``a``, ``b``, and ``c``.

   #.

      .. sourcecode:: C#
         :linenos:

         List<string> charStars = new List<string>();
         charStars.add('a');
         charStars.add('b');
         charStars.add('c');

   #.
      .. sourcecode:: C#
         :linenos:

         List<char> charStars = new List<string>();
         charStars.add('a');
         charStars.add('b');
         charStars.add('c');

   #.
      .. sourcecode:: C#

         List<char> charStars = new List<char>('a', 'b', 'c');

   #.
      .. sourcecode:: C#
         :linenos:

         List<string> charStars = new List<string>();
         charStars.add("a");
         charStars.add("b");
         charStars.add("c");

.. ans: List<string> charStars = new List<string>();
         charStars.add("a");
         charStars.add("b");
         charStars.add("c");
