Exercise Solutions: Data Types
==============================

Line numbers are for reference. They may not match your code exactly.

.. _data-types-solution1:

Input/Output
------------

1. Write a new “Hello, World” program to prompt the user for their name and greet them by name.

.. sourcecode:: csharp
   :linenos:

      Console.WriteLine("What is your name?");
      string myName = Console.ReadLine();
      Console.WriteLine("Hello " + myName + "!");

:ref:`Back to the exercises <data-types-exercises>`


Numeric Types
-------------

.. _data-types-solution2:

1. Write a program to calculate the area of a rectangle and print the answer to the console. You should prompt the user for the dimensions. (What data types should the dimensions be?)

a. Add a print line to prompt the user for the length of the rectangle.

.. sourcecode:: csharp

   Console.WriteLine("What is the length of your rectangle?");

:ref:`Back to the exercises <data-types-exercises>`

c. Repeat the previous two steps to ask for and store the rectangle’s width.

.. sourcecode:: csharp

   Console.WriteLine("What is the width of your rectangle?");
   string width = Console.ReadLine();

:ref:`Back to the exercises <data-types-exercises>`

e. Print a statement using concatenation to communicate to the user what the area of their rectangle is.

.. sourcecode:: csharp

   Console.WriteLine("The area of the rectangle is: " + area);

:ref:`Back to the exercises <data-types-exercises>`

More on Numeric Types
---------------------

.. _data-types-solution3:

1. Write a program that asks a user for the number of miles they have driven and the amount of gas they’ve consumed (in gallons), and print their miles-per-gallon.

.. sourcecode:: csharp
   :linenos:

      Console.WriteLine("How many miles did you drive on your trip?");
      string mi = Console.ReadLine();
      int miles = Int32.Parse(mi);

      Console.WriteLine("How many gallons of gas did you use?");
      string gal = Console.ReadLine();
      int gallons = Int32.Parse(gal);

      int mpg = miles / gallons;
      Console.WriteLine("The MPG for the trip was: " + mpg);

:ref:`Back to the exercises <data-types-exercises>`

Strings
-------

.. _data-types-solution4:

1. The first sentence of *Alice’s Adventures in Wonderland*
   is below. Store this sentence in a string, and then prompt the user
   for a term to search for within this string. Print whether or not the
   search term was found. Make the search case-insensitive, so that searching
   for "alice", for example, prints ``true``.

      ``Alice was beginning to get very tired of sitting by her sister on the
      bank, and of having nothing to do: once or twice she had peeped into the
      book her sister was reading, but it had no pictures or conversations in
      it, 'and what is the use of a book,' thought Alice 'without pictures or
      conversation?'``

.. sourcecode:: csharp
   :linenos:

      string alice = @"Alice was beginning to get very tired of sitting by her sister on the
      bank, and of having nothing to do: once or twice she had peeped into the
      book her sister was reading, but it had no pictures or conversations in
      it, 'and what is the use of a book,' thought Alice 'without pictures or
      conversation?'";
      
      Console.WriteLine(alice);
      Console.WriteLine("What sentence would you like to look for in the sentence above?");
      string searchTerm = Console.ReadLine();
      string compSearchTerm = searchTerm.ToLower();
      string compAlice = alice.ToLower();

      if (compAlice.IndexOf(compSearchTerm, 0) != -1)
      {
         Console.WriteLine("true");
      }
      else 
      {
         Console.WriteLine("false");
      }

:ref:`Back to the exercises <data-types-exercises>`




